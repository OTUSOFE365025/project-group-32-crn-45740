# Iteration 3:

## Step 2: Pick Drivers and Begin Iteration
This iteration targets the QA-2 scenario. To guide our design choices, we’ll prioritize four areas:  
**Usability:** Students should see information that is correct and tailored to them.

**Availability:** The dashboard must stay up and responsive for at least 99.5% of the month.

**Reliability:** Notifications should be sent accurately and at the right time.

**Performance:** Pages should load fast, and notification requests should be queued quickly.

During normal usage, a student opens their personal dashboard as described in QA-2, system needs to stay responsive and meet a minimum monthly availability of 99.5%, while also ensuring notifications are sent promptly under typical load. In this iteration, we’ll concentrate on faster dashboard response times, smoother notification delivery, and maintaining uptime during everyday use.

---

## Step 3: Refine Elements
For our scenario, the components we’re refining have a direct impact on the dashboard and notification system’s performance, reliability, availability, and usability so we have **DashboardController** and **NotificationManager**.

---

## Step 4: Select Design Concepts That Meet the Chosen Drivers
| Design Decision & Location | Rationale |
|----------------------------|-----------|
| Add caching inside DashboardController | Speeds up page rendering by cutting down repeated database lookups, improving dashboard load time. |
| Make notification fetching asynchronous in NotificationManager | Handles notifications in the background so dashboard requests don’t get stuck waiting. |
| Use load balancing across multiple DashboardController instances | Scales out the controller and spreads incoming traffic across replicas to keep response times low during heavier usage. |

---

## Step 5: Instantiate Components, Assign Responsibilities, and Define Interfaces
| Design Decision & Location | Rationale |
|----------------------------|-----------|
| DashboardCache | Enables the DashboardController to return cached dashboard data faster. |
| AsyncNotificationDispatcher | Sends notifications asynchronously so delivery doesn’t block the main request path. |
| NotificationStatusTracker | Tracks delivery issues or delays in the background without impacting the user interface. |

---

## Step 6: Draft the Architecture Views and Document Design Decisions

### Figure 1. Component View

| Element | Responsibility |
|---------|---------------|
| DashboardCache | Keeps recently produced dashboard results so fewer database calls are needed and pages load faster. |
| AsyncNotificationDispatcher | Sends notifications in the background so dashboard requests aren’t held up. |
| NotificationStatusTracker | Logs delivery outcomes and automatically retries failures without affecting the student’s experience. |

The UML sequence diagram below shows how these components communicate during the QA-2 scenario to support the required behavior.

---

## Step 7: Evaluate the Current Design and Check Progress Toward the Iteration Goal

| Scenario / Constraint | Status | Design outcome from this iteration |
|-----------------------|--------|-----------------------------------|
| QA-1 | Not addressed | This iteration did not include any updates related to authentication or authorization. |
| QA-2 | Partially addressed | Caching and asynchronous notifications improve responsiveness and support availability goals, but specific implementation technologies have not been chosen yet. |
| QA-3 | Not addressed | No additions were made for restart, retry, or synchronization recovery. |
| QA-4 | Not addressed | No changes were made that impact AI-related performance. |
| CON-1 | Partially addressed | Performance-focused updates help meet scalability-related constraints. |
| CON-5 | Partially addressed | Responsiveness improved, but real-time updates were not covered in this iteration. |
| CRN-2 | Partially addressed | The design can support higher request volume, but full scalability work is still pending. |
| CRN-4 | Not addressed | No new mechanisms were added to handle failures in this iteration. |
