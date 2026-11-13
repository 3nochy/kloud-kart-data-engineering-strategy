# Kloud Kart Data Engineering Strategy

## Project Overview

This project presents a practical data engineering strategy for Kloud Kart, an Accra-based e-commerce business processing approximately 4,000 orders per day.

Kloud Kart currently uses a MySQL production database of approximately 40 GB. Large reporting exports have coincided with website slowdowns, Operations and Finance produce inconsistent figures, and customer-list copies maintained by Marketing are not centrally tracked.

The objective is to establish a reliable, secure, and cost-controlled reporting foundation without introducing unnecessary technical complexity.

## Business Problems

- **Production performance:** Large reporting exports may compete with live application workloads.
- **Inconsistent reporting:** Operations and Finance report different figures.
- **Customer-data governance:** Customer-list copies are not centrally tracked.
- **Manual reporting:** Monday reports require repeated CSV exports and manual reconstruction.
- **Inventory freshness:** Standard daily reports may not reflect the latest stock changes.
- **Future growth:** The architecture must be assessed against a provisional 15–20% annual order-growth assumption.

The growth figure is a planning assumption to validate, not a confirmed forecast.

## Recommended Architecture

The proposed target architecture uses a small managed cloud data warehouse, controlled extraction, SQL transformations, automated quality checks, and a reporting layer.

```text
Production MySQL
       |
       v
Controlled extraction
Initial snapshot + incremental changes
       |
       v
Data protection and access controls
       |
       v
Managed cloud data warehouse
       |
       v
SQL transformations and quality checks
       |
       v
Approved reporting tables
       |
       v
Operations, Finance and management
```

Inventory stock-count changes are the single proposed near-real-time exception. An appropriate change-data-capture mechanism should update the inventory reporting view, with freshness and failure monitoring.

Production remains authoritative for checkout, stock reservation, and operational inventory decisions.

## Processing Strategy

### Extraction

- Establish a consistent initial snapshot.
- Use incremental extraction for subsequent changes.
- Assess change-data capture if reliable incremental extraction cannot be achieved using available source fields.
- Monitor load completion, failures, duplicate processing, and reconciliation results.

### Transformation

The proposed approach is hybrid ELT:

- Exclude or mask unnecessary personal identifiers before analytical landing where feasible.
- Apply approved access and retention controls to data that must be retained.
- Use SQL transformations to standardise orders, payments, cancellations, refunds, and inventory reporting.
- Validate results before publishing reports.

### Refresh Frequency

| Data domain | Proposed refresh |
|---|---|
| Orders and payments | Daily batch |
| Standard management reporting | Daily batch |
| Customer reporting | Daily batch, subject to approved data controls |
| Inventory reporting view | Near real time |
| Production checkout and stock reservation | Operational system remains authoritative |

## Project Deliverables

| Deliverable | Purpose |
|---|---|
| `Situation_Diagnosis_Kloud_Kart.md` | Ranked business and technical risks, assumptions, cost estimates, and data-quality dimensions |
| `Kloud_Kart_Recommendation.md` | Recommended architecture, extraction strategy, processing approach, and ownership |
| `Kloud_Kart_Implementation_Roadmap.md` | Quarterly implementation plan with verifiable outcomes |
| `decisions/` | Architecture Decision Records documenting decisions and rejected alternatives |
| `improvement/` | Additional operational controls and the proposed FinOps improvement |
| `Kloud-Kart-Board-Presentation.pptx` | Executive-level communication of the findings and recommendations |

## Data Quality and Reporting Controls

Every data load should be checked across six dimensions:

1. **Completeness:** Are required records and fields present?
2. **Accuracy:** Do values match the source and expected business rules?
3. **Consistency:** Are definitions and calculations consistent across reports?
4. **Timeliness:** Did the data arrive within the agreed window?
5. **Validity:** Do values meet accepted formats and rules?
6. **Uniqueness:** Are unintended duplicate records present?

Failed checks should be visible, assigned to an owner, and resolved before affected outputs are published.

Revenue definitions must be agreed with Finance and Operations, including the treatment of cancellations, refunds, failed payments, and reporting cut-off times.

## Customer Data Protection

The strategy includes an inventory of customer-data copies, named owners, access controls, retention rules, and documented handling of relevant customer requests.

The investigation must cover applicable production data, exports, spreadsheets, emailed files, reporting stores, and backups. Deletion from one location must not be assumed to remove every copy.

Applicable obligations under Ghana's Data Protection Act, 2012 (Act 843), should be confirmed with the designated privacy or compliance owner.

## Implementation Roadmap

- **Q1 — Investigate and agree:** Assign complaint ownership, investigate slowdowns, establish baselines, and approve business definitions.
- **Q2 — Protect and build:** Separate reporting from production where appropriate, configure the warehouse, and implement controlled extraction.
- **Q3 — Automate and validate:** Deliver daily reporting pipelines, inventory change capture, and automated data-quality checks.
- **Q4 — Measure and optimise:** Compare outcomes against baselines, review costs and capacity, and decide whether forecasting is justified.

## Ownership

- **Head of Operations:** Business priorities and approval of core business definitions.
- **Data Engineer:** Extraction, warehouse reliability, monitoring, and technical data controls.
- **Analytics Engineer / BI Developer:** SQL transformations, reporting logic, and reconciliation.
- **PHP/MySQL developer:** Production application support and database integration.
- **Designated privacy or compliance owner:** Customer-data complaint handling and applicable obligations.

## Cost Management

The proposed FinOps guardrail introduces an approved monthly budget, cost alerts, monthly spending reviews, and measures such as cost per 1,000 orders processed.

Alert thresholds and spending limits require management approval before implementation. Cost optimisation must not compromise essential production operations, required inventory updates, or customer-data protections.

## Success Measures

Progress will be measured against baselines established in Q1:

- Website performance during reporting workloads.
- Unexplained differences between Operations and Finance reports.
- Staff hours spent preparing and reconciling reports.
- Traceability of customer-data copies.
- Inventory reporting freshness.
- Pipeline reliability and data-quality failures.
- Infrastructure cost and cost per 1,000 orders.

Numerical improvement targets should be agreed after the baseline is measured.

## Important Limitations

This repository contains a proposed strategy and implementation plan. Recommendations, controls, and architecture diagrams describe the intended approach; they must not be interpreted as evidence that the infrastructure has already been deployed or that the identified risks have been fully resolved.
