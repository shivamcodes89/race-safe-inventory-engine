Project Glossary

Project: Race-Safe Inventory & Reservation Engine
Version: 1.0
Status: Initial Draft

Term| Definition
Inventory| The stock quantity maintained for a product
Total Stock| The total quantity currently owned by the system
Reserved Stock| The quantity temporarily held by active reservations
Available Stock| Quantity that can still be reserved; total stock minus reserved stock
Reservation| A temporary allocation of inventory for a customer
Reservation Expiry| The time after which an eligible pending reservation is no longer valid
Overselling| Accepting reservations or sales beyond the actual available stock
Race Condition| A situation where concurrent operations produce an incorrect result because their execution overlaps
Concurrency| Multiple operations executing during overlapping periods
Transaction| A group of database operations treated as one atomic unit
Atomicity| A transaction either commits its complete set of changes or does not commit them
Row-Level Lock| A database lock that controls concurrent access to selected rows
Idempotency| A property where repeating the same supported operation does not create additional unintended effects
Idempotency Key| A client-provided identifier used to recognize retries of the same operation
Source of Truth| The authoritative system that determines the correct value of data
PostgreSQL| The relational database used as the authoritative store for inventory and reservation data
Redis| An in-memory data store used for supporting caching and queue infrastructure
BullMQ| A job and queue library for Node.js that uses Redis
Background Worker| A process that performs asynchronous tasks outside the main request-response flow
Retry| Reattempting an operation after a failure
Deadlock| A situation where transactions wait on one another's locks and cannot proceed
Reconciliation| A process that checks and corrects inconsistencies between related system records
Modular Monolith| An application deployed as one unit but organized into separate logical modules
API| An interface that allows software components to communicate
Endpoint| A specific API URL and method used for an operation
Authentication| Verifying the identity of a user or system
Authorization| Checking whether an authenticated identity has permission to perform an operation
RBAC| Role-Based Access Control; permissions are assigned through roles
JWT| JSON Web Token, a token format commonly used to carry authentication claims
Validation| Checking whether input satisfies defined rules
Unit Test| A test that verifies a small isolated unit of code
Integration Test| A test that verifies multiple components work together
Concurrency Test| A test that checks behavior when operations execute at the same time
Load Test| A test that evaluates system behavior under an expected workload
Stress Test| A test that evaluates behavior beyond expected workload levels
CI/CD| Continuous Integration and Continuous Delivery or Deployment
Docker| A platform for packaging and running applications in containers
Health Check| A check that reports whether a service is functioning or ready
Observability| The ability to understand internal system behavior through logs, metrics, and traces
Pino| A structured logging library for Node.js
OpenAPI| A standard specification for describing HTTP APIs
Nginx| A web server and reverse proxy commonly used in application deployments

Naming Conventions

The project will use these terms consistently:

- "total_stock": total quantity recorded for a product.
- "reserved_stock": quantity held by active reservations.
- "available_stock": calculated quantity available for reservation.
- "PENDING": reservation awaiting completion.
- "CONFIRMED": reservation successfully confirmed.
- "EXPIRED": reservation whose validity period has ended.
- "CANCELLED": reservation cancelled according to business rules.

Exact database field names, API naming conventions, and state-transition rules will be finalized in the relevant design phases.