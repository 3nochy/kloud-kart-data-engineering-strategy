# ADR-004: Introduce traceable customer data access, exports and deletion handling

- **Status:** Proposed for approval
- **Date:** 2026-11-13
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Marketing maintains a customer list of approximately 300,000 people, and copies of that list are not tracked. Kloud Kart has also received a complaint concerning deleted customer data, with a 90-day response window specified in the case.

The facts provided do not establish whether a legal breach occurred or whether every copy of the data has been identified. The complaint needs a clear owner, documented investigation and a response plan. Customer data controls should not depend on a future warehouse implementation.

## Decision

Recommend assigning responsibility for the complaint and introducing a documented process for customer data access, exports and deletion. Record where approved exports are stored, who can access them and how deletion requests are tracked and verified. Confirm applicable obligations and deadlines with the appropriate privacy or compliance adviser.

## Alternatives considered

### Alternative A: Continue using untracked customer list copies

- **How it would work:** Marketing continues creating and sharing customer exports without maintaining a central record.
- **Why it is attractive:** It requires little immediate change and allows existing marketing activities to continue.
- **Why rejected:** The company may struggle to identify who holds customer data, which copies need updating or deletion, and whether a request has been completed.

### Alternative B: Wait until a warehouse is implemented

- **How it would work:** Introduce formal data access and deletion controls as part of the future data platform.
- **Why it is attractive:** Controls could be designed alongside a broader data architecture.
- **Why rejected:** The existing complaint and untracked copies require attention now. Waiting for a platform decision would leave current risks unresolved.

## Consequences

- **What this buys:** Clearer accountability, better visibility of customer data copies and evidence that requests have been investigated and handled.
- **What this costs:** Staff time to investigate the complaint, document exports, review access and verify deletion across identified locations.
- **What it costs the client if I am wrong:** The process may add unnecessary administrative effort or fail to identify copies outside the documented workflow. Periodic reviews and investigation findings should guide improvements.
- **What would make me revisit this:** The complaint investigation clarifies additional obligations, an audit identifies gaps in the process, or existing controls prove more effective than initially understood.

## What this survives

Customer data governance can begin before a warehouse is selected. Even if platform investment is delayed, the company can assign responsibility, document known data copies and establish a repeatable process for access and deletion requests.