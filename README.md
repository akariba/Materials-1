RPR STEP 2.5 — FINAL ARCHITECTURAL FIX.
END THE SEC/PREFLIGHT LOOP AND COMPLETE THE REAL STYLUS POC.

We now have enough evidence. Stop diagnosing the same failures.

The following are LIVE-PROVEN and FROZEN:

Step 2.1 persisted = YES
Step 2.2 persisted = YES
Step 2.3 confirmed = YES / exactly 5 real factors / weights 100%
Step 2.4 confirmed = YES / exactly 5 real factors / weights 100%

Step 2.5 single-company selector = PASS
Stale company selection clearing = PASS
Backend context registration = PASS

Current Step 2.5 test company:

DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
internal company ID = 9000008998

SEC identity resolution is already proven:

SEC canonical name = DEUTSCHE BANK AKTIENGESELLSCHAFT
CIK = 0001159508
SEC registrant = YES
Foreign private issuer = YES
expected filing families = 20-F / 6-K

DO NOT revisit or modify any of the above unless a direct regression is
caused by this implementation.

============================================================
CONFIRMED REMAINING PROBLEMS
============================================================

The latest real preflight proves:

REAL SEC GROUNDING READY = NO
VERIFIED SEC SOURCE COUNT = 0

because the LOCAL PYTHON process cannot resolve/reach:

www.sec.gov
data.sec.gov

This is an environment/network limitation.

At the same time, the Stylus preset itself has the approved:

- SEC filings integration
- Web Search integration

and manual Stylus execution has already demonstrated that these tools can
execute.

Therefore:

DO NOT continue making local Python SEC.gov connectivity a mandatory
precondition for the STYLUS execution path.

That design is causing the loop.

Second blocker:

Runner token exists but is expired.
Existing SSO/token acquisition mechanism already exists in this project.

============================================================
TARGET ARCHITECTURE FOR THIS POC
============================================================

For:

RPR_STEP25_ASSESSMENT_ENGINE=stylus

the execution path must be:

confirmed RPR state
    ->
compact Step 2.5 payload
    ->
existing Runner client
    ->
existing Stylus Step 2.5 preset
    ->
Stylus SEC Filings integration + Web Search
    ->
Runner SSE tool events
    ->
backend evidence validation
    ->
final model JSON
    ->
Step 2.5 scoring/result
    ->
Step 3 downstream aggregation

The local Python SEC transport is NOT the SEC retrieval boundary for this
Stylus mode.

It may remain available for hybrid/orchestrated/other existing modes.

Do NOT delete it.

Do NOT break other engines.

============================================================
1. REMOVE THE WRONG STYLUS PREFLIGHT DEPENDENCY
============================================================

Inspect the Step 2.5 readiness/preflight gates.

When engine == "stylus":

DO NOT require a successful direct Python connection to:

data.sec.gov
www.sec.gov

before /run is allowed.

DO NOT require deterministic Python SEC grounding sources to exist before
the Stylus preset can execute.

Those checks may remain for engines that genuinely use the Python SEC
transport.

For Stylus mode, readiness should instead require:

- selected company count = 1
- selected company belongs to confirmed Step 2.2 portfolio
- company identity is valid
- Step 2.1 context exists
- Step 2.3 confirmed and contains exactly 5 real factors
- Step 2.4 confirmed and contains exactly 5 real factors
- compact payload valid
- Runner authentication valid
- Stylus preset definition available
- SEC Filings integration enabled in the preset configuration
- Web Search integration enabled when SEC+Web mode is selected

Do NOT weaken company/upstream validation.

We are removing only the INVALID dependency on local SEC.gov network
connectivity for Stylus execution.

============================================================
2. SEC EVIDENCE MUST COME FROM ACTUAL STYLUS TOOL EVENTS
============================================================

NO FABRICATION IS ALLOWED.

Do NOT accept a model response as verified SEC evidence merely because the
model outputs:

source_type = "SEC"
filing_type = "20-F"
or writes a filing name in prose.

During the real Runner execution, capture the ACTUAL Runner SSE events.

Identify the real event shapes emitted for:

- SEC Filings tool invocation
- SEC Filings tool result
- Web Search invocation/result
- assistant/model final response

DO NOT guess the event schema.

Run one bounded instrumented execution if necessary and inspect the actual
event payloads.

From genuine SEC Filings tool-result events, extract whatever authoritative
provenance the integration actually provides, for example when available:

- form/type
- filing date
- company/registrant
- filing/document ID
- accession number
- SEC/EDGAR reference
- source URL
- retrieved document/result identifier
- relevant returned text/snippet

