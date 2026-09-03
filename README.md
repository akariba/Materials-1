RPR STEP 2.5 — POST-IMPLEMENTATION CHANGE / FEATURE / FAILURE REPORT

THIS IS A READ-ONLY REPORT TASK.

DO NOT MODIFY ANY FILE.
DO NOT RESTART ANY SERVICE.
DO NOT RE-RUN A 40-MINUTE ASSESSMENT.
DO NOT IMPLEMENT FIXES YET.
DO NOT ASK ME FOR APPROVAL.

I need a precise evidence-based record of what you have actually implemented in Step 2.5 since the recent v31-parity / batching / Runner work.

Do NOT reconstruct this from memory or from your previous answers.

Read the actual repository, current files, existing run artifacts, logs and persisted Step 2.5 results.

Project root:

C:\Users\ak54743\Downloads\OneDrive_2026-07-16\Rapid Portfolio Review_AI

============================================================
1. PURPOSE OF THIS REPORT
============================================================

I need to understand FOUR things before the next implementation pass:

A. Exactly what code/features you changed.

B. Which features are genuinely working versus only coded/not-live-tested.

C. Where the currently displayed Step 2.5 assessment outcome came from.

D. Why attempting the next company took approximately 41 minutes and then failed.

Keep the report factual.

Do not defend previous design decisions.

Do not describe intentions as completed functionality.

============================================================
2. SHORT FEATURE NAMES — REQUIRED
============================================================

For EVERY feature/change you implemented, assign a SHORT FEATURE NAME.

Use short names suitable for a project feature register.

Examples of the naming style only:

V31 Table Parity
ED/SI 80-20 Panel
Composite Detail
Factor Commentary
Portfolio Auto-Inherit
Batch-10 Orchestrator
Runner Retry
Runner Continuation
Token Pause/Resume
H2M Auto Refresh
Real OSUC Mapping
RRR/Class Mapping
Identity Fallback
Evidence Canonicalization

Do NOT blindly use these names unless they correspond to actual code.

Create the short name from the implementation you verify.

============================================================
3. FEATURE REGISTER
============================================================

Produce a table with EXACTLY these columns:

FEATURE NAME
PURPOSE
FILES CHANGED
CORE FUNCTIONS / SELECTORS
STATUS
LIVE VERIFIED?
LAST VERIFIED RESULT
KNOWN PROBLEM

STATUS must be one of:

WORKING
PARTIAL
FAILED
CODED_NOT_TESTED
OBSOLETE
DEBUG_ONLY

For example, do NOT write "working" if it was merely linted.

A feature is LIVE VERIFIED only if there is evidence of actual browser/backend execution.

============================================================
4. EXACT FILE CHANGES
============================================================

Inspect the current files and establish what was actually changed.

At minimum inspect:

UI Design/step23.html

UI Design/rpr_step25_append.js

UI Design/rpr_step25_append.css

