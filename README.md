IMPLEMENT NOW — RPR STEP 2.5 SEC + WEB END-TO-END COMPLETION

THIS IS AN IMPLEMENTATION TASK, NOT AN AUDIT, NOT A REPORT, NOT A DESIGN DISCUSSION.

A fresh Runner Service token has already been provided. Use it through the existing local token mechanism.

DO NOT ASK ME FOR APPROVAL.
DO NOT ASK ME TO CHOOSE OPTIONS.
DO NOT STOP TO PRESENT FINDINGS.
DO NOT PRODUCE ANOTHER FORENSIC REPORT.
DO NOT GIVE ME A PLAN AND WAIT.
DO NOT ASK “SHOULD I PROCEED?”
DO NOT ASK FOR CONFIRMATION BEFORE EDITING FILES.

Everything necessary within the scope below is PRE-APPROVED.

Make the necessary implementation decisions yourself, implement them, restart what is necessary, test them, fix failures, and continue until the complete requested UI flow is ready.

Only stop if there is a GENUINE EXTERNAL blocker that cannot be solved from the repository/environment, such as:
- Runner Service itself unavailable after retries;
- enterprise authentication genuinely unavailable;
- an external approved Citi service is down;
- required source data literally does not exist anywhere accessible.

A normal code bug, mapping problem, stale process, parser problem, timeout, input-field mismatch, frontend state bug, missing local wiring, or retry issue is NOT permission to stop. FIX IT.

============================================================
0. NON-NEGOTIABLE RPR BACKBONE RULE
============================================================

Project root:

C:\Users\ak54743\Downloads\OneDrive_2026-07-16\Rapid Portfolio Review_AI

This is a POC.

Preserve the existing working backbone.

Known-working code is an immutable building block.

DO NOT:
- refactor unrelated working code;
- redesign architecture;
- create a new framework;
- rebuild Steps 2.1–2.4;
- replace established routes unnecessarily;
- redesign the frontend;
- replace v31 styling;
- change working Step 1 behavior;
- change working Step 2.1 behavior;
- change working Step 2.2 behavior except mappings genuinely required for Step 2.5;
- change working Step 2.3/2.4 generation logic unless a missing field required by the approved functional contract is proven;
- alter CAM paths;
- alter legacy Step 2.5 paths unless directly required for this Stylus POC;
- weaken factual/evidence controls;
- fabricate portfolio data;
- invent CIK/ticker/RRR/classification/exposure values.

Changes must be MINIMUM and ADDITIVE wherever possible.

Use the current:
UI Design\step23.html

as the application being made runnable.

Use:
UI Design\icm-pm-rapid-portfolio-review-v31.html

as the immutable visual/functional reference for Step 2.5 presentation.

The final Step 2.5 should look and behave like v31, but show REAL backend results rather than demo/static data.

============================================================
1. FINAL OBJECTIVE
============================================================

When this task finishes I must personally be able to open the frontend and test:

Step 2.1
→ Step 2.2
→ Step 2.3
→ Step 2.4
→ Step 2.5
→ select SEC + Web
→ click Run Assessment
→ wait for the real Stylus execution
→ receive a valid real assessment
→ see the real Step 2.5 results populated in the v31-style table/details
→ inspect ED factors
→ inspect SI factors
→ inspect scores
→ inspect evidence
→ inspect credit conclusion
→ inspect RRR/classification information when supplied
→ add analyst-owned fields where applicable
→ confirm the assessment.

The final goal is NOT another successful terminal harness.

The final goal is:

READY_FOR_USER_UI_2_1_TO_2_5_SEC_WEB_TEST = YES

Do not finish before this condition is achieved unless a genuine external service blocker remains.

============================================================
2. USE THE CURRENT APPROVED STEP 2.5 FUNCTIONAL CONTRACT
============================================================

The current approved Stylus Step 2.5 preset is conceptually correct.

DO NOT redesign its methodology.

The authoritative methodology remains:

“Factor Analysis — Financials” / Step 3a.

The current Step 2.5 contract already established includes:

- exactly one company per individual assessment;
- confirmed Step 2.1 scenario;
- confirmed Step 2.3 Event-Driven factors;
- confirmed Step 2.4 Sector-Inherent factors;
- Step 2.2 company/portfolio data;
- assessment cut-off date;
- optional UserFeedback;
- SEC evidence;
- approved Web Search;
- five-scale Step 3a financial methodology;
- factor preservation;
- evidence discipline;
- ED score;
- SI score;
- 80% / 20% final composite;
- residual rating;
- credit impact rating;
- credit conclusion;
- RRR/classification recommendation logic;
- machine-readable JSON only;
- current Step 2.5 SEC+Web output schema.

Use the approved knowledge files already prepared.

DO NOT silently substitute an older Step25Assessment schema.

The backend inline Stylus definition and attached knowledge must use the CURRENT approved Step 2.5 schema/field dictionary/Step 3a rules.

If a local inline preset mirror is stale relative to the current approved files in preset_knowledge, update the local inline mirror to the approved current contract.

Do NOT invent a new prompt.

============================================================
3. MANAGER FUNCTIONAL REQUIREMENTS — THIS IS CRITICAL
============================================================

The previous technical test proved communication to Stylus, but the functional test payload was too minimal.

This implementation must now provide the FULL information expected by the functional Step 2.5 methodology.

The manager explicitly confirmed that Step 2.5 requires FOUR substantial upstream input groups:

A. STEP 2.1 SCENARIO

Pass the complete confirmed scenario context available from Step 2.1, including where available:

- scenario/event title;
- narrative;
- scenario description;
- critical assumptions;
- scenario assumptions;
- scenario metrics;
- relevant dates;
- scenario horizon;
- any confirmed analyst-edited scenario content.

Do not reduce Step 2.1 to a tiny one-line label if richer confirmed information exists.

The JSON structure can differ from the historical Word document, but informational content must be equivalent.

------------------------------------------------------------
B. STEP 2.3 EVENT-DRIVEN FACTORS
------------------------------------------------------------

Every CONFIRMED Event-Driven factor must be supplied.

For each factor inspect the ACTUAL Step 2.3 confirmed payload and carry everything genuinely available and analytically relevant, including:

- factor_id;
- factor name / label;
- factor description;
- source_step = 2.3;
- weight;
- narrative;
- rationale;
- metric/features;
- vulnerability description;
- buffer/mitigant information if present;
- scoring guidance if present;
- critical thresholds if present;
- industry sensitivity if present;
- industry sensitivity direction/effect if present;
- confirmed analyst edits;
- any structured supporting fields produced by Step 2.3.

DO NOT pass only:
factor name + weight.

The manager specifically called out INDUSTRY SENSITIVITY.

Inspect the real Step 2.3 models/payloads before deciding whether the field already exists under another name.

Do not invent it if Step 2.3 does not produce it.

If the functional Step 2.3 prompt generates industry sensitivity but the confirmed payload currently loses it during mapping/persistence, fix that mapping ADDITIVELY so the existing information reaches Step 2.5.

Do not redesign Step 2.3 itself unless the field is genuinely being discarded.

------------------------------------------------------------
C. STEP 2.4 SECTOR-INHERENT FACTORS
------------------------------------------------------------

Every CONFIRMED Sector-Inherent factor must be supplied.

For each factor pass all genuine available information equivalent to the manager's source material:

- factor_id;
- factor name / label;
- source_step = 2.4;
- weight;
- narrative;
- sector-specific rationale;
- metrics/features;
- vulnerability;
- buffers/mitigants;
- scoring guidance;
- critical thresholds;
- industry sensitivity or sector sensitivity where available;
- confirmed analyst edits;
- supporting structured fields.

Again:

DO NOT collapse the Step 2.4 input to a factor name and weight if richer confirmed information exists.

------------------------------------------------------------
D. STEP 2.2 CLIENT / PORTFOLIO INFORMATION
------------------------------------------------------------

This was another explicit manager requirement.

Step 2.5 needs the real company/client context.

Inspect the ACTUAL Step 2.2 data source and available columns.

Do not rely on assumptions from old mappings.

Map all genuinely available fields relevant to Step 2.5.

At minimum inspect availability for:

- CAGID;
- legal/company name;
- relationship/company name;
- ticker;
- CIK;
- full country of risk name;
- country code;
- current Relationship Risk Rating / RRR;
- current Credit Classification;
- industry L1;
- industry L2;
- industry L3;
- exposure;
- MLE if present;
- Total OSUC / OSUC Amt;
- OSUC-P;
- OSUC-PWL;
- OSUC-SM;
- OSUC-SS;
- OSUC-D/L;
- any other existing exposure/limit fields materially shown in v31.

IMPORTANT:
First inspect the real Step 2.2 source fields and map what ACTUALLY exists.

Do not fabricate absent fields.

If the underlying data already contains a full country name, do not discard it and show only a two-character country code.

If the underlying data contains RRR/classification, propagate it to Step 2.5.

If the underlying data contains OSUC/exposure fields, propagate them.

If they genuinely do not exist for a row, retain null / explicit “not supplied by Step 2.2 portfolio source” behavior.

============================================================
4. WEIGHTING — MUST BE MATHEMATICALLY CORRECT
============================================================

This is specifically important from the manager discussion.

Preserve each confirmed upstream factor weight.

DO NOT replace supplied weights with equal weights.

DO NOT invent missing weights.

Before assessment, validate the factor sets.

For Event-Driven factors:
- include every confirmed Step 2.3 factor exactly once;
- preserve every supplied weight;
- calculate the Event-Driven weighted score from Step 2.3 factors ONLY.

For Sector-Inherent factors:
- include every confirmed Step 2.4 factor exactly once;
- preserve every supplied weight;
- calculate the Sector-Inherent weighted score from Step 2.4 factors ONLY.

Use normalized weighted averages:

ED_SCORE =
SUM(EventDriven factor_score × supplied_weight)
/
SUM(EventDriven supplied_weight)

SI_SCORE =
SUM(SectorInherent factor_score × supplied_weight)
/
SUM(SectorInherent supplied_weight)

This accommodates percentage weights represented as:
20
or
0.20

after correct normalization.

Do not silently mix incompatible units.

Inspect actual upstream representations and normalize deterministically.

Where the complete upstream factor set is designed to total 100%, verify that it does.

If the confirmed source itself does not total 100%, do NOT invent weights merely to force 100%.

Record the upstream weight inconsistency and still use the mathematically normalized weighted-average formula if the weights are valid positive values.

Only AFTER ED_SCORE and SI_SCORE have independently been produced:

COMPOSITE_SCORE =
(ED_SCORE × 0.80)
+
(SI_SCORE × 0.20)

The 80/20 split belongs ONLY at final ED-vs-SI aggregation.

Do NOT apply 80/20 inside the individual factor sets.

Round only displayed aggregate values as required by the contract.

============================================================
5. STEP 3a METHODOLOGY GROUNDING
============================================================

Do not rely on generic LLM memory for the Step 3a thresholds/grids.

Use the approved Step 3a methodology knowledge already extracted from the authoritative “Factor Analysis — Financials” prompt/document.

Ensure the active inline preset definition references/contains the current approved Step 3a methodology knowledge required for:

- 1–5 factor scoring;
- vulnerability assessment;
- buffer/mitigant assessment;
- residual-risk determination;
- residual rating;
- credit-impact determination;
- current RRR anchoring where supplied;
- recommended RRR action;
- current classification anchoring where supplied;
- recommended classification action.

Do NOT use Step 4 portfolio thresholds as Step 3a name-level thresholds.

Step 3a and Step 4 thresholds are different.

Do not reuse the unrelated/dead credit_anchoring path if it is not part of Step 2.5.

============================================================
6. COMPANY IDENTITY / SEC BEHAVIOR
============================================================

Do not substitute a different better-known company.

Use the Step 2.2 selected legal/company name.

Identity hierarchy:

1. supplied CIK;
2. supplied ticker;
3. existing CikResolver using the exact company/legal name;
4. exact company name + country context for Web evidence.

If CIK is unresolved:

- do NOT fabricate a CIK;
- do NOT replace the company;
- do NOT hard-fail solely because the company is not a confirmed SEC registrant;
- record the limitation;
- allow the Web component to proceed for the exact supplied legal entity where appropriate.

If there is literally no usable legal/company identity at all, fail that company explicitly.

Preserve the already-approved distinction between:
NO_COMPANY_IDENTITY_AVAILABLE

and:
NO_CONFIRMED_SEC_REGISTRANT.

