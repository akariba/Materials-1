RPR STEP 2.5 — FINAL POC INTEGRATION / ROOT-CAUSE FIX
=====================================================

READ THIS ENTIRE INSTRUCTION BEFORE CHANGING ANYTHING.

This is a STRICT LOCAL WINDOWS POC task.

Do not broaden the scope.
Do not redesign the application.
Do not introduce production architecture.
Do not start another generic diagnostic loop.

Proceed autonomously through the approved scope.
Do not stop to ask me for approval after each step.
Make reasonable implementation decisions yourself.

Stop only for a genuine external blocker that cannot be resolved from the
repository, current running application, existing scripts, logs, or environment.

The objective is:

    get ONE genuine Deutsche Bank Step 2.5 assessment
    through the existing RPR UI/backend
    -> Stylus Runner
    -> the proven Step 2.5 Stylus preset
    -> Stylus SEC Filings / Web Search
    -> final schema-valid assessment
    -> persistence
    -> Step 2.5 UI

Do not work on Step 3 until Step 2.5 has genuinely passed.


======================================================================
1. POC RULES — NON-NEGOTIABLE
======================================================================

This is NOT production software.

Do NOT introduce:

- MCP
- production service-account architecture
- new authentication frameworks
- new orchestration frameworks
- new generic adapters
- dependency injection frameworks
- new persistence architecture
- broad refactoring
- abstractions for future production use
- Fiddler/Telerik unless a completely external blocker leaves literally no
  other way to inspect the request
- unrelated cleanup
- mass file rewrites

The future production team can rebuild this.

For this POC, prefer the smallest change that reproduces the already-proven
working behaviour.

Do NOT modify working code unnecessarily.

Do NOT modify v31 visual design.

Do NOT redesign Step 2.5.

Do NOT modify the manually configured Stylus preset itself.


======================================================================
2. FIXED FACTS — DO NOT RE-DIAGNOSE THESE
======================================================================

Treat the following as PROVEN facts.

A. STYLUS SEC RETRIEVAL IS PROVEN
---------------------------------

We already have multiple proofs that SEC retrieval itself is possible.

1. An older/hybrid Step 2.5 execution produced genuine validated SEC evidence,
   including a real Salesforce 10-K accession number and real EDGAR URL.

2. The manually configured Step 2.5 Stylus preset successfully ran for Apple.
   Stylus visibly executed:
       SEC Filings
       Web Search
   and returned a Step 2.5 JSON artifact.

3. A backend -> Runner -> Stylus execution also previously progressed through
   genuine Runner/tool activity and eventually produced an assessment even
   though the original client timed out before completion.

Therefore:

DO NOT diagnose "SEC does not work" again.

DO NOT require local Python to reach:
    data.sec.gov
    www.sec.gov

DO NOT add a Python SEC connectivity preflight to the active Stylus POC path.

DO NOT make direct Python SEC retrieval a prerequisite for Step 2.5.

The intended POC evidence route is:

    RPR backend
       -> Stylus Runner
       -> Step 2.5 Stylus preset
       -> Stylus SEC Filings integration
       -> optional Stylus Web Search
       -> model synthesis
       -> final JSON

Python may retain issuer/CIK identity helpers where already useful, but local
Python SEC transport is NOT the assessment evidence-retrieval gate.


B. AUTHENTICATION / TOKEN GENERATION IS PROVEN
-----------------------------------------------

Authentication is OUT OF SCOPE for redesign.

There is already a proven local script:

    fetch_refresh_token.py

Yesterday the following mechanism repeatedly generated fresh usable tokens:

    python fetch_refresh_token.py --chromedriver
    "C:\Users\ak54743\Downloads\chromedriver.exe"

The script:

    authenticated browser / Citi SSO
        -> authorization code
        -> exchange_code_for_tokens(...)
        -> access token / refresh token
        -> save_tokens(...)
        -> existing local token files

This repeatedly produced fresh credentials.

