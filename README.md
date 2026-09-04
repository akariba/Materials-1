STRICT FIX — STOP STEP 2.5 FROM AUTOMATICALLY RESTARTING THE OLD BATCH

We now have definitive evidence of the immediate problem.

After a clean backend restart with:

ACTIVE STEP 2.5 JOBS = 0
ACTIVE RUNNER CALLS = 0

the existing browser/UI automatically reconnects and immediately
re-triggers the previous 32-company Step 2.5 batch.

This contaminated BOTH previous Apple tests.

THIS MUST BE FIXED NOW.

Do NOT produce another diagnostic report.
Do NOT work on Step 3.
Do NOT change Stylus.
Do NOT change the preset.
Do NOT modify SEC logic.
Do NOT work on v31 styling.

Fix the Step 2.5 frontend execution/state logic.

============================================================
1. REQUIRED BEHAVIOUR
============================================================

A backend restart, page reload, reconnect, tab restore, or navigation
back to Step 2.5 must NEVER automatically start a new assessment.

Assessment execution must occur ONLY after an explicit user action:

Run Assessment

No other code path may invoke /api/v1/rpr/step25/run automatically.

============================================================
2. FIND THE AUTO-RETRIGGER
============================================================

Inspect the existing Step 2.5 frontend JavaScript.

Find every call path to:

POST /api/v1/rpr/step25/run

or the equivalent run function.

Identify the code that automatically resumes/restarts execution after:

- page load
- reconnect
- restored browser state
- localStorage/sessionStorage state
- workflow restoration
- polling
- "running" state recovery
- tab navigation.

Remove ONLY the automatic execution behaviour.

Do not remove normal workflow-state restoration.

============================================================
3. CORRECT RECOVERY SEMANTICS
============================================================

On Step 2.5 load/reconnect:

Frontend may restore:
- selected assessment mode
- selected company/cohort
- completed results
- confirmed workflow state
- filters
- display preferences.

Frontend may query backend job status.

BUT:

If backend reports NO active Step 2.5 job:

frontend MUST become IDLE.

It must NOT create a replacement job.

It must NOT interpret stale:

running=true
job_id=<old id>
assessmentInProgress=true

from browser storage as permission to rerun.

============================================================
4. STALE RUNNING STATE
============================================================

If browser/local/session storage says:

RUNNING

but backend says:

no active job

then:

clear the stale running/job state
set UI to IDLE
enable Run Assessment
do not issue POST /run.

Backend is authoritative for whether an execution is actually active.

============================================================
5. BACKEND RESTART
============================================================

After backend restart:

previous in-memory job is gone.

The frontend must detect this and show something equivalent to:

Previous assessment interrupted / no active job

or simply return to IDLE according to existing UI conventions.

It must NOT silently rerun 32 companies.

============================================================
6. NO AUTOMATIC COMPANY LOOP
============================================================

Find the current client-side loop that started the 32-company batch.

It must exist only INSIDE the explicit Run Assessment action.

It must never start from:

DOMContentLoaded
window.onload
reconnect
polling callback
restoreState()
navigation
workflow refresh.

============================================================
7. ADD A SAFE CANCELLATION/RESET PATH IF ALREADY COMPATIBLE
============================================================

Use the smallest existing approach.

When the user leaves/reloads during a client-side batch:

the client must stop submitting additional companies.

Do not invent a large job-control framework.

For the POC it is sufficient that:

closing/reloading the page stops the CLIENT from submitting new names,

and when reopened it does NOT resume automatically.

============================================================
8. DO NOT RUN 32 COMPANIES DURING VERIFICATION
============================================================

After implementing the fix:

restart backend cleanly.

Verify:

ACTIVE STEP 2.5 JOBS = 0.

Then leave Step 2.5 open for at least 60 seconds WITHOUT clicking Run.

Check backend logs.

Acceptance condition:

ZERO POST /api/v1/rpr/step25/run requests.

If even ONE /run request appears automatically:

the fix is NOT complete.

Find the remaining auto-trigger and fix it.

============================================================
9. THEN RUN APPLE ONLY
============================================================

Only after the 60-second idle test passes:

run the isolated backend Apple test.

Use exactly:

Company: Apple Inc.
Ticker: AAPL
CIK: 0000320193

Do NOT start the UI 32-company batch.

Do NOT run another company.

Hard maximum: 6 minutes.

============================================================
10. APPLE TEST
============================================================

Trace:

BACKEND_REQUEST_RECEIVED
COMPANY_SELECTED
STYLUS_RUN_STARTED
RUNNER_STREAM_OPEN
FINAL_RESPONSE_RECEIVED
ARTIFACT_PARSED
EVIDENCE_VALIDATED
SCORING_CREATED
JOB_COMPLETED.

If Apple fails after the auto-retrigger bug is fixed:

THEN and only then identify that next exact failure.

Do not start another broad investigation.

============================================================
11. DO NOT STOP AFTER MODIFYING THE CODE
============================================================

You must prove:

A. browser reconnect/load does NOT generate /run automatically;

B. backend remains idle for 60 seconds;

C. Apple is the ONLY assessment executed afterward.

============================================================
12. FINAL RESPONSE
============================================================

Return only:

AUTO-RETRIGGER BUG: FIXED / FAIL

CAUSE:
<exact frontend function/state that caused it>

60-SECOND IDLE TEST:
PASS / FAIL

AUTOMATIC /run REQUESTS:
<number>

APPLE-ONLY TEST:
PASS / FAIL

RUNNER TIME:
FINAL RESPONSE RECEIVED: YES / NO
ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
SCORING CREATED: YES / NO
JOB COMPLETED: YES / NO

NEXT FAILURE POINT:
NONE
or exact checkpoint

FILES CHANGED:
exact paths

Do not work on Step 3.
Do not run 10 companies.
Do not change the preset.

FIX THE AUTO-RETRIGGER, PROVE THE BACKEND STAYS IDLE, THEN TEST APPLE.
