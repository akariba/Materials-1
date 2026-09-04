STRICT LIVE-WIRING FIX — STOP STATIC-TESTING THE WRONG PATH

We now have definitive LIVE proof that the upstream persistence fix
is NOT connected to the actual RPR UI.

After a fresh real Apple workflow through Steps 2.1–2.4, backend state
is still:

COMPANY ID: 0000014508
COMPANY: NOT PRESENT
PORTFOLIO/SECTOR: NOT PRESENT

STEP 2.1 SCENARIO PRESENT: NO

STEP 2.3 CONFIRMED: NO
STEP 2.3 FACTOR COUNT: 0

STEP 2.4 CONFIRMED: NO
STEP 2.4 FACTOR COUNT: 0

SELECTED COMPANY COUNT: 0

SAFE TO RUN STEP 2.5: NO

Therefore your previous:

UPSTREAM PERSISTENCE FIX: PASS

was only a static/code-level pass.

IT IS NOT A LIVE PASS.

Do not ask the user to repeat Steps 2.1–2.4 again until you fix the
actual live wiring.

Do not produce another architecture report.

============================================================
1. FIRST DETERMINE THE ACTUAL LIVE FILES
============================================================

Identify exactly which HTML and JavaScript files are served/loaded by
the real RPR application currently visible at:

http://127.0.0.1:8000

Do not assume:

rpr_step25_append.js

or any other file is active simply because it exists in the repo.

Inspect the backend/static mounting and HTML script tags.

Determine the exact live implementation files for:

Step 2.1
Step 2.2
Step 2.3
Step 2.4
Step 2.5

Return to implementation immediately after identifying them.

Do NOT modify unused/reference/v31-only files.

============================================================
2. TRACE THE REAL CONFIRM BUTTONS
============================================================

In the ACTUAL live files, find the real user actions/functions for:

Step 2.1:
Confirm Scenario / corresponding real confirmation action

Step 2.2:
Confirm Portfolio Selection

Step 2.3:
Confirm Event-Driven Risk Factors

Step 2.4:
Confirm All Sector Risk Factors

Do not infer names from old versions.

Trace from the actual onclick/event handler through to completion.

============================================================
3. WIRE PERSISTENCE INTO THE ACTUAL CONFIRM ACTION
============================================================

For each live confirmation action:

the persistence POST must execute as part of the confirmation itself.

Not:
- when Technical Diagnostics opens;
- when Step 2.5 opens;
- from a separate helper that nothing calls;
- only in tests;
- only from an unused JS append file.

Required:

USER CONFIRMS STEP
        ↓
real existing UI confirmation logic succeeds
        ↓
POST confirmed object to backend
        ↓
backend acknowledges
        ↓
step shown as Confirmed.

============================================================
4. STEP 2.1 LIVE PERSISTENCE
============================================================

When the actual Step 2.1 scenario confirmation succeeds, persist the
real confirmed scenario.

Backend must then report:

step21_confirmed = true
scenario_context present = true.

Use the existing scenario object already shown in the UI.

Do not regenerate it.

============================================================
5. STEP 2.2 LIVE PERSISTENCE
============================================================

When the actual Step 2.2 portfolio selection is confirmed, persist:

- selected sector/portfolio
- selected companies
- company IDs
- company names
- genuine identifiers already available

For the Apple acceptance case:

company_id 0000014508

must resolve server-side to:

Apple Inc.

Do not hard-code Apple.

Use the real confirmed Step 2.2 record.

============================================================
6. STEP 2.3 LIVE PERSISTENCE
============================================================

When the actual Step 2.3 confirmation succeeds:

POST the exact real factors currently rendered/confirmed.

For the expected current workflow:

factor_count = 5.

NO synthetic factors.
NO fixtures.
NO replacement generation.

The backend must store the exact factor objects the analyst confirmed.

============================================================
7. STEP 2.4 LIVE PERSISTENCE
============================================================

When the actual Step 2.4:

Confirm All Sector Risk Factors

action succeeds:

