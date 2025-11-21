### ADD Step 1: Review Inputs

| Category | Details |
| :--- | :--- |
| Design purpose | This is a greenfield system from a mature domain. The purpose is to produce a sufficiently detailed design to support the construction of the AI-powered digital assistant platform (AIDAP) |
| Primary Functional requirements | UC1: Because it directly supports the core AI interaction<br>UC2: Because it directly supports course work<br>UC3: Because it directly supports student interaction<br>UC4: Because it directly supports technical issues regarding data synchronization |


| Scenario Id | Importance to customer | Difficulty of implementation |
| :--- | :--- | :--- |
| QA-1 | High | medium |
| QA-2 | high | high |
| QA-3 | high | high |
| QA-4 | medium | high |
| QA-5 | high | medium |


Quality Attributes: Among the quality attributes, QA-1, QA-2, QA-3, and QA-5 were chosen as drivers.

Constraints: All constraints are a part of the drivers

Concerns: All concerns are part of the drivers

### ADD Step 2:Establish Iteration Goal by Selecting Drivers

This is the first iteration in the design of a greenfield system, so the iteration goal is to achieve the overall architecture of the system keeping in mind:

Quality attributes:
- QA-1: Performance
- QA-2: Usability
- QA-3: Reliability
- QA-5: Interoperability

Constraints
- CON-3: The system must work across web, mobile, and voice devices.
- CON-5: All user authentication must go through the official university SSO system.
- CON-8: The platform can only connect to approved university systems (like the LMS, calendar, etc.) via official APIs.
- CON-9: System updates must happen with zero downtime and have a rollback option.

Concerns
- CRN-2: The AI needs to be dependable and give users accurate answers.
- CRN-3: Future feature additions must be easily supported by the system's design.
- CRN-5: All development must be guided by a strong, clearly defined initial architecture.
- CRN-9: To guarantee their independence and maintainability, system components should have distinct boundaries.

<img width="441" height="471" alt="image" src="https://github.com/user-attachments/assets/2756faef-cced-4f95-b667-3b094c5204fb" />


### ADD Step 3: Choose One or More Elements of the System to Refine

We want to refine the entire AIDAP because it is a greenfield system. We are using a top-down approach. We are going to focus on the entire system and then decompose it into smaller components with each iteration. For now we just want to develop the overall architecture.

### ADD Step 4: Choose One or More Design Concepts That Satisfy the Selected Drivers

