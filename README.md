STRICT FIX — STEP 2.5 CONTEXT HANDOFF

We now have a confirmed functional defect.

Current backend state after completing Steps 2.3 and 2.4 in the browser:

COMPANY ID: 0000014508
STEP 2.3 FACTOR COUNT: 0
STEP 2.4 FACTOR COUNT: 0
STEP 2.3 CONFIRMED: NO
STEP 2.4 CONFIRMED: NO

Backend logs prove:

NO POST /api/v1/rpr/step25/context was received.

Do NOT ask me to keep reopening Technical Diagnostics.

Critical business state must not depend on opening a diagnostics panel.

FIX THIS NOW.

Do NOT modify:
- Step 2.3 generation
- Step 2.4 generation
- Stylus preset
- Runner
- SEC grounding
- scoring methodology
- Step 3
- UI styling

============================================================
1. REQUIRED CORRECT BEHAVIOUR
============================================================

Immediately before any Step 2.5 assessment can start, the frontend must:

1. read the CURRENT real confirmed browser state;
2. build the Step 2.5 context;
3. POST it to:

   /api/v1/rpr/step25/context

4. verify backend accepted it;
5. verify the payload contains:
   - selected company
   - real Step 2.1 scenario
   - real confirmed Step 2.3 factors
   - real confirmed Step 2.4 factors;
6. only then allow:

   POST /api/v1/rpr/step25/run

This must happen automatically as part of the real Run Assessment flow.

It must NOT depend on opening Technical Diagnostics.

============================================================
2. USE REAL BROWSER STATE ONLY
============================================================

Use the actual existing browser objects/functions that already contain
confirmed workflow state.

You previously identified objects conceptually such as:

window.RPR_SAFE_APPEND_STATE
window.RPR_STEP24_APPEND_STATE
S25.selectedCompanyId
confirmedStep23Factors()
confirmedStep24FactorsForCompany(...)

Use the actual existing implementation.

DO NOT create synthetic factors.

DO NOT fabricate replacement factors.

DO NOT silently fall back to fixtures.

============================================================
3. PRE-RUN VALIDATION GATE
============================================================

Before /run, require:

selected company count = 1

Step 2.3 confirmed = true
Step 2.3 factor count = 5

Step 2.4 confirmed = true
Step 2.4 factor count = 5

Step 2.1 scenario present = true

If any condition fails:

DO NOT call /run.

Return the user to a controlled readiness state explaining exactly
which upstream state is missing.

No technical credit result.

============================================================
4. APPLE ACCEPTANCE SCOPE
============================================================

For the current acceptance case require:

Company ID: 0000014508

Confirm canonical company is Apple Inc.

The Run Assessment action for this acceptance test must execute:

ONE company only.

Not 32.

Do not change the broader Step 2.2 portfolio itself.

This is assessment execution scope only.

============================================================
5. CONTEXT REGISTRATION MUST BE IDEMPOTENT
============================================================

Calling context registration more than once must be safe.

For example:

enter Step 2.5
→ context can register

click Run Assessment
→ context MUST register/refresh again immediately before /run

This guarantees the backend receives the most current confirmed state.

Do not rely on stale backend memory after a restart.

============================================================
6. BACKEND RESTART BEHAVIOUR
============================================================

The backend is currently in-memory for this POC.

Therefore after backend restart:

the next Run Assessment action must re-register context automatically
from the browser state.

The user must NOT have to manually regenerate Steps 2.3/2.4 solely
because the backend restarted, provided the real confirmed browser
state still exists.

============================================================
7. DO NOT START STYLUS UNTIL CONTEXT IS VERIFIED
============================================================

Sequence must be:

CLICK RUN ASSESSMENT
        ↓
buildContextPayload()
        ↓
POST /step25/context
        ↓
backend response confirms:
company = Apple
ED count = 5
SI count = 5
        ↓
ONLY THEN
POST /step25/run.

Never call Runner first and discover later that the factor context was
empty.

============================================================
8. VERIFY THE FIX WITHOUT RUNNING APPLE YET
============================================================

After implementing this fix:

Do NOT start Stylus.

Use the current real browser session.

Trigger only the new context-registration/preflight path.

Then inspect backend state.

Required:

COMPANY: Apple Inc.
COMPANY ID: 0000014508

REAL STEP 2.3 FACTOR COUNT: 5
REAL STEP 2.4 FACTOR COUNT: 5

STEP 2.3 CONFIRMED: YES
STEP 2.4 CONFIRMED: YES

COMPANY COUNT FOR /run: 1

Do not run the actual assessment yet.

============================================================
9. STOP CONDITION
============================================================

Return only:

CONTEXT HANDOFF FIX: PASS / FAIL

COMPANY:
COMPANY ID:

REAL ED FACTORS:
<count>

REAL SI FACTORS:
<count>

STEP 2.3 CONFIRMED:
YES / NO

STEP 2.4 CONFIRMED:
YES / NO

COMPANY COUNT FOR NEXT RUN:
<number>

SAFE TO RUN APPLE:
YES / NO

FILES CHANGED:
exact paths

Do not start Apple.
Do not work on another task.
