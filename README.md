Proceed with Phase 1 of Unix portability for CCRIG.

Goal:

The same repository must work in:

1. Windows development
2. Unix/Linux development
3. Unix/Linux deployment

Do NOT change product behavior or redesign the UI.

Preserve:

Overview
Clients
Network
Relationship Explorer
External Research
Review Queue
Relationship Definitions
AI Create Relationship
CAM-authoritative separation
existing evidence and review behavior

Implement the following.

A. REMOVE PLATFORM-SPECIFIC PATH ASSUMPTIONS

Replace Windows-specific and absolute runtime paths with pathlib-based configurable paths.

Create a central runtime configuration layer.

Support at minimum:

CCRIG_HOME
CCRIG_DATA_DIR
CCRIG_LOG_DIR
CCRIG_DATABASE_PATH
CCRIG_HOST
CCRIG_PORT

Development defaults may derive from the repository root.

Do not hardcode /opt/ccrig.
Allow /opt/ccrig as a deployment example only.

All durable runtime data must use configurable locations.

B. FRONTEND PRODUCTION BUILD

Keep Vite dev mode for development.

For Unix deployment:

npm ci
npm run build

must produce the frontend production build.

Configure FastAPI to serve the built React frontend.

Target production architecture:

Browser
   |
   v
CCRIG backend :8001
   |- /api/...       FastAPI API
   |- /...           React production build

Support React SPA fallback for routes including:

/lending
/lending/clients
/lending/network
/lending/relationships
/lending/external-research
/lending/review

Do not require Vite port 5174 in production.

C. HOST / PORT

Do not force 127.0.0.1.

Use configurable host and port.

Development can default to:
127.0.0.1:8001

Deployment must support:
0.0.0.0:8001

D. PERSISTENCE

Ensure application restart does not lose:

relationship definitions
definition versions
published relationship instances
review state
external research cache
SEC evidence metadata
user-created configuration

Do not store durable application data in temp directories.

E. LOGGING

Use CCRIG_LOG_DIR.

Make logs work on Windows and Unix.

Do not log:
credentials
tokens
Authorization headers
cookies
secret environment values

F. HEALTH CHECK

Add:

GET /api/health

Return only non-sensitive status such as:

application
database
relationship_engine
external_research
frontend_build

Possible states:
ready
degraded
unavailable

Do not add SEC credential detail yet; that comes in the next phase.

G. VALIDATION

Run:

backend tests
frontend TypeScript check
frontend production build

Then start CCRIG in production-style mode using the frontend build served by FastAPI.

Validate:

/
/lending
/lending/clients
/lending/network
/lending/relationships
/lending/external-research
/lending/review
/api/health

Return:

FILES CHANGED
PATH CHANGES
NEW ENVIRONMENT VARIABLES
FRONTEND SERVING MODEL
PERSISTENCE MODEL
TEST RESULTS
MANUAL VALIDATION RESULTS
REMAINING UNIX BLOCKERS

Do not move to Helix/Stylus work yet.