| Design choice and location | Rationale |
| :--- | :--- |
| Use a Rich Internet Application (RIA) Architecture for the frontend. | Because the RIA architecture satisfies the requirement to support web and mobile devices, AIDAP can operate directly in the browser without the need for installation (CON-3). In order to support interactive use cases like course work (UC2) and student interaction (UC3), as well as usability (QA-2), it offers a rich, responsive user interface. It also enhances performance (QA-1) and maintains the application's speed by managing some processing on the client side. |
| Discarded: | Web application:<br>This reference architecture makes it difficult to produce a good user interface because it focuses on server-side rendering and requires full page refreshes.<br><br>Mobile application:<br>The system needs to work on laptops as well. Limiting it to mobiles invalidates our constraint 3 which is, The assistant shall support both text and voice communication modes for all user types and function across mobile, web, and voice-assistant devices. |
| Use a Service Application Architect feature for the backend. | Since AIDAP needs to integrate with several external institutional systems (LMS, registration, calendar) through standard APIs (CON-8), a service-oriented backend was chosen. This architecture effectively isolates AIDAP from these external systems, fostering high interoperability (QA-5) and reliability (QA-3). Additionally, it addresses the need for modularity and clearly defined interfaces by dividing important tasks like AI processing and authentication into manageable services (CRN-9). |
| Discarded: | Micro Services:<br>High complexity for iteration 1 of a greenfield system. |
| Deploy the system using a Three-Tier Deployment pattern. | This pattern gives our app a clear physical structure by splitting it into three parts: the Client Tier (the user's browser), the Web/App Tier (where the app runs), and the Database Tier (where the data is stored). Using these three layers is a common way to build reliable and scalable web applications. It also makes the system more secure because the database is kept away from direct public access. |
| Discarded: | This pattern combines the application logic and data management on a single server tier, which is less secure and scalable. It fails to provide the necessary separation of concerns to protect the database and does not adequately address security (QA-4) or reliability (QA-3). |


### ADD Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| Design Decision and Location | Rationale |
| :--- | :--- |
| Instantiate a Synchronization Service in the application tier. | This is essential to guaranteeing the system's dependability (QA-3) and interoperability (QA-5). As mandated by CON-8 and UC-4, it is in charge of overseeing all data flows and connections with external institutional systems (LMS, Registration, Calendar). Because complicated integration logic is isolated, the system is easier to maintain. |
| Instantiate a Security Component for authentication and authorization in the application tier. | Because it addresses the non-negotiable security constraint to use the official university SSO (CON-5), this decision is crucial. This part will oversee all authorization and authentication, guaranteeing that users can only access information that they are allowed to view (CRN-4). It is a fundamental component of trust and system integrity. |
| Instantiate an AI Interaction Component in the application tier. | This is essential to guaranteeing the system's dependability (QA-3) and interoperability (QA-5). As mandated by CON-8 and UC-4, it is in charge of overseeing all data flows and connections with external institutional systems (LMS, Registration, Calendar). Because complicated integration logic is isolated, the system is easier to maintain. |
| Remove isolated storage from the client side | If grades, chat history, or personal information are stored in the browser or a device-local store, they can be accessed by anyone using that device which conflicts with CON-4. Also Local copies can easily become stale which can conflict with CRN-10 |
| Instantiate a Client Data Access Module in the RIA client | To handle all communication with the application tier, a special module is added to the client. The module communicates with the backend via AJAX/Fetch API calls, guaranteeing real-time dashboard updates without necessitating complete page refreshes. This prevents academic information from being stored locally and keeps the user interface (UI) focused on interaction rather than data handling. By enabling dashboards to load data on demand without combining presentation logic and data retrieval, it also supports UC-3. |


### ADD Step 6: Sketch Views and Record Design Decisions

<img width="1814" height="723" alt="image" src="https://github.com/user-attachments/assets/e8548019-0770-4166-9901-2cf18fa8b0c6" />


### Step 7: Perform Analysis of Current Design and Review IterationGoal and Achievement of Design Purpose

| Not addressed | Partially Addressed | Completely Addressed | Design Decisions Made During the Iteration |
| :--- | :--- | :--- | :--- |
| | | UC-1 | The design defined backend services that retrieve grades and events through authorized APIs and instantiated an AI Interaction Component. This allows for real-time responses to academic questions. |
| | UC-2 | | Although rich user interface updates and content presentation are supported by the RIA architecture, there is no specific component designed for publishing lecturer announcements. Although there is infrastructure, the architecture does not fully define the feature. |
| | UC-3 | | Although client-server communication and real-time dashboards are part of the design, no Notification Service was specifically instantiated. Automation is not fully designed, but there are some supporting components. |
| | | UC-4 | For UC-4, a Synchronization Service was created with retry logic, API connections, and integration complexity isolation. |
| | QA! | | RIA improves user responsiveness, but no specific performance tactics were designed. |
| | | QA2 | RIA is chosen for a rich, responsive UI across devices, directly supporting usability. |
| | QA3 | | The design choices don't mention specific tactics for failover, redundancy, or error handling beyond what the sync service provides, making this only partially addressed. |
| | | QA5 | backend uses official university APIs and a service-oriented structure, satisfying interoperability fully. |
| | | CON3 | RIA was selected because it supports multi-device access, satisfying this constraint. |
| | | CON5 | A Security Component using university SSO was explicitly instantiated. |
| | | CON8 | Synchronization Service and service-oriented backend integrate only using official APIs. |
| | | CON9 | Three-tier structure provides separation but no deployment/rollback strategy described. |
| | | CRN2 | The AI Interaction Component directly addresses reliability and correctness of AI responses. |
| | CRN3 | | It's an inherent benefit, not a targeted design choice. |
| | CRN5 | | The existence of several partially addressed drivers suggests the architecture is not yet "strong" or "clearly defined" enough to be considered fully complete. |
| | | CRN9 | Communication is structured via APIs between client and backend services. |