POST the exact 5 confirmed sector-inherent factors.

Preserve their:

IDs
names
weights
importance
metric/scoring structures needed by Step 2.5.

Again:

NO regeneration.
NO synthetic data.

============================================================
8. CONFIRMATION MUST FAIL CLOSED IF PERSISTENCE FAILS
============================================================

This is important.

Do not visually display a step as successfully Confirmed if its
authoritative persistence POST failed.

For this POC, the order should be:

local validation
→ persistence POST
→ backend 200/accepted
→ Confirmed state.

If persistence fails, show a controlled failure and leave the step
unconfirmed.

This prevents the exact current situation:

UI says Confirmed
but backend has 0 factors.

============================================================
9. ADD MINIMAL SAFE BACKEND LOGGING
============================================================

For each successful confirmation POST, log only:

STEP21_CONFIRMED scenario=yes

STEP22_CONFIRMED sector=<sector> company_count=<n>

STEP23_CONFIRMED company/sector-key=<key> factor_count=<n>

STEP24_CONFIRMED company/sector-key=<key> factor_count=<n>

No huge JSON.
No secrets.

This lets us prove the live UI actually reached the backend.

============================================================
10. DO NOT RELY ON STEP 2.5 TO RECONSTRUCT HISTORY
============================================================

Step 2.5 should consume the authoritative confirmed backend state.

Do not keep adding more browser-global recovery logic to Step 2.5.

Do not make Step 2.5 guess what happened upstream.

============================================================
11. VERIFY THE LIVE-ASSET PATH
============================================================

Because previous static tests passed while the application failed,
verify that the files you changed are actually loaded by the served
application.

Add no permanent debug UI.

Use source/static routing inspection, file references and safe server
logging.

If browser cache could load an old JS asset, ensure the current local
POC page reloads the changed asset appropriately using the smallest
existing mechanism.

Do not introduce a build pipeline.

============================================================
12. TESTS
============================================================

Keep useful tests, but tests are not acceptance.

Fix failing persistence tests that represent this flow.

Do not spend time fixing unrelated test-suite path issues such as
missing historical Step 2.1 test files or missing Node tooling unless
they directly block this implementation.

Python/backend tests relevant to persistence must pass.

============================================================
13. DO NOT TOUCH DOWNSTREAM COMPONENTS
============================================================

Do NOT modify:

- Stylus
- SEC grounding
- Runner
- Runner token
- Step 2.5 assessment logic
- Step 2.5 schema
- Step 3
- v31 styling

Current blocker is strictly:

LIVE UI CONFIRMATION
→ BACKEND CONFIRMED STATE.

============================================================
14. REMOVE FALSE PASS CRITERIA
============================================================

Do not call this PASS because:

- routes exist;
- helper functions exist;
- static tests pass;
- mocked POST succeeds.

PASS requires the actual served UI files to be wired to the backend
confirmation endpoints.

============================================================
15. STOP BEFORE USER LIVE RETEST
============================================================

After implementation:

restart backend if necessary.

Do not ask the user to run Stylus.

Do not run Step 2.5.

Return only:

LIVE UPSTREAM WIRING FIX: IMPLEMENTED / FAIL

ACTUAL LIVE STEP 2.1 FILE:
<path>
ACTUAL LIVE STEP 2.2 FILE:
<path>
ACTUAL LIVE STEP 2.3 FILE:
<path>
ACTUAL LIVE STEP 2.4 FILE:
<path>

STEP 2.1 CONFIRM WIRED TO BACKEND: YES/NO
STEP 2.2 CONFIRM WIRED TO BACKEND: YES/NO
STEP 2.3 CONFIRM WIRED TO BACKEND: YES/NO
STEP 2.4 CONFIRM WIRED TO BACKEND: YES/NO

UI CONFIRM FAILS CLOSED IF PERSISTENCE FAILS: YES/NO

FILES CHANGED:
<exact paths>

USER LIVE RETEST REQUIRED: YES

Do not continue to Step 2.5.
