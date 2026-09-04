STRICT FIX — APPLE ONLY — RUNNER INVOCATION

We finally have a CLEAN reproducible failure.

Verified:

90-SECOND BACKEND IDLE TEST: PASS
Unexpected requests: NONE

Then Apple alone was executed:

Company: Apple Inc.
Ticker: AAPL
CIK: 0000320193

Result:

APPLE TEST: FAIL
RUNNER TIME: >360s
FINAL RESPONSE RECEIVED: NO
ARTIFACT PARSED: NO
EVIDENCE VALIDATED: NO
SCORING CREATED: NO
JOB COMPLETED: NO

FAILURE POINT:
RUNNER_STREAM_OPEN

Therefore:

DO NOT investigate SEC.
DO NOT investigate evidence citations.
DO NOT investigate scoring.
DO NOT modify Step 2.5 UI.
DO NOT modify Step 3.
DO NOT modify Step 2.4.
DO NOT modify the Stylus preset.
DO NOT run 10 companies.

None of those stages have been reached.

Your task is now to FIX ONLY:

Python backend
→ Runner Service / Stylus invocation
→ stream opens
→ final response returns.

Do not return another diagnostic-only report.

Find the actual difference between a working Runner invocation and the
currently failing stylus_engine.py invocation, fix it, and rerun Apple
until it succeeds.

============================================================
1. USE THE KNOWN WORKING IMPLEMENTATIONS AS REFERENCE
============================================================

Search the repository for every existing Runner invocation.

In particular inspect:

- the colleague's app.py / Swagger implementation that previously
  demonstrated working Runner execution;

- any direct_runner implementation;

- any previous working Step 2.5 Runner test scripts;

- the existing stylus_engine.py path;

- runner_client / Runner service helpers;

- any code that previously achieved:
  RUNNER_STREAM = OPEN / HTTP 200.

Do NOT create a new Runner framework.

We already have working patterns in this repository.

Compare the failing Stylus invocation against the known-working one
field by field.

============================================================
2. COMPARE THE ACTUAL RUNNER REQUEST
============================================================

For the failing Apple request, inspect exactly what is sent to Runner.

Compare with a known-working Runner call:

ENDPOINT
HTTP method
authentication header
content type
accept header
streaming flag
request body shape
preset representation
model settings
input/context field
conversation/message structure
timeout configuration.

Do not print secrets.

The objective is to find the concrete request-level discrepancy.

============================================================
3. CHECK TOKEN AT THE MOMENT OF THE RUN
============================================================

The backend startup log shows Runner token initialization and the
background token auto-refresher.

Verify immediately before Apple execution:

token exists
token is not expired
seconds_remaining is sufficient.

If the active request accidentally uses a stale cached token instead of
the refreshed token:

FIX THAT.

Do not build another token system.

Use the existing refreshed credential source.

============================================================
4. DETERMINE WHETHER RUNNER ACTUALLY RECEIVES THE REQUEST
============================================================

Instrument the existing Runner call minimally.

We need these checkpoints:

RUNNER_REQUEST_START

RUNNER_HTTP_STATUS

RUNNER_STREAM_OPEN

FIRST_SSE_EVENT

FINAL_SSE_EVENT

Do not dump all event bodies.

If there is no RUNNER_HTTP_STATUS:
the problem is connection/request establishment.

If there is a non-200 status:
fix the actual request/auth problem.

If HTTP 200 occurs but no FIRST_SSE_EVENT:
fix streaming/SSE consumption.

If events arrive but final event is missed:
fix final-response handling.

But DO NOT stop merely to tell me which one it is.

Fix it and rerun Apple.

============================================================
5. REUSE THE WORKING app.py PATTERN IF IT IS THE DIFFERENCE
============================================================

The project previously had a colleague's app.py / Swagger path that
successfully invoked the same enterprise Runner capability.

If that implementation has the working:

request construction
authentication
stream handling
SSE parsing

then reuse the MINIMUM working code pattern inside the existing
stylus_engine.py.

Do NOT rebuild the application around app.py.

Do NOT create another server.

Simply make the existing Step 2.5 Stylus path invoke Runner the same
known-working way.

============================================================
6. CHECK THE PRESET INVOCATION FORMAT
============================================================

The approved RPR POC decision remains:

use the existing inline full preset definition / Runner path.

No preset UUID investigation.

Do not change the manual Stylus preset.

However, confirm the backend Runner payload represents the preset in
the format the working Runner API actually expects.

If the failing code sends a different shape than the known-working
Runner call:

correct the serialization.

============================================================
7. DO NOT MIX THIS WITH SEC GROUNDING YET
============================================================

For this test, preserve the current Apple inputs and grounding exactly
as they are.

Do not redesign or expand them.

The immediate acceptance criterion is simply:

Runner receives the request
→ stream opens
→ final model response reaches Python.

Only after that can parsing/evidence/scoring matter.

============================================================
8. HARD TIMEOUT
============================================================

Keep the 6-minute maximum.

No retries.

If a fix does not work, terminate that Apple attempt, correct the
identified Runner invocation issue, and rerun Apple.

Do not leave another 20–40 minute process running.

============================================================
9. SUCCESS CONDITION
============================================================

Do not stop at:

HTTP request built
token valid
syntax correct
unit test passed.

Success requires the REAL Apple backend call to reach:

RUNNER_HTTP_STATUS = 200
RUNNER_STREAM_OPEN = YES
FIRST_SSE_EVENT = YES
FINAL_RESPONSE_RECEIVED = YES

Then continue through the existing pipeline:

ARTIFACT_PARSED
EVIDENCE_VALIDATED
SCORING_CREATED
JOB_COMPLETED.

If a later stage fails AFTER Runner is fixed, report that exact next
failure, but do not go back into broad architecture analysis.

============================================================
10. FINAL RESULT
============================================================

Return only after the fix/retest:

APPLE RUNNER FIX: PASS / FAIL

RUNNER HTTP STATUS:
STREAM OPENED: YES / NO
FIRST SSE EVENT: YES / NO
FINAL RESPONSE RECEIVED: YES / NO
RUNNER TIME:

ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
SCORING CREATED: YES / NO
JOB COMPLETED: YES / NO

ROOT CAUSE:
one sentence

FIX:
one sentence

FILES CHANGED:
exact paths

NEXT FAILURE POINT:
NONE
or exact next checkpoint

Do not work on any other RPR component.

FIX THE EXISTING RUNNER INVOCATION AND PROVE IT WITH APPLE.
