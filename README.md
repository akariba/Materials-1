STOP THE CURRENT DIAGNOSTIC LOOP.

We now have an explicit Stylus POC integration recommendation from Stylus itself. Treat the following as the approved POC architecture and implement it end-to-end.

DO NOT perform another broad audit.
DO NOT restart investigation from first principles.
DO NOT redesign Steps 2.1–2.4.
DO NOT create another architecture.
DO NOT fabricate test factors, SEC evidence, companies, scores, URLs, accession numbers, or Runner events.
DO NOT modify the manually-created Stylus preset unless there is a genuinely unavoidable preset-side blocker; if one exists, report the exact manual preset change required instead of modifying Stylus yourself.
DO NOT use MCP.
DO NOT productionize this.
This remains a Windows/local POC.

Proceed autonomously through the complete approved scope. Do not stop for confirmation between implementation steps. Stop only for a genuine external blocker requiring a user action such as interactive SSO/token acquisition or retrieval of a saved-preset identifier that cannot be obtained from the repository/environment.

============================================================
BUSINESS PURPOSE
============================================================

Step 2.5 is the ONE-COMPANY Name-Level Financial/Credit Assessment.

It must consume:

- confirmed Step 2.1 scenario;
- exactly one company from confirmed Step 2.2;
- exactly 5 REAL confirmed Step 2.3 Event-Driven factors;
- exactly 5 REAL confirmed Step 2.4 Sector-Inherent factors;
- assessment as-of date;
- optional analyst feedback.

The existing manually-created Stylus preset performs the financial analysis using:

- Claude Sonnet 5;
- Stylus SEC Filings integration;
- Stylus Web Search integration;
- Step 2.5 field dictionary/methodology Knowledge;
- Step 2.5 output-schema Knowledge.

Expected Step 2.5 result includes:

- factor assessments/evidence;
- ED weighted score;
- SI weighted score;
- composite score = 80% ED + 20% SI;
- residual-risk rating;
- credit-impact rating;
- commentary;
- schema-conformant JSON.

The persisted Step 2.5 outputs feed Step 3 Portfolio Level Assessment.

REAL DATA ONLY.
FAIL CLOSED rather than fabricate.

============================================================
APPROVED POC ARCHITECTURE
============================================================

The approved path is now:

confirmed Step 2.1
+
confirmed Step 2.2 single company
+
5 confirmed Step 2.3 factors
+
5 confirmed Step 2.4 factors

        ↓

compact Step 2.5 JSON payload

        ↓

local FastAPI backend

        ↓

SAVED Stylus Step 2.5 preset through Runner

        ↓

Stylus SEC Filings integration
+
Stylus Web Search integration

        ↓

Claude Sonnet 5 Step 2.5 analysis

        ↓

schema-conformant final JSON

        ↓

Runner completion/final output

        ↓

Python parsing + evidence validation

        ↓

persist Step 2.5 result

        ↓

Step 2.5 UI

        ↓

Step 3 aggregation

CRITICAL:

Python direct access to data.sec.gov / www.sec.gov is NOT the authoritative filing retrieval path for the Stylus engine.

The Stylus SEC Filings integration is the authoritative SEC evidence path for the POC.

============================================================
1. REMOVE PYTHON SEC NETWORK AS A STYLUS GATE
============================================================

Inspect the current Step 2.5 stylus execution path.

Find every check that makes successful Python access to:

- data.sec.gov
- www.sec.gov
- SEC submissions JSON
- direct EDGAR document download

a mandatory prerequisite to running the Stylus Step 2.5 assessment.

For RPR_STEP25_ASSESSMENT_ENGINE=stylus:

REMOVE/BYPASS ONLY THAT BLOCKING REQUIREMENT.

Do NOT delete useful modules from the repository unnecessarily.

The deterministic CIK/company resolver MAY remain as a NON-BLOCKING identity helper.

Example desired company context:

company_name
internal company_id / CAGID
ticker where legitimately available
CIK where legitimately resolved
SEC canonical name where legitimately resolved
SEC registrant flag where known
foreign-private-issuer flag where known

But inability of Python itself to download SEC filing content MUST NOT prevent the Stylus preset from running.

Do not duplicate filing retrieval by downloading SEC filings in Python and then also asking Stylus SEC Filings to retrieve them.

============================================================
2. KEEP THE REAL UPSTREAM STATE
============================================================

Do not change the now-working persistence architecture.

We have already live-proven:

Step 2.1 scenario persistence = PASS

