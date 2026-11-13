# Situation Diagnosis: Kloud Kart

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** External Data Consultant  
**Date:** 10 November 2026

## 1. Executive Summary

Kloud Kart has grown to approximately 4,000 orders per day and is preparing to expand into Nigeria. However, its current data practices have not developed at the same pace as the business. The company stores orders, inventory and customer accounts in a single MySQL database on the same server as its live website. Operations and Finance produce different figures from their spreadsheets, Marketing exports customer information without tracking where copies go, and large Monday exports have slowed the website twice in the past month.

These are not separate problems. They point to weaknesses in data ownership, reporting processes, customer information management and the separation of business reporting from live operations.

The four findings are ranked below according to their potential impact on the business, customers and the board's ability to make informed decisions.

1. **Uncontrolled customer data and deletion processes.** The absence of reliable tracking of exported customer lists creates privacy and compliance risks, particularly given the existing complaint concerning deleted customer data.
2. **Reporting activity affecting the live website.** Large exports compete with the live application for shared server resources, creating a risk to customer experience and sales.
3. **Inconsistent business reporting.** Different figures from Operations and Finance weaken confidence in business performance reports and decisions.
4. **Time-consuming manual reporting.** Repeated exports and spreadsheet preparation consume staff time and make reporting difficult to scale.

Kloud Kart should address these operational risks before investing in complex analytics or machine learning. The immediate priority is to establish control over customer information, protect the live website, and produce consistent business figures using a controlled reporting process.

The cost figures in this report are illustrative planning estimates. The case does not provide actual staff rates, the duration of website slowdowns, average order value or confirmed financial losses. These assumptions are stated explicitly so management can replace them with verified figures.

## 2. Root Causes Ranked by Business Risk

### 2.1 Uncontrolled Customer Data and Deletion Processes

**Risk ranking: First**

**What is happening**

Marketing exports a customer list containing approximately 300,000 people, but the company does not track how many copies are created or where those copies are stored. Kloud Kart has also received a complaint concerning deleted customer data and has a 90-day response window.

**Root cause**

The company lacks a sufficiently controlled process for managing customer information throughout its lifecycle. The problem is not simply that Marketing exports lists. It is that the company cannot reliably demonstrate where exported information goes, who has access to it, how long copies are retained, or whether deletion has been completed across relevant systems and copies.

This creates uncertainty when the company needs to investigate a complaint, demonstrate accountability or confirm that customer information has been handled appropriately.

**Business and compliance impact**

Under Ghana's Data Protection Act, 2012 (Act 843), organizations must take their responsibilities for personal data seriously. The facts provided are not enough to determine whether Kloud Kart has breached the law. However, the untracked exports and existing complaint create a clear reason to review its data-handling practices urgently.

The company could also lose customer trust if it cannot explain how personal information is accessed, retained or deleted.

**Illustrative cost estimate**

Assume the initial investigation and response require 60 staff hours, valued at GH₵150 per hour.

**60 hours × GH₵150 = GH₵9,000**

This is an estimated staff-time cost for planning purposes. Neither the 60 hours nor the hourly rate is provided by the case. The amount is not a regulatory penalty, legal-fee quotation or confirmed loss.

The actual cost could be higher or lower depending on the scope of the complaint, the records available and the work required to investigate it.

**Recommended action**

Immediately assign responsibility for the complaint and establish a documented response plan within the available 90-day window. Identify the relevant customer records, export locations, access permissions and deletion history. Preserve relevant evidence and document the investigation.

Marketing should use controlled access to customer information, with a record of authorized exports, their purpose and their retention or deletion. Deletion requests should have a documented process for identifying relevant copies and recording the outcome.

Management should seek appropriate data-protection or legal guidance where the complaint requires it.

**How success will be measured**

The complaint has an assigned owner, an evidence-based response plan and documented progress. Relevant customer-data locations and access permissions are identified, and customer-data exports and deletion activities can be traced.

### 2.2 Reporting Activity Affects the Live Website

**Risk ranking: Second**

**What is happening**

The website and the MySQL database share the same server. Twice last month, a Monday export slowed the live website to a crawl.

**Root cause**

The reporting process competes with the live application for server resources. Large queries and exports can consume database processing capacity, memory, storage activity and network resources that the website also needs to serve customers.

