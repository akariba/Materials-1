CLIENT CORRELATION — SAFE RESET CONTINUATION

We now know:

AUTHORITATIVE MASTER SOURCE:
backend/Customer_latest.parquet

ACTUAL MASTER ROWS:
3,670,650

COLUMNS:
21

Existing backend/data/ccr_clients.sqlite3 contains 3,658,305 rows and is NOT
yet accepted as the authoritative master database.

The previous cleanup was correctly blocked because this workspace was not a
Git repository.

OBJECTIVE

Create a safe recovery checkpoint, then complete the clean reset.

Do NOT build the new product yet.

==================================================
1. CREATE EXTERNAL RECOVERY SNAPSHOT
==================================================

Before deleting/moving anything, create a timestamped recovery directory
OUTSIDE the active repository, for example:

../ccrig-master-pre-reset-backup/

Preserve:

- frontend source
- backend source
- config
- scripts
- tests
- reports
- current relationship database
- existing client database
- provider implementation
- README/documentation

Do not duplicate large immutable source datasets unnecessarily if storage is
an issue.

For large authoritative source files, preserve their current location and
record:

path
size
SHA-256

At minimum record hashes for:

backend/Customer_latest.parquet
backend/data/ccr_clients.sqlite3
backend/data/ccr_relationship_intelligence.sqlite3
backend/thousandClients.csv

Verify recovery snapshot exists before continuing.

==================================================
2. INITIALIZE GIT FOR ACTIVE SOURCE
==================================================

Initialize Git in the active repository.

Create a sensible .gitignore excluding:

venv
node_modules
dist
__pycache__
pytest caches
temporary caches
large SQLite databases
Parquet source data
generated provider caches

Do NOT delete ignored files.

Commit the CURRENT code/config/frontend/scripts/tests state as:

pre-client-correlation-reset

This is the rollback checkpoint.

==================================================
3. COMPLETE THE CLEAN RESET
==================================================

Now remove the OLD PRODUCT from the active application.

Remove from active frontend:

Portfolio
old Entities
old Entity Intelligence
old Network
Radar
Events
Research dashboard
Evidence dashboard
Review
old Inspector
AI drawer
old CCR navigation
old CSS/dashboard components

The active frontend should become extremely small.

Keep only:

frontend/src/main.tsx
frontend/src/App.tsx
minimal base styles

Temporary page:

CLIENT CORRELATION

Master client universe:
3,670,650 source rows

New correlation workspace under construction.

No cards.
No dashboard.
No old navigation.

==================================================
4. REMOVE OLD ACTIVE BACKEND PRODUCT ROUTES
==================================================

Remove old CCR application routes from active mounting.

Do NOT destroy reusable provider code.

Preserve reusable:

SEC provider
GLEIF provider
Web provider
HTTP/proxy/TLS transport
source hashing
source provenance
evidence utilities

The active backend should temporarily contain only:

health/status
future client-universe foundation
reusable providers

Do not implement relationship discovery yet.

==================================================
5. REMOVE OLD GENERATED NOISE
==================================================

Move old:

CCR reports
phase reports
UI reports
research reports
test diagnostics
old relationship database
old derived client database

to the EXTERNAL recovery/archive location.

They should no longer clutter:

backend/data/

Keep the authoritative master source untouched.

Do not delete source data.

==================================================
6. IMPORTANT DATA DECISION
==================================================

Do NOT use ccr_clients.sqlite3 as the new master database yet.

Reason:

Customer_latest.parquet = 3,670,650 rows
ccr_clients.sqlite3     = 3,658,305 rows

Difference = 12,345 rows

The new master database will be rebuilt or reconciled from the authoritative
Parquet in the NEXT task.

Do not investigate the discrepancy deeply yet.

==================================================
7. FINAL ACTIVE PRODUCT SHAPE
==================================================

After reset, the active workspace should be conceptually:

frontend/
    minimal client-correlation shell

backend/
    minimal API
    providers/
    reusable evidence/source utilities

backend/Customer_latest.parquet
    authoritative 3.67M master source

No active old CCR application.

No active 16k-centered workflow.

No active old relationship dashboard.

==================================================
8. VALIDATE
==================================================

Verify:

authoritative parquet unchanged
row count still 3,670,650
SHA unchanged

SEC provider code preserved
GLEIF provider code preserved
Web provider code preserved

frontend builds

backend starts

minimal page loads

old routes are no longer active

Git rollback checkpoint exists

external recovery snapshot exists

==================================================
FINAL RESPONSE
==================================================

CLIENT CORRELATION SAFE RESET: PASS / FAIL

GIT CHECKPOINT:
PASS / FAIL

RECOVERY SNAPSHOT:
PASS / FAIL

AUTHORITATIVE MASTER:
backend/Customer_latest.parquet

MASTER ROWS:
3,670,650

MASTER MODIFIED:
NO / FAIL

OLD UI ACTIVE:
NO / FAIL

OLD CCR WORKFLOW ACTIVE:
NO / FAIL

SEC PRESERVED:
YES / NO

GLEIF PRESERVED:
YES / NO

WEB PRESERVED:
YES / NO

ACTIVE FRONTEND:
minimal client-correlation shell

ACTIVE BACKEND:
minimal API + reusable providers

STOP.

DO NOT BUILD THE NEW DATABASE YET.
