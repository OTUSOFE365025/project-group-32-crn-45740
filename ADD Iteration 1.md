# ADD Iteration 1 — AIDAP

## Table of Contents
- [Step 1: Review Inputs](#step-1-review-inputs)
- [Step 2: Select the Drivers](#step-2-select-the-drivers)
- [Step 3: Choose Elements to Refine](#step-3-choose-elements-to-refine)
- [Step 4: Select Design Concepts](#step-4-select-design-concepts)
- [Step 5: Instantiate Architectural Elements](#step-5-instantiate-architectural-elements)
- [Step 6: Sketch Views](#step-6-sketch-views)
- [Step 7: Analysis](#step-7-analysis)

---

## Step 1: Review Inputs

### Design Purpose and Requirements

| Category | Details |
| :--- | :--- |
| **Design Purpose** | This is a greenfield system from a mature domain. [cite_start]The purpose is to produce a sufficiently detailed design to support the construction of the AI-Powered Digital Assistant Platform (AIDAP)[cite: 7]. |
| **Primary Functional Requirements** | [cite_start]**UC1:** Because it represents core lecturer workflows.<br>**UC2:** Because it represents core student interaction [cite: 9][cite_start].<br>**UC3:** Because of the technical issues associated with data synchronization[cite: 9].<br>**UC5:** Because it represents the core AI interaction capability of the system. |

### Quality Attribute Scenarios

| Scenario ID | Importance to the Customer | Difficulty of Implementation according to Architect |
| :--- | :--- | :--- |
| **QA1** | [cite_start]High [cite: 14] | [cite_start]High [cite: 25] |
| **QA2** | [cite_start]High [cite: 16] | [cite_start]Medium [cite: 24] |
| **QA3** | [cite_start]High [cite: 18] | [cite_start]High [cite: 26] |
| **QA4** | [cite_start]High [cite: 14] | [cite_start]High [cite: 27] |
| **QA5** | [cite_start]Medium [cite: 20] | [cite_start]Medium [cite: 28] |

[cite_start]**Selection:** From this list, QA1, QA2, QA3, and QA4 are selected as drivers[cite: 29].

### Constraints & Concerns
[cite_start]All of the constraints and architectural concerns discussed are included as drivers in the following step[cite: 30, 31].

---

## Step 2: Select the Drivers

[cite_start]This is the first iteration in the design of a greenfield system[cite: 33]. The architect keeps in mind all of the drivers that influence the general structure of the system; however, the architect must be mindful of the following:

### Quality Attributes
* [cite_start]**QA-1:** Security, Usability, Performance[cite: 35].
* [cite_start]**QA-2:** Performance, Reliability, Availability, Usability[cite: 36, 37].
* [cite_start]**QA-3:** Reliability, Interoperability[cite: 38].
* **QA-4:** Performance, Usability.

### Constraints
* **CON-1:** System must be deployed in the cloud and scale with the number of users.
* [cite_start]**CON-2:** System must connect to external university systems through standard APIs[cite: 42].
* [cite_start]**CON-5:** Dashboards must provide real-time data and be responsive on both web and mobile[cite: 41].
* **CON-8:** The AI responses must be generated within approximately two seconds.

### Concerns
* **CRN-2:** System must remain scalable even under increasing load.
* **CRN-3:** Strong access control must be enforced all over.
* **CRN-4:** Integration with external university systems must be reliable.
* **CRN-7:** Personalization must be supported using stored interaction history.

<br>

> **[Insert Figure 1: Context Diagram of AIDAP System Here]**
>
> *Figure 1. Context Diagram of AIDAP System*

---

## Step 3: Choose One or More Elements of the System to Refine

[cite_start]We will refine the **entire system** in Iteration 1 because it is a greenfield system[cite: 61].

---

## Step 4: Choose One or More Design Concepts that Satisfy the Selected Drivers

### Design Decisions

| Design Decisions and Location | Rationale |
| :--- | :--- |
| **Logically structure the client part using the Rich Internet Application (RIA) reference architecture** | [cite_start]The RIA reference architecture allows AIDAP to run directly in the browser without installation and still provides a rich user responsive interface[cite: 65]. It supports web and mobile dashboards (**CON-5**) and keeps interactions fast and usable (**QA-2, QA-4**). [cite_start]It also allows for interactive dashboards and features from the browser (**UC-2, UC-5**) which involves processing on the client side[cite: 65]. This helps the system stay responsive even under heavy load. |
| **Logically structure the server using a Service-Based Application architecture** | A service-based backend is selected because the AIDAP server does not include its own user interface. [cite_start]This separates the major responsibilities such as authentication, dashboard generation, AI processing, and data synchronization, and it supports integration with external university systems using the standard APIs (**CON-2, UC-3**)[cite: 65]. It also helps keep the system reliable and have fast AI responses (**QA-3, QA-4**). |
| **Physically structure the system using a Three-Tier Deployment Pattern** | [cite_start]A three-tier structure is selected because AIDAP will run in the cloud and must scale as the number of users grows (**CON-1**), and also keep academic data stored securely in the database layer (**CON-3**)[cite: 66]. [cite_start]This deployment supports availability and reliability (**QA-3**) and keeps responsibilities clearly separated; the client focuses on interaction, the application tier handles AI and synchronization logic, and the database tier manages persistent records[cite: 66]. |
| **Deploy the system as a Cloud-Hosted Web Service** | Cloud deployment satisfies **CON-1**. It also simplifies integration with external university systems (**CON-2**) and supports the performance requirements of the AI component (**QA-4**). |
| **Use API-Based Integration for Communication with External University Systems** | [cite_start]The system needs to connect to LMS, registration, and calendar systems through standard APIs (**CON-2**)[cite: 42]. [cite_start]Using API connectors creates a clear separation between AIDAP and those external systems, and it helps keep data synchronization reliable by allowing retry logic when something temporarily fails (**QA-3, UC-3**)[cite: 65]. |

### Discarded Alternatives

| Discarded Alternative | Reason for Discarding |
| :--- | :--- |
| **Web-application** | [cite_start]This reference architecture focuses on server-side rendering and requires full page refreshes[cite: 65]. This makes it difficult to provide a rich user interface with real-time updating dashboards. |
| **Mobile Application** | [cite_start]The system needs to work the same way on laptops and browsers too, not just on phones[cite: 65]. Lecturers are more likely to use computers for publishing course material, so limiting AIDAP to mobile would prevent consistency across platforms. |
| **Microservices Architecture** | [cite_start]Although microservices is scalable, it adds complexity for Iteration 1, and the drivers can be achieved using a simpler service-based structure[cite: 65]. |

---

## Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

| Design Decision and Location | Rationale |
| :--- | :--- |
| **Instantiate a Client Data Access Module in the RIA client** | [cite_start]A dedicated module is added to the client to manage all communication with the application tier[cite: 70]. Using AJAX/Fetch API calls, the module communicates with the backend ensuring real-time dashboard updates, without requiring full page refreshes. [cite_start]This keeps the UI focused on interaction rather than data handling and avoids storing academic information locally[cite: 70]. It also supports **UC-2** by allowing dashboards to load data on demand without mixing presentation logic and data retrieval. |
| **Instantiate a Synchronization Service in the application tier** | [cite_start]A separate component is used to manage the connections with external university systems, as required by **CON-2** and **UC-3**[cite: 69]. This separates integration logic for future improvements in reliability. |
| **Instantiate a Security Component for authentication and authorization** | [cite_start]Because users can only access data they are allowed to see, an early security component is needed to manage login and permissions (**CRN-3**)[cite: 69]. Detailed interfaces will be defined in later iterations. |
| **Instantiate an AI Interaction Component in the application tier** | [cite_start]To support **UC-5**, a component is added to handle communication with the AI model and separate conversational logic from other services[cite: 69]. |

---

## Step 6: Sketch Views and Record Design Decisions

### Module View

<br>

> **[Insert Figure 2: Module View of AIDAP System Here]**
>
> *Figure 2. Module View of AIDAP System*

<br>

| Element | Responsibility |
| :--- | :--- |
| **Chatbot UI** | [cite_start]Displays the chat messages and also handles the user inputs and outputs for the conversation queries, sending them to the backend[cite: 86]. |
| **Dashboard** | [cite_start]The dashboard shows personalized data like the grades, schedules and important announcements[cite: 78]. |
| **Client Data Processor** | [cite_start]Manages the client side data logic, like validating user input, handling the sessions, formatting requests before they get sent to the API, and also managing language and preference settings[cite: 80]. |
| **Local Cache** | [cite_start]Temporarily stores any recent messages, announcements, and dashboard data for quick and offline access, or under weaker network conditions[cite: 82]. |
| **API Gateway** | [cite_start]The main entry point in between the client and the server, receives API requests, validates them and directs them through the backend, all while maintaining security[cite: 84]. |
| **Message Handler** | [cite_start]Manages how the messages and data are exchanged between the client and backend by structuring and interpreting the API requests as well as the response formats[cite: 91]. |
| **Interaction Controller** | [cite_start]Coordinates client requests to the appropriate business module, it also coordinates workflows between the different backend components that exist[cite: 92]. |
| **Chat Flow Manager** | [cite_start]Keeps track of context, manages the dialogue flow, and makes sure that the user interactions are consistent[cite: 93]. |
| **AI Execution Engine** | [cite_start]Runs the AI and natural language processing logic responsible for interpreting user questions and generating responses using the stores and live data[cite: 94]. |
| **Data Entities** | [cite_start]Represent the core business entities like users, courses, schedules, and announcements[cite: 95]. |
| **Data Access Module** | [cite_start]Manages the connection between the business logic and the database, performing all the data retrieval and updates in a secure way; this includes reading, writing, updating user data, logging chats, etc.[cite: 97]. |
| **Helpers and Utilities** | [cite_start]Provides the shared helper functions such as error handling, data validation, and logging, these are used across multiple layers to help keep the code clean and support backend operations[cite: 98]. |
| **AI Service Agent** | [cite_start]Connects the AIDAP with the external university systems like the LMS, calendar, registration, and email platforms to both sync and recover data from failed connection attempts[cite: 99]. |

### Deployment View

<br>

> **[Insert Figure 3: Initial Deployment Diagram for the FCAPS system Here]**
>
> *Figure 3. Initial deployment diagram for the FCAPS system*

<br>

| Element | Responsibility |
| :--- | :--- |
| **User Device (web/mobile browser)** | Hosts the client side application that is used by students and lectures to access AIDAP on a web or mobile browser. [cite_start]Uses HTTPS to send requests to the server[cite: 109, 113]. |
| **AIDAP Application Server (cloud-deployed)** | Hosts all the server-side business logic, including service interfaces, the API gateway, security, and all iteration components. Handles dashboard display and rendering, notifications, AI interaction, and manages synchronization. [cite_start]Checks requests for routing to external systems[cite: 110, 114]. |
| **Cloud Database Server** | Stores external system’s synchronized information, user profiles, dashboard data, interaction history with the AI model, notification preferences. [cite_start]Accessed through SQL/ORM using the application server[cite: 105]. |
| **LMS System** | [cite_start]LMS system is one of the external university learning platforms from which the AIDAP system retrieves the course assignments, materials, grades and analytics using REST API[cite: 107]. |
| **Registration System** | [cite_start]An external system that provides academic enrollment records, and course registration information retrieved by the AIDAP using REST API[cite: 115]. |
| **Calendar System** | [cite_start]External calendar that provides academic deadlines, events and schedules that AIDAP syncs using REST API[cite: 118]. |
| **Authentication System** | [cite_start]External identification checker, that verifies user credentials allowing for secure login before accessing the AIDAP[cite: 119]. |

### Reference Architecture

<br>

> **[Insert Figure 4: Reference Architecture Diagram for the FCAPS system Here]**
>
> *Figure 4. Reference Architecture diagram for the FCAPS system*

<br>

| Relationship | Description |
| :--- | :--- |
| **Between User Device and AIDAP Application Server** | [cite_start]Communication takes place over secure HTTPS for all client–server requests[cite: 111]. |
| **Between AIDAP Application Server and Cloud Database Server** | [cite_start]The server communicates with the cloud database using SQL and ORM for storing and retrieving any academic data[cite: 106]. |
| **Between AIDAP Application Server and LMS System** | [cite_start]Integration is done using the REST APIs to fetch the course materials, grades, and analytics[cite: 108]. |
| **Between AIDAP Application Server and Registration System** | [cite_start]The AIDAP retrieves the enrollment and course registration data using REST APIs[cite: 112]. |
| **Between AIDAP Application Server and Calendar System** | [cite_start]The AIDAP retrieves the academic events and schedules by using REST APIs[cite: 112]. |
| **Between AIDAP Application Server and Authentication System** | [cite_start]Login authentication is performed using an Auth API[cite: 117]. |

---

## Step 7: Perform Analysis of Current Design

Review Iteration Goal and Achievement of Design Purpose.

| Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made During the Iteration |
| :--- | :--- | :--- | :--- |
| | | **UC-1** | [cite_start]The RIA client architecture properly supports uploading any content & viewing analytics functionalities[cite: 152]. |
| | | **UC-2** | [cite_start]Fully supported through the responsive web/mobile dashboard that is implemented[cite: 152]. |
| | **UC-3** | | [cite_start]Partially supported because synchronization components do exist but the retry and conflict resolution are not defined yet[cite: 152]. |
| | | **UC-5** | [cite_start]Fully supported by the AI Execution Engine and the Chat Flow Manager[cite: 152]. |
| | **QA-1** | | Partially supported because the Security Component isn’t defined yet. [cite_start]The API Gateway makes the access controlled and reliable and the RIA architecture ensures that the interface stays fast and also user-friendly[cite: 152]. |
| | **QA-2** | | [cite_start]The RIA client, cloud deployment, and separation of concerns improves responsiveness and helps dashboards load quickly, but the iteration has not yet defined consistent performance guarantees[cite: 152]. |
| | **QA-3** | | [cite_start]Partially supported since reliability is addressed conceptually but the failure recovery is not designed yet[cite: 153]. |
| | **QA-4** | | AI processing is isolated in its own component, which helps keep responses fast and helps improve usability, but the specific performance guarantees have not been defined yet. |
| | | **CON-1** | [cite_start]Designing the system with a three-tier deployment with client, application, and database layers supports scaling in the cloud environment[cite: 153]. |
| | | **CON-2** | [cite_start]Fully satisfied through API integration and synchronization components for the external systems[cite: 153]. |
| | **CON-3** | | [cite_start]A Security Component was added to manage login and access control, however, the detailed role based permissions and secure session handling are not defined yet[cite: 153]. |
| | **CON-4** | | The system includes notification handling, and notification preferences are stored in the database. However, specific notification delivery rules are not designed yet. |
| | | **CON-5** | [cite_start]Fully satisfied using the RIA architecture, and responsive dashboard[cite: 153]. |
| | **CON-6** | | [cite_start]A Synchronization Service and API based integration were created, allowing for data syncing, but retry handling and conflict handling have not been defined yet[cite: 153]. |
| | **CON-7** | | The Security Component and Data Access Module provide a secure boundary for retrieving student data, but detailed rules have not been defined yet. |
| | **CON-8** | | Partially addressed because the AI is isolated for faster responses, but the performance guarantees and load-balancing are not specified or defined yet. |
| **CON-9** | | | [cite_start]No relevant decisions made[cite: 153]. |
| **CON-10** | | | No relevant decisions made. |
| **CON-11** | | | No relevant decisions made. |
| **CON-12** | | | No relevant decisions made. |
| **CRN-1** | | | No relevant decisions made. |
| | | **CRN-2** | [cite_start]The cloud based deployment and the service based backend allow the components to scale as the usage continues to grow[cite: 153]. |
| **CRN-3** | | | [cite_start]No relevant decisions made[cite: 153]. |
| | **CRN-4** | | The system supports reliable external communication, but decisions for retries and handling failures are still to be implemented. |
| **CRN-5** | | | [cite_start]No relevant decisions made[cite: 153]. |
| **CRN-6** | | | No relevant decisions made. |
| | **CRN-7** | | The interaction history will be stored, but the decision of how personalization will work from a user perspective has not been designed yet. |
| | | **CRN-8** | The RIA architecture ensures very consistent interface behavior across browsers and devices. |
| **CRN-9** | | | [cite_start]No relevant decisions made[cite: 153]. |
