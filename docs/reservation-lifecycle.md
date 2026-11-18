# Reservation Lifecycle

## Initial State

PENDING

## Allowed Transitions

PENDING -> CONFIRMED
PENDING -> EXPIRED
PENDING -> CANCELLED

## Business Rules

1. Only PENDING reservations can be confirmed.
2. Expired reservations cannot be confirmed.
3. Cancelled reservations cannot be confirmed.
4. Stock release must happen exactly once.
5. Every state transition must be transactional.

## Inventory Rules

Available Stock = Total Stock - Reserved Stock

On Reservation:
Reserved Stock increases.

On Confirmation:
Total Stock decreases.
Reserved Stock decreases.

On Expiry:
Reserved Stock decreases.

On Cancellation:
Reserved Stock decreases.

## Concurrency

Payment confirmation and reservation
expiry must safely compete for the
same reservation state transition.

Only one transition may succeed.