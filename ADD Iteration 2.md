### Iteration 2

Establishing a general system structure was our aim for the initial iteration. After achieving this objective,
our new objective for this second iteration is to consider the units of implementation, which have an
impact on interfaces, team formation, and the ways in which development activities can be assigned,
outsourced, and carried out in sprints.

### STEP 2:

Finding structures that support primary functionality is a general architectural concern that iteration 2
addresses.

In this second iteration the architect considers the system's primary use cases:
- UC-1
- UC-2
- UC-3
- UC-4

### STEP 3:

In this iteration, the components that will be improved are the modules found in the distinct layers that the
two reference architectures from the prior cycle defined. Generally speaking, the functionality of the
system is supported by the elements connected to modules located in various tiers

### STEP 4:

| Design Decisions and Location | Rationale |
| :--- | :--- |
| Implement a domain model for AIDAP | An initial domain model for the system must be created before beginning a functional decomposition. Users, courses, materials, announcements, timetables, chat sessions, interaction history, external systems, and notifications are the primary entities of AIDAP. In the absence of this, the domain structure would be developed ad hoc. |
| Figure out the domain objects that map to the functional requirements | At least one domain object that the system interacts with is linked to each of the main use cases and unique functional components. |
| Decompose domain object sin to general components | Every domain object is broken down into modules across levels. While the server manages business logic and database storage, the client manages user interaction (screens and request formats). This division makes the system simpler to modify and comprehend. Decomposing the layers into modules to provide functionality is the only viable option. |
| between the client and API Gateway, Use REST/JSON-based APIs | One popular formatting tool is REST/JSON. The client and server are clearly separated when REST/JSON is used. Because their interactions occur through API requests and answers, this facilitates correct integration with external systems and the AI service, making it simpler to update or test the individual modules. Since they would add complexity at this point, alternatives were not taken into consideration. |

### STEP 5:

| Design Decision | Rationale |
| :--- | :--- |
| Create a basic data map (domain model) | We identify the main things the system needs like users, courses, schedules, and notifications and create a basic map of them now. We do not need to wait for the whole project to be finished to start this. |
| Match main tasks to data items | We look at the main things users will do (like students talking to the AI or instructors managing classes) to figure out what data "objects" we need. This helps us organize and share information clearly |
| Split data across system layers | We break the big data objects down to see exactly what features belong in which "layer" of the software. This helps us make sure the different layers talk to each other correctly. |
| Use standard web connections (REST/JSON APIs) | We use a standard communication style (request and response). This allows all parts of the system to talk to each other easily and lets us fix or change one part without breaking the others. |
| Connect outside systems to specific modules | We handle the connections to outside school systems (like the calendar or class registration) specifically inside the AI Service Agent and synchronization tools to keep them organized. |

| Element | Methods | Description |
| :--- | :--- | :--- |
| User | Query Academic Info() | Initiates the request to query academic information and later receives and views the results. |
| Dashboard | PrepareQuery() UpdateUI() | Receives user input, triggers query preparation, and updates the interface with returned results. |
| Client Data Processor | PrepareQuery() sendQueryRequest() | Processes and formats the user's query, then sends the request to the server. |
| API Gateway | sendQueryRequest() validateSession() formalRequest() receiveData() | First entry point on the server; validates session, forwards the request to Security, and later receives data to send back to the client. |
| Security | validateSession() sessionValid (response) | Verifies the user's session/token and approves the request before passing it forward |
| Message Handler | processInformationRequest() streamResponse() | Interprets the validated request, prepares it for business logic, and streams the response back. |
| Interaction Controller | fetchRequestedData() formalResponseData() | Orchestrates retrieval of requested data and returns formatted results upward. |
| Data Access Module | executeSelectQuery() | Executes the actual database query and returns a result set. |
| Database | executeSelectQuery() | Stores academic information and returns the requested dataset when queried. |

This is the class diagram

