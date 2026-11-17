<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Flask
- Static-only hosting with no backend

## Decision Outcome

Chosen option: FastAPI 0.115, because With all computation client-side and no accounts or storage, the backend only serves the page and a health check. FastAPI 0.115 does this reliably as the platform default with essentially no custom code.

## Consequences

A dedicated backend is more than a pure static site strictly needs, but keeping the approved default avoids a stack change and leaves a clean place to add server logic later.
<!-- sdlc:auto:end adr -->