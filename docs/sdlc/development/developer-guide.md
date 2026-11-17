# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `ba3868a` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
Mini Calculator is a generated two-app repository: a Vite + React 19 single-page frontend that renders approved screens against seeded sample data, and a FastAPI 0.115 backend scaffold that currently exposes only a health-check route. The backend uses SQLAlchemy 2.0 models (none defined yet) against a SQLite file by default, with Postgres 16 available via docker-compose when DATABASE_URL is pointed at it. The frontend is not yet wired to the backend API client (src/lib/api.ts); screens still use static sample data.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm/Vite, React 19, TypeScript 5.6 tooling)
- npm
- Python 3.12
- pip
- Docker and Docker Compose (optional, for the Postgres 16 service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository
2. Copy .env.example to .env and fill in values as needed
3. cd backend && pip install -r requirements.txt
4. (optional) docker compose up -d db  # starts Postgres 16 if you want to use it instead of the default SQLite file
5. (optional) set DATABASE_URL to point at Postgres instead of the SQLite default (sqlite:///./app.db)
6. cd backend && uvicorn app.main:app --reload  # starts the API on http://localhost:8000
7. cd frontend && npm install
8. cd frontend && npm run dev  # starts the SPA on the Vite dev server (default http://localhost:5173)
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| backend dev | `uvicorn app.main:app --reload` | Runs the FastAPI app with auto-reload (run from backend/) |
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA (run from frontend/) |
| frontend build | `npm run build` | Bundles the app with Vite; does not typecheck |
| frontend preview | `npm run preview` | Serves the production build locally |
| db up | `docker compose up -d db` | Starts the Postgres 16 container defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `frontend/` | React 19 + Vite SPA: approved screens, navigation shell, UI/icon libraries, and API client seam |
| `frontend/src` | App source: main.tsx entry, lib/ (api.ts, ui.tsx, icons.tsx, navigate.ts), index.css |
| `frontend/e2e` | Playwright end-to-end specs and support helpers |
| `backend/` | FastAPI service: app package, tests, Dockerfile, requirements |
| `backend/app` | Application code: main.py (entrypoint/lifespan/CORS/health), database.py (engine/session), models.py (SQLAlchemy Base), schemas.py (Pydantic stub response), routers/ (empty, one router per component planned) |
| `backend/tests` | pytest suite: unit/ and integration/ test directories, with a health-check integration test |
| `.devcontainer/` | VS Code devcontainer configuration |
| `.quorq/` | Quorq platform handoff metadata |
| `docker-compose.yml` | Defines the Postgres 16 database service for local development |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend routes are generated as typed stubs (StubResponse in schemas.py) until a handler is implemented, keeping the service startable and its OpenAPI spec complete
- SQLAlchemy models inherit from the shared Base in app/database.py; app/main.py imports app.models before calling Base.metadata.create_all on startup (no migrations yet)
- One FastAPI router per architecture component that owns endpoints, under backend/app/routers/
- Backend tests are split into tests/unit and tests/integration
- DATABASE_URL env var selects the database; defaults to a local SQLite file so the backend runs with no external DB
- CORS allowed origins are controlled via the ALLOWED_ORIGINS env var (comma-separated), falling back to the Vite dev server origins
- Frontend API access is centralized in src/lib/api.ts (apiFetch, API_BASE_URL, session token helpers); screens currently render seeded sample data rather than calling it
- Frontend session token is stored in localStorage and sent as a Bearer token, falling back to a shared API secret (VITE_API_SECRET_KEY)
- Frontend component tests live beside the components they cover and run under Vitest with jsdom; Playwright e2e specs live in e2e/
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend test | `pytest` | Runs backend unit/integration tests (run from backend/) |
| backend lint | `ruff check .` | Lints backend Python code |
| backend format | `ruff format .` | Formats backend Python code |
| frontend test | `npm run test` | Runs Vitest component tests |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit (not run as part of build) |
| frontend lint | `npm run lint` | Runs ESLint over the app (gate during development) |
| frontend lint:fix | `npm run lint:fix` | Runs ESLint and applies automatic fixes |
| frontend format check | `npm run format:check` | Checks formatting with Prettier |
| e2e install | `npm run test:e2e:install` | Installs the Chromium browser for Playwright |
| e2e test | `npm run test:e2e` | Runs Playwright acceptance tests; without E2E_BASE_URL it boots the backend (from backend/.venv) and builds/serves the frontend itself |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend calls to the API fail with a CORS error | Set the ALLOWED_ORIGINS env var on the backend to include the frontend's origin, or run the frontend on the default dev origins (http://localhost:5173 or http://127.0.0.1:5173) |
| `npm run build` succeeds but the app has type errors | Run `npm run typecheck` (tsc --noEmit) separately -- build does not typecheck |
| `pytest` run from backend/ fails with 'cannot import app' | Run pytest from the backend/ directory so pytest.ini's pythonpath = . applies, or ensure you are not running it from elsewhere |
| Playwright e2e tests fail to start the backend | Ensure backend dependencies are installed into backend/.venv before running `npm run test:e2e`, since the Playwright config launches uvicorn from backend/.venv/bin/python |
| Backend can't reach a database | By default DATABASE_URL is unset and the backend uses a local SQLite file (sqlite:///./app.db) -- no server is required. Only set DATABASE_URL if you intentionally started the Postgres container via `docker compose up -d db` |
<!-- sdlc:auto:end troubleshooting -->