Use the REAL field names returned by the tool.

Do NOT manufacture missing accession numbers or URLs.

============================================================
3. BUILD EVIDENCE FROM TOOL RESULTS, NOT SELF-REPORTED CITATIONS
============================================================

Modify the existing Stylus evidence adapter minimally.

Authoritative evidence provenance for Stylus mode must originate from the
captured SEC Filings/Web Search tool-result events.

Create internal evidence records from those genuine tool results.

Assign backend evidence IDs such as:

EV1
EV2
EV3

only after an actual tool result exists.

The model's final JSON may reference those evidence IDs.

Validation rule:

A claimed SEC evidence item is accepted only when it can be matched to an
actual SEC Filings tool result captured from that SAME assessment run.

A claimed web evidence item is accepted only when it can be matched to an
actual Web Search result from that SAME run.

If a model claims evidence that has no corresponding tool result:

DROP IT.

Do not fabricate.

If a required metric cannot be supported:

mark it unavailable according to the existing Step 2.5 methodology.

============================================================
4. DO NOT FORCE ACCESSION NUMBER IF THE TOOL DOES NOT EXPOSE IT
============================================================

Previously the validator required the model itself to emit a parseable
EDGAR accession/URL.

That caused genuine Stylus SEC evidence to be discarded when the model
did not reproduce the metadata.

Correct this design.

The backend must validate against the authoritative tool-result metadata,
not against whether Claude happened to repeat that metadata correctly in
its prose/JSON.

If the SEC Filings integration returns an authoritative document/result
identifier but does not expose an accession number:

- retain the real integration identifier
- retain any real form/date/title/reference fields it provides
- mark accession_number unavailable/null
- DO NOT invent one

However, if the actual SEC tool result DOES expose accession/EDGAR URL,
capture and preserve them.

The evidence provenance must remain auditable.

============================================================
5. USE THE PRESET AS IT EXISTS
============================================================

DO NOT modify the Stylus preset automatically from VS Code.

The user owns the preset manually.

Do NOT recreate it.
Do NOT change its fields.
Do NOT change its Knowledge attachments.
Do NOT change the 80/20 methodology.
Do NOT change the output schema.

Current preset inputs remain:

CompanyContextJSON
ScenarioContextJSON
EventDrivenFactorsJSON
SectorInherentFactorsJSON
AssessmentASOFDATE
UserFeedback

The preset already has:

SEC Filings = enabled
Web Search = enabled

Use it.

Only if the actual Runner/tool-result evidence proves that a MANUAL preset
prompt change is strictly necessary, stop and report the exact single
manual change required.

Do not edit the preset yourself.

============================================================
6. RUNNER AUTH — FIX THE EXPERIENCE, NOT THE AUTH ARCHITECTURE
============================================================

The current Runner token is expired.

Use the existing approved SSO/token acquisition mechanism.

Do NOT build a new authentication framework.

The repository already contains the token acquisition helper/path.

For this acceptance run, obtain a fresh Runner token through the approved
interactive SSO mechanism.

Never print or paste the token in chat/output/logs.

Cache/store it using the existing local project mechanism.

Before starting a Step 2.5 assessment, perform a FAST auth check.

If auth is invalid:

FAIL IMMEDIATELY.

Do not open a 20–40 minute Step 2.5 job.

Return a clear readiness reason such as:

RUNNER_AUTH_REQUIRED

If the existing refresh mechanism can refresh automatically, use it.

If interactive SSO is genuinely required, launch/use the existing helper
and wait for the user to complete Citi SSO.

Do not silently retry Runner calls for many minutes with an expired token.

============================================================
7. RUNNER SSE COMPLETION MUST BE BOUNDED AND CORRECT
============================================================

Preserve the existing Runner SSE client.

The backend must recognize and log these logical checkpoints:

RUNNER_REQUEST_START
RUNNER_HTTP_STATUS
RUNNER_STREAM_OPEN
FIRST_SSE_EVENT
SEC_TOOL_START
SEC_TOOL_RESULT
WEB_TOOL_START
WEB_TOOL_RESULT
MODEL_FINAL_START/FINAL_RESPONSE
ARTIFACT_PARSED
EVIDENCE_VALIDATED
SCORING_CREATED
JOB_COMPLETED

Use actual available events; do not fabricate checkpoints.

The final model answer may arrive after tool execution.

Do NOT close the stream immediately after SEC/Web tool results.

After tool execution completes, wait for the genuine final assistant/model
response for a bounded grace period.