There is also an existing automatic periodic token-refresh process.

Therefore:

DO NOT:
- invent a manual JWT-copy process
- ask me to paste bearer tokens into chat
- introduce another authentication mechanism
- add another refresh-token API
- replace fetch_refresh_token.py
- redesign token storage
- redesign OIDC
- modify the proven ChromeDriver flow
- change its cadence unless concrete evidence shows cadence itself is broken

Treat:

    fetch_refresh_token.py

as the authoritative existing POC token-generation mechanism.

Only verify, if necessary, that the active Runner client reads the token files
that this existing mechanism updates.

If Runner client caches a stale token while the existing refresh script writes
a fresh one, make ONLY the minimum wiring fix required so the Runner client
uses the refreshed existing token.

Never print token contents.

Never log Authorization headers.

Never include token values in your final report.


C. UPSTREAM STEPS 2.1–2.4 ARE PROVEN AND CURRENTLY CONFIRMED
-------------------------------------------------------------

The complete browser workflow has just been rerun.

DO NOT regenerate it.

DO NOT modify it.

DO NOT fabricate replacement data.

Current genuine state:

STEP 2.1
--------
Confirmed scenario.

Assessment horizon:
    12+ months / long-term structural

The scenario is based on the ECB reversing from an easing cycle toward renewed
rate increases and associated macro/credit consequences.

It is genuine output generated through the application and has been confirmed.


STEP 2.2
--------
Confirmed Banks - Major portfolio.

It legitimately contains TWO matching companies:

    COMMERZBANK AG
    internal/CAGID: 9000024985

    DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
    internal/CAGID: 9000008998

This is CORRECT.

Do NOT force Step 2.2 to contain one company.

The portfolio filters legitimately produce both banks.

The one-company restriction belongs to STEP 2.5, not Step 2.2.


STEP 2.3
--------
Confirmed.

Exactly five genuine Event-Driven factors.

Current generated factors are:

RF1
Net Interest Margin Expansion vs. Deposit Beta Compression
Weight 25%

RF2
Credit Quality Deterioration and Loan Loss Provisioning Pressure
Weight 25%

RF3
Capital Adequacy and Regulatory Buffer Resilience
Weight 25%

RF4
Funding Structure and Liquidity Resilience Under Tightening
Weight 12.5%

RF5
Revenue Diversification and Fee Income Resilience
Weight 12.5%

Total = 100%.

These are genuine current application outputs.

Do NOT replace them with fixtures.
Do NOT regenerate them.
Do NOT synthesize alternative factors.


STEP 2.4
--------
Confirmed.

Exactly five genuine Banks - Major Sector-Inherent factors.

Current generated factors include:

RF1
Net Interest Margin Compression and Earnings Resilience

RF2
Regulatory Capital Framework Reforms and RWA Density Convergence

RF3
NBFI Interconnections and Concentrated Counterparty Exposure

RF4
Asset Quality Cyclicality and Credit Loss Absorption

RF5
Technology Disruption and Escalating Cyber/Operational Risk

Current weights are approximately:

    22.22%
    22.22%
    22.22%
    22.22%
    11.11%

Total = 100%.

Again:

DO NOT regenerate.
DO NOT replace.
DO NOT fabricate.


======================================================================
3. STEP 2.5 COMPANY SELECTION — IMPORTANT
======================================================================

Step 2.2 contains two legitimate companies.

Step 2.5 already has a single-company selector.

For the controlled acceptance test use ONLY:

    DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
    internal company ID / CAGID: 9000008998

Known SEC identity:

    canonical registrant:
    DEUTSCHE BANK AKTIENGESELLSCHAFT

    CIK:
    0001159508

    foreign private issuer:
    YES

Relevant SEC filing families may therefore include 20-F and 6-K.

Do NOT run Commerzbank during this acceptance test.

Do NOT run a batch.

Do NOT click/resume "remaining companies".

