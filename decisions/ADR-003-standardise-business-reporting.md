# ADR-003: Establish shared reporting definitions before building more dashboards

- **Status:** Proposed for approval
- **Date:** 2026-11-13
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Nana Adjei rebuilds Monday figures from CSV exports, but Finance's spreadsheet does not match hers. The exact cause of the disagreement has not been established. Possible causes include different definitions, date ranges, treatment of refunds and cancellations, data quality problems or spreadsheet errors.

Building dashboards before investigating these differences could make inconsistent figures easier to view without making them more reliable.

## Decision

Agree and document common definitions for orders, revenue, cancellations and refunds with Operations and Finance. Use those definitions to create repeatable reports with checks for missing, duplicated and unexpected data before expanding dashboard development.

## Alternatives considered

### Alternative A: Build dashboards immediately

- **How it would work:** Connect dashboards to the available database exports and present the figures in visual form.
- **Why it is attractive:** It provides a more convenient way to view performance and could reduce manual spreadsheet preparation.
- **Why rejected:** Visualising conflicting figures does not resolve why they disagree. It could create more confusion if different teams continue using different definitions.

### Alternative B: Let each department maintain its own reporting logic

- **How it would work:** Operations and Finance continue producing reports according to their existing spreadsheet methods.
- **Why it is attractive:** It avoids the immediate effort of agreeing on definitions and changing familiar processes.
- **Why rejected:** It preserves repeated reconciliation work and leaves staff without a shared basis for important business decisions.

## Consequences

- **What this buys:** A shared basis for business reporting, clearer explanations for discrepancies and a foundation for trustworthy dashboards.
- **What this costs:** Time from Operations, Finance and technical staff to agree on definitions, document exceptions and maintain the reporting logic.
- **What it costs the client if I am wrong:** The agreed definitions may not cover every department's needs. Documented exceptions and feedback from report users will help identify gaps.
- **What would make me revisit this:** The definitions do not support actual business decisions, report discrepancies remain unexplained, or the reporting process fails to reduce preparation and reconciliation effort.

## What this survives

Even if the warehouse investment is delayed, the company can standardise its most important Monday measures and improve report consistency. Dashboard development should expand when the underlying figures are sufficiently understood and validated.