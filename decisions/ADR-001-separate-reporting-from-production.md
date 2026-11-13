# ADR-001: Reporting reads from a read replica, not from the production database

- **Status:** Proposed for approval
- **Date:** 2026-11-13
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Orders, inventory and customer accounts share one MySQL database on the same machine as the live website. Monday data exports have been associated with two website slowdowns in the past month, although the exact technical cause has not been independently verified.

Kloud Kart must keep the website available, maintain current stock counts and work within a limit of two data hires. A second server or read replica has already been pre-approved.

## Decision

Move routine reporting queries and Monday exports to a read replica, provided testing confirms that it protects the live website and meets agreed data freshness requirements. Keep live stock checks on the production database. If a replica cannot meet these requirements, evaluate the pre-approved separate server as the alternative.

## Alternatives considered

### Alternative A: Keep reporting on production and schedule exports overnight

- **How it would work:** Run exports during quieter hours and limit their resource usage.
- **Why it is attractive:** It avoids additional infrastructure and reduces the immediate operational burden on a small team.
- **Why rejected:** Scheduling may reduce the risk but does not separate reporting from live transactions. As order volumes grow and the Nigeria pilot progresses, the problem could recur.

### Alternative B: Introduce a managed cloud warehouse immediately

- **How it would work:** Copy data from MySQL into a cloud warehouse and direct reporting queries to that platform.
- **Why it is attractive:** It creates a foundation for historical analysis and more advanced analytics.
- **Why rejected:** Platform costs, data requirements, migration effort and ongoing support needs have not been established. It also does not resolve the need to agree on reporting definitions first.

## Consequences

- **What this buys:** Separates routine reporting workloads from live transactions and provides a controlled path for improving reporting reliability.
- **What this costs:** Additional infrastructure, monitoring, replication management, testing and another copy of customer data to include in data governance and deletion procedures.
- **What it costs the client if I am wrong:** Replication lag could make reports inaccurate or stale. If live stock checks were moved to a lagging replica, overselling could result. Stock checks must therefore remain on production unless a separately tested design proves the freshness requirement can be met.
- **What would make me revisit this:** Testing shows unacceptable replication lag, the replica cannot support required reporting queries, infrastructure costs outweigh the benefits, or new business requirements demand a different architecture.

## What this survives

This approach allows reporting capacity to grow separately from the live website as order volumes increase. It still requires monitoring and operational ownership. If the replica cannot meet freshness or reliability requirements, the design must be reviewed rather than assumed to work.