Step 2.2 portfolio persistence = PASS

Step 2.3 confirmation persistence = PASS
exactly 5 real confirmed factors
weights total = 100%

Step 2.4 confirmation persistence = PASS
exactly 5 real confirmed factors
weights total = 100%

The Step 2.5 single-company selector is also required.

Do not reintroduce the old 30/32-company batch execution.

Exactly ONE company must be selected for an individual Step 2.5 run.

============================================================
3. USE THE SAVED STYLUS PRESET
============================================================

The manually-created saved preset is already demonstrated to work interactively.

Prefer invoking the SAVED preset rather than transmitting/rebuilding the complete inline preset definition every run.

Do NOT guess the saved-preset identifier or Runner parameter names.

First inspect:

- existing repository Runner code;
- existing successful/recorded Runner requests if available;
- browser/network/request capture artifacts if already present;
- any existing application logs;
- current YAML/configuration.

If the exact saved-preset identifier/version and request shape can be determined from existing evidence, wire it.

Potential terminology reported by Stylus documentation includes fields conceptually like:

team_id
team_version_id

BUT DO NOT hardcode those names merely because this prompt mentions them.

Use the ACTUAL contract used in this environment.

If the exact saved preset identifier cannot be obtained without the user's browser interaction, STOP ONLY AT THAT EXTERNAL BLOCKER and report:

SAVED_PRESET_IDENTIFIER_REQUIRED

plus the exact minimum browser action the user needs to perform.

Do not fall back to an invented identifier.

Do not silently return to inline-preset execution unless the actual Runner contract proves saved-preset invocation is unavailable.

============================================================
4. COMPACT PAYLOAD ONLY
============================================================

Preserve the payload compaction already implemented.

The Runner/model should receive ONLY information needed by the existing preset fields:

CompanyContextJSON
ScenarioContextJSON
EventDrivenFactorsJSON
SectorInherentFactorsJSON
AssessmentASOFDATE
UserFeedback

Do NOT send:

- the full 30+ company portfolio;
- complete browser JS state;
- unrelated Step 1 data;
- duplicate SEC filing text;
- giant backend objects;
- unnecessary diagnostic metadata.

Requirements:

ONE company
5 ED factors
5 SI factors
real scenario
as-of date
optional feedback

Before sending, log only structural telemetry such as:

company
company_id
CIK if available
ED factor count
SI factor count
payload bytes/chars
preset reference/version
as-of date

Never log bearer tokens.

============================================================
5. SEC EVIDENCE OWNERSHIP
============================================================

For the Stylus Step 2.5 path:

STYLUS SEC FILINGS = AUTHORITATIVE SEC RETRIEVAL.

Do NOT require accession_number or url to be non-null as a universal hard acceptance gate.

Instead validate provenance using the strongest evidence actually exposed by Runner.

At minimum, where technically observable, validate:

A. genuine SEC integration/tool activity occurred during this run;

B. SEC evidence corresponds to the same selected company/CIK/identity;

C. filing type/date is internally consistent and does not violate AssessmentASOFDATE;

D. substantive evidence was returned rather than the model merely claiming it consulted a filing.

If accession_number / URL / document identifier is genuinely returned, preserve and validate it.

If the actual SEC integration does not provide accession_number or URL for an otherwise genuine evidence item:

- retain null/unavailable;
- do NOT invent a value;
- do NOT reject the entire evidence item solely for that reason.

However:

If the model asserts a specific SEC filing fact but there was NO observable SEC integration activity/support for it, fail that evidence item closed.

============================================================
6. WEB SEARCH
============================================================

Web Search remains enabled through the saved preset.

It is supplementary evidence.

Do not introduce a separate Python web-search requirement for Step 2.5.

Preserve evidence provenance/source type distinctions between SEC and Web.

============================================================
7. AUTHENTICATION — REMOVE THE BAD REFRESH LOOP
============================================================

The Stylus response states that this POC uses a short-lived H2M authenticated-browser JWT, approximately 30 minutes.

There is no documented long-lived refresh-token flow for the detached local POC client.

Therefore:

Remove/disable the current logic that repeatedly attempts an unsupported refresh endpoint and receives HTTP 400.

Do NOT implement fake refresh-token derivation.

Do NOT persist browser bearer tokens long term.

Use the existing current valid bearer token if present.

On Runner HTTP 401:

1. mark the Step 2.5 request as AUTH_REQUIRED;
2. do NOT retry repeatedly;
3. do NOT spin a refresh loop;
4. surface a clear message indicating that the authenticated Stylus browser session/token must be refreshed/re-obtained;
5. preserve all Step 2.1–2.4 state so the analyst can retry Step 2.5 without rebuilding the workflow.

If an existing repo mechanism securely reads the manually-captured current token, preserve the smallest working mechanism.

Never print the token.

============================================================
8. FIX RUNNER COMPLETION CORRECTLY
============================================================

This is critical.

Previous failures showed:

HTTP accepted
Runner HTTP 200
stream opens
FIRST_SSE_EVENT received
tool/model work continues
but /run waits excessively or does not recognize final completion.

Do not treat:

- HTTP 200;
- STREAM_OPEN;
- FIRST_SSE_EVENT;
- first assistant-looking text;
- first tool result;

as completion.

Inspect the ACTUAL Runner event objects produced by this environment.

Do not invent event names.

Determine from actual payload fields how Runner signals:

- workflow running;
- tool execution;
- assistant messages;
- terminal/completed workflow;
- failure.

Stylus documentation referenced a conceptual workflow status including:

NOT_STARTED_WORKFLOW
RUNNING_WORKFLOW
COMPLETED_WORKFLOW
FAILED_WORKFLOW

and task states such as WORKING_TASK / COMPLETED_TASK.

Use these ONLY if they are actually present in the environment's returned payload.

Authoritative completion must be based on the actual terminal Runner state.

Continue buffering assistant/artifact content while the workflow remains active.

After the terminal successful workflow state:

- select/extract the final schema-conformant Step 2.5 JSON;
- do not accidentally parse an intermediate tool payload as the assessment.

If both conversational final output and artifact payload exist, inspect both and use the final schema-conformant assessment.

============================================================
9. TIME BOUNDS
============================================================

Manual execution of the same preset is approximately 2 minutes.

For this POC use bounded execution.

Target:

connection / stream-establishment timeout:
15–30 seconds

total Runner execution budget:
approximately 5 minutes

final-output grace after the last real tool activity:
approximately 60–90 seconds, provided the actual workflow has not already emitted a definitive terminal failure.

Do NOT allow routine Step 2.5 calls to silently run for 20–40 minutes.

On timeout:

mark the request TIMEOUT/STALLED
preserve upstream state
do not fabricate a result
do not automatically start another assessment
do not retry indefinitely.

If actual observed valid Runner behavior proves the 5-minute bound slightly insufficient, report the measured timing before changing it; do not simply return to a 40-minute timeout.

============================================================
10. JSON SCHEMA
============================================================

Keep the existing Step 2.5 output schema.

The JSON schema is the contract between:

Stylus/model result
→ backend parser
→ Step 2.5 UI
→ Step 3.

Do not weaken the schema merely to make a bad response pass.

Validate the final object.

A successful assessment must populate legitimate non-null values for at least:

scoring.ed_score
scoring.si_score
scoring.composite_score
scoring.residual_rating
scoring.credit_impact_rating

when sufficient factor evidence was successfully assessed according to the methodology.

Composite must remain:

0.80 * ED weighted score
+
0.20 * SI weighted score

Do not substitute Step 3/portfolio thresholds for Step 2.5 name-level thresholds.

============================================================
11. STEP 2.5 UI
============================================================

Do not redesign the UI.

v31 remains the visual baseline.

Once a valid persisted assessment is returned, populate the existing Step 2.5 table/detail presentation with:

ED score
SI score
Composite score
Residual rating
Credit impact rating
factor details
evidence/commentary
applicable RRR/classification recommendations where legitimately supported.

Do not fill placeholders from partially completed Runner messages.

Only completed validated Step 2.5 results populate the assessment columns.

============================================================
12. STEP 3 INTEGRATION
============================================================

Do not stop after making Step 2.5 display a JSON artifact.

After one successful Step 2.5 assessment:

verify that the persisted object is consumable by the existing Step 3 aggregation logic.

Do NOT redesign Step 3.

Do NOT fabricate missing company results.

For the controlled one-company acceptance test, prove that the completed company can be consumed as a real assessed company by Step 3's existing aggregation contract.

============================================================
13. CONTROLLED ACCEPTANCE TEST
============================================================

Do ONE controlled live company only.

Do not launch a portfolio batch.

Use an actually selected company from the confirmed Step 2.2 portfolio.

Prefer the currently prepared Deutsche Bank case if it is still the confirmed selected company:

DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
internal company id: 9000008998

Identity previously resolved as:

