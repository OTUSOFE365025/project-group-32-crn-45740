# Quality Attributes

This table summarizes the key quality attributes for our AIDAP, describing the scenarios in which they are evaluated and the associated use cases.

| ID    | Quality Attribute | Scenario | Associated UC |
|-------|-----------------|---------|---------------|
| QA-1  | Performance     | During normal academic operations, numerous students use the AI assistant to inquire about their grades, deadlines, and future events. In this high-volume scenario, such as midterm week, the system executes each query efficiently and gives accurate replies without delay. All requests are expected to be answered within 2 seconds on average. | UC-1, UC-4 |
| QA-2  | Usability       | An international student accesses the AI assistant on their phone and asks a question in their local language. The AI assistant's interface and natural language processing handle the interaction. The goal is met when students receive clear, relevant responses in their preferred language 100% of the time. | UC-1, UC-3 |
| QA-3  | Reliability     | During the system's nightly synchronization process, the link between the AI assistant and an external university database fails briefly. The data synchronization service instantly retries the connection. Synchronization is considered reliable if it is restored within 30 seconds and no data is lost or duplicated. | UC-4 |
| QA-4  | Security        | When a user logs in using the school's single sign-on portal, the system encrypts all communication and ensures each user can access only allowed information. Security is maintained when 100% of login sessions are successfully authenticated and there is no unauthorized access. | UC-2, UC-5 |
| QA-5  | Interoperability | A student or administrator can export assignment or exam dates to an external calendar, and synchronize institutional data with other university systems such as LMS or email servers. The system ensures all data is transmitted accurately and consistently. Interoperability is achieved when 100% of exported events appear correctly on external calendars and data synchronization has a success rate of at least 99%. | UC-4, UC-6 |