The deeper problem is the lack of separation between operational workloads and reporting workloads.

**Business impact**

Website slowdowns can delay customer orders, reduce confidence in the shopping experience and place additional pressure on the development team. As Kloud Kart expands, this shared arrangement could become increasingly difficult to manage.

The two incidents establish that the problem has occurred, but they do not establish how many orders were lost or how much revenue was affected.

**Illustrative cost estimate**

The following calculation estimates possible gross sales exposure during the two reported incidents. It is a scenario, not a measurement of confirmed lost sales.

For planning purposes, assume the following:

1. Kloud Kart receives 4,000 orders per day.
2. The business operates across 16 active trading hours per day.
3. Each slowdown lasts 45 minutes.
4. Ten percent of the orders expected during each slowdown window are not completed at that time.
5. The average order value is GH₵150.

**Step 1: Estimate orders per trading hour**

4,000 orders ÷ 16 hours = 250 orders per hour

**Step 2: Estimate orders during a 45-minute slowdown**

45 minutes ÷ 60 minutes = 0.75 hours

250 orders × 0.75 hours = 187.5 expected orders

**Step 3: Estimate potentially affected orders**

187.5 orders × 10% = 18.75 potentially affected orders per incident

**Step 4: Estimate gross sales exposure**

18.75 orders × GH₵150 = GH₵2,812.50 per incident

GH₵2,812.50 × 2 incidents = **GH₵5,625 across the two incidents**

This estimate depends entirely on the stated assumptions. The case does not confirm that either slowdown lasted 45 minutes, that 10% of orders failed, or that the average order value was GH₵150.

The figure represents illustrative gross sales exposure, not confirmed lost revenue or lost profit. Some customers may have completed their orders later, and the actual impact may differ considerably.

**Recommended action**

Move reporting workloads away from the live website and its production database. The company has already approved a second server or read replica, making separation a practical early improvement.

A read replica could reduce reporting pressure on the production database, although replication lag and resource limits would still need to be monitored. Management should also review the most expensive reporting queries and schedule large exports appropriately.

**How success will be measured**

Routine reporting no longer causes the same observed website slowdowns. Website response times and database performance are monitored, and any reporting-related incidents can be identified and investigated.

### 2.3 Operations and Finance Produce Different Figures

**Risk ranking: Third**

**What is happening**

Every Monday, Nana rebuilds business figures from CSV exports, but Finance's spreadsheet does not match hers.

**Root cause**

The company lacks a consistently governed reporting process with agreed definitions, calculation rules and a common source for business figures. Different spreadsheets may use different filters, reporting periods, adjustments or calculation methods.

The case does not establish which spreadsheet is correct. It would therefore be premature to assume that either Operations or Finance is responsible for the discrepancy.

**Business impact**

Management cannot confidently explain the differences between reports. This weakens decision-making and creates additional work whenever figures must be reconciled.

As the company expands into Nigeria, inconsistencies could become more difficult to investigate if new reporting processes and definitions are introduced without agreement.

**Illustrative cost estimate**

Assume Finance spends two hours each week reconciling figures, across 50 working weeks per year, at an estimated staff-time value of GH₵60 per hour.

2 hours × 50 weeks × GH₵60 = **GH₵6,000 per year**

The two hours and the hourly rate are assumptions, not case facts. This estimates the value of staff time spent on reconciliation. It does not establish a confirmed cash loss.

**Recommended action**

Operations and Finance should agree on definitions for key measures such as orders, revenue, completed orders, cancellations and refunds. The reporting period and treatment of adjustments should also be consistent.

Kloud Kart should establish a controlled reporting dataset and use the same documented calculations for both departments. The first version can use straightforward SQL queries and a repeatable reporting process rather than introducing a complex analytics platform immediately.

**How success will be measured**

Operations and Finance use the same definitions and reporting period. Any remaining differences can be traced to documented adjustments or identified data-quality issues instead of unexplained spreadsheet variations.

### 2.4 Manual Reporting Consumes Staff Time

**Risk ranking: Fourth**

**What is happening**

Nana relies on manual CSV exports and spreadsheet work to prepare the Monday figures.

**Root cause**

