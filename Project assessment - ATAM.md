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


## 3. ATAM utility tree

![Utility Tree](https://www.plantuml.com/plantuml/png/TPFVQnD14CVVyrSCYD26gct1GAL8szIWq8eQgozzcUvESaFtnpapsv9A_tTtqwESY0yBDz_R-tnsPxWJDHIBd7p4VdAijWdqVZBKvunhmGY_9m0fUze-09oXkrrBBidFSyW2BpxC5eUBnVRTqYJVqf3lxyzcy_asN-Hadp4Id0fZgD5ZNUyyzTRjxEyEu37w7yG0USf_TcmqIfVyG70m6oVj9d2MW_zRTb1b_z_sE3b-C_HWCeKhuy2scKodS7g77F1cg6km9BbZHp2l44vbYAUmyt7lOXUM6pMA496JrQLmTFJwxSlhb7iIDCu90vJUE1Ba10YnKhgmWHjKrkRxGhBA4Z4vgcMj9JjIvRI6xvtaikxwOeFnSkzo5qu3YIcW46XnRU-gX4gazAjG8N-TxjawRhA3Lqek9m_M2MdNxjuutqZxd9JW0esIUxvFev-ZTZSPnODGyYJj72x7Ff2HFgCFuGciKDecKCFasqSXOtKqHU1n4oz95TS4dvBHMcewTdvjvmOKrsRjh0W19ItIX0ya6JmQLhGg-B8zaGacZQpAEJNTbOvbFvZkOLxKSkI7xH2U-rSdrkP8oO0LqBaYQ5Ixj-9W9ArxTJBasx2q9yShTb2K1DXJicOueUI7t-OF)
