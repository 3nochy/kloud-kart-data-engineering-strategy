# ADR-002: Defer selection of a full warehouse platform until requirements and costs are measured

- **Status:** Proposed for approval
- **Date:** 2026-11-13
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart is considering a data warehouse or lakehouse. The developer has expressed a preference for Snowflake or BigQuery, while Finance is concerned about recurring costs. The company can hire only two data professionals this financial year, and its reporting definitions, expected data volumes, platform requirements and support costs have not been fully established.

## Decision

Defer selecting a full warehouse platform until reporting requirements, data quality needs, expected usage and total costs have been documented. First establish a reliable reporting process separated from the production workload, then compare suitable platforms using the same evaluation criteria.

## Alternatives considered

### Alternative A: Adopt a managed cloud warehouse immediately

- **How it would work:** Select a platform and begin loading operational data into it for reporting and analytics.
- **Why it is attractive:** It could support larger datasets, historical analysis and future forecasting.
- **Why rejected:** Choosing a platform before defining requirements could create unnecessary expenditure and implementation work. The preferred platform has not yet been justified through a cost comparison.

### Alternative B: Continue using spreadsheets as the main reporting solution

- **How it would work:** Continue exporting data and maintaining separate spreadsheets for Operations and Finance.
- **Why it is attractive:** It avoids a new platform bill and allows staff to continue using familiar tools.
- **Why rejected:** It preserves manual reporting effort, inconsistent figures and weak control over copied customer lists as the business grows.

## Consequences

- **What this buys:** Time to establish reporting requirements and compare costs before committing to a platform.
- **What this costs:** Advanced analytics and warehouse capabilities will be delayed, and a later platform assessment will still require staff time.
- **What it costs the client if I am wrong:** Deferring the platform could delay benefits that an earlier implementation might have delivered. A scheduled review and documented selection criteria will reduce the risk of indefinite postponement.
- **What would make me revisit this:** Reporting needs exceed what the initial reporting setup can support, historical analysis becomes a clear business requirement, or a costed proposal demonstrates sufficient value to justify investment.

## What this survives

The company can improve reporting without committing to a large platform prematurely. If leadership requests a platform decision earlier, compare realistic costs, technical fit, security and support requirements before selecting one.