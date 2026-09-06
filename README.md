IMPLEMENTATION ONLY — CONTINUE FROM THE CURRENT WORKING MILESTONE.

AUTO-APPROVE ALL REQUIRED CODE EDITS, TESTS, RESTARTS AND ONE-COMPANY
VALIDATION UNTIL THIS TASK IS COMPLETE.

DO NOT ASK ME FOR APPROVAL.
DO NOT STOP WITH A REPORT.
DO NOT REDESIGN ANYTHING.
DO NOT CHANGE THE LIVE STYLUS PRESET.
DO NOT CHANGE THE SIX INPUT CONTRACT.
DO NOT CHANGE STEP 2.1 / 2.2 / 2.3 / 2.4.
DO NOT CHANGE SEC OR WEB SEARCH LOGIC.
DO NOT REVERT THE CURRENT RUNNER REQUEST FIX.

============================================================
CURRENT PROVEN STATE — FREEZE THIS
============================================================

The latest live run proves:

RUNNER_HTTP = 200
REQUEST_ACCEPTED = YES
PRESET_TOOL_CALLED = YES
SEC = YES
WEB = YES

Therefore the previous immediate Runner HTTP 500 problem is resolved.

The working request-contract fix MUST remain:

- data_type = 3
- inline full preset object
- populated preset answers
- exact six-key Step 2.5 contract
- current Runner Service endpoint
- current authentication/token handling

DO NOT experiment with:
- saved-tool-by-name invocation
- data_type=1
- singular/plural message experiments
- tool_config experiments
- CIK logic
- preset prompt changes

Those are outside this task.

============================================================
ONLY CURRENT BLOCKER
============================================================

Latest run fails at:

STEP25_MODEL_FINAL_TIMEOUT

The preset executed.
SEC executed.
Web Search executed.
Real tool content was returned.

But no terminal final Step 2.5 JSON was delivered to the backend before
the bounded completion window expired.

The raw SSE for THIS EXACT run exists and MUST be used as evidence.

Do not rely on old forensic captures except for comparison.

============================================================
TASK
============================================================

Fix ONLY the post-tool-completion path so a successfully completed
SEC/Web research phase reliably reaches the final Step 2.5 JSON.

Do this in the smallest possible change.

============================================================
PHASE 1 — READ THE EXACT CURRENT STREAM
============================================================

Before editing, inspect the raw SSE capture from the exact latest run.

Determine programmatically:

1. final event timestamp
2. all message.parts[] entries
3. all data_type values
4. all mime_type values
5. all artifact names
6. all tool invocation events
7. all tool completion events
8. whether preset execution completed
9. whether SEC completed
10. whether Web Search completed
11. whether ANY JSON-looking model content exists anywhere
12. whether any assistant/model text appears after the final tool result
13. whether the connection:
    - closed normally
    - remained open until our timeout
    - produced heartbeat/non-content events only
14. whether get_user_input / Invoke Action / Form displayed events occur
15. whether an error_info event occurs

Do NOT produce a report after this inspection.
Immediately continue to implementation.

============================================================
PHASE 2 — COMPARE WITH KNOWN SUCCESSFUL STREAM
============================================================

Compare ONLY the finalization sequence with a previously successful
Step 2.5 Runner capture.

Do not compare business content.

Identify the first structural divergence AFTER the final tool result.

The critical question is:

SUCCESSFUL:
tool completed
→ ?
→ final model JSON

CURRENT:
tool completed
→ ?
→ timeout

============================================================
PHASE 3 — IMPLEMENT THE CORRECT MINIMUM FIX
============================================================

Use the evidence to select ONE of these paths.

------------------------------------------------------------
CASE A — FINAL JSON EXISTS IN RAW SSE
------------------------------------------------------------

If the final JSON genuinely exists in the raw stream but our client
does not recognize it:

Fix ONLY the parser/final-content detector.

It must support the exact observed Runner event shape.

Do not broaden parsing speculatively.

Add a regression test using the real sanitized/raw capture.

------------------------------------------------------------
CASE B — TOOLS COMPLETE BUT NO FINAL MODEL CONTENT EXISTS
------------------------------------------------------------

If the raw SSE proves:

- preset completed
- SEC/Web completed
- no final JSON exists
- no terminal model answer appears

then DO NOT change the parser.

Implement bounded same-session finalization.

