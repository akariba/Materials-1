The backend is confirmed clean:

OLD 32-COMPANY BATCH: STOPPED
ACTIVE OLD RUNNER CALLS: 0
BACKEND HEALTH: PASS
ACTIVE STEP 2.5 JOBS: 0
READY FOR CLEAN APPLE TEST: YES

NOW RUN THE CLEAN APPLE TEST.

Use exactly ONE company only:

Company: Apple Inc.
Ticker: AAPL
CIK: 0000320193

Use the exact Step 2.5 backend route used by the real application.

IMPORTANT:

- Apple only.
- Do NOT run the 32-company population.
- Do NOT run another company.
- Do NOT modify code before this test.
- Do NOT modify the Stylus preset.
- Do NOT work on Step 3.
- No retries.
- Hard maximum runtime: 6 minutes.

Trace these checkpoints:

1. BACKEND_REQUEST_RECEIVED
2. COMPANY_SELECTED
3. STYLUS_RUN_STARTED
4. RUNNER_STREAM_OPEN
5. FINAL_RESPONSE_RECEIVED
6. ARTIFACT_PARSED
7. EVIDENCE_VALIDATED
8. SCORING_CREATED
9. JOB_COMPLETED

At the end return ONLY:

APPLE TEST: PASS / FAIL

RUNNER TIME:
FINAL RESPONSE RECEIVED: YES / NO
ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
SCORING CREATED: YES / NO
JOB COMPLETED: YES / NO

FAILURE POINT:
NONE or exact failed checkpoint

Do not do anything else after this test.