Do not reintroduce the previous false blanket 422 gate.

============================================================
7. RUNNER SERVICE — USE THE FRESH TOKEN AND COMPLETE THE FIX
============================================================

A fresh Runner token has already been supplied.

DO NOT ask me for another token unless an actual live response proves that this fresh token is expired/invalid.

Use the existing secure local token-seeding/cache mechanism.

Never print the token.

Never place it in source control.

Never expose it in final chat output.

Keep the recently implemented bounded resilience behavior only if it is genuinely required:

- bounded retry for the proven upstream go-worker EOF / UPSTREAM_SERVER_ERROR class;
- max 2 retries;
- max 2 continuation nudges for the proven get_user_input stalled-model pattern;
- no infinite retry;
- no general retry framework;
- no retry storm.

Use the already proven app.py / Runner interaction behavior as the reference when useful.

Do NOT rewrite the parser unless raw evidence proves a parser defect.

If the Runner returns actual final model content, capture it robustly, parse it, validate it, persist it and render it.

============================================================
8. FIX THE FULL RUN ASSESSMENT PATH
============================================================

Trace and make the real frontend button work:

Run Assessment
→ frontend request
→ Step 2.5 /run
→ correct company context
→ Step 2.1 context
→ Step 2.3 confirmed factors
→ Step 2.4 confirmed factors
→ assessment as-of date
→ optional feedback
→ Stylus inline preset
→ SEC/Web tools
→ final JSON
→ backend Pydantic model
→ persistence
→ frontend polling/render
→ completed assessment row.

No fixture result may be presented as a successful real assessment.

No hard-coded Apple result.

No fake scores.

No demo substitutions.

============================================================
9. FRONTEND TIMEOUT / LONG-RUN BEHAVIOR
============================================================

Real SEC + Web + model runs can take several minutes.

The frontend must not falsely report:

STEP25_BACKEND_UNAVAILABLE

simply because a long assessment is still running.

Retain/fix the long-running request handling already introduced.

Requirements:

- frontend timeout must be longer than legitimate backend Step 2.5 maximum;
- timeout must produce STEP25_RUN_TIMEOUT, not BACKEND_UNAVAILABLE;
- backend /health must distinguish actual backend outage;
- Run Assessment button must enter a clear “assessment running” state;
- duplicate clicks must be prevented;
- existing page must remain responsive;
- success must render when the result arrives;
- a genuine failed assessment must render the real backend error;
- do not leave rows permanently saying “assessment in progress” after a terminal failure.

============================================================
10. STEP 2.5 DATA MODEL — DO NOT DROP MODEL OUTPUT
============================================================

The backend persisted model must retain the complete Step 2.5 audit data required by the approved output schema.

At minimum every factor assessment must retain:

- factor_id;
- factor_name;
- source_step;
- supplied weight;
- score;
- direction;
- impact_rating;
- rationale;
- evidence_ids.

Do not silently discard:
weight,
score,
impact_rating,
or other schema fields.

Persist:

scoring.ed_score
scoring.si_score
scoring.composite_score
scoring.residual_rating
scoring.credit_impact_rating

All five are mandatory after a successful completed assessment.

Persist:

credit_conclusion.headline
credit_conclusion.key_risk_driver
credit_conclusion.current_rrr
credit_conclusion.recommended_rrr_action
credit_conclusion.current_class
credit_conclusion.recommended_class_action
credit_conclusion.confidence

Persist:

evidence[]
evidence_gaps[]
analyst_questions[]

Do not put “Not available” into one of the five mandatory final scoring fields after successful factor assessment.

============================================================
11. RRR / CLASSIFICATION / CREDIT ACTION
============================================================

This was explicitly called out in the manager demo.

If Step 2.2 supplies:

current RRR
and/or
current classification,

they MUST reach Step 2.5.

The model must not manufacture them.

Use Step 3a methodology to derive:

recommended_rrr_action
recommended_class_action

when the required current anchor and evidence permit it.

The UI must display the actual supplied current values and the model recommendation in the corresponding v31-style columns.

Do not show a blank current RRR/classification merely because the Step 2.5 mapping forgot to carry Step 2.2 data.

============================================================
12. V31 STEP 2.5 OUTPUT / UI EXPECTATION
============================================================

