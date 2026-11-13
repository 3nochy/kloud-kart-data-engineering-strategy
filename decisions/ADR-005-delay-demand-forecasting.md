# ADR-005: Defer demand forecasting until reporting and inventory data are dependable

- **Status:** Proposed for approval
- **Date:** 2026-11-13
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart has expressed interest in machine learning for demand forecasting, but it is not yet an immediate operational requirement. Reporting figures currently disagree, and the quality and historical coverage of sales, stock movements, returns, promotions and stockout data have not been established.

Inventory information must remain current. A forecasting model built on inconsistent or incomplete data could create misleading recommendations about what to stock.

## Decision

Defer deployment of a production demand forecasting model until reporting definitions, historical data quality and inventory reporting are sufficiently reliable. In the meantime, document the business question, identify the required data and define a simple baseline against which a future model can be evaluated.

## Alternatives considered

### Alternative A: Start developing a forecasting model immediately

- **How it would work:** Use available historical sales data to train a model and produce demand predictions.
- **Why it is attractive:** It could eventually support stock planning, reduce avoidable shortages and improve purchasing decisions.
- **Why rejected:** Data completeness, historical coverage and business definitions have not been validated. Predictions could be misleading, and a model's technical accuracy alone would not demonstrate business value.

### Alternative B: Abandon forecasting entirely

- **How it would work:** Focus exclusively on reporting and operational data controls without planning for predictive analytics.
- **Why it is attractive:** It avoids the cost and complexity of a machine learning project.
- **Why rejected:** Forecasting may become valuable once the data is reliable and Operations has a clearly defined decision that predictions can improve.

## Consequences

- **What this buys:** A lower-risk path towards forecasting, with clearer data requirements and a baseline for measuring whether a model improves decisions.
- **What this costs:** Potential forecasting benefits are delayed, and future development will still require data preparation, testing and evaluation.
- **What it costs the client if I am wrong:** Kloud Kart could miss an opportunity to improve stock availability or reduce excess inventory. A time-limited feasibility assessment can be considered if a pressing business need emerges.
- **What would make me revisit this:** Reliable historical data becomes available, stock movements and stockouts can be interpreted consistently, and Operations identifies a measurable decision that forecasting could improve.

## What this survives

The company can continue improving its data foundation while preserving forecasting as a future opportunity. If leadership requests an early AI initiative, begin with a bounded feasibility assessment and a comparison against a simple baseline. Do not rely on unvalidated predictions for operational stock decisions.