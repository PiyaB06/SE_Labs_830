# Reflection Questions

### 1. Did your estimations reflect the actual effort?
* **Estimation Accuracy:** Overall, story point estimations provided a strong baseline, though initial estimates for complex technical stories slightly underestimated the required effort.
* **Underestimated Complexity:** **Story 6.2 (Zero Ledger Balance Drift)** and **Story 4.2 (Anti-Double-Spending Locking)** required extra effort due to race conditions during concurrent user load testing.
* **Well-Estimated Scope:** Frontend UI integration stories (e.g., viewing balances and browsing the gift card catalog) closely matched their estimated point values.

---

### 2. Was your backlog well-prioritized?
* **Strategic Alignment:** Yes, the backlog prioritized high-value core user journeys before administrative and optimization features.
* **Core First:** High-priority epics covering point aggregation (Epic 1), dynamic conversion (Epic 2), and anti-fraud voucher handling (Epic 4) were completed first to build a working MVP.
* **Secondary Scope:** Merchant administrative tools (Epic 5) and advanced platform optimization (Epic 6) were appropriately scheduled for later stages once core processing was validated.

---

### 3. How did your simulated sprint align with your plan?
* **Velocity Tracking:** The sprint aligned closely with planned velocity, though progress slowed mid-sprint during the implementation of cryptographic checksum validation (Story 4.1).
* **Scope Discipline:** Unplanned scope creep was successfully prevented by keeping advanced merchant analytics (Story 5.4) out of the initial development cycle.
* **Adaptation:** Blockers encountered during dynamic conversion rate testing were resolved by re-allocating developer focus from low-priority UI polish to backend logic.

---

### 4. What insights did the burndown chart give about your team’s capacity?
* **Mid-Sprint Plateau:** The burndown chart revealed a plateau around Days 4–6, highlighting an integration bottleneck when connecting real-time conversion rates to the transaction ledger.
* **Capacity Overestimation:** The initial velocity target was slightly optimistic given the complex cryptographic and financial verification testing required for Problem Statement 34.
* **Predictable Tail-End:** Once core backend dependencies cleared, the burndown rate steepened steadily towards zero, proving that testing and verification capacity stabilized in the final days.