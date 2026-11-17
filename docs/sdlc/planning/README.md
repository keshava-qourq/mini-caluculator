# Planning

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### EPIC-001 · approved · source: planning:EPIC-001

Core arithmetic engine for the calculator: performs addition, subtraction, multiplication and division on user-entered numbers and displays the result.

Goal: The calculator performs the four standard arithmetic operations (addition, subtraction, multiplication, division) on numbers the user enters, and shows the result on a display. All computation happens in the browser. Scientific functions and special-purpose calculator features are explicitly out of scope. Associated stories: US-001 (basic operations), US-002 (decimal number entry/calculation), US-003 (safe division-by-zero handling).

**Related:** US-001, US-002, US-003

### EPIC-002 · approved · source: planning:EPIC-002

The calculator's user interface: a single responsive web page with on-screen number pad, operator/equals/clear controls, a live display, and keyboard input support.

Goal: The calculator is a single responsive web page with an on-screen number pad, operator buttons, equals and clear/reset controls, and a live result display. Users can also enter numbers and operators from the keyboard. The layout adapts to desktop and mobile browsers. Associated stories: US-004 (on-screen button entry), US-005 (live display of entry/result), US-006 (keyboard entry), US-007 (clear/reset control), US-008 (desktop/mobile responsive layout).

**Related:** US-004, US-005, US-006, US-007, US-008

### EPIC-003 · approved · source: planning:EPIC-003

Session-only history of recently completed calculations, held client-side with no server persistence.

Goal: The calculator keeps a list of recently completed calculations for the current browser session only. History is held client-side and is not stored on any server. Assumption stated in the epic: there is no server-side persistence; history is kept at most for the duration of the browser session and is lost when the session ends. Associated stories: US-009 (view recent calculations), US-010 (history limited to browser session), US-011 (clear session history).

**Related:** US-009, US-010, US-011

### EPIC-004 · approved · source: planning:EPIC-004

The calculator is free, anonymous, and performs all computation client-side with no accounts, login, payment, or server-side storage.

Goal: The calculator is free to use and usable anonymously with no accounts, login or payments. All computation runs in the browser with no server-side storage of calculations. These assumptions are surfaced here as explicit requirements. Associated stories: US-012 (anonymous use, no account), US-013 (free of charge), US-014 (computation runs entirely in the browser, not persisted server-side).

**Related:** US-012, US-013, US-014

### SPRINT-1 · approved · source: planning:Sprint 1

First sprint of the approved version-1 plan, delivering the core arithmetic engine along with the on-screen number pad, live display, clear/reset, decimal entry, and safe divide-by-zero handling.

Sprint: Sprint 1. Goal: Core calculator: arithmetic engine, on-screen number pad, live display, clear/reset, decimal entry and safe divide-by-zero handling. Capacity: 20 points. Part of plan version 1 (status: approved).

**Related:** EPIC-001, EPIC-002

### SPRINT-2 · approved · source: planning:Sprint 2

Second sprint of the approved version-1 plan, delivering keyboard input, responsive desktop/mobile layout, session-only calculation history, and confirmation of anonymous/free/client-side-only operation.

Sprint: Sprint 2. Goal: Keyboard input, responsive desktop/mobile layout, session-only calculation history, and confirmation of anonymous/free/client-side-only operation. Capacity: 20 points. Part of plan version 1 (status: approved).

**Related:** EPIC-002, EPIC-003, EPIC-004
<!-- sdlc:auto:end narrative -->
