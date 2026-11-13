# Kloud Kart: Recommendation

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** External Data Consultant  
**Date:** 13 November 2026

## 1. Recommended Approach

Kloud Kart should establish a reliable, secure and cost-controlled data foundation before investing in advanced analytics or machine learning.

The company processes approximately 4,000 orders daily, but reporting workloads share a server with the live website. Operations and Finance produce inconsistent figures, while Marketing exports customer information without tracking copies. These problems create operational, reporting and customer-data risks.

I recommend four priorities: separate reporting from production, standardize reporting, strengthen customer-data controls, and defer major analytics investments until the business case is clear.

## 2. What to Implement First

### Priority 1: Protect the live website

Use the approved second server or a MySQL read replica to move reporting workloads away from the production database. Choose a read replica only if testing confirms that it can handle reporting queries without unacceptable performance or replication delays. Monitor website performance and replication lag. Inventory decisions must continue to use sufficiently current stock information, not a delayed reporting copy.

### Priority 2: Establish trusted reporting

Agree on shared definitions for orders, revenue, cancellations and refunds with Operations and Finance. Automate the most important Monday reports using repeatable SQL queries and data-quality checks. This should reduce manual reconciliation and make differences easier to explain.

### Priority 3: Strengthen customer-data controls

Assign an owner to the existing customer-data complaint and document the investigation and response within the applicable 90-day window. Introduce controlled access, traceable customer-list exports, retention rules and a documented deletion process. Review the approach against Ghana’s Data Protection Act, 2012 (Act 843), seeking qualified guidance where necessary. The available facts do not establish whether a legal breach has occurred.

### Priority 4: Build gradually

Start with manageable reporting infrastructure rather than committing immediately to a complex warehouse. Evaluate BigQuery or Snowflake only after requirements, expected benefits and total costs have been assessed. Consider demand forecasting when sales and inventory data are sufficiently reliable.

## 3. Staffing and Accountability

Use the two available data hires for complementary responsibilities:

1. **Data Engineer:** builds and maintains data pipelines, separates reporting workloads, monitors data movement and supports reliable data delivery.
2. **Analytics Engineer or BI Developer:** defines business measures, develops reports, implements data-quality checks and works with Operations and Finance to validate results.

The existing PHP/MySQL developer should support production database changes and application integration. A named business owner should oversee customer-data processes, with specialist advice where necessary.

## 4. Measures of Success

Establish baselines in Q1 and track:

- Reporting-related website slowdowns and website performance.
- Unexplained differences between Operations and Finance reports.
- Weekly hours spent preparing and reconciling reports.
- Traceability of customer exports and deletion activities.
- Inventory freshness and stock accuracy.
- Actual infrastructure costs against the approved budget.

The goal is to eliminate reporting-related website slowdowns, resolve unexplained differences in agreed measures, reduce manual reporting effort and improve customer-data accountability. Set numerical improvement targets after the baseline is measured.

## Recommendation

Address the existing customer-data complaint and production-performance risk first. Then standardize and automate priority reports. Defer warehouse selection and demand forecasting until measured results show that the business is ready and the investment is justified.