Do NOT run both companies.

Exactly ONE company must be sent to Step 2.5.


======================================================================
4. CURRENT CONCRETE FAILURE — THIS IS THE PRIMARY TARGET
======================================================================

The latest live Step 2.5 attempt produced a real upstream Runner HTTP 500.

The important validation error is:

    "messages: at least one message is required"

This is now the PRIMARY defect.

Do NOT divert back into:

- SEC DNS
- CIK investigation
- Step 2.2 identity mapping
- factor generation
- sector generation
- Fiddler
- generic network diagnostics
- token architecture
- Step 3

The Runner endpoint is rejecting the request body because the request contract
is wrong/incomplete.

We need to determine precisely why.


======================================================================
5. VERY IMPORTANT CONTROL CASES
======================================================================

Do not guess the Runner request schema.

Use WORKING EVIDENCE.

Compare the current failing backend invocation against these control cases,
in this priority order:

CONTROL 1 — COLLEAGUE'S WORKING app.py
---------------------------------------

There is/was a colleague-provided working app.py / Swagger implementation that
successfully invoked the same enterprise service pattern.

Inspect it.

This is extremely important because it is a Python-side implementation from
the same environment.

Determine:

- exact Runner endpoint/path
- HTTP method
- request-body top-level keys
- whether it sends `messages`
- exact structure of a message
- role/content fields
- where preset/team/workspace identifiers are supplied
- how the request communicates the user input
- how it handles streaming
- how it recognizes completion

Do NOT copy unrelated app.py architecture.

Only reuse the proven request contract/pattern that is relevant.


CONTROL 2 — YESTERDAY'S SUCCESSFUL BACKEND RUN
----------------------------------------------

Yesterday a backend -> Runner -> Stylus run genuinely progressed and produced
a final assessment after a long execution, even though the requesting client
timed out earlier.

Locate any:

- logs
- debug output
- request snapshots
- previous code state
- git diff/history
- test fixture derived from that real run
- Runner request logging

that shows the request shape used when the backend actually reached the
Stylus execution/tool phase.

Ask:

    What did the previously successful backend request send that the current
    failing request no longer sends?

This comparison is critical.

Do NOT treat the current implementation as automatically correct simply because
offline unit tests pass.


CONTROL 3 — MANUAL STYLUS PRESET
--------------------------------

The manually configured Step 2.5 preset is already proven.

It has these logical inputs:

    CompanyContextJSON              REQUIRED
    ScenarioContextJSON             REQUIRED
    EventDrivenFactorsJSON          REQUIRED
    SectorInherentFactorsJSON       REQUIRED
    AssessmentASOFDATE              REQUIRED
    UserFeedback                    OPTIONAL

Model:
    Claude Sonnet 5

Integrations:
    SEC Filings
    Web Search

Knowledge includes:
    Step 2.5 field dictionary
    Step 2.5 SEC/Web output schema

The preset itself is NOT to be changed.

If there is an already captured successful manual browser/Runner request in
the repository/logs, inspect it.

Do not ask me to recreate network captures unless there is absolutely no
existing evidence and it becomes a genuine external blocker.


======================================================================
6. ROOT-CAUSE ANALYSIS — REQUIRED BEFORE CODING
======================================================================

Trace:

    Step 2.5 Run Assessment
        ->
    POST /api/v1/rpr/step25/run
        ->
    router/service
        ->
    stylus_engine.py
        ->
    runner_client.py
        ->
    actual outgoing Runner HTTP request

Determine the ACTUAL live request.

Safely inspect/log:

- final URL/path
- HTTP method
- Content-Type
- top-level JSON keys
- whether `messages` exists
- messages type
- messages count
- roles/types of messages
- content type
- preset/team/version/workspace identifier fields
- whether an input goal/prompt exists
- where the six Step 2.5 logical inputs are embedded
- approximate payload size

DO NOT log:

- Authorization
- bearer JWT
- refresh token
- cookies
- secrets


