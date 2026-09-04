STOP THE CURRENT BATCH TEST.

We now have a very important comparison:

MANUAL STYLUS:
- Apple Inc.
- ticker AAPL
- CIK 0000320193
- preset completes in approximately 2 minutes
- apple_step25_assessment.json is produced

CURRENT UI:
- shows 32 entities
- 0 assessed / 32
- visible population includes Banks / Banks-SPV
- first assessment remains Running for 30+ minutes

These are NOT equivalent tests.

Do ONE thing only now.

Do NOT modify:
- Stylus preset
- Step 2.4
- Step 2.5 UI design
- Step 3
- scoring methodology
- evidence validation
- 10-company logic

Do NOT run 32 companies.

Take EXACTLY ONE company:

Apple Inc.
ticker = AAPL
CIK = 0000320193

Use the same scenario / ED factors / SI factors that were used in the
successful manual Stylus test.

Now invoke Apple through the EXACT backend Step 2.5 route that the UI
Run Assessment button uses.

The purpose is to determine why:

manual Stylus = ~2 minutes

but

UI/backend path = 30+ minutes.

Use a HARD upper timeout of 6 minutes for this diagnostic.

NO retries.
NO second company.
NO batch loop.

Trace these exact checkpoints with timestamps:

1. BACKEND_REQUEST_RECEIVED

2. COMPANY_SELECTED
   Confirm only Apple is being assessed.

3. STYLUS_RUN_STARTED

4. RUNNER_STREAM_OPEN

5. STYLUS_FINAL_RESPONSE_RECEIVED

6. ARTIFACT_PARSED

7. EVIDENCE_VALIDATION_STARTED

8. EVIDENCE_VALIDATION_FINISHED

9. SCORING_CREATED

10. JOB_STATUS_SET_COMPLETED

11. HTTP_RESPONSE_RETURNED

At each checkpoint print only elapsed seconds and safe status.

Also compare the actual backend payload sent to Stylus with the manual
Apple preset inputs.

Confirm whether they are materially the same.

IMPORTANT:

The manual Apple artifact currently appears to contain SEC evidence
entries where some fields show:

url = null
accession_number = null

Do NOT hide this.

If that causes backend evidence validation to reject the assessment,
report exactly:

EVIDENCE_VALIDATION_FAIL

and identify which evidence IDs failed.

Do NOT retry for 30 minutes.

If the Runner sends its final answer but our backend fails to recognize
it, report exactly:

FINAL_HANDOFF_FAIL

If the final answer is recognized but parsing fails, report:

PARSE_FAIL

If parsing succeeds but evidence validation fails, report:

EVIDENCE_VALIDATION_FAIL

If everything succeeds:

ONE_COMPANY_UI_PATH_PASS

Your final response must contain ONLY:

COMPANY: Apple Inc.
BACKEND POPULATION USED: <number>
RUNNER TIME: <seconds>
FINAL RESPONSE RECEIVED: YES/NO
ARTIFACT PARSED: YES/NO
EVIDENCE VALIDATED: YES/NO
SCORING CREATED: YES/NO
JOB COMPLETED: YES/NO
TOTAL TIME: <seconds>
FAILURE POINT: <exact checkpoint or NONE>

Do not continue to another task.
