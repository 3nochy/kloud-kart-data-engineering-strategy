# Kloud Kart: Situation Diagnosis

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** External Data Consultant  
**Date:** 13 November 2026

## 1. Executive Summary

Kloud Kart processes approximately 4,000 orders per day using a production application backed by a MySQL database of approximately 40 GB. Reporting relies on large exports, Operations manually rebuilds Monday figures from CSV files, Finance produces different figures, and Marketing maintains customer-list copies that are not centrally tracked.

The main problem is not simply a lack of analytics tools. Kloud Kart lacks sufficient separation between operational and analytical workloads, consistent business definitions, reliable reporting controls, and visibility over where customer data is copied.

Two website slowdowns occurred during Monday exports last month. Their precise technical cause has not yet been verified, so the exports should be treated as a plausible contributor requiring investigation, not as the confirmed root cause.

**My recommendation is to:**

1. Investigate and contain customer-data handling risks.
2. separate reporting workloads from the production application.
3. establish one agreed definition for revenue and other core business measures.
4. build a small managed cloud data warehouse with controlled extraction, predominantly daily batch processing, and a narrowly scoped near-real-time inventory exception.
5. automate reporting checks before expanding into forecasting or more advanced analytics.

For capacity planning, I assume annual order volume could grow by 15–20%. This is a planning assumption to validate with management, not a confirmed forecast.

## 2. Current Situation and Root Causes

| Observed situation | Likely underlying cause | Business consequence |
|---|---|---|
| Website slowdowns occurred twice during Monday exports | Reporting queries and large exports may compete with live application workloads for database resources | Potentially slower customer experience and operational disruption |
| Operations and Finance report different figures | Business definitions, extraction times, filters, or treatments of cancellations and refunds may differ | Decisions and financial discussions are harder to reconcile |
| Marketing maintains customer-list copies without central tracking | No complete register of personal-data copies or consistently enforced handling process | Customer requests may not reach every relevant copy |
| Operations rebuilds Monday reports from CSVs | Reporting depends on manual steps rather than a controlled, repeatable pipeline | Staff time is consumed and errors are harder to detect |
| Inventory information can become stale in reports | Regular batch reporting alone may not reflect the latest stock changes | Staff may make decisions using outdated stock information |
| Investors are asking about real-time analytics and forecasting | The business wants more advanced insight before its foundational data controls are fully established | Risk of spending on complexity before basic reporting is dependable |

These are working diagnoses. Database monitoring, query analysis, export logs, report comparisons, and a customer-data copy review are required to confirm the technical and operational causes.

## 3. Ranked Risks

### Risk 1: Uncontrolled customer-data copies and deletion requests

**Priority: Critical to investigate promptly**

Marketing maintains untracked customer-list copies, and a customer has raised a complaint concerning deleted customer data. The available information does not establish that a legal breach occurred or prove exactly how the deletion was handled.

The underlying control weakness is that the organisation may not have a complete view of where customer data exists, who owns each copy, and how a request is propagated to relevant systems.

**Potential impact**
- Delayed or incomplete handling of the customer's request.
- Difficulty demonstrating what action was taken and when.
- Unnecessary retention or access to personal information.
- Staff time spent searching for copies and reconstructing events.

**Recommended action**
- Assign a named complaint owner and verify the applicable response deadline and requirements.
- Document the request, its dates, the actions taken, and supporting evidence.
- Inventory relevant locations, including production MySQL, exports, spreadsheets, emailed files, reporting stores, and backups.
- Identify owners, access controls, retention rules, and approved deletion or restriction procedures for each location.
- Verify and document completion rather than assuming that deleting the production record removes every copy.

**Cost exposure:** An illustrative investigation estimate is 60 staff-hours at GH₵150 per hour, or **GH₵9,000 in one-off staff time**. This is an assumption for planning, not a confirmed expense, fine, or estimate of legal liability.

As I understand Ghana's Data Protection Act, 2012 (Act 843), personal-data handling must be assessed against applicable obligations. The organisation should confirm the legal requirements with its responsible privacy lead or qualified adviser. This diagnosis does not conclude that a breach has occurred.

### Risk 2: Reporting may affect production performance

**Priority: High**