The reporting process depends too heavily on individual effort rather than a repeatable and documented procedure. The business has not established a reliable reporting workflow that can produce the required figures consistently.

This creates a dependency on manual work and makes the process difficult to scale as order volumes increase.

**Business impact**

Time that could be spent investigating operational problems and improving performance is instead spent collecting, checking and rebuilding numbers.

The current process also makes reporting vulnerable to inconsistent filters, accidental spreadsheet changes and differences in how staff prepare their figures.

**Illustrative cost estimate**

Assume Nana spends four hours preparing the report each Monday, across 50 working weeks per year, with an estimated staff-time value of GH₵100 per hour.

4 hours × 50 weeks × GH₵100 = **GH₵20,000 per year**

The four hours and the hourly rate are assumptions. The figure estimates the value of Nana's time, not a confirmed cash saving that the company would automatically realize by automating the process.

**Recommended action**

Document the existing Monday reporting process, agree on the required measures and automate the repeatable extraction and calculation steps. Start with the reports that Operations and Finance use most frequently.

The process should include basic checks for missing records, duplicate orders and unexpected changes in totals. Nana should receive an understandable report with clear definitions rather than needing to rebuild the figures herself.

**How success will be measured**

The Monday report can be generated using a repeatable process, the time required to prepare it decreases, and Nana can explain the reported figures without manually rebuilding them.

## 3. Overall Financial Assessment

The estimates in this diagnosis demonstrate why Kloud Kart should investigate the problems rather than assume that they have no cost.

The illustrative figures are:

1. **Customer complaint investigation:** GH₵9,000 in assumed staff time for a one-off investigation.
2. **Website slowdown scenario:** GH₵5,625 in estimated gross sales exposure across the two reported incidents.
3. **Finance reconciliation:** GH₵6,000 in assumed annual staff time.
4. **Manual reporting:** GH₵20,000 in assumed annual staff time.

These figures must not be presented to the board as confirmed losses or added together as if they represent a verified annual financial impact.

The estimates cover different types of exposure and different time periods. The complaint estimate is a one-off planning scenario, the website estimate concerns two reported incidents, and the reconciliation and reporting estimates represent assumed annual staff-time values. The estimates also depend on unverified rates and durations.

The immediate financial task is to replace these assumptions with evidence. Kloud Kart should record actual time spent preparing and reconciling reports, measure the duration and performance impact of website slowdowns, and verify average order value and order-completion data before claiming lost sales.

This approach provides a defensible starting point for prioritizing improvements without overstating the financial case.

## 4. Data Protection and the 90-Day Complaint

The complaint concerning deleted customer data requires specific attention because the company has a stated 90-day response window and does not currently track customer-list exports reliably.

The available facts do not establish exactly what information was deleted, which systems or copies were involved, what the complainant has requested, or whether a legal breach has occurred. These details must be investigated rather than assumed.

Kloud Kart should take the following action immediately:

1. Assign a responsible person to coordinate the complaint and maintain a record of actions and deadlines.
2. Identify the relevant customer records, systems, exports and known copies.
3. Review available access records, deletion records and other relevant evidence.
4. Document the findings and the steps taken to investigate and respond.
5. Review the company's customer-data handling procedures against its obligations under Ghana's Data Protection Act, 2012 (Act 843).
6. Seek qualified guidance where necessary and ensure that the response is prepared within the applicable deadline.

The company should not claim that customer data has been fully deleted until the relevant systems and copies have been checked to the extent reasonably possible and the outcome documented.

Longer term, Kloud Kart needs clear ownership of customer information, controlled access, traceable exports and a repeatable process for responding to deletion requests. These controls are more urgent than building advanced analytics because they address an existing complaint and a current weakness in the handling of personal information.

## 5. Recommended Direction for Kloud Kart

The diagnosis supports a practical direction rather than an immediate investment in a large analytics platform.

First, stabilize the existing environment by separating reporting activity from the live website and reviewing the queries that create the greatest pressure.

Second, establish consistent reporting definitions and a repeatable process for producing the figures used by Operations and Finance.

Third, introduce appropriate controls for customer information, including access, export tracking, retention and deletion.

Finally, build the reporting foundation gradually so the company can introduce broader analytics and eventually evaluate demand forecasting when the underlying data is reliable enough.

