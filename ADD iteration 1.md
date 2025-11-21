# ADD Iteration 1 – Architecture Design

## ADD Step 1: Review Inputs

### Category Details

| Category | Details |
|---------|---------|
| **Design purpose** | This is a greenfield system from a mature domain. The purpose is to produce a sufficiently detailed design to support the construction of the AI-powered digital assistant platform (AIDAP). |
| **Primary Functional Requirements** | **UC1:** Core AI interaction<br>**UC2:** Supports coursework<br>**UC3:** Supports student interaction<br>**UC4:** Supports data synchronization issues |
| **Scenario Id** | **Importance / Difficulty**<br>QA-1 → High / Medium<br>QA-2 → High / High<br>QA-3 → High / High<br>QA-4 → Medium / High<br>QA-5 → High / Medium |
| **Quality Attributes** | QA-1, QA-2, QA-3, and QA-5 are design drivers. |
| **Constraints** | All constraints are part of the drivers. |
| **Concerns** | All concerns are part of the drivers. |

---

## ADD Step 2: Establish Iteration Goal by Selecting Drivers

This iteration aims to establish the overall architecture.

### Quality Attributes
- QA-1: Performance  
- QA-2: Usability  
- QA-3: Reliability  
- QA-5: Interoperability  

### Constraints
- CON-3: Must work across web, mobile, and voice devices  
- CON-5: Authentication via university SSO  
- CON-8: Connect only via official APIs  
- CON-9: Zero-downtime updates + rollback option  

### Concerns
- CRN-2: AI must be dependable  
- CRN-3: Future features must be easily supported  
- CRN-5: Architecture must be clearly defined  
- CRN-9: Components must maintain strong boundaries  

---

## ADD Step 3: Choose Elements of the System to Refine

We refine the entire AIDAP using a **top-down approach**.

---

## ADD Step 4: Choose Design Concepts

| Design Choice | Rationale |
|---------------|-----------|
| **Use RIA (Rich Internet Application) for frontend** | Supports web + mobile (CON-3), improves usability (QA-2), and performance (QA-1). |
| **Discarded: Web Application** | Requires full page reloads; poor UI interactivity. |
| **Discarded: Mobile Application Only** | Fails multi-device constraint (CON-3). |
| **Use Service-Oriented Architecture for backend** | Integrates via APIs (CON-8), supports modularity and interoperability (QA-5). |
| **Discarded: Microservices** | Too complex for iteration 1. |
| **Use Three-Tier Deployment** | Better scalability, security, reliability. |
| **Discarded: Single-Tier** | Weak for modularity and security. |

---

## Step 5: Instantiate Architectural Elements

| Element | Rationale |
|--------|-----------|
| **Synchronization Service** | Ensures dependability (QA-3), handles all external system integrations (CON-8). |
| **Security Component** | Required for SSO (CON-5), controls authentication + authorization. |
| **AI Interaction Component** | Handles AI queries, supports academic responses (UC-1). |
| **Remove isolated client storage** | Prevents exposure of grades/chat history (CON-4), avoids stale data. |
| **Client Data Access Module** | Provides AJAX/Fetch communication; supports real-time dashboards (UC-3). |

---

## Step 6: Sketch Views & Record Decisions

*(Diagrams can be added here if needed.)*

---

## Step 7: Analysis of Design

| Driver | Status | Notes |
|--------|--------|-------|
| UC-1 | ✔️ Complete | Real-time academic responses supported. |
| UC-2 | ⚠️ Partial | No specific lecturer announcement component. |
| UC-3 | ⚠️ Partial | No Notification Service instantiated. |
| UC-4 | ✔️ Complete | Sync service fully handles API integration. |
| QA-1 | ⚠️ Partial | No explicit performance tactics yet. |
| QA-2 | ✔️ Complete | RIA improves usability. |
| QA-3 | ⚠️ Partial | Missing redundancy/failover tactics. |
| QA-5 | ✔️ Complete | Official APIs + service-oriented backend. |
| CON-3 | ✔️ Complete | RIA supports multi-device. |
| CON-5 | ✔️ Complete | SSO component instantiated. |
| CON-8 | ✔️ Complete | Sync service uses official APIs. |
| CON-9 | ⚠️ Partial | No rollback strategy defined. |
| CRN-2 | ✔️ Complete | AI Interaction Component improves reliability. |
| CRN-3 | ⚠️ Partial | Extensibility is possible but not targeted. |
| CRN-5 | ⚠️ Partial | Several drivers still partial—architecture not fully strong. |
| CRN-9 | ✔️ Complete | Clear API-based boundaries. |
