<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- No database
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Named as the platform default. There is no server-side storage of calculations and history is browser-session only, so no schema is defined and the instance stays idle in this build.

## Consequences

Provisioning an unused database adds a little cost and ops surface; it is retained for stack consistency and future server-side features and can be left out of the dev environment to save cost.
<!-- sdlc:auto:end adr -->