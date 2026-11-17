# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECH-STACK · approved · source: requirements:technology-stack

Product owner approved a fixed technology stack: FastAPI backend, AWS cloud, PostgreSQL database, React frontend.

- Backend: FastAPI 0.115 -- all computation happens client-side with no accounts or server-side storage, so FastAPI's only job is serving the single web page; it is the platform default with minimal custom code.
- Cloud: AWS -- hosts a free, publicly reachable responsive page for desktop and mobile; platform default, uses CDN for fast delivery to anonymous visitors; hosting footprint stays small and cheap since there are no accounts or stored data.
- Database: PostgreSQL 16 -- not actually needed since there is no server-side storage of calculations (history lives only in the browser session); named as the platform default and would sit unused unless server-side storage is added later.
- Frontend: React 19 -- hosts the entire product experience: number pad, operator/clear/equals buttons, keyboard input, live display, and the arithmetic logic itself; well suited to a single interactive responsive page; also holds the optional in-session recent-calculation history client-side.
Design must use exactly this stack, no substitutions.

### REQ-SCOPE · approved · source: requirements:scope

Defines what the calculator includes and explicitly excludes. Delivery scope is 'lightweight', requirements version 1.

In scope: addition, subtraction, multiplication, division; live result display; on-screen number pad and operator buttons; equals and clear/reset controls; keyboard entry of numbers and operators; responsive layout for desktop and mobile; recent-calculation history within the browser session; anonymous use with no accounts/sign-in; all calculations run client-side with no server-side storage; free to use with no payments or subscriptions.
Out of scope: scientific functions (trig, powers, roots, logarithms, parentheses) and special-purpose calculators (loan, tip, BMI, etc.) -- not to be designed or built.

### REQ-FEAT-CALC-SCREEN · approved · source: requirements:feature:Calculator screen

Functional requirements for the main calculator screen: on-screen buttons, live display, keyboard entry, clear/reset, responsive layout.

- On-screen number pad and buttons: digits 0-9, decimal point, four operators (add, subtract, multiply, divide), equals, clear/reset; tapping/clicking adds to the current calculation and is reflected on the display.
- Live result display: updates as digits/operators are entered; shows computed result once equals is pressed.
- Keyboard entry: supports typed digits, operators (+, -, *, /), decimal point, Enter for equals, Escape or Delete to clear; each keypress reflected the same way as the matching on-screen button.
- Clear and reset: discards current entry, returns display to empty/zero starting state, leaves no pending operation.
- Responsive layout: single page adapts to screen size, laying out display and controls appropriately on narrow mobile and wide desktop screens.

### REQ-FEAT-MATH · approved · source: requirements:feature:Doing the maths

Functional requirements for the arithmetic logic: the four basic operations, decimal entry, and safe division-by-zero handling.

- Four basic operations: adds, subtracts, multiplies and divides entered numbers, showing the result when equals is pressed.
- Decimal number entry: supports non-whole numbers via a decimal point; if a decimal point already exists in the current number, any further decimal point is ignored so the number keeps a single decimal point.
- Safe division by zero: dividing by zero and pressing equals shows an error indication (e.g. 'Error') instead of a number; the calculator can be cleared to continue.

### REQ-FEAT-HISTORY · approved · source: requirements:feature:Recent history

Functional requirements for viewing and clearing the in-session calculation history.

- View session history: lists calculations completed during the current session, each with its expression and result in the order performed; shows an empty state when no calculation has been completed yet.
- Clear session history: when history has one or more entries, the user can clear it, returning the history area to its empty state without ending the session.

### REQ-FEAT-ANON · approved · source: requirements:feature:Anonymous & free use

Functional requirement that the calculator is fully usable anonymously and free of charge.

- Anonymous, free use: usable without signing up, logging in or identifying oneself; all functionality is free with no payment, billing, subscription or paywall presented at any point.

### NFR-001 · approved · source: requirements:NFR-001

Privacy: all calculations are computed in the user's own browser and never sent to or stored on any server.

Category: privacy. All calculations are worked out in the user's own browser and are never sent to, or stored on, any server.

### NFR-002 · approved · source: requirements:NFR-002

Privacy: recent-calculation history is held only in the current browser session and is cleared when that session ends.

Category: privacy. The recent-calculation history is held only in the current browser session and is cleared when that session ends, so no previous calculations are retained when the page is opened again in a new session.

### NFR-003 · approved · source: requirements:NFR-003

Compatibility: calculator works on both desktop and mobile browsers with no horizontal scrolling.