Do NOT synthesize a fake final assessment.

Do NOT leave the job open indefinitely.

Use one overall bounded timeout appropriate to the demonstrated manual
Stylus runtime.

If final response never arrives, return a precise timeout/failure state
rather than "Running..." forever.

============================================================
8. COMPACT INPUT — KEEP IT
============================================================

Keep the compact payload work already implemented.

For Deutsche Bank the payload must contain only:

1 selected company
real confirmed Step 2.1 scenario
5 real Step 2.3 factors
5 real Step 2.4 factors
assessment date
optional analyst feedback

Do not send the whole portfolio.
Do not send unused rows.
Do not send synthetic factors.
Do not add duplicate SEC grounding text if Stylus will retrieve SEC itself.

The SEC identity information required to disambiguate Deutsche Bank should
be included compactly:

company name
internal ID
canonical SEC name if already resolved
CIK 0001159508
FPI flag if available

============================================================
9. EXECUTE THE REAL ACCEPTANCE TEST
============================================================

After implementing the above:

1. Ensure Runner auth is valid.
2. Do NOT regenerate Steps 2.1–2.4.
3. Use the existing selected Deutsche Bank context.
4. Start exactly ONE Step 2.5 SEC+Web assessment.
5. No parallel company batch.
6. No synthetic test factors.
7. No fixture evidence.
8. No second assessment.
9. Monitor the real Runner SSE execution to completion.

The test is successful only if:

- Runner HTTP request succeeds
- stream opens
- real SEC Filings tool event(s) occur
- real Web Search event(s) occur if used
- final assistant response arrives
- returned artifact/JSON parses
- every accepted evidence item maps to a real tool result from this run
- ED score is created from the 5 real Step 2.3 factors
- SI score is created from the 5 real Step 2.4 factors
- composite = 0.80*ED + 0.20*SI
- residual rating populated where methodology permits
- credit impact rating populated
- no fabricated evidence
- Step 2.5 UI displays readable completed results
- job status becomes COMPLETED

Then verify Step 3 can consume this real completed Step 2.5 assessment.
Do not redesign Step 3 during this test.

============================================================
10. ABSOLUTE FREEZE
============================================================

DO NOT alter:

Step 2.1
Step 2.2
Step 2.3 business methodology
Step 2.4 business methodology
Step 2.5 single-company selector
v31 visual baseline
5-factor requirement
confirmed upstream data
80% ED / 20% SI weighting
Step 3 methodology
CAM paths
hybrid paths
legacy paths

No production architecture.
No new framework.
No broad refactor.

This is a POC.

============================================================
11. NO MORE DIAGNOSTIC LOOP
============================================================

Do not stop after another diagnostic report.

Do not report "SEC DNS unavailable" as the final result again.
That is already known and is precisely why this architecture is being
changed for Stylus mode.

Do not run repeated preflights.

Implement the fix and continue through the ONE real Deutsche Bank
acceptance test.

Only stop before completion for:

A. interactive Citi SSO that physically requires the user, or
B. a genuine external Stylus/Runner outage.

If A occurs, return only the exact action the user must perform and nothing
else. Resume from that checkpoint afterward.

============================================================
FINAL RESPONSE ONLY
============================================================

Do not generate progress reports.

When completed, return:

STEP 2.5 STYLUS ARCHITECTURE: PASS / FAIL
LOCAL PYTHON SEC DEPENDENCY REMOVED FOR STYLUS: YES / NO

COMPANY:
COMPANY ID:
SEC IDENTITY:
CIK:

RUNNER AUTH: PASS / FAIL
RUNNER STREAM: PASS / FAIL

SEC FILINGS TOOL EXECUTED: YES / NO
REAL SEC TOOL RESULTS CAPTURED:
WEB SEARCH TOOL EXECUTED: YES / NO
REAL WEB RESULTS CAPTURED:

FINAL MODEL RESPONSE RECEIVED: YES / NO
ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
FABRICATED EVIDENCE ACCEPTED: 0

ED FACTORS ASSESSED:
SI FACTORS ASSESSED:
ED SCORE:
SI SCORE:
COMPOSITE SCORE:
RESIDUAL RATING:
CREDIT IMPACT RATING:

JOB COMPLETED: YES / NO
STEP 2.5 UI POPULATED: YES / NO
STEP 3 CAN CONSUME RESULT: YES / NO

TOTAL EXECUTION TIME:

FAILURE POINT:
NONE or one exact external blocker

FILES CHANGED:
<exact paths>
