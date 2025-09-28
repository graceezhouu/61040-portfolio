# Assignment 2: Functional Design
Author: Grace Zhou

## Problem Statement

### Problem Domain: High Demands in Busy Cities result in Long Lines 
Living in a major city often involves long waits for high-demand events such as concerts, restaurant openings, pop-ups, and more. Attendees invest time and effort commuting, only to face uncertainty about whether the wait will be worthwhile. I personally experienced frustrations from many wasted hours in lines this summer while living in NYC, never successfully getting into the events. 

### Problem: Lack of Reliable Information 
The central difficulty is the absence of reliable, real-time information about line lengths, wait times, and entry likelihood. Attendees cannot assess whether commuting or staying in line is worth the cost, leading to frustration, wasted time, and missed opportunities.

### Stakeholder List
- **Attendees**: Experience wasted time and need transparency to make informed decisions.
- **Event Organizers & Venues**: Reputation is tied to attendee satisfaction, so they benefit from tools that smooth demand and improve crowd management.
- **Competitors (other venues/events)**: Gain attendees when long waits deter customers. Greater transparency may redistribute foot traffic. 
- **City/Community**: Experiences secondary effects such as crowding in public areas. Smoother flows reduce congestion and provide a more pleasant environment for everyone. 

### Evidence and Comparables
1. **Consumer Frustration in the Event Scene**: [This blog](https://cosmeticsbusiness.com/why-booming-beauty-pop-ups-are-letting-consumers-down) reports that many are unsatisfied with events due to long lines, which result in high expectations that events frequently cannot meet, and therefore result in major letdowns. Attendees reported lack of communication and poor crowd management. This is frustrating and damanges brand repuation simultaneously as people leave disapointed. 
1. **Disney Parks’ Queue Apps** – Disney provides estimated ride wait times via its app, [My Disney Experience](https://plandisney.disney.go.com/question/find-wait-times-parks-app-483280/), proving users value transparency and prediction. However, the scope is very small (Disney amusement park visitors). 
2. **Yelp Wait Times** – Based on historical data, [Yelp shows how crowded a business usually is](https://blog.yelp.com/news/waitlist-times-get-line-remotely-yelp-nowait/), demonstrating that demand prediction is feasible. However, Yelp is primarily for restaurants only. 
3. **Restaurant Waitlist Apps (e.g., OpenTable, Nowait)** – These apps allow diners to [remotely join a queue](https://www.opentable.com/blog/how-opentable-works-for-restaurants/), reducing wasted waiting. However, once again, this is primarily developed in the food service industry. 
4. **Personal Observation (Summer 2025)** – This past summer, I waited in line for 7 events with 0 success. This demonstrates wasted personal time and high uncertainty.
5. **Google Maps “Live Popular Times”** – This feature provides [real-time levels](https://www.theguardian.com/technology/2016/nov/22/google-bar-shop-busy-real-time-live-data-black-friday) using location data, showing that crowd data can be gathered from users at scale. However, without user input, this information may be inaccurate / hard to validate. Additionally, this is for places that stay relatively constant, so this would not work for a one-time event someone may want to attend. 

## Application Pitch

### Name: LineLens 🔍
A real-time transparency app for urban event-goers.

### Motivation 
LineLens empowers users to decide whether waiting is worthwhile by providing real-time queue data and predictive insights with the help of user input so people don't waste time waiting in long lines.

### Key Features
1. ***Live Queue Tracking + Predictive Insights***

    - **Explanation:** Crowdsourced updates from attendees already in line. 
    - **Why?** Users can see current wait times and entry likelihood.
    - **Stakeholder Impact:** Attendees benefit from reduced uncertainty. Once the technical basics are established, more creativity can be added to the app to incentivize users to provide such information (ex. point system with rewards). 

2. ***Predictive Insights***

    - **Explanation:** Predict wait times based on historical data and current demand/input. 
    - **Why?** Users can have concrete expectations based on predictive data. 
    - **Stakeholder Impact:** Attendees benefit from reduced uncertainty once again, and event planners can gauge the demand and plan ahead. 


3. ***Virtual Check-In***

    - **Explanation:** Event coordinators can list their events on LiveLens and enable remote reservations. 
    - **Why?** Attendees avoid waiting in physical lines.  
    - **Stakeholder Impact:** Attendees can arrive when it is their turn in the virtual queue instead of waiting in-person. This is particularly helpful on hot days. Organizers can better distribute arrivals and plan quantities of items.

## Concept Design

### Concept Specifications 
1. ***QueueStatus***

    - **concept** QueueStatus
    - **purpose** Capture and share real-time information about queue length and estimated wait time.
    - **principle** Update queue length and estimated wait time information based on present information.
    - **state** 

        a set of Queues with 

        - queueID
        - location 
        - estWaitTime
        - estPplInLine
        - lastUpdated

        
    - **actions**

        updateStatus(queueID: String, estPplInLine: Number): (estWaitTime: Number, lastUpdated: Time)

        **requires** queueID must exist aka the event must exist in the system

        **effect** generates a best-effort estimated wait time based on historical data and current inputs
        
        viewStatus(queueID: String): (estPplInLine: Number, estWaitTime: Number, lastUpdated: Time)
        
        **requires** queueID must exist

        **effect** outputs any current information, including the number of people in line, the estimated wait time, and the last updated time (these values may be null if there is insufficient information)

2. ***UserReport***

    - **concept** UserReport
    - **purpose** Allow attendees to contribute data (e.g., position in line, entry success).
    - **principle** Gather reliable crowd-sourced information from attendees to keep queue estimates accurate.
    - **state** 

        a set of UserReports with 

        - userID
        - queueID
        - timeStamp
        - estPplInLine (optional, if user self-reports line length)
        - currWaitTime (optional, if user logs how long they’ve waited)
        - entryOutcome (entered / denied / left line)
            
    - **actions** 
    
        submitReport(userID: String, queueID: String, estPplInLine?: Number, currWaitTime?: Number, entryOutcome?: String): ReportID: String

       **requires** userID and queueID must exist

       **effect** creates a new UserReport associated with the given queue, timestamped. Information is passed to QueueStatus and PredictionEngine for processing.
    
       validateReport(reportID: String): validity: Boolean

       **requires** report must exist.

       **effect** confirms report accuracy by cross-checking with other reports (e.g., consistency with recent entries). Invalid reports may be flagged or excluded.

3. ***PredictionEngine***

    - **concept** PredictionEngine
    - **purpose** Generate forecasts of wait times and entry likelihood using historical + live data.
    - **principle** Combine statistical models with user reports and current queue status to generate predictions.
    - **state** 

        a set of Predictions with

        - queueID
        - historicalData (past attendance, average wait times)
        - liveReports (inputs from UserReport)
        - predictionResult (estWaitTime, entryProbability, confidenceInterval)
        - lastRun
    
    - **actions** 
    
        runPrediction(queueID: String): predictionResult: Object, lastRun:DateTime

       **requires** queueID must exist 

       **effect** generates updated prediction results for wait time and entry likelihood based on historical + live inputs, generates nothing if there is insufficient information
    
       getForecast(queueID: String): predictionResult: Object, lastRun:DateTime

       **requires** queueID must exist

       **effect** returns the most recently available prediction and lastRun

4. ***VirtualCheckIn***

    - **concept** VirtualCheckIn
    - **purpose** Allow remote spot reservations for eligible events.
    - **principle** Minimize wasted time by enabling users to check in virtually and arrive closer to their actual entry time.
    - **state** 

        a set of VirtualCheckIns with:

        - queueID
        - userID
        - checkInTime (time reservation was created)
        - arrivalWindow (recommended arrival interval, e.g., 7:40–8:00 PM)
        - status (active, used, cancelled, expired)
    
    - **actions** 
    
        reserveSpot(userID: String, queueID: String): ReservationID

       **requires** userID and queueID must exist; the event must support virtual check-in.

       **effect** creates a virtual reservation entry, assigns an arrival window predicted by PredictionEngine
    
       cancelSpot(reservationID: String)

       **requires** reservation must exist and be active

       **effect** cancels the virtual reservation, freeing capacity for others.

### Essential Synchronizations 
1. sync UserReport → PredictionEngine

when a UserReport is validated and accepted

then PredictionEngine.runPrediction(queueID) incorporates the new report to adjust predictionResult.

2. sync PredictionEngine → QueueStatus

when PredictionEngine finishes runPrediction(queueID) and produces a new predictionResult

then QueueStatus.updateStatus() is called with the predicted estWaitTime so that the status reflects both real-time reports and model-based forecasts.

3. sync PredictionEngine → VirtualCheckIn

when PredictionEngine produces a new predictionResult for a queueID with active reservations

then VirtualCheckIn adjusts arrivalWindow for those reservations if the predicted entry likelihood changes significantly.

4. sync VirtualCheckIn → QueueStatus

when a VirtualCheckIn.reserveSpot() action succeeds for a queueID

then QueueStatus.updateStatus() increments estPplInLine to reflect the remote reservation.

### Brief Notes
Each concept plays a distinct role, and together they form the backbone of LineLens’s functionality. QueueStatus acts as the central record for line conditions at any event. It aggregates information, ensuring users and businesses alike can see the current state of a queue. UserReport provides the raw, crowd-sourced data that fuels the system. It ensures the app can operate without requiring direct data from venues. PredictionEngine connects past and present, combining historical patterns with live reports to forecast outcomes like wait time and entry likelihood. This provides value not just as raw data, but as actionable insight for users. VirtualCheckIn turns predictions into practical utility by letting users reserve spots and receive tailored arrival windows. It directly reduces wasted time and enhances the user experience.

Together, these concepts remain modular: UserReport contributes to PredictionEngine, and PredictionEngine informs VirtualCheckIn. Ultimately, all information is gathered in QueueStatus. Generic types are instantiated in natural ways: userID always refers to attendees registered in the app, queueID refers to event queues created in QueueStatus, and prediction outputs are bound generically to the queue they describe rather than any user-specific assumptions. This separation ensures each concept is independent but capable of synchronizing through clear, declarative rules.

## UI Sketches 
![UI sketches for line lens app](/assets/ui_sketches.jpeg)

## User Journey(s)
**Scenario 1: Attendee using LineLens to make decision**
Sarah wants to attend a concert pop-up for her favorite artist but dreads wasting another evening in line, especially since it takes her an hour to get to the venue. She opens LineLens, searches for the event, and immediately sees a red “3+ hour wait” alert. Curious, she clicks in and views live reports from people currently in line, including updates on entry success rates. The app then estimates that the line will close in 45 minutes due to capacity. Realizing that commuting would be a waste of her evening, Sarah decides not to go. Instead, she chooses a restaurant opening she finds through the app and has a much better experience. LineLens helps her avoid frustration, save hours of time, and build trust in the app.

**Scenario 2: Attendee uses LineLens Virtual Check In to attend Coordinated Event**
A makeup brand leverages LineLens to organize their product launch party with the Virtual Check-In feature. Emily, who lives just 15 minutes away, finds the event on LineLens and reserves a spot remotely. She receives a notification to arrive in 40 minutes, but she leaves her house too late and misses her turn. Instead of losing her chance completely, LineLens automatically moves her five stops down in the queue. When she finally arrives, she waits a short time before entering. Although Emily had to wait longer because she was late, the delay was still far shorter and more predictable than standing in a physical line with no information. LineLens made her experience smoother and more flexible.

**Scenario 3: User finds a new event on the street and adds it on LineLens and other users come**
Fred is strolling through SoHo when he notices a matcha cafe setting up an interactive station with a small line forming. He opens LineLens, searches for the event, and when nothing comes up, he creates a new listing with the details he knows: the type of event, its location, and the approximate number of people in line. Later, Sam, a matcha enthusiast, discovers Fred’s post and decides to attend. By the time Sam arrives an hour later, the line has doubled. Still interested, Sam updates the posting by reporting the new line length. Based on his update, LineLens estimates his wait will be 45 minutes. This experience shows how the app empowers users to discover events spontaneously and keep information current for the community.