Then explain exactly why Runner says:

    "messages: at least one message is required"


Explicitly evaluate these possibilities against evidence:

1. We are calling a chat-style Runner endpoint that requires a non-empty
   `messages` list, but the backend sends no messages.

2. We are mixing a workflow/saved-preset payload shape with a chat endpoint.

3. The preset/team/version identifier is correct, but Runner additionally
   requires an initial user message.

4. The six Step 2.5 inputs are currently placed in `goal` or another field
   when this endpoint expects them inside a user message.

5. The current saved-preset change altered the request shape compared with the
   previously successful backend call.

6. We are using the wrong endpoint for the saved-preset invocation.

Do NOT choose one by assumption.

Prove it from code / working app.py / previous successful run / available
Runner contract.


======================================================================
7. SAVED PRESET VS INLINE PRESET — DO NOT GUESS
======================================================================

The current direction is to use the manually built and proven Step 2.5 preset.

Do NOT recreate or modify that preset.

Do NOT arbitrarily switch between:

- saved preset by ID/version
- inline full preset definition

based on speculation.

Instead determine which request form the proven Runner contract actually
supports for the manual preset we need.

If current saved-preset invocation is correct and only the initial message is
missing, keep saved-preset invocation and add the correct message.

If hard evidence from the working implementation shows a different invocation
contract is required, use the smallest proven form.

Do not guess UUIDs, team IDs, version IDs, or endpoint paths.


======================================================================
8. THE SIX STEP 2.5 INPUTS MUST BE PRESERVED
======================================================================

Whatever the correct Runner message/request representation is, preserve exactly
the six logical Step 2.5 preset inputs:

1. CompanyContextJSON
2. ScenarioContextJSON
3. EventDrivenFactorsJSON
4. SectorInherentFactorsJSON
5. AssessmentASOFDATE
6. UserFeedback

CompanyContext must contain exactly ONE company during the live acceptance test:

    Deutsche Bank
    CAGID 9000008998

The backend should NOT send:

- complete two-company assessment batch
- all browser state
- unrelated UI state
- full portfolio
- duplicated SEC filing contents
- synthetic data
- fake citations
- fake metrics
- test fixtures

Keep the compact payload work already done unless concrete evidence says a
specific required field was removed.


======================================================================
9. DO NOT BREAK THE CURRENT UPSTREAM STATE
======================================================================

The user has JUST rerun Steps 1–2.4.

The backend store is currently process-memory based.

Repeated server restarts previously erased the confirmed state and forced the
user to redo the entire workflow.

DO NOT make the user repeat Steps 1–2.4 again unnecessarily.

Before any backend restart that could erase the current state:

1. Query the existing authoritative backend state using existing read/context
   endpoints.

2. Capture the CURRENT genuine confirmed Step 2.1, 2.2, 2.3 and 2.4 payloads
   into a TEMPORARY local acceptance snapshot.

3. This snapshot must contain ONLY the exact genuine current backend state.

4. Do not manufacture or alter values.

5. After a required restart, restore that exact state only through the existing
   application/finalize APIs or existing state-loading mechanism.

6. Do NOT implement a new persistence architecture merely for this test.

7. Delete/ignore the temporary acceptance snapshot after the controlled test.

If the server can be tested without restart, prefer that.

The purpose is simply to avoid making the user manually rerun 2.1–2.4 because
of our code test.


======================================================================
10. IMPLEMENT THE SMALLEST RUNNER CONTRACT FIX
======================================================================

Once the exact difference is proven:

Make the SMALLEST possible change.

Likely files may include:

    backend/step25/runner_client.py
    backend/step25/stylus_engine.py

and narrowly focused Step 2.5 tests.

Do NOT assume both need modification.

Do NOT touch unrelated routes.

Do NOT rewrite the application.

Do NOT perform broad cleanup.


The fixed outgoing request must:

- use the proven Runner endpoint
- use the proven saved-preset/workspace contract
- include the required non-empty user/message input where the API expects it
- preserve the six logical Step 2.5 input fields
- represent exactly one selected company
- not expose secrets
- not add Python SEC retrieval
- not contain synthetic factors


======================================================================
11. TOKEN MECHANISM — KEEP IT SIMPLE
======================================================================

Do NOT stop and ask me to manually paste a JWT.

Do NOT add a new token mechanism.

Use the existing proven token infrastructure.

If a fresh token is needed for the final live run:

First determine whether the automatic refresher has already provided one.

If not, use the existing proven script/environment, e.g. the existing
fetch_refresh_token.py + ChromeDriver mechanism.

Do not expose the token.

After refresh, verify only:

    TOKEN PRESENT
    TOKEN NOT EXPIRED
    TOKEN HAS SUFFICIENT REMAINING LIFETIME

Do not print the token.

If the active Runner client is reading stale token state, fix only that narrow
consumption issue.

Authentication must NOT become another redesign project.


======================================================================
12. FOCUSED OFFLINE TESTS
======================================================================

Before the live run, add/run narrowly targeted tests proving:

A. RUNNER REQUEST CONTRACT
--------------------------
- correct endpoint/path selected
- request contains required message/input structure
- messages is non-empty if that is the proven API contract
- correct role/type is used
- saved preset identifiers are preserved if required


B. STEP 2.5 INPUT CONTRACT
--------------------------
All six logical inputs survive the conversion:

- CompanyContextJSON
- ScenarioContextJSON
- EventDrivenFactorsJSON
- SectorInherentFactorsJSON
- AssessmentASOFDATE
- UserFeedback


C. SINGLE COMPANY
-----------------
Exactly one company is sent to Runner.


D. NO FABRICATION
-----------------
Tests may test structure, but the LIVE acceptance run must use the existing
confirmed real factors.

Do not create a fake acceptance result.


E. SECURITY
-----------
No token value is logged.


F. SEC ARCHITECTURE
-------------------
The active Stylus Step 2.5 path has no hard dependency on local Python reaching
data.sec.gov.


Run only focused Step 2.5 tests.

Do not run the full project test suite unless directly required.


======================================================================
13. IMPORTANT UI ERROR-MESSAGE CORRECTION
======================================================================

The latest failed UI displayed language suggesting:

    "SEC and web evidence were collected..."

while the same attempt also failed at the Runner request-contract stage with:

    "messages: at least one message is required"

That statement may be misleading.

Inspect whether the frontend/backend is unconditionally claiming SEC/Web
evidence collection on any Stylus failure.

If so, make the smallest correction:

Only say SEC evidence was collected when actual tool activity for THAT JOB
proves Stylus SEC Filings executed.

Only say Web evidence was collected when actual tool activity for THAT JOB
proves Web Search executed.

A request rejected before tool execution must NOT claim evidence was collected.

This is an important POC data-integrity requirement.


======================================================================
14. SSE / COMPLETION HANDLING — ONLY IF THE LIVE RUN REACHES IT
======================================================================

Do NOT proactively redesign streaming again.

We previously had Runner calls where:

    stream opened
    tools ran
    final completion took a long time

Existing bounded completion handling was added for that problem.

Preserve it.

For the final live acceptance run:

If Runner accepts the corrected request and opens the stream:

- continue consuming actual SSE events
- preserve tool activity evidence
- do not treat STREAM_OPEN as success
- do not stop after first assistant/tool event
- wait for actual terminal workflow completion
- capture final schema-conformant model output/artifact
- keep execution bounded

Only modify SSE completion again if the corrected request reaches the stream
and concrete current evidence shows the existing handling is still wrong.

Do not reopen it merely because it was a historical issue.


======================================================================
15. SEC / WEB EVIDENCE VALIDATION
======================================================================

For the live Deutsche Bank run, we require genuine Stylus tool activity.