Do not redesign Step 2.5.

Use v31 as the visual baseline.

The real Step 2.5 result must populate the equivalent v31 fields including where available:

- Company Name
- CAGID
- Ticker / ID
- Country of Risk
- Industry L1
- Industry L2
- Industry L3
- Total OSUC
- OSUC-P
- OSUC-PWL
- OSUC-SM
- OSUC-SS
- OSUC-D/L
- ED Score
- SI Score
- Composite Score
- Residual Rating
- Credit Impact Rating
- Current RRR
- Recommended RRR Action
- Current Class
- Recommended Class Action
- Key Risk Driver
- Impact Rating Override
- User Credit Commentary

Expanded row/details must show:

EVENT-DRIVEN FACTORS
with real factors, real weights and real Step 2.5 scores.

SECTOR-INHERENT FACTORS
with real factors, real weights and real Step 2.5 scores.

Also show the assessment commentary/evidence in the existing v31-style area.

Analyst-owned fields:
- Impact Rating Override
- User Credit Commentary

must remain user/UI owned.

The model must not fabricate them.

============================================================
13. STEP 2.5 EXECUTION SCALE / MINI-BATCHING
============================================================

The manager clarified the target behavior.

The final portfolio may contain more than one company.

Individual Step 2.5 analytical execution remains ONE COMPANY PER MODEL ASSESSMENT.

For the POC, process the selected confirmed portfolio as mini-batches.

Maximum:
10 companies per batch.

If 1–10 companies:
run those companies.

If >10:
process:
1–10
then 11–20
then 21–30
etc.

Do not create a single giant prompt containing the entire portfolio.

For each company:
- use its own Step 2.2 context;
- use the confirmed shared Step 2.1 scenario;
- use the confirmed Step 2.3 factors;
- use the confirmed Step 2.4 factors;
- execute one company-level Step 2.5 assessment;
- persist independently;
- render that company's row when complete.

One company failure must not erase already completed companies.

For the first technical proof after this implementation:
DO NOT begin by running 149 companies.

Prove one known public-company assessment first.

Then prove a second company.

Then ensure the UI batching machinery is ready.

The user's manual UI test can then exercise the desired portfolio.

============================================================
14. INSPECT ACTUAL DATA — DO NOT ASSUME
============================================================

Before implementing mappings, inspect the actual structures returned by:

Step 2.1 confirmed state
Step 2.2 portfolio source
Step 2.3 confirmed state
Step 2.4 confirmed state

Search the existing code/models for every available field.

Especially inspect whether these exist under alternate names:

RRR
relationship_risk_rating
current_rrr

credit classification
current_class

country_name
country_of_risk
relationship_country

OSUC
OSUC Amt
total_osuc
OSUC-P
PWL
SM
SS
D/L

industry sensitivity
sensitivity
sector sensitivity
industry impact

Do not create duplicate fields unnecessarily.

Map actual upstream names into the Step 2.5 CompanyContextJSON / factor JSON payload.

============================================================
15. LIVE TESTING — REQUIRED, NOT OPTIONAL
============================================================

After implementation:

A. Restart backend cleanly using the current working environment.

B. Verify:
/health = 200

C. Verify token/preflight with the freshly supplied token.

D. Run ONE real known public-company assessment.

Use a company with reliable SEC identity such as the existing Apple test only for the initial integration proof.

This must be a REAL Runner execution.

Acceptance for that run:

CONTEXT_HTTP = 200
RUNNER_AUTH = PASS
PRESET_TOOL_CALLED = PASS
PRESET_TOOL_COMPLETED = PASS
SEC = PASS or legitimate evidence-specific PARTIAL with explanation
WEB = PASS
MODEL_FINAL_RESPONSE = PASS
JSON_PARSED = PASS
SCHEMA_VALID = PASS
ASSESSMENT_PERSISTED = PASS

and:

ED_SCORE = numeric 1.0–5.0
SI_SCORE = numeric 1.0–5.0
COMPOSITE_SCORE = numeric 1.0–5.0
RESIDUAL_RATING = LOW | MEDIUM | HIGH
CREDIT_IMPACT = LOW_IMPACT | MEDIUM_IMPACT | HIGH_IMPACT

Also verify:

- factor count matches confirmed upstream factors;
- every factor appears exactly once;
- factor IDs preserved;
- weights preserved;
- scores persisted;
- impact ratings persisted;
- evidence references point to returned evidence;
- Step 2.1 scenario content is present;
- Step 2.2 company data is present;
- Step 2.3 full factor content is present;
- Step 2.4 full factor content is present.

E. Run a second real company to prove the solution is not Apple-specific.

If it lacks a confirmed CIK, validate the graceful non-fabricating Web path.

F. Verify frontend receives and renders the persisted results.

============================================================
16. COMPLETE UI READINESS TEST
============================================================

After backend live success, verify the CURRENT:

UI Design\step23.html

can support the user's manual workflow.

Do not replace it with another HTML file.

Confirm:

Step 2.1 = confirmed
Step 2.2 = confirmed
Step 2.3 = confirmed
Step 2.4 = confirmed
Step 2.5 = eligible

Company dropdown uses the confirmed Step 2.2 portfolio.

SEC + Web can be selected.

Run Assessment is enabled when genuine prerequisites are satisfied.

Clicking Run Assessment invokes the REAL backend.

The row shows running state.

Successful result replaces running state.

ED/SI factor details appear.

The v31 columns populate from real persisted data.

No fake demo scores remain in the real run path.

Technical diagnostics can remain collapsed.

Feedback input remains functional.

============================================================
17. DO NOT BREAK THESE THINGS
============================================================

Do not break:

- Trigger 1;
- Step 1;
- AI Assist replacement theme;
- feedback controls;
- Step 2.1;
- Step 2.2 confirmed portfolio;
- Step 2.3 confirmed factors;
- Step 2.4 confirmed factors;
- v31 visual backbone;
- legacy/non-Stylus Step 2.5 code paths;
- CAM paths;
- existing token cache behavior;
- existing company-selection behavior.

Do not convert this POC into production architecture.

============================================================
18. NO REPORTING LOOP
============================================================

During implementation:

DO NOT stop and tell me:
“I found X.”
“I need your confirmation.”
“Would you like me to change Y?”
“Here are 20 findings.”
“Here is a forensic report.”
“Which option do you want?”

You have approval for all bounded fixes required by this prompt.

Work autonomously.

If something differs from your expectation:
inspect it,
make the safest minimal decision consistent with this contract,
implement it,
test it,
continue.

============================================================
19. STOP CONDITION
============================================================

You may stop only when either:

A.

READY_FOR_USER_UI_2_1_TO_2_5_SEC_WEB_TEST = YES

OR

B.

A genuinely external blocker remains that cannot be fixed in this repository/environment.

If B occurs, do not give a huge report.

Give only:
EXTERNAL_BLOCKER=<exact blocker>
LAST_SUCCESSFUL_STAGE=<stage>
USER_ACTION_REQUIRED=<single action>

============================================================
20. FINAL RESPONSE — KEEP IT SHORT
============================================================

Do not give me another long report.

When complete, respond only with this compact format:

IMPLEMENTATION = PASS/FAIL
BACKEND = PASS/FAIL
RUNNER_AUTH = PASS/FAIL
REAL_SEC_WEB_RUN_1 = PASS/FAIL
REAL_SEC_WEB_RUN_2 = PASS/FAIL
JSON_SCHEMA = PASS/FAIL
STEP22_FULL_CONTEXT = PASS/FAIL
STEP23_FULL_FACTORS_WEIGHTS_SENSITIVITY = PASS/FAIL
STEP24_FULL_FACTORS_WEIGHTS_SENSITIVITY = PASS/FAIL
RRR_CLASSIFICATION_MAPPING = PASS/FAIL
OSUC_EXPOSURE_MAPPING = PASS/FAIL
V31_REAL_RESULT_RENDERING = PASS/FAIL
MINI_BATCH_READY = PASS/FAIL
READY_FOR_USER_UI_2_1_TO_2_5_SEC_WEB_TEST = YES/NO

If YES:
give me only the exact commands needed to start the backend and open the UI.

If NO:
give me only the single first remaining blocker.

START IMPLEMENTING NOW.
DO NOT ASK FOR APPROVAL.
CONTINUE AUTONOMOUSLY UNTIL THE STOP CONDITION ABOVE IS MET.
