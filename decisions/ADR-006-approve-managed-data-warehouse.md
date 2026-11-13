# ADR-006: Approve a Small Managed Cloud Data Warehouse

**Status:** Accepted  
**Date:** 13 November 2026  
**Decision owner:** Nana Adjei, Head of Operations

## Context

Kloud Kart processes approximately 4,000 orders per day using a production MySQL database of approximately 40 GB. Large Monday exports have coincided with two website slowdowns, and Operations and Finance produce inconsistent figures.

The business needs a dependable reporting foundation without creating unnecessary operational complexity. Two data hires are planned, and the PHP/MySQL developer must continue supporting the production application.

ADR-002 previously recommended deferring the warehouse platform. This decision supersedes that earlier direction because the revised assessment establishes a defined reporting architecture and a staged implementation path. The business should still avoid unnecessary platform expansion.

A provisional annual order-growth assumption of 15–20% will guide capacity planning until actual growth trends are validated.

## Decision

Establish a small, managed cloud data warehouse as the central analytical reporting layer.

The implementation will follow these principles:

1. **Separate reporting from production.** Test and use an approved reporting replica or other suitable isolated extraction approach so analytical workloads do not unnecessarily compete with live application activity.
2. **Use incremental extraction.** Start with a consistent initial snapshot, then extract changes incrementally. Assess change-data capture if dependable incremental extraction cannot be achieved with the source fields available.
3. **Use hybrid ELT.** Exclude or mask unnecessary personal identifiers before analytical landing where feasible. Load approved data under appropriate access and retention controls, then transform and validate it using SQL in the warehouse.
4. **Use daily batch processing by default.** Orders, payments, customer reporting, and standard management measures refresh daily.
5. **Allow one scoped near-real-time exception.** Inventory stock-count changes may update a reporting view through change-data capture. Production remains authoritative for checkout, stock reservation, and inventory operations.
6. **Validate before publishing.** Every load must be checked for completeness, accuracy, consistency, timeliness, validity, and uniqueness.
7. **Keep the platform proportionate.** Select tools by capability and operational fit rather than introducing a complex lakehouse or machine-learning platform before there is a demonstrated need.

The Data Engineer owns pipeline reliability and monitoring. The Analytics Engineer or BI Developer owns SQL transformations, metric definitions, and reporting reconciliation. The PHP/MySQL developer supports production integration and performance investigations.

## Alternatives considered

### Alternative A: Continue reporting directly from production

**How it would work**

Keep the existing MySQL database as the source for both live transactions and analytical exports, using query scheduling and operational controls to limit contention.

**Why it is attractive**

It has the lowest initial infrastructure complexity and requires no separate analytical platform.

**Why rejected**

It does not adequately separate reporting workloads from live application activity. The observed slowdowns make it important to investigate and reduce this risk rather than assume scheduling alone will solve it.

### Alternative B: Use a separate reporting replica but postpone the warehouse

**How it would work**

Move reporting queries to a replica and continue producing CSV files or reporting tables without establishing a central analytical warehouse.

**Why it is attractive**

It can reduce pressure on production and provides a relatively simple first step.

**Why rejected**

It improves workload separation but does not, by itself, provide a durable central layer for consistent definitions, repeatable transformations, quality checks, and consolidated reporting. It remains a possible interim measure during implementation.

### Alternative C: Build a complex lakehouse and advanced analytics platform immediately

**How it would work**

Introduce a broader data platform with multiple processing services and prepare for advanced analytics and forecasting from the outset.

**Why it is attractive**

It offers flexibility for future use cases and could support a wider range of analytical workloads.

**Why rejected**

The present requirements do not justify the additional implementation and operational burden. Kloud Kart should establish dependable reporting first and expand only when measured business needs justify it.

## Consequences

### What this buys

- A central location for approved analytical data and standard reporting.
- Better separation between analytical workloads and production transactions.
- Repeatable transformations and agreed business definitions.
- Automated quality checks and more traceable reporting.
- A foundation that can be tested against expected business growth.

### What this costs

- Cloud infrastructure, data movement, storage, monitoring, and support costs.
- Engineering time to build, test, secure, and maintain the pipelines.
- Work to reconcile existing reports and establish approved business definitions.
- Ongoing responsibility for access control, retention, failure recovery, and data quality.

### What it costs the client if I am wrong

If a warehouse is unnecessary at Kloud Kart's current scale, the business may incur avoidable infrastructure and engineering costs. If extraction or transformation rules are incorrect, the warehouse may reproduce misleading figures with greater consistency. If personal data is copied without adequate controls, the number of places requiring oversight may increase.

These risks must be controlled through staged implementation, reconciliation, access restrictions, monitoring, and regular cost review.

### What would make me revisit this

Reassess the decision if:

- Measured reporting requirements can be met reliably and economically without a warehouse.
- Total warehouse and pipeline costs exceed the approved budget without sufficient business value.
- Actual order growth, data volume, or reporting requirements differ materially from planning assumptions.
- The chosen extraction method cannot deliver acceptable reliability or inventory freshness.
- New regulatory, security, or business requirements make the architecture unsuitable.

Any replacement decision should be documented in a new ADR.

## What this survives

The decision remains defensible if Kloud Kart grows by the assumed 15–20% annually, provided capacity and cost are reviewed against actual measurements. It does not depend on a particular cloud vendor or a commitment to advanced analytics.

It also survives the possibility that the warehouse implementation must be delayed: production protection, customer-data controls, metric definitions, and the initial reporting-isolation work remain valuable independently.

The decision is not a claim that a warehouse will automatically fix slowdowns, inconsistent revenue, or customer-data handling. Those outcomes depend on implementation quality, agreed definitions, and verified controls.