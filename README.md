STRICT FIX — STEP 2.5 JOB COMPLETION / POLLING

We now have definitive evidence.

DO NOT investigate anything else.

VERIFIED:

- Runner invocation works.
- Initial stale-token 401 is recovered automatically.
- Retry returns HTTP 200.
- Runner stream opens.
- First SSE event arrives.
- Genuine final Apple response is received.
- Apple assessment JSON parses successfully.
- The backend eventually completes the Apple assessment.
- The diagnostic/client gives up after ~360 seconds BEFORE the backend
  has finished returning the result.

Therefore the remaining problem is NOT:

- SEC
- Stylus preset
- Runner connectivity
- SSE stream opening
- model execution
- artifact parsing
- Step 2.4
- Step 3
- UI styling.

The problem is the Step 2.5 HTTP/job lifecycle.

FIX IT NOW.

============================================================
1. DO NOT KEEP /run OPEN FOR THE WHOLE STYLUS EXECUTION
============================================================

Inspect the existing RPR job/poll infrastructure.

Reuse it.

Do NOT invent a new framework.

The intended behaviour must be:

User clicks Run Assessment
        ↓
POST /api/v1/rpr/step25/run
        ↓
backend creates/starts Step 2.5 job
        ↓
POST returns quickly with job_id / accepted state
        ↓
Runner/Stylus continues in backend
        ↓
frontend polls existing job/status endpoint
        ↓
when real final response exists:
artifact parsed
evidence validated
scores created
job = COMPLETED
        ↓
frontend displays completed assessment.

The browser must NOT hold one request open for 6–10 minutes.

============================================================
2. REUSE EXISTING JOB INFRASTRUCTURE
============================================================

Search the repository for the existing job/poll pattern already used by:

- Step 1 discovery/enrichment
- other long-running RPR operations
- existing Step 2.5 job storage/status functions.

Reuse the smallest working pattern.

Do NOT add:
Celery
Redis
queues
new frameworks
production architecture.

POC only.

============================================================
3. BACKEND MUST OWN THE LONG RUN
============================================================

Once the Step 2.5 job starts:

closing the original HTTP request must NOT kill the Runner execution.

The backend job continues until:

COMPLETED
FAILED
or bounded backend timeout.

The browser is only polling status.

============================================================
4. FIX THE STALE TOKEN FIRST-REQUEST ISSUE TOO
============================================================

The latest test showed:

first Runner request = 401
because it used a stale in-memory token

then token refresh
then retry = HTTP 200.

This wastes time and is unnecessary.

Before every new Runner execution, obtain the CURRENT token from the
existing canonical refreshed token source.

Do not use a stale token captured when the engine/client object was
constructed.

Do NOT redesign auth.

Simply make the existing Runner request read the freshest token before
sending.

Acceptance:

first Apple Runner request should normally be HTTP 200 without an
intentional stale-token 401/retry.

============================================================
5. PRESERVE REAL RUNNER COMPLETION
============================================================

Do not change the successful Runner/SSE logic you just proved.

We already know:

STREAM_OPENED = YES
FIRST_SSE_EVENT = YES
FINAL_RESPONSE_RECEIVED = YES
ARTIFACT_PARSED = YES.

Preserve this.

Do not rewrite Runner handling again.

============================================================
6. COMPLETE THE PIPELINE AFTER THE FINAL RESPONSE
============================================================

Once the Apple final assessment is parsed, the backend job must continue
through the existing pipeline:

ARTIFACT_PARSED
        ↓
EVIDENCE_VALIDATION
        ↓
SCORING
        ↓
NORMALIZED RESULT
        ↓
JOB COMPLETED.

The job status endpoint must expose the completed result.

============================================================
7. FAILURE MUST ALSO TERMINATE CLEANLY
============================================================

If a genuine backend failure occurs:

job = FAILED

with a bounded technical error.

Do not leave:

Running...

forever.

Do not convert technical failure into a credit judgment.

============================================================
8. FRONTEND POLLING
============================================================

Modify only the minimum Step 2.5 frontend execution logic necessary.

On Run Assessment:

1. submit job;
2. receive job id;
3. display Running;
4. poll status at a reasonable interval;
5. when COMPLETED:
   render assessment;
6. when FAILED:
   stop polling and show controlled failure state.

No duplicate /run submission while a job is active.

No automatic restart.

No 32-company test during this task.

============================================================
9. APPLE ONLY ACCEPTANCE TEST
============================================================

After implementation:

clean backend.

Run ONLY:

Apple Inc.
AAPL
CIK 0000320193.

Do not run another company.

Verify:

POST /run returns promptly with a job id.

Then poll.

Runner continues in backend.

Final Apple response arrives.

Artifact parses.

Evidence validates.

Scoring is created.

Job becomes COMPLETED.

UI/status endpoint retrieves the result.

No 6-minute client timeout failure.

============================================================
10. DO NOT STOP AT "JOB STARTED"
============================================================

Success requires:

RUN REQUEST RETURNED QUICKLY: YES
JOB ID CREATED: YES
RUNNER HTTP 200: YES
STREAM OPENED: YES
FINAL RESPONSE RECEIVED: YES
ARTIFACT PARSED: YES
EVIDENCE VALIDATED: YES
SCORING CREATED: YES
JOB STATUS COMPLETED: YES
RESULT RETRIEVABLE: YES

============================================================
11. DO NOT WORK ON ANYTHING ELSE
============================================================

Do NOT:

- run 10 companies
- work on Step 3
- change the Stylus preset
- alter SEC logic
- alter evidence validation rules
- redesign Step 2.5
- work on v31 CSS
- revisit Step 2.4.

Get ONE Apple assessment completely through the job/poll path first.

============================================================
12. FINAL RESPONSE ONLY
============================================================

Do not send another diagnostic essay.

Return only:

APPLE JOB/POLL FIX: PASS / FAIL

POST /run RETURN TIME:
JOB ID:
FIRST RUNNER HTTP STATUS:
RUNNER EXECUTION TIME:
FINAL RESPONSE RECEIVED: YES / NO
ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
ED SCORE:
SI SCORE:
COMPOSITE SCORE:
RESIDUAL RATING:
CREDIT IMPACT RATING:
JOB COMPLETED: YES / NO
RESULT RETRIEVABLE BY UI: YES / NO

ROOT CAUSE:
one sentence

FILES CHANGED:
exact paths

NEXT FAILURE:
NONE or exact checkpoint

IMPLEMENT THE FIX AND TEST APPLE END TO END.