backend/step25/*

backend/server.py

backend/llm_gateway.py if touched

backend/rpr_search_agent.py if touched

backend/step22_portfolio_service.py

backend/step22_real_data_loader.py

preset_knowledge/* relevant to Step 2.5

token/auth scripts

any Quick Setup files

any batch/pause/resume code

any run-storage files/models

For every file that was actually changed by the recent Step 2.5 work, give:

FILE
WHAT CHANGED
WHY
FEATURE NAME(S)
STILL REQUIRED?
RISK OF REMOVING IT

Do not list unrelated files.

============================================================
5. STEP23.HTML VS APPEND FILES
============================================================

I specifically need this clarified.

You previously said:

step23.html itself was NOT edited

and that Step 2.5 changes were implemented through:

rpr_step25_append.js
rpr_step25_append.css

Confirm that from the actual current source.

Explain exactly:

1. how step23.html loads these files;
2. what original Step 2.5 DOM exists in step23.html;
3. what JS creates/replaces/overrides at runtime;
4. what CSS overrides v31/current page styling;
5. whether the current architecture can genuinely achieve pixel/structural parity with v31 WITHOUT changing step23.html;
6. whether any existing step23 DOM constraint is causing the current formatting differences.

DO NOT IMPLEMENT A CHANGE YET.

Just establish the facts.

============================================================
6. SOURCE OF THE CURRENT DISPLAYED ASSESSMENT
============================================================

This is extremely important.

In the browser I currently see ONE company with a completed Step 2.5 assessment.

It appears to be ADG TECHNOLOGY INC / Carry1st-related output.

I need to know EXACTLY where that outcome came from.

Trace it end-to-end.

Identify:

company_name
CAGID
run_id
assessment_as_of
created_at
updated_at
execution_engine
assessment_type
Runner request if available
Stylus execution identifier if available
result persistence file/database
browser endpoint used to load it

Then classify the displayed result as ONE of:

CURRENT LIVE RUN RESULT
OLDER PERSISTED LIVE RUN
TEST HARNESS RESULT
MANUAL STYLUS RESULT
FIXTURE / DEMO RESULT
UNKNOWN

Do not guess.

Prove it from files/logs/run persistence.

Also identify why the UI automatically shows this result when I open/reload Step 2.5.

Is the browser loading previously persisted Step 2.5 results?

If yes, identify the exact code path.

============================================================
7. VERIFY THE CONTENT OF THAT RESULT
============================================================

For the displayed completed company, report the actual stored values for:

ED score
SI score
Composite score
Residual rating
Credit impact rating
Current RRR
Recommended RRR Action
Current Class
Recommended Class Action
Key Risk Driver

Then report:

number of Event-Driven factors
number of Sector-Inherent factors

For each factor family report the weights.

Verify:

ED source = Step 2.3
SI source = Step 2.4

Verify whether:

ED weights represent the complete confirmed ED set.

SI weights represent the complete confirmed SI set.

Do not simply rely on the UI labels.

Inspect the stored model metadata/input context.

============================================================
8. COMPOSITE RESULT PROVENANCE
============================================================

The UI currently displays an Overall / Composite outcome.

I need the exact source of that text.

Identify whether it came directly from:

credit_conclusion.headline

credit_conclusion.key_risk_driver

model narrative

frontend-generated concatenation

legacy assessment data

or another field.

Show the exact mapping:

BACKEND FIELD
→ FRONTEND FUNCTION
→ DISPLAYED v31 SECTION

Do this for:

Overall Composite Score Details
Risk Direction
Confidence
RRR Recommendation
Key Risk Driver

I need to know which parts are model output and which parts the frontend is constructing.

============================================================
9. FACTOR COMMENTARY PROVENANCE
============================================================

The current Factor Assessment Commentary shows:

factor name
Vulnerability
Buffer
score/impact labels
supporting evidence
disconfirming evidence
evidence gaps
analyst questions

For each of these identify the exact backend field feeding it.

Use:

DISPLAY ITEM
→ STORED JSON FIELD
→ FRONTEND MAPPING FUNCTION

If Vulnerability/Buffer are being parsed from a generic rationale string instead of structured fields, state that clearly.

============================================================
10. V31 PARITY — WHAT WAS ACTUALLY COPIED
============================================================

Do NOT tell me simply "v31 parity completed."

Inspect actual current source against:

UI Design/icm-pm-rapid-portfolio-review-v31.html

Report separately:

COPIED EXACTLY
APPROXIMATED
NEWLY INVENTED
NOT YET MATCHED

for:

table column order
header colors
table header styling
score colors
score chip geometry
font size
font weight
cell padding
row height
expanded-row structure
ED 80% panel
SI 20% panel
Overall Composite Score Details
Factor Assessment Commentary
Factor Commentary closed state
Factor Commentary open state
Vulnerability
Buffer
Impact Scale legend
Impact Rating Override
User Credit Commentary
Export
Confirm Assessment
feedback area
horizontal scrolling
vertical scrolling

This section should be concise but factual.

============================================================
11. SCORE COLOR THRESHOLDS
============================================================

You stated that the UI uses thresholds such as:

<=2.1
<=3.5

and factor-level threshold variants.

I need the EXACT source.

For every threshold currently used for visual coloring:

show:

CURRENT VALUE
SOURCE FILE
SOURCE LINE/FUNCTION
WHETHER IT EXISTS IN V31
WHETHER IT IS ONLY UI COLORING OR ALSO ANALYTICAL LOGIC

Important:

Do NOT conflate:

V31 visual coloring

with:

Step 3a analytical residual/credit methodology.

State clearly if the current implementation accidentally mixes these.

============================================================
12. SECOND-COMPANY 41-MINUTE FAILURE
============================================================

This requires an exact timeline.

I attempted to run another company.

The run lasted approximately 41 minutes and then failed.

Do NOT execute another long run.

Use existing logs/artifacts.

Identify:

company
CAGID
run_id
start timestamp
end timestamp
total duration
Runner attempt count
retry count
continuation count
SEC tool calls
Web tool calls
last successful stage
first failed stage
final exception/error
frontend timeout if any
backend timeout if any
Runner timeout if any
token status at start
token status at failure

Construct a compact timeline such as:

00:00 request accepted
xx:xx Runner connected
xx:xx SEC called
xx:xx ...
41:xx failure

Only include stages actually evidenced in logs.

============================================================
13. TOKEN PAUSE/RESUME FEATURE
============================================================

The UI currently shows something like:

"Still paused: Runner Service token is not yet healthy enough to resume..."

and a:

Resume Batch

button.

Document the exact current behavior.

Answer:

1. What condition pauses the batch?
2. What token-lifetime threshold is used?
3. Which file/function implements it?
4. Is this based on Leslie's requirement or purely technical POC handling?
5. Does it pause before starting a company or can it interrupt one?
6. Can a single company execution itself exceed one Runner token lifetime?
7. Is that what happened in the ~41 minute failure?
8. What state is persisted when paused?
9. What happens after a fresh token is supplied?
10. Does it resume at the failed company or restart the batch?

Do not change anything yet.

============================================================
14. BATCHING IMPLEMENTATION
============================================================

Verify exactly what "max 10" currently means in CODE.

Does the orchestrator:

A. send 10 companies together to one model request?

B. execute one company independently, sequentially, for up to 10 companies?

C. execute multiple companies concurrently?

D. something else?

This is critical.

Report:

BATCH_SIZE
PER-COMPANY CALL MODEL
CONCURRENCY
STOP/CONTINUE RULE
FAILURE RULE
PERSISTENCE RULE

Also report why the UI says:

1 assessed / 226 portfolio companies

and how subsequent companies are expected to populate.

============================================================
15. QUICK SETUP / QUICK SCAN
============================================================

Document every feature introduced to solve token/runtime problems.

Separate:

QUICK SETUP

from any:

QUICK SEC SCAN

If Quick SEC Scan still exists anywhere, say whether it is:

visible business UI
hidden technical path
obsolete code
debug only
removed

Do not call it a business requirement unless there is evidence it existed in v31/original prompts.

============================================================
16. CURRENT PRESET CONTRACT
============================================================

Do NOT redesign the preset.

Document what the backend currently sends to Stylus.

Identify the actual current inputs for:

CompanyContextJSON
ScenarioContextJSON
EventDrivenFactorsJSON
SectorInherentFactorsJSON
AssessmentAsOfDATE
UserFeedback

For each give:

SOURCE STEP
ACTUAL PAYLOAD FIELDS
FIELDS DROPPED OR MISSING
APPROXIMATE PAYLOAD SIZE

Then verify which knowledge files/config are actually attached to the inline preset.

I specifically need to know whether the current live/backend preset uses:

rpr_step25_secweb_output_schema_v1.json

RPR_STEP25_FIELD_DICTIONARY.md

RPR_STEP3A_THRESHOLDS_AND_GRIDS.md

Step25Assessment.schema.json

or any other old/new files.

State which schema is ACTUALLY authoritative at runtime.

============================================================
17. DO NOT CLAIM LIVE PRESET = LOCAL YAML WITHOUT PROOF
============================================================

There have previously been concerns that:

STYLUS_SEC_WEB_PRESET_DEFINITION.yaml

could be a local mirror rather than the exact current live Stylus preset.

Therefore state:

LIVE_PRESET_VERIFIED_FROM_CURRENT_CAPTURE = YES/NO

LOCAL_YAML_MATCHES_LIVE = YES/NO/UNKNOWN

Do not claim YES without evidence.

============================================================
18. CURRENT KNOWN FUNCTIONAL PROBLEMS
============================================================

Based ONLY on the current implementation/evidence, list the remaining problems.

Keep this short.

I already observe at least:

- formatting still differs from v31;
- only one company has completed;
- another run took approximately 41 minutes and failed;
- token pause/resume is visible in the business UI;
- some factor/result rendering appears structurally different;
- source/provenance of the currently displayed completed outcome is unclear to the user.

Add others only if verified.

============================================================
19. FEATURE SUMMARY — SHORT NAMES ONLY
============================================================

At the very end give me a simple list:

FEATURES IMPLEMENTED

Use only:

SHORT FEATURE NAME — STATUS

Example format:

V31 Table Parity — PARTIAL
Portfolio Auto-Inherit — WORKING
Batch-10 Orchestrator — PARTIAL

No explanations in this section.

This is the feature-name list I will reuse later.

============================================================
20. ABSOLUTELY NO IMPLEMENTATION
============================================================

This report must NOT:

edit files
fix code
restart backend
seed tokens
run Stylus
run another SEC assessment
change UI
change preset
change batching
change CSS

This report establishes the current truth before the next implementation
prompt.

============================================================
21. FINAL REPORT FORMAT
============================================================

Use these sections only:

1. Executive State
2. Feature Register
3. Files Changed
4. Current Outcome Provenance
5. Step 2.5 Data/Score Provenance
6. v31 Parity State
7. 41-Minute Failure Timeline
8. Token / Batch Behavior
9. Current Preset Runtime Contract
10. Remaining Problems
11. Features Implemented — Short Names

No long historical essay.

No recommendations yet.

No implementation plan yet.

No approval questions.

Start by reading the CURRENT repository and run artifacts.
