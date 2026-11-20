Problem Statement

Project: Race-Safe Inventory & Reservation Engine
Version: 1.0
Status: Initial Draft

1. Background

Online inventory systems allow multiple customers to view and reserve products. When product demand is high and stock is limited, multiple customers may attempt to reserve the same available units within a very short period.

A basic implementation may read the available stock, validate the requested quantity, and then update the inventory. However, when multiple requests execute concurrently, they may all read the same stock value before any request updates it.

This creates a race condition.

2. Main Problem

The system must prevent more stock from being reserved or sold than actually exists.

For example:

- Total stock: 1 unit.
- Available stock: 1 unit.
- Customer A requests the product.
- Customer B requests the same product at almost the same time.

Both requests must not receive successful reservations for the same unit.

Only one request may successfully reserve the available unit.

3. Root Causes

Potential causes of inventory inconsistency include:

1. Concurrent requests reading the same stock value.
2. Inventory validation and update not being performed atomically.
3. Missing database transaction boundaries.
4. Missing concurrency control.
5. Duplicate API requests caused by retries.
6. Reservation expiry jobs processing the same reservation more than once.
7. Payment confirmation racing with reservation expiry.
8. Incorrect handling of partial failures.

4. Consequences

If the system does not control these problems, it may experience:

- Overselling.
- Incorrect available stock.
- Duplicate reservations.
- Duplicate order or payment processing.
- Reservations that never expire.
- Stock that remains reserved unnecessarily.
- Inconsistent reservation and payment states.
- Customer complaints and operational difficulties.

5. Required System Behavior

The system must:

1. Validate requested quantities.
2. Check stock using an authoritative database operation.
3. Prevent concurrent requests from reserving the same units.
4. Create reservations and update inventory consistently.
5. Support safe retries using idempotency keys.
6. Release reserved stock when a reservation expires or is cancelled.
7. Confirm payment and update inventory safely.
8. Prevent expiry and payment operations from incorrectly changing the same reservation.
9. Recover from background job failures.
10. Maintain an auditable record of important state changes.

6. Important Failure Scenarios

The design must account for these scenarios:

Scenario| Expected behavior
Two customers request the last unit| At most one reservation succeeds
Customer submits the same request again| Idempotency prevents duplicate processing
Reservation expires| Reserved stock is released once
Payment succeeds before expiry| Reservation is confirmed
Expiry and payment processing overlap| Only a valid state transition succeeds
Background worker restarts| Pending expiry work can be recovered
Database transaction fails| Partial inventory changes are not committed
Customer requests more stock than available| Reservation is rejected

7. Problem Boundary

This project focuses on inventory reservation correctness, reservation lifecycle management, concurrency control, and related order/payment simulation.

It does not attempt to build a real banking or payment-processing platform.

8. Problem Statement

The objective is to design and develop a reliable inventory reservation system that prevents overselling and maintains consistent inventory and reservation states under concurrent customer requests, duplicate requests, reservation expiry, payment processing, and background worker failures.

9. Success Condition

The problem will be considered addressed when automated tests demonstrate that concurrent requests cannot reserve more units than the available inventory and that reservation lifecycle operations preserve the defined inventory invariants.