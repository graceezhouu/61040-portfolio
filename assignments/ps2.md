# Problem Set 2: Composing Concepts
Author: Grace Zhou

## Concept Questions
### 1. Contexts

In `NonceGeneration`, contexts exist to separate various domains of uniqueness. Each context keeps track of its own nonces in its own scope so that two different contexts can safely generate the same string without conflict.

In the URL shortening app, the context naturally corresponds to the `shortURLbase` (e.g., `bit.ly` vs. `mydomain.com`). Each base domain maintains its own set of used strings, so `bit.ly/abc` and `mydomain.com/abc` can coexist without clashing.

### 2. Storing used strings

The concept must store sets of used strings to ensure that no nonce is repeated for a given context. 

If only the generation procedure existed without memory, duplicates would be possible.
If the implementation uses a counter per context, the abstraction allows the mapping of each counter value to its corresponding generated string. The abstraction function is:

`counter = n` → `used = {f(0), f(1), …, f(n−1)}` where used is the set of used strings.

Thus, the specification’s “set of used strings” corresponds exactly to the range of values already produced by *incrementing* the counter.


### 3. Words as nonces 

- **Advantage**: From the user's perspective, it is easier to remember and share (e.g., `bit.ly/hello` instead of `bit.ly/X7z9Q`).

- **Disadvantage**: From the user's perspective, limited dictionary size increases collision risk and may reduce availability of unique shortenings that are also short/simple to remember. Also, words may be less secure (easier to guess).

- **Modification**: Adjust the state to include a dictionary of available words per context. The `generate` action would then select an unused word from this set and mark it as used.

        state  
            a set of Contexts with  
                a used set of Strings  
                a dictionaryWords set of Strings

And the `generate` action requires that an unused word exists, and returns one.


## Synchronizations for URL Shortening
### 1. Partial matching

In `generate`, only `shortUrlBase` appears in the `when` clause because the goal is to produce a nonce for that base domain, and it does not matter what target URL will eventually be connected. The `targetUrl` is not needed until registration, so it is omitted.


In `register`, both `targetUrl` and `shortUrlBase` appear because both are required to create the full mapping in `UrlShortening` (we need to know what the short URL should be connected to). In this case, both appear in the `when` clause. 


### 2. Omitting names

The convention isn’t always used for clarity. When a variable has a different role name in the `then` clause, explicitly binding prevents ambiguity. 

For example, in `generate`, explicitly writing `context: shortUrlBase` makes clear that the context argument is bound to the base URL. Without explicit naming, the sync could become confusing or misleading.

### 3. Inclusion of request

The first two syncs respond to explicit user actions (`Request.shortenUrl`) that initiate the process of shortening. The third sync (`setExpiry`) responds to a system event (automatic expiration), not a user request, so no request action is included there.

### 4. Fixed domain

If the app always uses a fixed domain name like `bit.ly`, then the `shortUrlBase` argument becomes unnecessary. We could remove `shortUrlBase` from the syncs and hardcode the base. Specifically, for `generate`, no context would need to be provided because everything has the same domain name, and for `register`, the output will not have `shortUrlBase` / it will be hardcoded. 

Example change to `register`:

    then UrlShortening.register (shortUrlSuffix: nonce, shortUrlBase: "bit.ly", targetUrl)


### 5. Adding a sync

We need a sync to delete expired shortenings:

    sync expireShortening  
        when ExpiringResource.expireResource(): (resource: shortUrl)  
        then UrlShortening.delete (shortUrl: shortUrl)  


## Extending the design
### 1.

I will describe $2$ new concepts: `Analytics` and `Ownership` to realize this extension. 

1. 

        concept Analytics  

        purpose count/document how many times each short URL is accessed  

        principle track when a short URL is created and after each lookup, the count for that short URL increases by one  

        state  
            a set of Records with  
                shortUrl String  
                count Number  
        actions  
            firstAccess (shortUrl: String)  
                requires: no record exists for shortUrl  
                effect: creates a record with count = 1 

            increment (shortUrl: String)  
                requires: record exists for shortUrl  
                effect: increases count by one  

            getCount (shortUrl: String): (count: Number)  
                requires: record exists for shortUrl  
                effect: returns count  
    
2. 

        concept Ownership  

        purpose ensure only the creator of a short URL can view its analytics  

        principle users may see analytics only for shortenings they registered
         
        state  
            a set of Ownerships with  
                shortUrl String  
                owner User  
        actions  
            assignOwner (shortUrl: String, user: User) 
                effect associates shortUrl with user  

            checkOwner (shortUrl: String, user: User): (allowed: Boolean)  
                requires shortUrl is in Ownership and has been assigned to a user
                effect returns true iff user is owner  

Note that it is possible to only add one new concept by combining Analytics and Ownership (ex. begin by adding a owner for each Record... etc.)

### 2.

1. When a shortening is created (we do not increment access count in Analytics because creation != first access):

        sync assignOwner  
        when 
            Request.shortenUrl(targetUrl, shortUrlBase)
            UrlShortening.register(shortUrlSuffix, shortUrlBase, targetUrl)
        then
            Analytics.assignOwner(shortUrl, user)              
            
2. When a shortening is accessed:

        sync incrementAnalytics  
        when UrlShortening.lookup(shortUrl)  
        then Analytics.increment(shortUrl)   

3. When a user examines analytics: 

        sync viewAnalytics  
        when Request.viewAnalytics(shortUrl, user)  
            Ownership.checkOwner(shortUrl, user): (allowed)  
        then Analytics.getCount(shortUrl)  [requires allowed == true ]
         

### 3.
- #### Allowing users to choose their own short URLs：
Add a new sync that uses user-supplied `shortUrlSuffix` instead of calling `NonceGeneration` to generate. No changes are needed to existing concepts and preserves modularity.
- #### Using words as nonces:
Extend `NonceGeneration` with a dictionary word set instead of generating a random string. `generate` will rely on this dictionary. No changes are needed in other concepts, which emphasizes modularity. 
- #### Including target URL in analytics:
I believe this feature is not desireable. Although multiple short URLs may map to the same target, these short URLs may have different owners. We have an ownership constraint that only the owner of a shortURL can access its analytics, so this feature is implementable by also checking if all short URLs mapping to the target have the same owner, but it defeats the purpose of being user-specfic and calculating a total count would violate our privary restriction. 
- #### Generate unguessable short URLs:

This is possible by adding a stronger nonce generator (e.g., random cryptographic strings), but it is undesireable in my opinion. Recall the purpose of URLShortening, which is to provide a "shorter or more memorable way to link". Making "not easily guessed" short URLs also makes it difficult for everyone, including the people who actually need the link. 


- #### Reporting analytics to non-registered creators:
This would break the ownership model. Either remove `Ownership` restriction (undesirable for privacy) or add an explicit concept for “public analytics.” This is likely undesirable unless requirements demand it in some tightly constrained situation.