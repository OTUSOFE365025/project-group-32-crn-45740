# ATAM Assessment Phase 3

## 1. ATAM risk assessment table

| Scenario Component     | Description                                                                                           |
| :--------------------- | :-------------------------------------------------------------------------------------------------- |
| **Scenario**           | A student initiates a dashboard session immediately following the broadcast of a new system announcement. |
| **Quality Attributes** | Performance, Reliability, Availability, Usability                                                  |
| **Stimulus**           | User triggers a read request for the personalized dashboard view.                                   |
| **Environment**        | Standard operational runtime conditions.                                                            |
| **Response**           | The system retrieves the view from the `DashboardCache` to minimize latency, while notification retrieval is enqueued for asynchronous background processing. |

### Architectural Decision Analysis

| Architecture Decision                           | Sensitivity | Tradeoff     | Risk       | Non‑Risk |
| :--------------------------------------------- | :----------:| :----------- | :--------- | :------- |
| **AD1** – Implementation of server-side `DashboardCache`     | S1, S3      | T1           | R1         | N2       |
| **AD2** – Integration of dedicated `NotificationManager`      | S2          | T2           | R2         | N1       |
| **AD3** – Utilization of asynchronous delivery mechanisms      | S2          | T2, T3       | R2, R3     | N3       |
| **AD4** – Orchestration via `DashboardController`             | —           | —            | —          | N1       |


## 2. Description of the risks, non-risks, sensitivity, and tradeoffs

### Architectural Decisions 
| AD ID | Decision | Simple Explanation |
|:-----:|:---|:---|
| **AD1** | Add DashboardCache | We are adding a temporary memory storage (cache) so the dashboard loads faster. |
| **AD2** | Add NotificationManager | We are creating a specific tool just to handle sending alerts to users. |
| **AD3** | Use async notification retrieval | We will load notifications in the background so the screen doesn't freeze while waiting for them. |
| **AD4** | DashboardController prompts notifications | The main dashboard program is in charge of telling the system when to show alerts. |

### Architectural Risks 
| ID | Risk | Simple Explanation |
|:--:|:---|:---|
| **R1** | No refresh rules defined | We haven't decided exactly when to throw away old data yet, so users might see stale info. |
| **R2** | Queue failure | If the system that lines up the messages breaks, some users might never get their alerts. |
| **R3** | No backup plan for Cache | If the speed-memory tool breaks, we don't have a "Plan B" to keep things running smoothly. |

### Architectural Non-Risks  
| ID | Non-Risk | Simple Explanation |
|:--:|:---|:---|
| **N1** | Separation of Concerns | Because we split the dashboard and the alerts into different parts, one won't drag the other down. |
| **N2** | Server-side Security | Keeping the saved data on our server is fast, and it keeps secret information away from the user's computer. |
| **N3** | Background Processing | Because alerts happen in the background, the screen stays clickable and smooth even if there are a million alerts coming in. |

### Sensitivity Points 
| ID | Sensitivity Point | Simple Explanation |
|:--:|:---|:---|
| **S1** | Performance depends on Cache | If the temporary memory (cache) stops working, the whole system will get slow. |
| **S2** | Responsiveness depends on Async vs. Sync | The dashboard will only feel fast if we successfully load alerts in the background. |
| **S3** | Accuracy depends on Refresh rules | If we don't update the saved data often enough, users will see wrong information. |

### Tradeoffs
| ID | Tradeoff | Simple Explanation |
|:--:|:---|:---|
| **T1** | Speed vs. Freshness | Saving data (caching) makes the site fast, but sometimes users might see data that is a few seconds old. |
| **T2** | Smoothness vs. Difficulty | Loading things in the background makes the app feel better to use, but it is harder for programmers to build. |
| **T3** | Heavy Load vs. Accuracy | Saving data very aggressively helps handle lots of users at once, but the data might not be 100% up-to-date. |

## 3. ATAM utility tree

![Utility Tree](https://www.plantuml.com/plantuml/png/TPFVQnD14CVVyrSCYD26gct1GAL8szIWq8eQgozzcUvESaFtnpapsv9A_tTtqwESY0yBDz_R-tnsPxWJDHIBd7p4VdAijWdqVZBKvunhmGY_9m0fUze-09oXkrrBBidFSyW2BpxC5eUBnVRTqYJVqf3lxyzcy_asN-Hadp4Id0fZgD5ZNUyyzTRjxEyEu37w7yG0USf_TcmqIfVyG70m6oVj9d2MW_zRTb1b_z_sE3b-C_HWCeKhuy2scKodS7g77F1cg6km9BbZHp2l44vbYAUmyt7lOXUM6pMA496JrQLmTFJwxSlhb7iIDCu90vJUE1Ba10YnKhgmWHjKrkRxGhBA4Z4vgcMj9JjIvRI6xvtaikxwOeFnSkzo5qu3YIcW46XnRU-gX4gazAjG8N-TxjawRhA3Lqek9m_M2MdNxjuutqZxd9JW0esIUxvFev-ZTZSPnODGyYJj72x7Ff2HFgCFuGciKDecKCFasqSXOtKqHU1n4oz95TS4dvBHMcewTdvjvmOKrsRjh0W19ItIX0ya6JmQLhGg-B8zaGacZQpAEJNTbOvbFvZkOLxKSkI7xH2U-rSdrkP8oO0LqBaYQ5Ixj-9W9ArxTJBasx2q9yShTb2K1DXJicOueUI7t-OF)