Large Monday exports may compete with live application activity. However, the two observed slowdowns do not prove that exports caused them.

**Potential impact**
- Slower browsing or checkout.
- Lost or delayed orders.
- Reduced confidence in the reliability of the platform.

**Recommended action**
- Review database logs, query plans, resource utilisation, export timing, and application monitoring around both incidents.
- Establish a baseline for website response time, checkout performance, and database load.
- Test a separate reporting environment, such as an approved read replica, before moving reporting workloads.
- Monitor replication lag and confirm that recovery and access controls work as expected.
- Keep the production database authoritative for checkout, stock reservation, and order processing.

A reporting replica reduces contention risk but does not guarantee that every performance issue will disappear. Its effect must be measured.

### Risk 3: Operations and Finance report inconsistent figures

**Priority: High**

Operations rebuilds Monday numbers from CSVs, while Finance reports different figures. The exact cause of the mismatch is not yet known.

Possible causes include different definitions of revenue, inconsistent reporting cut-off times, duplicate or missing records, inconsistent treatment of cancellations and refunds, and manual spreadsheet changes.

**Potential impact**
- Decisions based on conflicting figures.
- Time spent reconciling reports.
- Reduced confidence in management and investor reporting.

**Recommended action**
- Agree a business definition for each core metric before automating it.
- Define revenue explicitly: for example, whether the measure is based on orders placed, payments received, or fulfilled orders, and how cancellations, refunds, and failed payments are treated.
- Standardise the reporting period, time zone, filters, and source records.
- Compare the agreed report with Operations and Finance outputs and investigate differences before publication.
- Record the owner and version of each approved definition.

A shared warehouse will not resolve inconsistent figures unless the underlying business definitions and transformation rules are agreed.

### Risk 4: Manual reporting consumes staff time

**Priority: Medium to high**

Repeated CSV exports, spreadsheet processing, and manual reconstruction make reporting slower and harder to reproduce.

**Potential impact**
- Staff time diverted from operational work.
- Repeated manual errors.
- Delayed access to trusted management information.

**Recommended action**
- Document the current Monday reporting process.
- Automate the highest-value reports after metric definitions have been agreed.
- Add automated quality checks to each data load.
- Retain reconciliation evidence and a clear process for investigating failures.

Automation should follow a validated manual process rather than reproduce inconsistent calculations at greater speed.

### Risk 5: Inventory reporting may be stale

**Priority: High for inventory-dependent decisions**

Daily batch reporting is suitable for many management metrics, but inventory changes may require more frequent updates. A reporting copy must not be treated as the authoritative stock record for checkout.

**Potential impact**
- Decisions made using outdated availability information.
- Increased risk of stock discrepancies and customer dissatisfaction.

**Recommended action**
- Keep stock reservation and checkout decisions on the operational system.
- Assess a controlled change-data-capture process to update an inventory reporting view near real time.
- Monitor update delay, duplicates, failures, and recovery.
- Display the latest update time so users can judge the freshness of reported stock.

## 4. Illustrative Cost and Exposure Estimates

The following estimates indicate the potential scale of the problem. The assumptions must be validated before these figures are used as budgets, savings commitments, or evidence of actual loss.

| Item | Calculation | Illustrative estimate |
|---|---|---:|
| Customer-data investigation | 60 hours × GH₵150/hour | GH₵9,000 one-off staff time |
| Finance reconciliation | 2 hours/week × 50 weeks × GH₵60/hour | GH₵6,000/year |
| Manual reporting | 4 hours/week × 50 weeks × GH₵100/hour | GH₵20,000/year |
| Potential gross sales exposure during slowdowns | See scenario below | GH₵5,625 across two incidents |

### Slowdown scenario calculation

Assumptions requiring validation:
- 4,000 orders per day.
- 16 active trading hours per day.
- Each slowdown lasted 45 minutes.
- 10% of orders in the affected period were potentially affected.
- Average order value was GH₵150.
- Two incidents occurred.

Calculation:

1. Estimated orders per active hour: 4,000 ÷ 16 = 250.
2. Estimated orders during 45 minutes: 250 × 0.75 = 187.5.
3. Potentially affected orders under the 10% assumption: 187.5 × 10% = 18.75.
4. Illustrative gross sales exposure per incident: 18.75 × GH₵150 = GH₵2,812.50.
5. Across two incidents: GH₵2,812.50 × 2 = **GH₵5,625**.

