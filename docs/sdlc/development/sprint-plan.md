# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Core calculator: arithmetic engine, on-screen number pad, live display, clear/reset, decimal entry and safe divide-by-zero handling.

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Perform the four basic operations | 5 | frontend-agent | — |
| US-002 | Story | Enter and calculate with decimal numbers | 3 | frontend-agent | US-001 |
| US-003 | Story | Handle division by zero | 2 | frontend-agent | US-001 |
| US-004 | Story | Enter calculations using the on-screen buttons | 5 | frontend-agent | US-001 |
| US-005 | Story | See the current entry and result on a live display | 3 | frontend-agent | US-001 |
| US-007 | Story | Clear and reset the calculator | 2 | frontend-agent | US-001 |

## Sprint 2: Sprint 2

Keyboard input, responsive desktop/mobile layout, session-only calculation history, and confirmation of anonymous/free/client-side-only operation.

Capacity: 20 points · Committed: 16

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-006 | Story | Enter calculations using the keyboard | 3 | frontend-agent | US-004 |
| US-008 | Story | Use the calculator on desktop and mobile | 3 | frontend-agent | US-004 |
| US-009 | Story | View recent calculations from this session | 3 | frontend-agent | US-001, US-005 |
| US-010 | Story | History is limited to the browser session | 2 | frontend-agent | US-009 |
| US-011 | Story | Clear the session history | 1 | frontend-agent | US-009 |
| US-012 | Story | Use the calculator anonymously with no account | 1 | frontend-agent | — |
| US-013 | Story | Use the calculator free of charge | 1 | frontend-agent | — |
| US-014 | Story | Calculations run entirely in the browser | 2 | backend-agent | US-001 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