This approach fits the company's current constraints. Kloud Kart has only two data hires available this financial year, its existing developer is experienced in PHP and MySQL, and the company has not yet established a professional data engineering function. The initial solution should therefore be manageable by the team, with specialist support where required.

The choice of warehouse technology should follow the reporting and operational requirements. Snowflake and BigQuery may be reasonable future options, but selecting either before establishing the core requirements could create unnecessary cost and complexity. A modest, well-controlled reporting foundation is the most defensible first step.

Stock counts are the exception to the otherwise daily reporting requirement. Any future design must preserve sufficiently fresh inventory information rather than treating all data as suitable for a daily refresh.

## 6. Decisions and Assumptions

Nana is unavailable for follow-up questions, so the diagnosis makes provisional decisions based on the available facts.

**Decision 1: Protect the production website before expanding analytics.**  
The two reported slowdowns provide direct evidence of an operational risk. Reporting workloads should be separated from production as an early priority.

**Decision 2: Address the customer-data complaint immediately.**  
The complaint has a stated response window, and the company lacks adequate visibility into customer-list copies. Investigation and documented controls should begin without waiting for a new data platform.

**Decision 3: Establish shared reporting definitions before building more dashboards.**  
A new dashboard will not resolve disagreements if Operations and Finance continue to use different definitions or calculations.

**Decision 4: Delay advanced forecasting until the reporting foundation is reliable.**  
Demand forecasting may be useful in the future, but its value depends on reliable historical data, clear business measures and a process for checking forecast performance.

The following assumptions remain unverified:

1. The actual duration and business impact of the two website slowdowns.
2. The average order value and proportion of orders affected during those incidents.
3. The actual time Operations and Finance spend preparing and reconciling reports.
4. The staff-time rates used in the illustrative calculations.
5. The number and locations of exported customer-list copies.
6. The exact scope and facts of the customer-data complaint.
7. The existing database performance limits, replication requirements and infrastructure costs.

These assumptions should be replaced with measured evidence as the work progresses. They should not be treated as established facts in a board discussion.

## 7. Priority Actions

**Immediate priority**

Assign ownership of the customer-data complaint, begin the investigation and document the response plan. Review the reporting activity associated with the website slowdowns and identify the queries responsible.

**Stabilization priority**

Move large reporting workloads away from the production environment using the approved infrastructure option. Introduce monitoring for website and database performance.

**Reporting improvement priority**

Agree on common definitions with Operations and Finance. Document the current reporting process and create a repeatable version of the most important Monday reports.

**Control and review priority**

Introduce traceable customer-data exports and documented deletion procedures. Review the measured results to confirm whether the changes have reduced reporting effort, improved consistency and protected website performance.

These actions establish the immediate direction. Their detailed quarterly schedule, staffing plan and delivery measures should be developed as part of the recommendation and roadmap work.

## 8. Discovery Questions for Validation

The following questions should be answered during implementation to replace assumptions with evidence.

1. What specifically caused each of the two website slowdowns, how long did each last, and what did the monitoring records show?
2. Which measures differ between the Operations and Finance reports, and what definitions or calculation steps explain the differences?
3. How much time does each team spend exporting, preparing and reconciling the Monday reports?
4. Where are customer-list exports stored, who can access them, and what process is currently used to handle deletion requests?
5. What does the existing customer-data complaint concern, what evidence is available, and what actions are needed to prepare an appropriate response within the 90-day window?
6. What level of inventory freshness is required operationally, and how can it be maintained if reporting workloads are moved to a separate environment?

These questions are not a reason to delay urgent action. They identify the evidence required to refine the plan and make subsequent investment decisions defensible.

## 9. Conclusion

Kloud Kart's immediate challenge is not a lack of advanced analytics. It is that its existing data processes are creating operational risk, inconsistent business reporting and uncertainty around customer information.

The most defensible response is to address the customer-data complaint, protect the live website from reporting workloads, establish shared reporting definitions and reduce dependence on manual spreadsheet preparation.

The cost calculations provide an initial basis for understanding the potential impact, while making clear where evidence is missing. As those assumptions are verified, management will be better positioned to evaluate investment choices and demonstrate that its data strategy addresses real business needs.

The priority is to establish reliable, controlled and maintainable data practices before expanding into more complex analytics.
