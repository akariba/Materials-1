STRICT COMPLETION / FREEZE MODE.

The current live test has crossed the critical acceptance milestone:

RUNNER_HTTP = 200
REQUEST_ACCEPTED = YES
MESSAGES_REQUIRED_500 = NO

The proven material change is:
working browser contract = data_type=3 + inline preset object + populated answers.

DO NOT make any additional architectural, prompt, preset, SEC, UI, token,
batching, Step 2.3, Step 2.4, schema, or parser changes.

DO NOT ask me for approval.
AUTO-APPROVE the remaining validation steps until completion.
DO NOT produce another long report.

Let the CURRENT run finish.

Then validate ONLY:

1. Runner stream reaches terminal completion.
2. Preset tool actually executes.
3. SEC/Web tool activity is observed where applicable.
4. Final model JSON is returned.
5. JSON parses.
6. Step 2.5 schema validates.
7. All mandatory fields are populated:
   - ED score
   - SI score
   - Composite score
   - Residual rating
   - Credit impact rating
8. Assessment persists successfully.
9. Existing frontend can retrieve that run.

If ALL pass:
- KEEP the current minimal request-contract fix.
- Remove temporary test/debug files only if they were created solely for
  this experiment.
- DO NOT touch any other production behavior.
- Freeze this as the new known-working Runner transport baseline.

If the stream fails AFTER having been accepted:
- do NOT modify request construction again.
- identify only the first post-acceptance failure stage.
- do not attempt a second fix without evidence.

FINAL RESPONSE MAXIMUM 12 LINES:

RUNNER_HTTP =
REQUEST_ACCEPTED =
PRESET_TOOL_CALLED =
SEC =
WEB =
MODEL_FINAL_RESPONSE =
JSON_PARSED =
SCHEMA_VALID =
ED_SCORE =
SI_SCORE =
COMPOSITE_SCORE =
READY_FOR_UI_TEST =

NO HISTORY.
NO REPORT.
NO NEW DESIGN.
NO APPROVAL QUESTION.
