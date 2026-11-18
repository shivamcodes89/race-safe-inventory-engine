# Requirements Traceability Matrix

| Requirement | Implementation | Test |
|---|---|---|
| FR-05 | Reservation Service | TC-01 |
| FR-06 | Inventory Repository | TC-02 |
| FR-07 | Expiry Worker | TC-03 |
| FR-08 | Reservation Service | TC-04 |
| FR-09 | Payment Service | TC-05 |
| FR-10 | Order Service | TC-06 |
| FR-12 | Idempotency Service | TC-07 |
| NFR-01 | Database constraints and locking | TC-08 |
| NFR-06 | Worker recovery | TC-09 |
| NFR-08 | k6 load tests | TC-10 |

## Critical Test Cases

TC-01: Successful reservation

TC-02: Concurrent reservation without overselling

TC-03: Automatic reservation expiry

TC-04: Reservation cancellation

TC-05: Payment failure

TC-06: Payment success

TC-07: Duplicate idempotency key

TC-08: Stock invariant verification

TC-09: Background worker recovery

TC-10: Load testing