CCR — TODAY DELIVERY BATCH 1
RUNTIME HARDENING + CLEAN REGRESSION + SAFE READ PATHS

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_FINAL_DELIVERY_READINESS_AUDIT.md

This is an IMPLEMENTATION task.

Do not redesign the frontend.
Do not fabricate relationships.
Do not fabricate events.
Do not fabricate evidence.
Do not alter Phase-2 protected business data.
Do not rebaseline protected hashes.
Do not create synthetic production intelligence.
Do not weaken evidence standards.

OBJECTIVE

Remove the technical blockers identified by the final delivery audit and
prove the CURRENT product works as a running application.

==================================================
1. FIX THE BROKEN BACKEND TEST GATE
==================================================

Inspect:

backend/tests/test_distance_map.py

The audit found invalid Python syntax at line 1.

Determine whether this is:

A. an obsolete/dead test,
B. a corrupted copied fixture,
C. an active test that should still exist.

Do not blindly delete it.

If obsolete:
- quarantine/remove it from the active backend test collection in a clean,
  explainable way.

If active:
- repair the syntax while preserving the intended assertions.

Then require:

python -m pytest backend/tests -q

to collect normally.

Do NOT use an exclusion flag in the final validation.

Expected:

0 collection errors
0 failed tests
0 errors

==================================================
2. REMOVE GET-SIDE DATABASE MUTATION
==================================================

The audit identified:

GET /api/ccr/relationship-config

as potentially calling a store method that opens the SQLite database writable
and may create/seed configuration tables.

This is not acceptable for a read route.

Inspect the full call chain.

Make GET routes observational/read-only.

If initialization/seeding is required, move it to one of:

- explicit migration/bootstrap
- application startup initialization
- existing governed setup path

Do not modify business records.

Prove repeated GET requests cause:

schema delta = 0
row delta = 0
relationship delta = 0
research delta = 0
evidence delta = 0

==================================================
3. PRESERVE PHASE-2 INTEGRITY
==================================================

Do NOT rebaseline the two historical exposure-record fingerprint FAIL entries.

The current read-only recomputation passes.

Preserve the historical records as audit history.

Add a concise documented disposition explaining:

- historical verification contains two failed observations
- current protected-table recomputation matches the approved fingerprint
- no evidence of current corruption exists
- historical rows were intentionally retained

Do not erase or rewrite history.

==================================================
4. ZERO-BYTE DATABASE HYGIENE
==================================================

The audit identified a zero-byte duplicate:

backend/data/ccrig_relationship_intelligence.sqlite3

while the actual runtime database is:

backend/data/ccr_relationship_intelligence.sqlite3

Determine references.

If nothing valid references the zero-byte artifact:
remove it.

If something does reference it:
fix the reference to the canonical runtime database first,
then remove the obsolete artifact.

There must be ONE clearly documented runtime relationship-intelligence DB.

==================================================
5. START THE REAL LOCAL APPLICATION
==================================================

Use the repository-supported launch path.

Start:

BACKEND
127.0.0.1:8000

FRONTEND
127.0.0.1:5173

Do not merely inspect code.

Verify actual HTTP runtime.

Required backend checks:

/api/health
/api/ccr/status
/api/ccr/overview
/api/ccr/entities/summary
/api/ccr/entities
/api/ccr/map
/api/ccr/ai/status

Also verify one real selected entity through:

entity detail
entity research
network
evidence
events

==================================================
6. BROWSER ACCEPTANCE
==================================================

Using the running frontend, verify:

/portfolio
/entities
/network
/radar
/events
/research
/evidence
/review

For each route:

HTTP / RENDER = PASS
NO JS CRASH = PASS
NAVIGATION = PASS
ENTITY CONTEXT = PASS
EMPTY STATE = TRUTHFUL

Test:

global entity search
entity selection
URL entity persistence
browser back
browser forward
left navigation
inspector open/close
inspector tabs
Network navigation
Research navigation
Evidence navigation
AI drawer opening

Do not create production data merely to make an empty screen non-empty.

==================================================
7. NETWORK RENDERING
==================================================

Select an entity with candidate edges.

Verify:

selected entity renders
candidate nodes render
candidate edges render
candidate edges remain visibly differentiated from evidence relationships
no candidate appears confirmed
node click works
entity switch works
inspector stays synchronized
graph remains usable at approximately 50 visible nodes

If current layout overlaps badly, fix layout/rendering only.

Do not change relationship semantics.

==================================================
8. PROVIDER TRANSPORT READINESS
==================================================

Reuse ONLY the already-approved Windows/ZSA transport configuration.

Do not invent a proxy.

Execute bounded connectivity tests only.

GLEIF:
maximum 1 identity request

SEC:
maximum 1 identity/reference request

Do not execute broad discovery.

Report:

transport
TLS
HTTP
provider status
cache status

If transport works, persist only the existing governed audit/status information.

Do not create a relationship from connectivity testing.

==================================================
9. HELIX READINESS
==================================================

Inspect the actual environment.

Do not fabricate credentials.

If approved HELIX credentials/configuration already exist:

run ONE safe read-only analyst request.

Question:

Explain the selected entity using only currently supplied CCR context.
Clearly distinguish stored facts, research candidates, missing evidence,
and unknown information.

The call must NOT create:

relationship
relationship claim
evidence
external entity
event
candidate
production mutation

If HELIX is not configured:

do not fake READY.

Return the precise missing configuration requirement.

==================================================
10. FRONTEND WARNING
==================================================

Inspect the existing lint warning in the inactive legacy:

CcrPlatform.tsx

If the file is genuinely not part of the active UI:

exclude/remove the dead legacy surface cleanly from the active lint/build scope
or repair the warning with no behavioral change.

Final desired state:

lint errors = 0
lint warnings in active application = 0

==================================================
11. FULL REGRESSION
==================================================

Run without exclusions:

python -m pytest backend/tests -q

Frontend:

npm run lint
npm run build

Database:

PRAGMA integrity_check
PRAGMA foreign_key_check

Protected Phase-2 fingerprint validation.

==================================================
12. REPORT
==================================================

Create:

backend/data/CCR_TODAY_DELIVERY_BATCH1_REPORT.md

Include:

changes
root causes
runtime verification
browser route results
API results
provider transport results
HELIX result
test results
database safeguards
remaining blockers

==================================================
FINAL RESPONSE
==================================================

CCR DELIVERY BATCH 1: PASS / FAIL

LOCAL BACKEND:
PASS / FAIL

LOCAL FRONTEND:
PASS / FAIL

BROWSER ROUTES:
PASS / FAIL

BACKEND FULL TEST:
passed / failed / errors

FRONTEND BUILD:
PASS / FAIL

FRONTEND LINT:
PASS / FAIL

GET READ-ONLY SAFETY:
PASS / FAIL

DATABASE INTEGRITY:
PASS / FAIL

FOREIGN KEYS:
PASS / FAIL

PHASE-2 FINGERPRINT:
PASS / FAIL

NETWORK CANDIDATE VIEW:
PASS / FAIL

GLEIF CONNECTIVITY:
READY / UNAVAILABLE

SEC CONNECTIVITY:
READY / UNAVAILABLE

HELIX:
READY / NOT_CONFIGURED / FAIL

PRODUCTION RELATIONSHIPS CREATED:
0 / FAIL

SYNTHETIC EVENTS CREATED:
0 / FAIL

REMAINING DELIVERY BLOCKERS:
<count>

REPORT:
backend/data/CCR_TODAY_DELIVERY_BATCH1_REPORT.md

STOP.