SEC canonical name:
DEUTSCHE BANK AKTIENGESELLSCHAFT

CIK:
0001159508

SEC registrant:
YES

Foreign Private Issuer:
YES

likely relevant forms:
20-F / 6-K

Do not hardcode these as evidence; they are identity/context only.

Before Runner starts verify:

STEP21_PRESENT = YES
STEP22_PORTFOLIO_PRESENT = YES
SELECTED_COMPANY_COUNT = 1
STEP23_CONFIRMED = YES
STEP23_FACTOR_COUNT = 5
STEP24_CONFIRMED = YES
STEP24_FACTOR_COUNT = 5
PAYLOAD_COMPACT = YES
RUNNER_AUTH_READY = YES
SAVED_PRESET_RESOLVED = YES

Then execute ONE Step 2.5 assessment.

============================================================
14. PASS CRITERIA
============================================================

The acceptance test is PASS only if ALL applicable conditions below hold:

1. exactly one company sent;
2. selected company identity is correct;
3. Step 2.1 scenario included;
4. exactly 5 real confirmed ED factors supplied;
5. exactly 5 real confirmed SI factors supplied;
6. compact payload used;
7. saved manual Stylus Step 2.5 preset invoked;
8. genuine Stylus SEC Filings activity occurs;
9. SEC evidence belongs to the correct company;
10. no post-as-of-date evidence is improperly used;
11. Web Search is used only through Stylus where required;
12. Runner reaches genuine terminal successful state;
13. final Step 2.5 JSON is extracted;
14. JSON conforms to the existing schema;
15. evidence validation passes without demanding fields the SEC integration genuinely does not expose;
16. ED score populated;
17. SI score populated;
18. composite score populated;
19. residual rating populated;
20. credit-impact rating populated;
21. job marked complete;
22. result persisted;
23. Step 2.5 UI populated;
24. persisted result can be consumed by Step 3.

NO fabricated values are permitted merely to achieve PASS.

============================================================
15. WHAT MUST NOT BE CHANGED
============================================================

Do NOT change:

- Step 1;
- Step 2.1 business logic;
- Step 2.2 portfolio-selection business logic except existing persistence fixes already implemented;
- Step 2.3 factor methodology;
- Step 2.4 factor methodology;
- exactly-5 ED requirement;
- exactly-5 SI requirement;
- confirmed factor weights;
- Step 2.5 financial-analysis methodology;
- 80/20 weighting;
- Step 2.5 output schema;
- manually-created Stylus preset unless a genuine external/manual preset blocker is proved;
- preset Knowledge attachments;
- v31 visual baseline;
- Step 3 aggregation methodology.

Do not introduce production frameworks or abstractions.

============================================================
16. FINAL REPORT
============================================================

Do not give me a long narrative.

After implementation/test return this exact concise report:

STEP 2.5 POC ARCHITECTURE FIX: PASS / FAIL

COMPANY:
COMPANY ID:
CIK:

SAVED PRESET USED: YES / NO
INLINE PRESET REMOVED FROM ACTIVE PATH: YES / NO
PYTHON SEC HARD GATE REMOVED FROM STYLUS PATH: YES / NO
CIK RESOLUTION RETAINED: YES / NO

ONE COMPANY SENT: YES / NO
STEP 2.1 PRESENT: YES / NO
REAL ED FACTORS: <count>
REAL SI FACTORS: <count>
PAYLOAD SIZE:

RUNNER AUTH: PASS / FAIL
RUNNER REQUEST: PASS / FAIL
STREAM OPEN: YES / NO
SEC TOOL ACTIVITY: YES / NO
WEB TOOL ACTIVITY: YES / NO / NOT REQUIRED
TERMINAL WORKFLOW COMPLETION: YES / NO
FINAL RESPONSE RECEIVED: YES / NO
ARTIFACT/JSON PARSED: YES / NO
SCHEMA VALID: YES / NO
EVIDENCE VALIDATED: YES / NO

ED SCORE:
SI SCORE:
COMPOSITE SCORE:
RESIDUAL RATING:
CREDIT IMPACT RATING:

STEP 2.5 RESULT PERSISTED: YES / NO
STEP 2.5 UI POPULATED: YES / NO
STEP 3 CONSUMABLE: YES / NO

TOTAL RUNNER TIME:
TOTAL END-TO-END TIME:

FILES CHANGED:
- ...

FAILURE POINT:
NONE
or exactly one concrete remaining external blocker.

Do not continue to another task after this report.