This is a scenario-based estimate of gross sales exposure, **not confirmed lost revenue**. It does not establish that any orders were lost, that all affected orders would have completed, or that the assumed duration, affected proportion, and average order value are accurate.

The staff-time estimates and slowdown scenario describe different cost categories. They should not be added together and presented as confirmed financial loss. Likewise, estimated time released through automation is not automatically a cash saving.

## 5. Data Quality: Six Dimensions and Required Checks

Every data load should be checked before its results are published.

| Dimension | What it means for Kloud Kart | Example check |
|---|---|---|
| Completeness | Required records and fields are present | Compare extracted order counts with source counts; flag missing order IDs |
| Accuracy | Values correctly represent the source transaction | Reconcile sampled order totals against the source system |
| Consistency | Related reports use the same definitions and rules | Reconcile revenue totals across Operations and Finance using agreed cancellation and refund rules |
| Timeliness | Data arrives within the agreed reporting window | Record load completion time and inventory update delay |
| Validity | Values follow accepted formats and business rules | Validate status values, timestamps, amounts, and required fields |
| Uniqueness | Records are not unintentionally duplicated | Check duplicate order IDs and duplicate source change events |

Failed checks should create a visible exception, identify an owner, and prevent unreliable outputs from being silently published. Thresholds should be agreed with the relevant business owners and adjusted using observed baselines.

## 6. Recommended Direction

Kloud Kart should establish a small, managed cloud data warehouse, with reporting separated from production and a controlled hybrid ELT pipeline.

- **Extraction:** Begin with a consistent initial snapshot, then use incremental extraction. Assess change-data capture if reliable incremental extraction cannot be achieved with available source fields.
- **Transformation:** Apply approved SQL transformations and business definitions in the warehouse.
- **Personal data:** Exclude or mask unnecessary identifiers before analytical landing where feasible, and apply access and retention controls to any approved raw data that must be retained.
- **Refresh strategy:** Use daily batch processing for ordinary management reporting. Treat inventory stock-count updates as the one specifically scoped near-real-time exception.
- **Publication:** Validate data before reports are made available.
- **Capacity planning:** Test the architecture against a provisional 15–20% annual order-growth assumption and review actual volume, performance, and cost regularly.

The two planned data hires should have clear responsibilities: a Data Engineer to own extraction, pipeline reliability, and data controls; and an Analytics Engineer or BI Developer to own metric definitions, transformations, reconciliation, and business reporting. The PHP/MySQL developer should remain involved in changes affecting the production application.

## 7. Immediate Actions and Ownership

| Action | Accountable owner | Evidence of completion |
|---|---|---|
| Confirm the customer-data complaint owner and applicable deadline | Nana / designated privacy or compliance owner | Recorded owner, dates, and action log |
| Inventory customer-data copies and document their owners | Designated data owner with Marketing and IT | Completed copy register with unresolved locations flagged |
| Investigate both slowdown incidents | PHP/MySQL developer with Data Engineer | Findings based on logs, monitoring, and query analysis |
| Agree revenue and order definitions | Nana with Finance and Operations | Approved metric definitions and reconciliation rules |
| Baseline reporting time, discrepancies, performance, and data freshness | Data Engineer with Operations and Finance | Recorded baseline measures |
| Test separation of reporting from production | Data Engineer and PHP/MySQL developer | Documented performance, replication-lag, and recovery test results |
| Approve warehouse, extraction, and access-control design | Management with the two data hires | Approved architecture and implementation plan |

## 8. Conclusion

Kloud Kart's immediate need is a dependable, controlled data foundation—not a complex analytics platform built ahead of business requirements. Customer-data handling, production performance, and inconsistent reporting should be addressed first. A small managed warehouse, agreed business definitions, automated quality checks, daily batch processing, and a narrowly scoped near-real-time inventory feed provide a proportionate path forward.

Success should be measured through evidence: fewer unexplained report differences, reduced manual reporting effort, improved production performance, traceable customer-data copies, timely inventory updates, and controlled infrastructure costs. Baselines should be established before numerical improvement targets are promised.
