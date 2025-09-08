# Assignment 1: Problem Framing

## Structure Breakdown

The first section ([**Domains and Problems**](#domains-and-problems)) details the $10$ domains I selected. For $3$ of the domains, I specifically explain $3$ problems surrounding each. For every problem, I explain why I selected or rejected it. There are $9$ problems in total.

The second section ([**Stakeholders**](#stakeholders)) contains $3-4$ stakeholders per problem with explanations about their impact and how they could be affected.

The third section ([**Evidence**](#evidence)) contains citations and explanations per problem.

The final section ([**Features**](#features)) suggests features of a solution per problem.

Click any section to jump directly.
_________________________________________________________________________________________________

### Domains and Problems
1. Fashion & personal style
    - **Context**: I find myself spending a lot of time discovering different outfits. My friends and I frequently cross-reference many social media apps like Instagram, TikTok, and Pinterest to find new styles and trends.
2. Healthcare processes **(Selected Domain 1)**
    - **Context**: I fell very ill last semester. As a result, I had to quickly familiarize myself with the entire process, from filling out forms to getting a diagnosis to finding a specialist.
        - **Problem 1 - Slow Pipeline**: The limited availability of doctors and the high amount of coordination required by insurance providers, doctors' offices, and the patients themselves results in an *extremely* slow pipeline for scheduling appointments and getting any help.
            - **Rejected**: This issue requires many groups of people to all be on board in order to resolve. If a single point in the pipeline does not cooperate, the pipeline will continue to be slow. However, the process of getting so many parties to be on board draws attention away from the software creation process.
        - **Problem 2 - Missing records**: For people constantly on the move, they may have health records in a variety of places and accounts. However, a complete and timely set of records is crucial for diagnosis.
            - **Selected**: It is feasible to create a unified platform to improve the organization of medical records. This will help patients track dates, prescriptions, appointments, lab results, and more instead of managing piles of papers.
        - **Problem 3 - Billing contentions**: There is very little transparency in healthcare regarding pricing of services, examinations, and lab work, and how these charges are distributed to insurances and what the responsibilities of the patient are. This leads to confusing bills, overcharging, undercharging, and many disputes that take months to years to settle for patients.
            - **Rejected**: Significant domain knowledge is needed to resolve pricing transparency issues. Medical charges are complex, as are the insurance processes and legal perspectives. I do not have this background, so coming up with a software-focused solution would be difficult.
3. Online shopping
    - **Context**: Online shopping has grown tremendously in popularity over the years. Many retailers sell *similar* versions of a product. I always lose track and struggle with comparing these products exhaustively to find the best one for me.
4. Studying
    - **Context**: Although there are a lot of apps and websites for studying (e.g., Khan Academy), I think many lack the personalization aspect. Personalized systems for deep work, balancing study/work/life priorities, and long-term continuous learning are helpful to people at any stage in life who want to pick up new journeys.
5. Language learning **(Selected Domain 2)**
    - **Context**: For the past months, I've been spending time learning Spanish. Learning a new language has so much potential to be made interesting beyond traditional learning methods like flashcards, worksheets, exercises, etc.
        - **Problem 1 - Routine methods**: Many language learners struggle with traditional learning methods like flashcards, worksheets, exercises, etc.
            - **Selected**: I believe this problem can be solved with software elements! Developing and automating new learning techniques is a common and strong purpose for software. I would be interested in combining unique learning strategies that worked for me from experience into a system, which is both technically and creatively challenging.
        - **Problem 2 - Slow process**: Language learning is a slow process that can take months to years to get the basics and even longer to understand the cultural aspects.
            - **Rejected**: Speeding up any learning process requires putting in more time or utilizing different learning techniques, so this may be solved simultaneously through problem 1, but directly creating software that speeds up learning is not exactly intuitive or straightforward to implement.
        - **Problem 3 - Outdated**: Many phrases and vocabulary taught in older textbooks are outdated as languages are constantly evolving.
            - **Rejected**: It requires significant market research and interviews per language to understand the current status of words, phrases, and how they are used in various contexts. They also change frequently. Understanding everything draws emphasis away from software design.
6. AI usage
    - **Context**: AI is used for a wide range of tasks, from drafting essays to writing emails. After a psychology class, I became interested in analyzing user behavior with AI and exploring what insights can be gained from usage data.
7. Financial literacy tools
    - **Context**: My finance studies and experience in valuation/derivatives showed me that investing is intimidating for most people. Existing apps either oversimplify or overwhelm with jargon; I learned best from short, direct videos.
8. Waiting in line **(Selected Domain 3)**
    - **Context**: I am always waiting in lines, whether it is to check out groceries or buy a concert ticket. This past summer, I lived in a major city for the first time ever and experienced the tedious process of lining up and waiting hours in the unbearable heat. In total, I waited in 7 lines for a range of reasons including brand pop-ups, sample sales, gifting events, restaurant grand openings, buying concert tickets, and more, and got into 0 events.
        - **Problem 1 - Physical discomfort**: Standing for long periods can cause fatigue or pain. Lack of seating, shade, heating, or cooling, and carrying heavy belongings with no place to set them down can significantly worsen one's experience.
            - **Rejected**: Physical discomfort is a serious problem, but this cannot be directly resolved with software solutions.
        - **Problem 2 - Maximum uncertainty**: In these scenarios, there are many uncertain factors. You don't know if the commute to the destination is worth it, or how long you will be waiting, or if you will ever get to the end of the line before the event ends or products sell out.
            - **Selected**: The central problem here is lack of transparency. Venues, companies, or events may not be willing to provide this information in order to maximize profits or exposure, but a simple software tracking system with user input can help with this issue. This is not a widespread issue, but I argue that it can help people save time and has potential to be expanded into other domains. Software can't directly alleviate pain (Problem 1), but can help users with decision making on whether a line is worth staying in.
        - **Problem 3 - Massive Disruptions**: Massive lines of people that span many blocks cause disruptions for other people who live or work nearby and the neighboring businesses.
            - **Rejected**: Forming and maintaining good neighbor relationships requires genuine face-to-face communication, so the solution to this problem relies on human interaction-dependent solutions.

9. Misinformation & online trust
    - **Context**: The rise of AI-generated content on social media has led to a surge in misinformation, making vulnerable groups like children and older adults more susceptible to scams and false claims. I learned about these issues—including deepfakes and disinformation—in 6.4590.
10. Traveling
    - **Context**: In my opinion, traveling is the best form of therapy, but the most difficult part is getting people together, balancing everyone's schedules and responsibilities.
_________________________________________________________________________________________________

### Stakeholders

- **Missing records in healthcare processes**
    1. *Patients*: Directly affected by incomplete records, facing stress, delays, and misdiagnosis. A unified system reduces confusion and streamlines care.
    2. *Healthcare Providers*: Depend on accurate records for diagnosis and treatment. Unified records save time, reduce errors, and improve collaboration.
    3. *Insurers & Administrators*: Handle approvals and billing. Centralized records minimize disputes, paperwork, and compliance issues.
    4. *Epic Systems (MyChart)*: Dominant EHR vendor. New solutions may compete or integrate with existing systems.

- **Routine methods in language learning**
    1. *Learners*: Struggle with repetitive methods, risking burnout. Innovative software can boost engagement and motivation.
    2. *Platforms & Developers*: Outdated methods limit user retention. New strategies improve satisfaction and market position.
    3. *Educators*: Need effective tools to keep classes engaging. Software solutions enhance teaching with interactive elements.

- **Maximum uncertainty in waiting in lines**
    1. *Attendees*: Waste time and face frustration due to unpredictability. Transparency tools help them make informed decisions.
    2. *Event Organizers & Venues*: Reputation depends on customer experience. Real-time data can improve satisfaction and crowd management.
    3. *Competitors*: Benefit when long waits drive customers away. Transparency can shift foot traffic to alternative options.

_________________________________________________________________________________________________

### Evidence
- Problem: Missing records in healthcare processes
    1. [Many electronic health record systems exist.](https://www.praxisemr.com/top-ehr-physicians-systems.html) Data transfer between systems takes much effort and time and is tedious. Each has unique features for different needs, but results in inconsistency.
    2. [Epic (MyChart)](https://isthmus.com/news/news/epic-dominates-the-marketplace/) currently dominates online resource management in healthcare services. However, each hospital or medical center that uses MyChart requires a unique account. Accounts can be linked but there are many limitations.
    3. UCF Associate Professor Varadraj Gurupurr compares incomplete medical records to a [leaking pipe](https://www.ucf.edu/news/what-happens-if-your-medical-records-are-incomplete/). His previous studies have documented that the biggest reasons for missing health information are communication and education, emphasizing the need for an organized system.
    4. This write-up by the American Medical Association details all the possible scenarios where patients can lose their records and the [significant barriers](http://ama-assn.org/system/files/2021-02/Patient-access-obtaining-medical-records-from-closed-practices.pdf) to obtaining these. Often, patients are the last to be notified or not notified at all.
    5. The [American Health Information Management Association (AHIMA)](https://www.abramslaw.com/media/announcements/destroyed-medical-records/) has posted guidance on what to do if medical records are destroyed. However, they are limited and provide no guarantees, further emphasizing the need for digital organization.
    6. [Huddle Health](https://huddle-health.com/missing-medical-record/) is an existing platform patients can use to organize their records. The downside is that it is completely separate from hospital record systems, so users need to be proactive and ensure accuracy.
    7. The NIH breaks down the good, bad, and ugly of current electronic medical records. A key highlight is that it requires [constant evolution](https://pmc.ncbi.nlm.nih.gov/articles/PMC7043175/) to meet the needs of doctors and patients to achieve efficiency, and many components are still disconnected.
    8. This research article dives deeper into existing issues with these electronic records, specifically related to how they can generate statistically significant [selection bias, informed presence bias, misclassification bias, and more](https://pmc.ncbi.nlm.nih.gov/articles/PMC10938158/).
    9. From the perspective of companies that set up electronic health record systems, there are many [hurdles](https://www.officepracticum.com/blog/6-common-challenges-in-ehr-implementation) that need to be overcome in order to achieve a working system, including cost of use, technical ability, privacy concerns, and more.
    10. From the perspective of physicians, many are unhappy with existing systems. A key complaint was [too much time is spent keying in data and too little making eye contact with patients](https://www.commonwealthfund.org/blog/2018/electronic-health-record-problem).

- Problem: Routine methods in language learning
    1. [Language learning enrollment declines over the past 20 years and language teaching programs are feeling the impact.](https://multilingual.com/magazine/november-2024/the-decline-of-language-learning-in-us-higher-education/) This is caused by complex reasons and signifies that change is needed.
    2. The [benefits](https://pmc.ncbi.nlm.nih.gov/articles/PMC5662126/) of learning multiple languages are highlighted in this research article. However, as learning methods fall behind, this results in missed opportunities for many.
    3. [This blog](https://blog.thelinguist.com/duolingo-review/) highlights pros and cons of Duolingo, a well-established language learning platform from a user's perspective. A key limitation is the lack of depth in the learning, which makes achieving fluency difficult for some.
    4. [Another limitation](https://growingglobalcitizens.com/is-duolingo-effective-my-personal-review-as-a-language-teacher/) of Duolingo is the extreme gamification of language learning, which can easily skew the intention from learning to collecting points, gems, treasure chests, and more.
    5. Another popular platform is [LingQ](https://linguistmag.com/lingq-review-2022/), but its limitations include that it only has a small selection of languages and the free version has limited features.
    6. The blog highlights more [general limitations](https://www.lucalampariello.com/language-learning-apps/) of language learning apps, explaining boredom and burnout, screen distractions, and limited depth.
    7. This article explains the concept of [language immersion](https://en.wikipedia.org/wiki/Language_immersion), a different method compared to gamification that is useful for language learning.
    8. This [forum](https://www.reddit.com/r/languagelearning/comments/1lze50r/what_are_your_biggest_problems_with_language/) includes the opinions of many on why they struggle with using language apps. Some reflect that the emphasis is solely on vocabulary, and others mention various learning needs that are not met.
    9. This research article used statistical methods to quantify a variety of measurements related to learning on language apps. One measurement was [student concerns](https://rsisinternational.org/journals/ijriss/articles/the-impacts-of-language-learning-apps-on-students-perceptions-of-language-proficiency/). Key concerns include lack of speaking practice, technical issues with the apps, and lack of motivation.
    10. This forum contains people's [open-ended opinions](https://www.reddit.com/r/languagelearning/comments/12w7b6p/what_has_been_your_best_way_of_learning_a_new/) about the most effective learning strategies for them. Unlike the traditional games and strategies in apps, here we see many more diverse ideas from watching sports channels to children's cartoons.
- Problem: Maximum uncertainty in waiting in lines
    1. This news report from today.com tries to understand the [phenomenon of long lines](https://www.today.com/video/inside-the-growing-phenomenon-of-long-lines-for-viral-sensations-238236229785) in cities. People's motives range from wanting to try a popular slice of pizza to buying a trending tote bag. The reasons are endless, demonstrating how many people experience long lines.
    2. [Not all people hate a long line](https://www.reddit.com/r/AskNYC/comments/14tc0xg/what_long_lines_are_worth_waiting_for_in_nyc/). This forum gathers many opinions and some reflect that certain places are well worth the wait.
    3. Pop-ups are here to stay due to their [effectiveness as a marketing campaign](https://www.luxury-briefing.com/2019/08/pop-up-spaces-robert-soning/) to introduce new products, collaborate with other brands, or launch exclusive products. However, this also indicates that brands are less incentivized to resolve the problem of long lines since such events are such a success.
    4. [How long are people willing to wait?](https://www.glossy.co/pop/pop-up-culture-how-far-will-consumers-go-for-free/) Often, the incentive you receive does not correlate with the long hours spent in line, but the immersive and personal experience of events repeatedly draws people who are willing to wait.
    5. Aritzia, a popular Canadian clothing brand, allegedly experiences [lines over 1 km](https://dailyhive.com/vancouver/vancouver-aritzia-warehouse-sale-lineup-2025) for their annual warehouse event. This can quickly become an unpleasant experience and emphasizes the importance of properly monitoring lines.
    6. This article reports that many are [unsatisfied](https://cosmeticsbusiness.com/why-booming-beauty-pop-ups-are-letting-consumers-down) with such experiences. Long lines result in high expectations that events frequently cannot meet, and therefore result in major letdowns. Attendees reported lack of communication and poor crowd management.
    7. Another common place to see massive lines is at [sample sales](https://www.gq.com/story/sample-sales-nyc-sensoria), which is where highly coveted brands discount their items for a short amount of time. However, people report overwhelming crowds, staggering queues, and poor selections after the long waiting period.
    8. This blog shares another key reason for [unpleasant lines](https://verticalledge.com/blogs/news/lessons-from-the-shadows-a-case-study-on-pop-up-failures?srsltid=AfmBOoptOyXARpsvlaiyaTTHX-bM6chyUKgGIs3M0YTtku5hX-yyvwBL): events often suffer from logistical issues, such as overcrowding, stock shortages, or inadequate staffing, which can lead to a negative customer experience.
    9. [Solutions to long lines don't necessarily need to be technical](https://www.bizbash.com/event-production-planning/how-do-you-keep-guests-happy-while-waiting-in-line). This article explains how events can keep customers happy in long lines with physical measures.
    10. For certain event types that require tickets, [online ticket vendors](https://lifehacker.com/best-ticket-sites) become a solution to waiting in long lines. This is a saturated field with many competitors trying to offer the lowest resale prices.

_________________________________________________________________________________________________

### Features
Problem: Missing records in healthcare processes
- *Feature 1*: Automated data reconciliation – The system cross-checks patient records across different databases to detect and flag missing or inconsistent entries, reducing errors for providers and stress for patients.
- *Feature 2*: Interoperability API hub – Connects disparate electronic health record (EHR) systems, allowing seamless transfer of data across hospitals, clinics, and pharmacies.
- *Feature 3*: Patient-facing record portal – Patients can view and upload their own documents, giving them agency and filling gaps that staff or systems may overlook.

Problem: Routine methods in language learning
- *Feature 1*: New learning methods to retain interest – Learners learn through watching movies with subtitles, listening to music, and more in the desired language instead of traditional vocabulary flashcards, worksheets, etc.
- *Feature 2*: Personalized practice – Lessons adjust dynamically based on mistakes and progress. Learners are introduced to topics based on their interests instead of going through a fixed set of curriculums.
- *Feature 3*: Contextual conversation simulations – Learners practice through role-play in real-life scenarios (e.g., ordering food) with other learners, making skills more transferable. Peer-to-peer practice matching. Learners are paired with others at complementary skill levels for conversational exchange, adding variety and real interaction to the routine.

Problem: Maximum uncertainty in waiting in lines
- *Feature 1*: Real-time queue tracking – Customers see live wait times on an app or display, reducing frustration from unpredictability. The app knows information about current queue status through feedback from people in line, who can be incentivized to provide this information instead of the event itself. 
- *Feature 2*: Virtual check-in system with predictions – People reserve a spot remotely and arrive just-in-time, minimizing wasted hours (only feasible for some event types). Uses historical data and current demand to estimate future queue lengths, helping customers plan visits and businesses smooth traffic flow.
- *Feature 3*: Competitor benchmarking insights – Businesses compare their wait times to competitors, incentivizing efficiency and improving customer retention. 