Expected conceptual path:

    Deutsche Bank context
       ->
    Runner
       ->
    saved Step 2.5 preset
       ->
    Stylus SEC Filings
       ->
    optional Web Search
       ->
    Claude Sonnet 5
       ->
    final JSON


SEC provenance should be evaluated using the strongest observable evidence.

Do not require accession_number or URL to be non-null in every evidence item
if the Stylus SEC tool itself did not return those fields.

However:

- SEC tool activity must actually be present in the Runner event stream/log
  for claims relying on SEC evidence.
- issuer identity must correspond to Deutsche Bank / CIK 0001159508.
- filing dates must respect AssessmentASOFDATE.
- filing type/content must be internally consistent.
- preserve accession number/URL whenever actually returned.
- do not invent missing provenance.
- null is acceptable when genuinely unavailable.
- model claims unsupported by actual SEC tool activity must not be presented as
  verified SEC evidence.


======================================================================
16. ONE CONTROLLED LIVE ACCEPTANCE TEST
======================================================================

After:

    focused tests PASS
    current confirmed upstream state restored/preserved
    Runner token valid with sufficient remaining lifetime

perform EXACTLY ONE live Step 2.5 assessment.

Company:

    DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
    CAGID 9000008998
    CIK 0001159508

Do NOT run Commerzbank.

Do NOT resume a batch.

Do NOT run all names.

Do NOT automatically run the second company after Deutsche completes.


The live test must use:

- current confirmed Step 2.1 scenario
- genuine confirmed Step 2.2 context
- exactly current 5 Step 2.3 factors
- exactly current 5 Step 2.4 factors
- current AssessmentASOFDATE
- optional actual UserFeedback only if supplied


======================================================================
17. STEP 2.5 METHODOLOGY MUST REMAIN UNCHANGED
======================================================================

Do not alter business logic.

The Step 2.5 methodology remains:

    ED score
    SI score

Composite:

    80% Event-Driven
    20% Sector-Inherent

Composite =
    0.80 * ED
    + 0.20 * SI

Final output should populate where supported:

- factor-level assessments
- factor scores
- evidence
- commentary
- ED score
- SI score
- composite score
- residual rating
- credit-impact rating
- recommendations / RRR action where legitimately supported

Do not invent unavailable values.


======================================================================
18. SUCCESS CRITERIA
======================================================================

A successful acceptance run requires ALL relevant items below:

UPSTREAM
--------
STEP 2.1 CONFIRMED: YES
STEP 2.2 CONFIRMED: YES
STEP 2.2 COMPANY COUNT: 2
STEP 2.3 CONFIRMED: YES
STEP 2.3 FACTOR COUNT: 5
STEP 2.3 WEIGHT: 100%
STEP 2.4 CONFIRMED: YES
STEP 2.4 FACTOR COUNT: 5
STEP 2.4 WEIGHT: 100%


STEP 2.5 SELECTION
------------------
SELECTED COMPANY COUNT: 1
SELECTED COMPANY: DEUTSCHE BANK AG
SELECTED COMPANY ID: 9000008998


AUTH
----
EXISTING TOKEN MECHANISM USED: YES
MANUAL JWT COPY REQUIRED: NO
RUNNER AUTH: PASS


RUNNER CONTRACT
---------------
RUNNER REQUEST CONTRACT VERIFIED: YES
MESSAGES/INPUT STRUCTURE VALID: YES
RUNNER REQUEST ACCEPTED: YES
HTTP 500 "messages required": RESOLVED


STYLUS
------
PROVEN PRESET USED: YES
SEC FILINGS TOOL ACTIVITY: YES
WEB SEARCH TOOL ACTIVITY: YES / NOT REQUIRED
PYTHON SEC HARD GATE: NO


COMPLETION
----------
STREAM OPEN: YES
TERMINAL WORKFLOW COMPLETION: YES
FINAL RESPONSE/ARTIFACT RECEIVED: YES
FINAL JSON PARSED: YES
SCHEMA VALID: YES


