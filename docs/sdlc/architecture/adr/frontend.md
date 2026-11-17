<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-11-17

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Svelte

## Decision Outcome

Chosen option: React 19, because The entire product is one interactive page — number pad, operators, keyboard input, live display and in-session history — which React 19 keeps in sync cleanly with component state and a small arithmetic module. It also makes the responsive desktop/mobile layout straightforward.

## Consequences

React is heavier than needed for a calculator, but it is the approved stack and gives a familiar, maintainable component model; the bundle stays small for a single page and is CDN-cached.
<!-- sdlc:auto:end adr -->