Category: compatibility. The calculator works in both desktop and mobile browsers, with all buttons and the display visible, legible and usable on narrow mobile-width screens without any horizontal scrolling.

### NFR-004 · approved · source: requirements:NFR-004

Usability: a first-time visitor can start using the calculator immediately with no account, login, payment or paywall.

Category: usability. A first-time visitor can start using the calculator straight away, with no prompt to create an account, log in, identify themselves, pay or face a paywall at any point.

### NFR-005 · approved · source: requirements:NFR-005

Performance: the display updates immediately as the user types or presses buttons, and shows the result as soon as equals is pressed.

Category: performance. The display reflects each on-screen button press and each keypress immediately as it is entered, and shows the computed result as soon as equals is pressed.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-11-17

**Capabilities in scope:** Addition, subtraction, multiplication and division, Live result display, On-screen number pad and operator buttons, Equals and clear/reset controls, Keyboard entry of numbers and operators, Responsive layout for desktop and mobile browsers, Recent-calculation history within the browser session, Anonymous use with no accounts or sign-in, All calculations run in the browser with no server-side storage, Free to use with no payments or subscriptions

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | You confirmed all computation happens in the browser with no accounts and no server-side storage, so there is no business logic for a backend to run. FastAPI's only job here is to serve the single web page to visitors. It is the platform default and does that reliably with essentially no custom code. |
| cloud | AWS | You need somewhere to host a free, publicly reachable web page that works on desktop and mobile. AWS is the platform default and comfortably hosts a single responsive page, and its CDN can serve it quickly to anonymous visitors anywhere. Because there are no accounts or stored data, your hosting footprint stays very small and cheap. |
| database | PostgreSQL | You confirmed there is no server-side storage of calculations and the only history is kept in the browser session, so the product needs no database at all. PostgreSQL is named here as the platform default; in this build it would sit unused unless you later decide to store something server-side. |
| frontend | React | Your whole product lives in the browser — the number pad, operator and clear/equals buttons, the keyboard input, the display, and the arithmetic itself. React is well suited to a single interactive page like this: it handles the button presses and keystrokes and keeps the display in sync, and it makes the responsive desktop-and-mobile layout you asked for straightforward. The optional in-session recent-calculation history also fits naturally here, held in the browser with no server involved. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Core Arithmetic Calculation

The calculator performs the four standard arithmetic operations — addition, subtraction, multiplication and division — on numbers the user enters, and shows the result on a display. All computation happens in the browser. Scientific functions and special-purpose calculators are explicitly out of scope.

### US-001: Perform the four basic operations

**Priority:** critical

> As a anonymous web user, I want to add, subtract, multiply and divide numbers I enter, so that I can get the result of a basic arithmetic calculation.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | the calculator is open with no input | I enter 7, then +, then 5, then equals | the display shows 12 |
| AC-002 | the calculator is open with no input | I enter 9, then -, then 4, then equals | the display shows 5 |
| AC-003 | the calculator is open with no input | I enter 6, then ×, then 3, then equals | the display shows 18 |
| AC-004 | the calculator is open with no input | I enter 8, then ÷, then 2, then equals | the display shows 4 |

### US-002: Enter and calculate with decimal numbers

**Priority:** high

> As a anonymous web user, I want to enter numbers with a decimal point, so that I can calculate with non-whole numbers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | the calculator is open | I enter 2.5, then +, then 1.25, then equals | the display shows 3.75 |
| AC-006 | I am entering a number that already contains a decimal point | I attempt to add a second decimal point to the same number | the additional decimal point is ignored and the number keeps a single decimal point |

### US-003: Handle division by zero

**Priority:** high

> As a anonymous web user, I want the calculator to respond safely when I divide by zero, so that I understand the operation is not valid rather than seeing a broken result.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | the calculator is open | I enter 6, then ÷, then 0, then equals | the display shows an error indication (for example 'Error') instead of a number, and the calculator can be cleared to continue |

## EPIC-002: Calculator Interface and Input

The calculator is a single responsive web page with an on-screen number pad, operator buttons, equals and clear/reset controls, and a live result display. Users can also enter numbers and operators from the keyboard. The layout adapts to desktop and mobile browsers.

### US-004: Enter calculations using the on-screen buttons

**Priority:** critical

> As a anonymous web user, I want an on-screen number pad and operator buttons, so that I can build a calculation by tapping or clicking.

| ID | Given | When | Then |
|---|---|---|---|
| AC-008 | the calculator page is open | I view the page | I see on-screen buttons for digits 0-9, a decimal point, the four operators (+, -, ×, ÷), equals and clear/reset |
| AC-009 | the calculator is open | I tap or click the on-screen buttons to enter a calculation | each press is reflected in the display as it is entered |