CREDIT OUTPUT
-------------
ED SCORE: POPULATED
SI SCORE: POPULATED
COMPOSITE SCORE: POPULATED
RESIDUAL RATING: POPULATED
CREDIT IMPACT RATING: POPULATED


DATA INTEGRITY
--------------
NO FABRICATED COMPANY DATA: PASS
NO FABRICATED FACTORS: PASS
NO FABRICATED SEC CITATIONS: PASS
ISSUER IDENTITY VALIDATED: PASS


APPLICATION
-----------
STEP 2.5 RESULT PERSISTED: YES
STEP 2.5 UI POPULATED: YES
STEP 3 CONSUMER CONTRACT READY: YES

Do NOT actually work on Step 3 yet.


======================================================================
19. IF THE LIVE TEST FAILS
======================================================================

Do NOT start another broad investigation.

Stop at the FIRST newly proven failing boundary.

Examples:

If:
    Runner rejects request

Report exact Runner response.

If:
    Runner accepts request but no SEC tool activity appears

Report that exact boundary.

If:
    SEC executes but final model completion never arrives

Report that exact boundary.

If:
    final JSON exists but parser rejects it

Report exact schema/parser mismatch.

Do not respond to one failure by changing five unrelated components.

Do not re-investigate components already proven in the same run.


======================================================================
20. FILE SCOPE
======================================================================

There are currently many modified files in the working tree.

DO NOT mass-revert them.

DO NOT mass-clean them.

DO NOT perform broad formatting.

Touch only the smallest number of files directly necessary for this Step 2.5
request-contract fix and focused verification.

If you notice unrelated modifications, leave them alone and mention them only
if they directly interfere with this task.


======================================================================
21. FINAL RESPONSE FORMAT
======================================================================

Do not give me a long narrative.

At completion return this exact style of report:

ROOT CAUSE
----------
<precise reason Runner returned "messages: at least one message is required">


WORKING CONTROL USED
--------------------
app.py request pattern: <used/not available>
previous successful backend request: <used/not available>
manual Stylus contract evidence: <used/not available>


OLD RUNNER REQUEST
------------------
endpoint:
top-level keys:
messages present:
messages count:
where six Step 2.5 inputs were placed:


FIXED RUNNER REQUEST
--------------------
endpoint:
top-level keys:
messages present:
messages count:
message role/type:
where six Step 2.5 inputs are placed:
preset identifier method:


AUTH
----
existing fetch_refresh_token.py preserved: YES/NO
existing auto-refresh preserved: YES/NO
new auth mechanism introduced: MUST BE NO
Runner auth: PASS/FAIL


UPSTREAM
--------
Step 2.1 confirmed:
Step 2.2 companies:
Step 2.3 factors:
Step 2.4 factors:
selected Step 2.5 company:


FOCUSED TESTS
-------------
PASS/FAIL
<test names>


LIVE DEUTSCHE BANK ACCEPTANCE
-----------------------------
RUNNER REQUEST: PASS/FAIL
SEC TOOL ACTIVITY: YES/NO
WEB TOOL ACTIVITY: YES/NO/NOT REQUIRED
TERMINAL COMPLETION: YES/NO
FINAL JSON: YES/NO
SCHEMA VALID: YES/NO
EVIDENCE VALIDATED: YES/NO

ED SCORE:
SI SCORE:
COMPOSITE SCORE:
RESIDUAL RATING:
CREDIT IMPACT RATING:

STEP 2.5 PERSISTED: YES/NO
STEP 2.5 UI POPULATED: YES/NO
READY FOR STEP 3: YES/NO


FILES CHANGED
-------------
<exact list>


IF BLOCKED
----------
FIRST GENUINE EXTERNAL BLOCKER:
<one exact blocker only>

Do not propose another architecture.

Do not restart investigation from SEC or authentication.

Execute the approved scope now.
