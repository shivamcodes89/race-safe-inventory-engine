# Race-Safe Inventory & Reservation Engine

A production-oriented inventory reservation
backend designed to prevent overselling
under concurrent requests.

## Problem

Multiple users may request the last available
product simultaneously.

## Solution

- PostgreSQL transactions
- Row-level locking
- Atomic inventory updates
- Temporary stock reservations
- Idempotency keys
- Redis caching
- BullMQ background workers
- Automated testing and load testing

## Technology Stack

- Node.js
- Express.js
- PostgreSQL
- Redis
- BullMQ
- React
- Docker
- Jest
- Supertest
- k6

## Project Status

Currently under development.

## Development Duration

4 Weeks