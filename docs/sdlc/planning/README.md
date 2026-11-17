# Planning

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### EPIC-001 · approved · source: planning:EPIC-001

Core arithmetic calculation: the calculator performs addition, subtraction, multiplication and division on user-entered numbers and shows the result on a display.

All computation happens in the browser. Scientific functions and special-purpose calculators are explicitly out of scope.

**Related:** US-001, US-002, US-003

### EPIC-002 · approved · source: planning:EPIC-002

Calculator interface and input: a single responsive web page with an on-screen number pad, operator buttons, equals/clear controls, keyboard entry and a live result display.

The layout adapts to desktop and mobile browsers.

**Related:** US-004, US-005, US-006, US-007, US-008

### EPIC-003 · approved · source: planning:EPIC-003

Recent calculation history kept client-side for the current browser session only, with no server-side persistence.

History is held client-side and is not stored on any server. Assumption: there is no server-side persistence; history is kept at most for the duration of the browser session and is lost when the session ends.

**Related:** US-009, US-010, US-011

### EPIC-004 · approved · source: planning:EPIC-004

Anonymous, free, client-side use: no accounts, login or payments, with all computation running in the browser and no server-side storage.

These assumptions are surfaced here as explicit requirements.

**Related:** US-012, US-013, US-014
<!-- sdlc:auto:end narrative -->
