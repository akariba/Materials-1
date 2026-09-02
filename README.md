STOP.

You have ignored the execution instruction.

I explicitly said ENOUGH REPORTS.

Your latest response again contains:

FILES_CHANGED = NONE
LIVE_RUN_EXECUTED = NO
READY_FOR_USER_UI_TEST = NO
STOP THERE

That is NOT completion of the task.

DO NOT produce another forensic report.
DO NOT repeat ROOT_CAUSE.
DO NOT produce another acceptance table before doing implementation.
DO NOT spend another turn summarizing the 4 previous failed runs.
DO NOT stop merely because you can label the problem "Runner Service/model reliability".

We already know:

RUNNER_AUTH = PASS
PRESET_TOOL_CALLED = PASS
PRESET_TOOL_COMPLETED = PASS
SSE parser defect = NOT PROVEN
structured-data parsing defect = NOT PROVEN
manual Stylus SEC + Web preset = WORKING
manual Stylus final model output = WORKING

Therefore a generic statement that "Runner is unreliable" is NOT sufficient.

==================================================
YOUR JOB NOW IS EXECUTION
==================================================

Start making progress toward a successful Step 2.5 run.

You may report ONLY AFTER you have performed the actions below.

==================================================
ACTION 1 — COMPARE THE ACTUAL WORKING REQUEST
==================================================

Open the proven working colleague implementation:

app.py / app 1.py

and compare its ACTUAL Runner Service call to the current Step 2.5 request.

I want you to inspect the code, not describe it from memory.

Compare actual runtime request construction for:

- endpoint
- HTTP method
- headers
- Authorization
- Accept
- Content-Type
- SSE/stream settings
- request JSON root
- model field
- preset structure
- message structure
- inputs structure
- integrations
- SEC configuration
- Web Search configuration
- knowledge attachments
- workflow/thread/session fields
- tools/actions supplied to the model
- streaming options
- continuation behaviour after a tool call
- final response handling

Do NOT give me the comparison as a long report.

Use it internally to find the actionable difference.

==================================================
ACTION 2 — EXPLAIN THE Invoke Action FAILURE IN CODE
==================================================

Your own evidence shows some failing calls end after:

Invoke Action -> get_user...

Do not merely report this.

Trace exactly:

1. what action is being requested;
2. where that action becomes available to the model;
3. whether the working manual Stylus run exposes it;
4. whether working app.py exposes it;
5. whether Step 2.5 actually needs it;
6. whether the Runner expects a continuation response from the caller;
7. whether our RPR implementation fails to continue the workflow after that tool/action;
8. whether the inline preset/request is accidentally asking for an interactive user action.

If there is an implementation defect here, FIX IT.

==================================================
ACTION 3 — INVESTIGATE THE UPSTREAM ERROR
==================================================

You also found a Runner error_info with an upstream failure.

Read the complete raw error object.

Determine from the actual payload whether it is:

- retryable infrastructure failure;
- malformed invocation;
- tool configuration failure;
- unsupported action;
- timeout;
- request contract mismatch.

If it is genuinely transient and retryable:

implement the MINIMUM bounded retry consistent with the working app.py behaviour.

Maximum:
initial call + 2 retries.

No infinite retries.

Do not mask deterministic failures.

==================================================
ACTION 4 — MODIFY CODE
==================================================

Once the first proven discrepancy is identified:

MAKE THE MINIMUM CODE CHANGE.

Do not ask me whether to make it.

You are authorized to modify the necessary Step 2.5 files.

Preserve the RPR working backbone.

Likely candidates are:

backend/step25/stylus_runner_client.py
backend/step25/runner_client.py
backend/step25/stylus_engine.py
backend/step25/router.py

but MODIFY ONLY what evidence requires.

Do not touch unrelated Step 1 / Step 2.1 / Step 2.2 / Step 2.3 / Step 2.4 behaviour.

Do not refactor.

==================================================
ACTION 5 — RESTART
==================================================

If Python/backend code changes:

restart the Step 2.5 backend so that the changed code is actually loaded.

Verify:

/health -> HTTP 200

Do not accidentally start a second server on an already occupied port.

==================================================
ACTION 6 — EXECUTE ONE REAL RUN
==================================================

Run ONE real controlled Step 2.5 assessment.

Prefer Apple first because we already have:

Apple Inc.
ticker = AAPL
CIK = 0000320193

and direct Stylus has already proven this company can produce a valid assessment.

This test MUST use:

REAL Runner Service
REAL preset
REAL SEC
REAL Web Search
REAL model

No fixture.
No mock.
No previous JSON reuse.
No fabricated output.

==================================================
ACTION 7 — ITERATE
==================================================

If the real run fails:

DO NOT STOP AND WRITE A REPORT.

Read the new exact failure.

If it is locally actionable:
FIX IT.

Restart if necessary.

Run again.

Repeat.

Only stop when:

A. one genuine complete Step 2.5 result succeeds;

OR

B. you have PROVEN that an external Citi service is currently preventing the exact same request pattern that otherwise works, and there is no local corrective action.

An intermittent upstream failure does NOT qualify as B until bounded retries have also failed.

==================================================
SUCCESS CONDITION
==================================================

I want to reach:

RUNNER_AUTH = PASS
PRESET_TOOL_CALLED = PASS
PRESET_TOOL_COMPLETED = PASS
SEC = PASS
WEB = PASS
MODEL_FINAL_RESPONSE = PASS
JSON_PARSED = PASS
SCHEMA_VALID = PASS
ASSESSMENT_PERSISTED = PASS

with real:

ED_SCORE
SI_SCORE
COMPOSITE_SCORE
RESIDUAL_RATING
CREDIT_IMPACT

Then:

POST /api/v1/rpr/step25/run = HTTP 200

Then prove the existing Step 2.5 UI can consume it.

==================================================
VERY IMPORTANT
==================================================

DO NOT answer me now with:

"ROOT_CAUSE = ..."
"FILES_CHANGED = NONE"
"LIVE_RUN_EXECUTED = NO"
"READY = NO"
"STOP THERE"

That will be considered failure to follow the instruction.

Your next substantive response should come AFTER:

- at least one concrete implementation action, AND
- at least one new live execution attempt.

While working, keep commentary minimal.

START WITH THE ACTUAL app.py vs Step 2.5 REQUEST DIFF AND THEN EXECUTE.
