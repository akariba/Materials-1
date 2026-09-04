STRICT FIX — PERSIST CONFIRMED UPSTREAM STATE FOR STEP 2.5

STOP trying to make Step 2.5 infer critical confirmed state from
fragile browser-memory globals.

The latest live test proves the current handoff still fails:

COMPANY ID: 0000014508
COMPANY: NOT REGISTERED
STEP 2.1 SCENARIO PRESENT: NO
STEP 2.3 FACTOR COUNT: 0
STEP 2.3 CONFIRMED: NO
STEP 2.4 FACTOR COUNT: 0
STEP 2.4 CONFIRMED: NO

The Step 2.5 pre-run gate correctly BLOCKED /run.

That gate is correct. KEEP IT.

The defect is upstream state persistence.

============================================================
GOAL
============================================================

For this POC, confirmed business state must be persisted to the
existing backend immediately when the user confirms each upstream step.

Required chain:

Step 2.1 Confirm
→ backend stores confirmed scenario

Step 2.2 Confirm / selected company
→ backend can resolve company context from company_id

Step 2.3 Confirm
→ backend stores exactly the real confirmed ED factors

Step 2.4 Confirm
→ backend stores exactly the real confirmed SI factors

Then:

Step 2.5
→ reads those backend-confirmed objects
→ validates them
→ registers context
→ only then allows /run.

Do NOT make Step 2.5 depend primarily on inspecting window.* browser
state.

============================================================
1. USE EXISTING BACKEND ROUTES/STORES FIRST
============================================================

Inspect the current repository for existing persistence/routes for:

- confirmed Step 2.1 scenario
- confirmed Step 2.2 portfolio/company
- confirmed Step 2.3 event factors
- confirmed Step 2.4 sector factors

You previously found backend routes related to Step 2.3 and Step 2.4.

REUSE THEM.

Do not create a parallel persistence framework.

This is a POC:
in-memory backend persistence or the existing lightweight JSON/state
store is sufficient.

No database.
No Redis.
No production architecture.

============================================================
2. STEP 2.1 CONFIRMATION
============================================================

Find the real Step 2.1 confirmation handler.

When Step 2.1 is confirmed, persist the actual confirmed scenario to
the backend.

Store only the data required downstream.

At minimum:

scenario
assessment horizon
confirmed assumptions/shocks
assessment as-of context where applicable

Do not persist UI decoration.

============================================================
3. STEP 2.2 COMPANY CONTEXT
============================================================

For company_id:

0000014508

Step 2.5 currently knows the ID but not the company name.

Do not hard-code Apple.

Use the existing confirmed Step 2.2 portfolio/company data to resolve:

company_id
company_name
ticker if available
country
sector
other genuine identifiers already present

Step 2.5 should be able to retrieve the company context by company_id.

============================================================
4. STEP 2.3 CONFIRMATION
============================================================

Find the actual Step 2.3 CONFIRM action.

When the user confirms Step 2.3:

persist the EXACT confirmed Event-Driven factors to the backend.

For the current workflow acceptance target:

factor count must be exactly 5.

NO synthetic factors.
NO generated substitutes.
NO fixtures.

Persist the actual confirmed factors the user sees in Step 2.3.

Preserve:

factor_id
factor_name
weight
score/methodology fields required by Step 2.5
relevant narrative/metrics required downstream.

============================================================
5. STEP 2.4 CONFIRMATION
============================================================

Do the same for Step 2.4.

When the user clicks:

Confirm All Sector Risk Factors

persist the EXACT confirmed Step 2.4 factors.

Expected:

5 real confirmed factors
weights = 100%

Key them using the real sector/company/workflow key already used by the
application.

Do not regenerate Step 2.4 inside Step 2.5.

============================================================
6. BACKEND IS THE AUTHORITATIVE CONFIRMATION SOURCE
============================================================

After confirmation:

Step 2.5 should retrieve confirmed state from backend.

Browser state may still be used for immediate rendering, but it must
not be the only source of truth for the Step 2.5 assessment.

This solves:

- browser reload
- backend context registration
- Technical Diagnostics dependency
- guessed window globals
- losing confirmed factors between steps.

============================================================
7. STEP 2.5 PRE-RUN FLOW
============================================================

Immediately before /run:

retrieve/build:

CompanyContext
ScenarioContext
EventDrivenFactors
SectorInherentFactors

from the real confirmed backend state.

Then POST/register the Step 2.5 context.

Gate requirements:

company_name present
company_id present

Step 2.1 scenario present = true

Step 2.3 confirmed = true
Step 2.3 factor count = 5

Step 2.4 confirmed = true
Step 2.4 factor count = 5

selected assessment company count = 1

Only after ALL pass:

allow /step25/run.

Otherwise remain BLOCKED.

============================================================
8. DO NOT TOUCH DOWNSTREAM WORK
============================================================

Do NOT modify:

- Stylus preset
- SEC grounding
- Runner
- token handling
- Step 2.5 scoring
- Step 3
- v31 styling

Those are not the current blocker.

============================================================
9. REMOVE TEST SYNTHETIC FACTORS
============================================================

The diagnostic helper previously added synthetic ED factors.

Those must never leak into the real acceptance path.

Real acceptance state must be traceable to the actual Step 2.3
confirmation.

============================================================
10. TEST THE PERSISTENCE DIRECTLY
============================================================

After implementation, run static/unit tests as useful.

But do not claim PASS from static tests.

We need one live confirmation cycle after the updated JS/backend is
loaded.

After the user confirms 2.1 → 2.2 → 2.3 → 2.4 once, the backend itself
must be able to report:

COMPANY: Apple Inc.
COMPANY ID: 0000014508

STEP 2.1 SCENARIO PRESENT: YES

REAL STEP 2.3 FACTOR COUNT: 5
STEP 2.3 CONFIRMED: YES

REAL STEP 2.4 FACTOR COUNT: 5
STEP 2.4 CONFIRMED: YES

without depending on opening Technical Diagnostics.

============================================================
11. IMPORTANT RESTART BEHAVIOUR
============================================================

For the current POC, if backend persistence is only in-memory, a backend
restart may still clear it.

That is acceptable for now.

Do NOT build production persistence merely to survive process restart.

What matters is that during a normal live workflow:

2.1 → 2.2 → 2.3 → 2.4 → 2.5

the confirmed state is reliably available server-side.

============================================================
12. FINAL RESPONSE
============================================================

Do not start Stylus.

Return only:

UPSTREAM PERSISTENCE FIX: PASS / FAIL

STEP 2.1 CONFIRM PERSISTS: YES / NO
STEP 2.2 COMPANY RESOLUTION: YES / NO
STEP 2.3 CONFIRM PERSISTS: YES / NO
STEP 2.4 CONFIRM PERSISTS: YES / NO

FILES CHANGED:
exact paths

USER LIVE RETEST REQUIRED: YES

Do not continue to another task.