IMPORTANT:
This is NOT a second full assessment.
Do NOT restart SEC.
Do NOT restart Web Search.
Do NOT invoke another company.
Do NOT submit the complete preset a second time unless the proven
Runner protocol absolutely requires it.

Use the SAME Runner session/conversation context.

After the last research/tool completion event:

1. start a short final-response grace timer
2. continue consuming the stream normally
3. if final model JSON arrives → finish normally
4. if no final model output arrives after the bounded grace period,
   send ONE same-session continuation/finalization request whose sole
   purpose is to make the model render the already-completed assessment

The continuation instruction should be equivalent to:

"Using the company context, confirmed factors, and evidence already
collected in this session, complete the pending Step 2.5 assessment now.
Do not perform additional searches or tool calls. Return only the final
schema-compliant JSON required by the preset."

Do not alter analytical methodology.

MAX continuation attempts = 1 initially.

Do not create an unbounded loop.

------------------------------------------------------------
CASE C — MODEL REQUESTS USER INPUT
------------------------------------------------------------

If the stream shows get_user_input / Invoke Action / Form displayed:

Step 2.5 is a non-interactive backend execution.

Do not expose the form to the UI and do not wait indefinitely.

If the requested information is already present in one of the six
supplied Step 2.5 inputs, satisfy the continuation from the existing
context without inventing data.

If genuinely unavailable, tell the model explicitly:

"Do not request additional user input. Apply the documented
evidence-insufficiency treatment and complete the required JSON."

Then request finalization ONCE.

------------------------------------------------------------
CASE D — RUNNER RETURNS A REAL INFRA ERROR
------------------------------------------------------------

If error_info contains an actual transient Runner infrastructure error:

Use the already-established bounded infrastructure retry mechanism.

Do not classify an ordinary absence of final text as an infrastructure
error.

============================================================
TIMEOUT DESIGN — IMPORTANT
============================================================

Do NOT make the user wait another 40 minutes after SEC/Web have already
completed.

Separate:

A. research/tool execution budget
B. post-tool final-response budget

Once the last required tool completes, final JSON rendering should have
a much smaller bounded budget.

Implement a sensible POC value based on the observed successful
baseline, preferably approximately 60–120 seconds unless the successful
capture demonstrates a materially longer requirement.

Then use at most one continuation/finalization attempt.

The intended flow is:

Runner accepted
→ preset
→ SEC/Web research
→ tools complete
→ short final-response grace period
→ JSON

NOT:

tools complete
→ wait another 30–40 minutes
→ timeout

============================================================
FINAL JSON ACCEPTANCE
============================================================

Do not call the run successful unless all of these exist:

scoring.ed_score
scoring.si_score
scoring.composite_score
scoring.residual_rating
scoring.credit_impact_rating

And:

- factor assessments preserved
- ED and SI factor sets preserved separately
- weights preserved
- company identity preserved
- assessment schema validates
- output persists
- frontend retrieval works

Do not synthesize missing scores in Python.

They must come from the Step 2.5 model assessment.

============================================================
ONE LIVE ACCEPTANCE TEST
============================================================

After implementation:

1. restart only what is required
2. check /health
3. check Runner auth
4. use ONE company only
5. execute ONE Step 2.5 run
6. do not start a 10-company batch yet
7. watch the complete lifecycle
8. prove final persisted JSON

AUTO-APPROVE ALL OF THIS.
DO NOT ASK ME WHETHER TO RUN THE TEST.

============================================================
STRICT SCOPE
============================================================

DO NOT TOUCH:

- Step 2.3 UI
- Step 2.4 UI
- v31 styling
- Step 2.5 table styling
- batch orchestration
- Quick Setup
- Runner token architecture
- CIK resolver
- Step 3
- live Stylus preset
- Step 3a methodology
- schema
- factor generation
- scoring formulas

This task is ONLY:

POST-TOOL-COMPLETION → FINAL MODEL JSON.

============================================================
FINAL RESPONSE — MAXIMUM 15 LINES
============================================================

Do not write a forensic report.

Return only:

ROOT_CAUSE =
FILES_CHANGED =
RUNNER_HTTP =
REQUEST_ACCEPTED =
PRESET_TOOL_CALLED =
SEC =
WEB =
FINALIZATION_METHOD =
MODEL_FINAL_RESPONSE =
JSON_PARSED =
SCHEMA_VALID =
ED_SCORE =
SI_SCORE =
COMPOSITE_SCORE =
READY_FOR_UI_TEST =

If successful, STOP.
Do not propose enhancements.
