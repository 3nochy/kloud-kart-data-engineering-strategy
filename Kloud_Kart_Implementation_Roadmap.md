# Kloud Kart: 12-Month Implementation Roadmap

**Prepared for:** Nana Adjei, Head of Operations  
**Date:** 13 November 2026

## Objective

Establish reliable, controlled reporting without compromising production performance. Plan capacity around a provisional 15–20% annual order-growth assumption, to be validated against actual business trends. Deliver daily reporting for standard business measures and near-real-time updates for inventory reporting.

| Quarter | Priority and key activities | Outcomes Nana can verify |
|---|---|---|
| **Q1: Investigate and agree** | Assign an owner to the customer-data complaint and verify the applicable response requirements. Inventory customer-data copies. Investigate both website slowdowns. Establish baselines for reporting effort, performance, report discrepancies, inventory freshness, and infrastructure cost. Agree revenue and order definitions. | A documented complaint action log; customer-data copy register with unresolved locations identified; slowdown investigation findings; approved metric definitions; and a baseline report. |
| **Q2: Protect and build the foundation** | Test and implement an approved reporting replica or separate reporting environment. Select and configure a small managed cloud data warehouse. Define access, retention, and data-minimisation controls. Implement an initial consistent snapshot followed by incremental extraction. | Evidence that reporting has been separated from production where technically appropriate; documented performance and recovery tests; approved architecture and access controls; and a successful initial data load with reconciliation results. |
| **Q3: Automate and validate** | Implement daily batch pipelines for orders, payments, customer reporting, and agreed management measures. Implement the scoped near-real-time inventory reporting feed using an appropriate change-data-capture approach. Automate the priority Monday reports. Apply checks for completeness, accuracy, consistency, timeliness, validity, and uniqueness. | Repeatable reports using approved definitions; documented load and reconciliation results; visible failed-load alerts and assigned owners; measured inventory update delay; and a comparison of reporting effort against the Q1 baseline. |
| **Q4: Measure and optimise** | Compare results with Q1 baselines. Review reliability, data controls, staff effort, and total platform costs. Test capacity against actual order growth and the provisional 15–20% annual growth assumption. Decide whether a limited demand-forecasting pilot is justified. | A results report showing changes in reporting effort, unexplained discrepancies, website performance, inventory freshness, and infrastructure cost; a capacity review; and a documented decision to proceed with, defer, or reject forecasting. |

## Ownership

- **Nana Adjei:** Business priorities, metric-definition approval, and quarterly outcome review.
- **Data Engineer:** Extraction, pipelines, warehouse reliability, monitoring, and technical data controls.
- **Analytics Engineer / BI Developer:** SQL transformations, reporting definitions, quality checks, and reconciliation.
- **PHP/MySQL developer:** Production database changes, application performance, and coordination of operational-system integration.
- **Designated privacy or compliance owner:** Customer-data complaint handling and confirmation of applicable obligations.

## Delivery and Decision Controls

1. Production MySQL remains authoritative for orders, checkout, stock reservation, and operational inventory decisions.
2. Standard management reporting refreshes daily. Inventory reporting is the only initially approved near-real-time exception.
3. No report is published silently after a failed quality check; the failure must be visible and assigned for resolution.
4. Infrastructure spending and cost per reporting workload are reviewed regularly. Any budget thresholds must be approved by management.
5. Forecasting is not a committed deliverable. It proceeds only if the data foundation is reliable, a business owner defines the intended decision, and the expected value justifies the cost.

**Success means Nana can verify improved reporting consistency, reduced manual effort, protected production performance, traceable customer-data handling, timely inventory reporting, and controlled costs against the Q1 baseline.**