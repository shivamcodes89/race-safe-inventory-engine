Race-Safe Inventory & Reservation Engine

Document: Project Overview
Version: 1.0
Status: Initial Draft

1. Introduction

The Race-Safe Inventory & Reservation Engine is a full-stack application designed to manage product inventory and temporary reservations safely, even when multiple customers attempt to reserve the same stock at the same time.

The primary focus of this project is to prevent overselling, maintain accurate inventory records, and handle reservation lifecycle operations reliably.

The system will use PostgreSQL as the authoritative database for inventory and reservation data. Redis and background workers will support caching and asynchronous tasks.

2. Problem Summary

In an online inventory system, multiple customers may attempt to reserve the last available units of a product simultaneously.

If the application does not handle concurrent requests correctly, more customers may receive successful reservations than the actual available stock allows.

This problem is commonly known as a race condition and can result in overselling and inconsistent inventory records.

3. Proposed Solution

The system will provide a controlled reservation workflow using:

- Database transactions.
- PostgreSQL row-level locking.
- Inventory validation.
- Reservation expiry.
- Idempotency keys.
- Background workers.
- Reliable reservation state transitions.
- Automated testing of concurrent requests.

PostgreSQL will remain the final authority for stock availability. Redis will not be used as the source of truth for inventory.

4. Project Objectives

The main objectives are:

1. Prevent inventory overselling.
2. Support temporary product reservations.
3. Maintain accurate stock quantities.
4. Handle simultaneous reservation requests safely.
5. Prevent duplicate operations using idempotency.
6. Expire unpaid reservations automatically.
7. Maintain consistent reservation and payment states.
8. Provide APIs for customer and administrative operations.
9. Test system behavior under concurrent load.
10. Deploy the application using production-oriented practices.

5. Target Users

- Customers who reserve products.
- Administrators who manage products and inventory.
- Developers who maintain the system.
- Operators who monitor system health.

6. Technology Overview

Area| Technology
Backend| Node.js, Express.js
Programming language| JavaScript
Database| PostgreSQL
Cache| Redis
Background jobs| BullMQ
Frontend| React, Vite
Validation| Zod
Authentication| JWT
Logging| Pino
API documentation| OpenAPI, Swagger
Unit and integration testing| Jest, Supertest
Load testing| k6
Containerization| Docker, Docker Compose
CI/CD| GitHub Actions
Reverse proxy| Nginx

7. Architecture Approach

The initial system will use a modular monolith architecture.

Different business modules will be organized separately within one backend application. Microservices are not part of the initial implementation.

8. Core Features

- Product management.
- Inventory management.
- Temporary reservations.
- Reservation confirmation.
- Reservation cancellation.
- Reservation expiry.
- Simulated payment processing.
- Idempotent API operations.
- Background expiry processing.
- Customer and admin interfaces.
- Monitoring and logging.

9. Core Inventory Rules

The system must maintain these invariants:

- "0 <= reserved_stock <= total_stock"
- "available_stock = total_stock - reserved_stock"

When a reservation is created, reserved stock increases.

When payment succeeds, total stock and reserved stock both decrease by the reserved quantity.

When a reservation expires or is cancelled, reserved stock decreases and the quantity becomes available again.

10. Project Boundaries

This project will demonstrate safe inventory reservation and order-related workflows.

It will use simulated payment processing rather than integrating a real payment gateway.

11. Expected Outcome

The expected outcome is a tested and deployable full-stack application that demonstrates reliable inventory management, concurrency control, reservation expiry, and production-oriented backend engineering.

12. Document Status

This document establishes the initial project direction. Detailed requirements, architecture, database design, API contracts, security, testing, and deployment decisions will be documented in their respective project phases.