![Diagram 1](https://private-us-east-1.manuscdn.com/sessionFile/So1bponG8mWPZkdYXrKUQT/sandbox/T14lIWiU3bfQjHSxT8X03u-images_1763699546983_na1fn_L3RtcC9wZGZfaW1hZ2VzLzIvMDA1.webp?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvU28xYnBvbkc4bVdQWmtkWVhyS1VRVC9zYW5kYm94L1QxNGxJV2lVM2JmUWpIU3hUOFgwM3UtaW1hZ2VzXzE3NjM2OTk1NDY5ODNfbmExZm5fTDNSdGNDOXdaR1pmYVcxaFoyVnpMekl2TURBMS53ZWJwIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=BV7Id7JzfGqeu5tmmlnnCCfNHar57k4xeHboF8c6jvkEhhv7wmYwaUXOqlrFL07y1bCI~dvvPlACDc8eqSr~47bWNM3Fi2jvxzg7BtlFR-x7Ompij-MTT7PAgtvWkxwi5ozMuazcvm7uDqXp2KdPwUimgBibACaRm7QqITaGF7YHAqDJuB0hAqwiIjkChVc7o49VWKaN9gYJC-Yh9wYpnTDrtYhX4qmoqtC0RzZ81geLrDtn~PKVXioM7m~kyY~5DzGlm~w5yNEb2Jnvk~DXKjNSvR7kUkoxZFmFBROUxYWy6GexXdwqTqh7AgkiBCntU8JZtkiGJ9-bDEhA8emd7g__)

This is the system arch layered design

![Diagram 2](https://private-us-east-1.manuscdn.com/sessionFile/So1bponG8mWPZkdYXrKUQT/sandbox/T14lIWiU3bfQjHSxT8X03u-images_1763699546985_na1fn_L3RtcC9wZGZfaW1hZ2VzLzIvMDA3.webp?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvU28xYnBvbkc4bVdQWmtkWVhyS1VRVC9zYW5kYm94L1QxNGxJV2lVM2JmUWpIU3hUOFgwM3UtaW1hZ2VzXzE3NjM2OTk1NDY5ODVfbmExZm5fTDNSdGNDOXdaR1pmYVcxaFoyVnpMekl2TURBMy53ZWJwIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=hgPec732TzSHrw9uVCbiGStA5Dtg-JtkeMuTn0R88DtMZ7MlDPTppG41o7rbhzr7F7w5-wmBCjYUuQELRtfsE8LRSRLfMTHXKGhZuk4T1N1bmIjF7CPt5rl9ORci-AbwraA5wn6E5gDLuzzFtlV0pNJY~pv81hE6gKokL8DjLRY88UtzxjqxAA1ffqvWnBRjx1cnh9MIcrL2VcYv7Mo8nErCRb48LiFrZYt2y6JlSPt421GYr5cKy6Dn9NTmIkfVi6cKYBuMxgJP5pviOLNV5HIKlEJ0bZo7~slZTIkud4GB7U0xJEuJyRiCjboAUkc1M0V5SiBSe5vSdDjwaYD1ww__)

| Element | Method | Description |
| :--- | :--- | :--- |
| Lecturer (Actor) | write announcement & click post | Starts the process by composing a course announcement and submitting it. |
| Dashboard | packageAnnouncement() showSuccessAlert() | Collects announcement input, prepares the announcement package, and displays success notification after completion. |
| Client Data Processor | packageAnnouncement() sendPublishRequest() | Packages the announcement data into a structured request and sends it to the server via API Gateway. |
| API Gateway | sendPublishRequest() authenticateLecturer() processPublishReq() | Entry point on the server; verifies lecturer identity and forwards the validated publish request to the Interaction Controller. |
| Security | authenticateLecturer() authOK | Authenticates the lecturer before allowing the announcement to be processed. |
| Interaction Controller | processPublishReq() saveAnnouncement() broadcastToCourse() | Handles the incoming publish request, stores the announcement, and passes it to Communication Manager for broadcasting. |
| Data Access Module | insertPost() | Executes the SQL insert operation to save the announcement into the database. |
| Database | Accessed through insertPost() | Stores the announcement and returns confirmation that the save operation succeeded. |
| Communication Manager | broadcastToCourse() notificationsQueued | Queues notifications to all enrolled students or course participants after the announcement is saved successfully. |

| Element | Method | Description |
| :--- | :--- | :--- |
| Student (Actor) | | End user who receives automated alerts on their device; does not initiate the process. |
| Scheduler / Timer | triggerRoutineCheck() checkComplete | Periodically triggers the automated notification cycle and signals completion once all alerts are processed. |
| Notification Manager | getUpcomingDeadlines() getUserPreferences() filterAndPersonalize() sendPushNotification(userID, message) | Central logic component; retrieves deadlines, fetches user preference data, applies personalization filters, and dispatches push notifications to each relevant user. |
| Data Access Module | queryEvents() queryPrefs() | Queries the database for upcoming events and user notification preferences. |
| Database | Accessed through queryEvents() and queryPrefs() | Stores events, deadlines, and user preference records; returns requested data to the system. |
| Communication Manager | push alert to device | Sends the personalized notification to the student's device and confirms successful delivery. |

| Element | Method | Description |
| :--- | :--- | :--- |
| Maintainer (Actor) | send email/SMS alert | Notified only when sync fails; receives alerts about data synchronization issues. |
| Data Source Systems (Actor) | requestLatestAcademicData() | External systems that provide updated academic data to the server upon request. |
| Scheduler / Timer | initiateSyncJob() jobFinish | Triggers synchronization at scheduled intervals and finalizes the sync process. |
| Synchronization Manager | initiateSyncJob() requestLatestAcademicData() parseAndValidate() updateLocalRecords() alertMaintainer(errorLog) | Coordinates the sync: requests updated data, validates incoming data, updates local records, and alerts the maintainer in case of failure. |
| Data Access Module | batchUpsert() | Writes or updates multiple database records in bulk during synchronization. |
| Database | Accessed through batchUpsert() | Stores academic datasets and confirms successful commit operations. |
| Communication Manager | send email/SMS alert | Notifies the maintainer in case of sync failure, sending alerts according to system configuration. |

| Not addressed | Partially addressed | Completely addressed | Justification |
| :--- | :--- | :--- | :--- |
| | | UC-1 | Yes. A full sequence diagram for this use case was created. |
| | | UC-2 | Yes. A full sequence diagram for this use case was created. |
| | | UC-3 | Yes. A full sequence diagram with a Scheduler was created. |
| | | UC-4 | Yes. A full sequence diagram with a Synchronization Manager was created. |
| | | QA-1 | No design decisions for performance were made in Iteration 2. |
| | | QA-2 | No design decisions for performance were made in Iteration 2. |
| | | QA-3 | An error-handling path was defined for data sync, but not for other areas. |
| | | QA-5 | No design decisions for performance were made in Iteration 2. |
| | | CON-3 | No new design decisions for multi-device support were made. |
| | | CON-5 | No new design decisions for SSO authentication were made. |
| | | CON-8 | No new design decisions for API integration were made. |
| | | CON-9 | No design decisions for deployment or rollback were made. |
| | | CRN-2 | No new design decisions for AI correctness were made. |
| | | CRN-3 | Yes. The system was decomposed into specific layers and components. |
| | | CRN-5 | Yes. Detailed diagrams for all primary use cases were produced. |
| | | CRN-9 | No new design decisions for component boundaries were made. |
