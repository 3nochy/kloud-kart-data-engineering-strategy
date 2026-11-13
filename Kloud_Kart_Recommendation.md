# Kloud Kart: Data Engineering Recommendation

**Prepared for:** Nana Adjei, Head of Operations  
**Prepared by:** External Data Consultant  
**Date:** 13 November 2026

## 1. Recommendation

Kloud Kart should establish a small, managed cloud data warehouse supported by controlled extraction, SQL transformations and reliable reporting. At approximately 4,000 orders per day, with around 40 GB of MySQL data and only two planned data hires, a focused warehouse is more appropriate than building a complex lakehouse or machine-learning platform.

The priorities are to protect the live website, establish trusted business figures, control customer-data copies and prepare for the anticipated 15–20% annual order growth. This growth assumption should be confirmed with management and used for capacity planning, rather than treated as a guaranteed forecast.

## 2. Proposed Architecture and Data Movement

**Source:** Existing MySQL production database.

**Extraction:** Take an initial consistent snapshot, then use incremental extraction to capture new and changed records. Use reliable change timestamps or keys where available; assess change-data capture if the source cannot support dependable incremental extraction. Track extraction progress, failed loads and duplicate records.

**Privacy and storage:** Mask or exclude unnecessary personal identifiers before data enters the analytical landing area. Retain only the raw data needed for approved reporting, with documented access and retention controls. Load the approved data into the warehouse.

**Transformation:** Use SQL inside the warehouse to standardise orders, payments, cancellations, refunds and inventory reporting. Apply validation checks before publishing results.

**Serving:** Provide consistent, documented reporting datasets for Operations and Finance. Automate the highest-priority Monday reports first.

This is a **hybrid ELT approach**: protect sensitive fields before analytical storage, load approved source data, then transform it in the warehouse using SQL. Extraction reliability and data protection are essential because loading incomplete or uncontrolled data would reproduce the current problems in a new platform.

## 3. Processing Frequency

Use scheduled batch processing for orders, payments, customer reporting and other routine management measures. Run ordinary reports daily, with the main Monday report generated from the same approved definitions and validated data.

The single streaming exception is **inventory stock-count changes**. Assess a change-data-capture mechanism to propagate stock changes to a near-real-time reporting view, with monitoring for delays, duplicate events and recovery after interruptions. The production inventory system remains authoritative for checkout and stock reservation; a delayed reporting view must never be treated as the source of truth for available stock.

## 4. First Implementation Priorities

1. **Protect production:** Investigate the two reported website slowdowns. Test the approved second server or a MySQL read replica, compare cost and capacity, and move reporting workloads only after performance, security, backups and recovery have been tested.
2. **Standardise reporting:** Agree with Finance and Operations on reporting periods and definitions for orders, revenue, payments, cancellations and refunds. Reconcile existing reports before automating them.
3. **Strengthen personal-data controls:** Assign an owner to the existing customer-data complaint, verify the applicable deadline, inventory known data copies, and document access, retention and deletion procedures. Review these arrangements against Ghana’s Data Protection Act, 2012 (Act 843), seeking qualified guidance where needed. The available facts do not establish that a legal breach has occurred.
4. **Build incrementally:** Start with the essential warehouse, extraction, transformation, validation and reporting capabilities. Avoid a large platform rollout or forecasting project until the core data is reliable and the business case is demonstrated.

## 5. Tools, Ownership and Growth

Use a small set of tool categories: a managed cloud data warehouse, a controlled extraction or change-data-capture mechanism, SQL transformation and validation, and a reporting interface. Select specific products only after assessing cost, security, compatibility, maintenance and staff capability.

The two planned hires should have complementary responsibilities:

- **Data Engineer:** extraction, loading, pipeline reliability, infrastructure monitoring and data access controls.
- **Analytics Engineer or BI Developer:** business definitions, SQL transformations, validation, reconciliation and reporting.

The existing PHP/MySQL developer should support production database changes and application integration. Business owners remain responsible for approving financial definitions and customer-data procedures.

Plan capacity against the 15–20% annual growth assumption and the possible Nigeria expansion. Review actual volume, query performance, storage, cost and data freshness quarterly. Reassess the design if measured demand exceeds its tested capacity.

## 6. Success Measures and Decision Gates

Establish Q1 baselines, then track reporting-related website slowdowns, unexplained Operations/Finance differences, staff hours spent preparing reports, customer-data copy traceability, inventory freshness and actual infrastructure costs.

Proceed with broader automation only after reporting definitions are approved and validation checks pass. Consider demand forecasting only when historical sales and inventory data are sufficiently complete and consistent, and management approves measurable pilot objectives.

**Decision:** Establish a controlled, managed warehouse with hybrid ELT, predominantly batch processing and one explicitly scoped streaming exception for inventory stock-count updates. Resolve the immediate customer-data and production-performance risks first, then expand only when measured business needs justify it.