### US-005: See the current entry and result on a live display

**Priority:** critical

> As a anonymous web user, I want a display that updates as I enter numbers and operators and shows the result, so that I can follow what I am calculating and read the answer.

| ID | Given | When | Then |
|---|---|---|---|
| AC-010 | the calculator is open | I enter digits and an operator | the display updates to reflect the current entry immediately |
| AC-011 | I have entered a complete calculation | I press equals | the display shows the computed result |

### US-006: Enter calculations using the keyboard

**Priority:** high

> As a anonymous web user on a device with a keyboard, I want to type numbers and operators and press keys for equals and clear, so that I can calculate without using the mouse or touch.

| ID | Given | When | Then |
|---|---|---|---|
| AC-012 | the calculator page is focused | I type 3, *, 4 and press Enter | the display shows 12 |
| AC-013 | the calculator page is focused | I press the keys for digits, the operators (+, -, *, /) and the decimal point | each keypress is reflected in the display the same way as the matching on-screen button |
| AC-014 | the calculator has an entry | I press the Escape or Delete key mapped to clear | the entry is cleared |

### US-007: Clear and reset the calculator

**Priority:** critical

> As a anonymous web user, I want a clear/reset control, so that I can discard the current entry and start a new calculation.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | the calculator shows a number or result | I press the clear/reset control | the display returns to its empty/zero starting state and no previous operation remains pending |

### US-008: Use the calculator on desktop and mobile

**Priority:** high

> As a anonymous web user on any device, I want the calculator layout to adapt to my screen size, so that I can use it comfortably on both desktop and mobile browsers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-016 | I open the calculator on a narrow mobile-width screen | the page loads | all buttons and the display are visible, legible and usable without horizontal scrolling |
| AC-017 | I open the calculator on a wide desktop screen | the page loads | the calculator is laid out appropriately for the larger viewport with all controls accessible |

## EPIC-003: Recent Calculation History (Browser Session)

The calculator keeps a list of recently completed calculations for the current browser session only. History is held client-side and is not stored on any server. Assumption: there is no server-side persistence; history is kept at most for the duration of the browser session and is lost when the session ends.

### US-009: View recent calculations from this session

**Priority:** medium

> As a anonymous web user, I want to see a list of calculations I have completed during this session, so that I can refer back to earlier results.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | I have completed one or more calculations by pressing equals | I view the history area | each completed calculation is listed with its expression and result in the order it was performed |
| AC-019 | I have not completed any calculation yet | I view the history area | it shows an empty state and no entries |

### US-010: History is limited to the browser session

**Priority:** medium

> As a anonymous web user, I want my calculation history to exist only within my current browser session, so that nothing I calculate is stored on a server or retained after my session.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | I have a history of calculations in the current session | my browser session ends (for example I close the browser and reopen the page in a new session) | the history is empty and no previous calculations are retained |
| AC-021 | I am using the calculator | any calculation is completed | the calculation is not sent to or stored on any server |

### US-011: Clear the session history

**Priority:** low

> As a anonymous web user, I want to clear my recent-calculation history, so that I can remove earlier entries without ending my session.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | the history contains one or more entries | I choose to clear the history | the history area returns to its empty state |

## EPIC-004: Anonymous, Free, Client-Side Use

The calculator is free to use and usable anonymously with no accounts, login or payments. All computation runs in the browser with no server-side storage of calculations. These assumptions are surfaced here as explicit requirements.

### US-012: Use the calculator anonymously with no account

**Priority:** high

> As a anonymous web user, I want to use the calculator without signing up, logging in or identifying myself, so that I can calculate immediately with no barriers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I open the calculator page for the first time | the page loads | the calculator is immediately usable with no prompt to create an account, log in or identify myself |

### US-013: Use the calculator free of charge

**Priority:** medium

> As a anonymous web user, I want the calculator to be free with no payment or subscription, so that I can use all of its functionality at no cost.

| ID | Given | When | Then |
|---|---|---|---|
| AC-024 | I am using the calculator | I perform any operation offered by the tool | no payment, billing, subscription or paywall is presented at any point |

### US-014: Calculations run entirely in the browser

**Priority:** high

> As a anonymous web user, I want all computation to happen in my browser with no server-side storage, so that my calculations stay private to my device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-025 | I perform a calculation | the result is computed | the computation is performed client-side in the browser and the calculation is not persisted on any server |
<!-- sdlc:auto:end epics -->
