# Problem Set 1: Reading and Writing Concepts


## Exercise 1: Reading a concept
1. ### Invariants ###

Invariant 1 (requests vs. purchases): For every request, the sum of all purchases’ counts for that item ≤ the request’s count at the time the purchase was made. Phrasing this in another way: purchase count and unpurchased count remaining for a given request must equal the total number of that item requested.  

Invariant 2 (count non-negativity): Request counts must always be ≥ 0.

More important: Invariant 1, because it ensures the concept’s core purpose (preventing overselling of requested items).

Action most affected: `purchase`. It preserves the invariant by requiring a request with at least the given count and decrementing it exactly by the purchased amount.

2. ### Fixing an action ###

The `removeItem` action might break Invariant 1 if a request is later reduced while purchases already exist. This is because `removeItem` only checks if a request for this item exists in the registry, but does not check for purchases. This is problematic because the request will no longer be in registry (request count=0) but its purchase count is greater than 0. 

Fix: we need to add stronger preconditions to ensure that all factors are checked. An item can only be removed  if no purchases have been made (in addition to the existing requirements).


3. ### Inferring behavior ###

A registry can indeed be opened and closed repeatedly based on. the spec, since open requires only inactive and close requires active (opposite states). 

Reason: allows temporary suspension (e.g., registry user wants to pause purchases while doing other actions like editing/increasing/decreasing the items).

4. ### Registry deletion ###

Not having delete may clutter the state, but practically it matters less — inactive registries could just be ignored, especially since this is most widely used only at weddings. However, from a privacy/storage perspective, deletion could be valuable.

5. ### Queries ###

    - By recipient: “Which items remain unpurchased in my registry?”

    - By giver: “Is item X in registry Y, and how many / what is still available to purchase?”  

6. ### Hiding purchases ###

Add a hidePurchases Flag on registries. Then, modify purchase so that recipient queries respect the flag (return only aggregated counts without purchaser identities or simply not see any purchase information).

7. ### Generic types ###

Generic Item avoids over-specifying. Items may be SKUs in some systems, IDs in others. If names/descriptions were stored directly (repetitive names, similar or identical descriptions), it would duplicate product catalog functionality, create consistency issues, and break modularity. 

## Exercise 2: Extending a familiar concept
1. 

    state 
        a set of Users with  
            a username String  
            a password String 

2. 

***Actions***

**register(username: String, password: String): (user: User)**

*Requires*: no existing user with that username.

*Effects*: create new user with given username and password; return it.

**authenticate(username: String, password: String): (user: User)**

*Requires*: user exists with the username and password matches.

*Effects*: return that user (no state change).

3. 

***Essential Invariant***

Usernames are unique (one username should correspond to only one user). 

Preserved by register’s precondition.

In other words, users should not be able to creact accounts with a username that already exists. 

4. 

**state**

a set of Users with  

    a username String  
    a password String 
    a confirmed Flag
    
a set of PendingRegistrations with  

    a username String  
    a password String  
    a secretToken String  

**register(username: String, password: String): (token: String)**

*Requires*: no existing user with that username.

*Effects*: creates user (confirmed Flag set to false) and create PendingRegistration with generated token; return token.

**confirm(username: String, token: String): (user: User)**

*Requires*: PendingRegistration exists with matching username and token.

*Effects*: change confirmed Flag entry to True for the given username; return new user.

**authenticate(username: String, password: String): (user: User)**

*Requires*: user exists with the username and password matches and confirmed Flag is True.

*Effects*: return that user (no state change).

## Exercise 3: Comparing concepts
***Personal Access Tokens Concept***

    concept: PersonalAccessToken [User]  

    purpose: authenticate users with revocable, application-specific tokens  

    principle: a user generates a token string, uses it like a password,  
    and can revoke it at any time without affecting their main password  

    state  
    a set of Users with  
        a set of Tokens  

    a set of Tokens with  
        a value String  
        a valid Flag  

    actions  
    createToken(user: User): (token: Token)      
        Requires: user exists
        Effects: generate new token with valid=true and add to user and return the token 

    authenticate(username: String, token: String): (user: User)  
        Requires: user exists with a valid token matching value  
        Effects: return user  

    revoke(user: User, token: Token)  
        Requires: both user and token exist and valid=true  
        Effects: set valid=false  

*Differences from PasswordAuthentication*
- Tokens are multiple per user; each user only has one password.
- Tokens can be revoked without resetting password.
- Tokens can be used to limit scope of actions.

*Improving GitHub docs*
Docs should clearly explain why tokens differ from passwords: 
1. multiple per user
2. revocable independently
3. should not be stored like passwords. 

Currently the docs blur tokens and passwords instead of emphasizing these distinctions especially revocability and scope.

## Exercise 4: Defining familiar Concepts
I choose URL Shortener, Conference Room Booking, Time-Based One-Time Password (TOTP).
1. **URLShortener**

Concept: URLShortener

Purpose: shorten URLs for easier sharing

Principle: a user submits a long URL, receives a short alias (custom or generated), and requests to the alias redirect to the original URL

State:

    a set of URLs with  
        a longURL String  
        a shortCode String  
        an owner User (optional)

Actions: 

**autoShorten(longURL: String, owner: User): (shortCode: URL)**

    Requires: longURL is valid

    Effects: generate a working shortCode that directs users to the same url as longURL. return shortCode. 

**manualShorten(longURL: String, owner: User, shortCode: URL)**

    Requires: longURL is valid, shortCode is not in use

    Effects: create a mapping that connects the provided shortCode to the longURL. 

**resolve(shortCode: String): (longURL: String)**

    Requires: shortCode URL exists and is valid.

    Effects: return longURL.

2. **ConferenceRoomBooking**

Concept: ConferenceRoomBooking

Purpose: schedule rooms without conflicts

Principle: a user requests a room for a time slot; booking succeeds only if no conflict

State:

    a set of Rooms with  
        a name String  
        a set of Bookings  

    a set of Bookings with  
        a room Room  
        a startTime DateTime  
        an endTime DateTime  
        a user User  


Actions: 

**book(user: User, room: Room, start: DateTime, end: DateTime): (booking: Booking)**

    Requires: no existing booking overlaps with [start, end).
    
    Effects: create new booking for the given user.

**cancel(user: User, booking: Booking)**

    Requires: booking exists and user matches the user of the Booking.

    Effects: remove booking.

Notes: overlap check is crucial invariant. An edit booking action is not included for simplicity and because it can be completed by canceling and re-booking. 

3. **TOTPAuthentication**

Concept: TOTP

Purpose: improve login security by requiring a time-limited code in addition to user's password

Principle: user registers a shared secret; an authenticator app generates time-based codes; login requires password + current code

State:

    a set of Users with
        a username String  
        a password String  
        a totpSecret String  


Actions:

**registerTOTP(username: String, password: String): (totpSecret: String)**

    Requires: user exists with corresponding username and password

    Effects: generate secret, store it, return it to user (to sync with authenticator app).

**authenticate(username: String, password: String, code: Number): (user: User)**

    Requires: username and password matches AND code matches what secret generates for current time window.

    Effects: return user.

Notes: We are assuming users and their passwords already exist and then adding this second factor. Prevents password-only theft attacks, though still vulnerable if both password + device are compromised (e.g., malware or phishing).