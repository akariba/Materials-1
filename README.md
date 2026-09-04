CONTINUE THE RPR END-TO-END FIX FROM THE CURRENT CHECKPOINT.

DO NOT RESTART THE DESIGN WORK.
DO NOT CHANGE THE STYLUS PRESET YET.
DO NOT DECLARE SEC LIVE PASS FROM FIXTURE TESTS.

We now have a very specific checkpoint.

CURRENT VERIFIED STATE:

1. The Step 2.5 SEC grounding CODE PATH has been wired so the active
   Stylus engine can use deterministic SEC evidence.

2. Fixture/known-data testing proves the mechanism can pass:
   - real-format CIK
   - real accession number
   - real EDGAR URL
   - real filing text/excerpts
   through the strict evidence validator.

3. The strict anti-fabrication validator remains intact.

4. A real live attempt is currently blocked by TWO separate issues:

   BLOCKER A:
   Runner Service bearer token is expired.

   BLOCKER B:
   direct Python/backend DNS/network access to:
   data.sec.gov
   currently fails from this development environment.

The purpose of this task is to RESOLVE THESE TWO BLOCKERS using existing
approved project/environment mechanisms and then COMPLETE the actual
end-to-end live test.

Do not ask me broad architectural questions.

Proceed autonomously until a genuinely external action from the user
is unavoidable.

============================================================
1. FIRST: FIX THE RUNNER TOKEN USING THE EXISTING MECHANISM
============================================================

Do NOT ask the user to paste a bearer token into chat.

The project has previously implemented/used Runner token refresh logic.

Search the repository for all existing mechanisms including terms such
as:

runner-token
refresh token
runner_service
token refresh
seconds_remaining
RPR_STEP25
admin/runner-token
RUNTIME_ENV
refresh_runner
bearer

Determine exactly how the currently working project is supposed to
refresh the Runner Service credential.

Reuse that mechanism.

Do NOT build another token framework.

If an existing script can refresh it automatically, run it.

If an existing application/admin endpoint such as:

POST /api/v1/rpr/step25/admin/runner-token

is the intended route, use it through the project's existing
authenticated mechanism.

Then prove:

TOKEN:
expired = false

seconds_remaining > 0

and preferably enough remaining time for the full test.

Do not proceed to a 10-company Runner execution with an expired or
nearly expired token.

============================================================
2. IF TOKEN REFRESH REQUIRES A GENUINE USER AUTH ACTION
============================================================

Only if the repository/environment genuinely cannot obtain the token
without an interactive user login:

STOP ONLY THAT SUBTASK.

Do NOT ask the user to send the token into chat.

Give the user the exact existing local command/UI action required to
refresh it securely.

Then continue all other investigation while waiting.

Do not redesign authentication.

============================================================
3. SECOND: DO NOT ASSUME data.sec.gov DIRECT EGRESS IS REQUIRED
============================================================

The current failure:

getaddrinfo / DNS resolution failure for data.sec.gov

is an environment/network failure.

Before calling this an unavoidable blocker, inspect the repository and
environment to determine how approved outbound access is normally done.

Search for existing:

HTTP_PROXY
HTTPS_PROXY
NO_PROXY

enterprise proxy settings

requests.Session configuration

httpx clients

corporate certificates / CA bundle

enterprise API adapters

web-search adapters

SEC adapters

network gateways

approved internal endpoints

proxy-aware utility modules

environment variables in RUNTIME_ENV.ps1

Do NOT invent a proxy hostname.

Do NOT bypass corporate security.

Only reuse already-existing approved configuration.

============================================================
4. TRACE THE PREVIOUS REAL HYBRID SEC SUCCESS
============================================================

This is critical.

You previously identified a persisted successful evidence artifact from
the hybrid engine containing a genuine validated Salesforce 10-K:

- real accession number
- real EDGAR URL
- evidence accepted by the validator.

Trace EXACTLY how that evidence was obtained.

Do not assume.

Follow the code path from:

hybrid engine
→ SEC retrieval/discovery
→ filing metadata
→ filing content
→ evidence object.

Determine whether the successful hybrid run used:

A. direct sec_filings.py → data.sec.gov

B. enterprise web search

C. Runner/LLM web tooling

D. an internal proxy

E. cached previously downloaded SEC data

F. another approved service.

This matters because the same network-accessible real evidence path may
be reusable by Stylus.

============================================================
5. IF THE HYBRID PATH HAS AN APPROVED LIVE SEC NETWORK ROUTE
============================================================

If the existing hybrid path can currently obtain genuine live SEC data
through an approved network route:

reuse the MINIMUM necessary network/retrieval component in the Stylus
grounding path.

Do NOT switch Step 2.5 back to the hybrid assessment engine.

The target remains:

deterministic SEC grounding
→ Stylus assessment.

But SEC transport may reuse an existing approved component.

Do not duplicate it.

============================================================
6. DIRECT SEC RETRIEVAL REMAINS PREFERRED WHEN AVAILABLE
============================================================

If approved proxy/network configuration exists and allows
sec_filings.py to access:

data.sec.gov

then use it.

Test a single known public issuer first.

The test must actually resolve:

company
→ CIK
→ submissions metadata
→ real filing
→ accession number
→ EDGAR URL
→ useful filing content.

No fixtures.

No static fake response.

============================================================
7. USE A KNOWN RESOLVABLE SOFTWARE ISSUER FOR THE FIRST LIVE TEST
============================================================

Do NOT begin with an ambiguous company such as a private LLC.

Take ONE company from the confirmed Step 2.2 Software population with
the strongest public identifiers.

Preference:

ticker/RIC
+
CUSIP/ISIN
+
recognizable public issuer.

The candidate must still actually originate from Step 2.2.

Preflight it.

Show internally:

Canonical Company
Ticker
CIK
Form
Filing Date
Accession
EDGAR URL.

Only then call Stylus.

============================================================
8. VERIFY THE ACTUAL SEC PAYLOAD ENTERING STYLUS
============================================================

Before executing Stylus, inspect/log a SAFE summarized version of the
payload.

Prove it contains:

company identity

Step 2.1 scenario

5 confirmed Step 2.3 RFs

5 confirmed Step 2.4 RFs

real SEC evidence entries

real evidence IDs

real form

real filing date

real accession

real SEC URL

real extracted SEC text/context.

Do not log bearer tokens or secrets.

The objective is to prove the model is actually grounded before it is
called.

============================================================
9. TEST ONE REAL STYLUS ASSESSMENT
============================================================

Once:

Runner token = valid

and

SEC evidence = live/real

run ONE issuer through the actual active Stylus path.

Use the real Runner.

Do not use fixture mode.

Do not use mock SEC.

Do not use static JSON result.

Verify the complete runtime sequence:

preflight
→ deterministic SEC evidence
→ Stylus payload
→ Runner stream
→ model/tool execution
→ bounded completion
→ final model response
→ parser
→ evidence validation
→ normalized Step 2.5 result.

============================================================
10. STRICT SEC PROVENANCE TEST
============================================================

The final assessment must reference supplied SEC evidence IDs.

For example conceptually:

SEC_1

Backend must be able to map that exact ID to:

real CIK
real accession
real form
real filing date
real EDGAR URL.

Do NOT accept a model-written free-form SEC citation as proof.

Do NOT weaken the validator.

============================================================
11. IF THE MODEL IGNORES THE PROVIDED SEC EVIDENCE IDS
============================================================

Only AFTER we prove real evidence is entering the Stylus context:

inspect the current manual Stylus preset prompt contract.

Do NOT modify the preset yourself.

If the model is failing purely because the preset prompt does not tell
it to cite the supplied evidence IDs, report the MINIMUM manual prompt
change required for the user.

Do not redesign the preset.

Do not add unnecessary input fields if the current context field can
already contain the SEC bundle.

============================================================
12. DO NOT USE FIXTURE SEC FOR FINAL ACCEPTANCE
============================================================

The current backend may report things such as:

sec_mode=fixture
web_mode=fixture

unless explicit production/approval variables are set.

Fixture mode is useful for unit tests.

It is NOT acceptable for the final POC evidence run.

Determine the intended existing environment switches such as:

RPR_STEP25_LIVE_ENABLED
RPR_SEC_EGRESS_APPROVED
RPR_SEC_USER_AGENT

or actual equivalents.

Do NOT simply force them to true.

Verify what each gate means and whether the environment satisfies it.

Use the existing approved live-mode mechanism only.

============================================================
13. USER-AGENT REQUIREMENT
============================================================

SEC requires appropriate request identification.

If sec_filings.py expects an SEC user-agent setting, use the project's
existing configured value.

Do not fabricate contact data.

Do not silently send a blank or invalid user agent if the current
implementation requires one.

============================================================
14. IF DIRECT SEC ACCESS IS GENUINELY IMPOSSIBLE
============================================================

Only after:

- checking existing proxy settings,
- tracing previous hybrid success,
- checking approved adapters,
- checking RUNTIME_ENV,
- checking current network configuration,

may you declare direct SEC access unavailable.

If direct access is genuinely unavailable, determine whether another
ALREADY APPROVED enterprise path can return:

real SEC filing content
+
real accession
+
real URL
+
real filing date

with deterministic provenance.

The alternative must satisfy the same evidence validator.

Do NOT replace this with an LLM saying:

“I found a 10-K.”

============================================================
15. NEVER FALL BACK SILENTLY TO FIXTURE DATA
============================================================

For the live POC:

if live SEC retrieval fails,

the application must not silently substitute fixture evidence and then
present the result as real.

Keep live/fixture state explicit.

============================================================
16. AFTER ONE REAL ISSUER PASSES
============================================================

Only after ONE genuine issuer passes end-to-end:

expand to the 10-company Software cohort.

Do not run 10 expensive calls before proving the first one.

This prevents another 40-minute blind failure.

============================================================
17. TEN-COMPANY COHORT
============================================================

Preflight candidates from confirmed Step 2.2 Software population.

Continue until 10 have:

canonical issuer
ticker where applicable
CIK
real qualifying filing
real accession
real filing URL.

Then execute Stylus sequentially or using the existing safe concurrency
logic.

Do not introduce a new concurrency architecture.

============================================================
18. FAILED ISSUER HANDLING
============================================================

If issuer #N fails for an issuer-specific reason:

record technical failure internally

do NOT create a credit result

move to the next preflighted Software candidate.

Final POC target:

10 successful validated assessments.

============================================================
19. STEP 2.5 TABLE
============================================================

Render only the successful 10-company cohort in the POC assessment
outcome.

No 226-company global dump.

No raw technical errors.

No giant JSON.

No diagnostics in business columns.

Use v31 layout.

============================================================
20. THEN CONFIRM STEP 2.5
============================================================

After:

10 real issuer assessments
+
validated SEC provenance
+
valid Step 2.3/2.4 scoring

confirm Step 2.5.

Verify the confirmation state persists.

============================================================
21. THEN EXECUTE STEP 3
============================================================

Do not stop after Step 2.5.

Use the SAME served workflow/session.

Step 3 must consume:

confirmed Step 2.2 portfolio/exposure
confirmed Step 2.3
confirmed Step 2.4
confirmed Step 2.5.

No file:// functional test.

No static v31 demo data.

============================================================
22. STEP 3 MUST BE REAL
============================================================

Populate from actual assessed cohort:

Total Exposure
IG
NIG
Criticized
Classified

Exposure Segmentation

Weighted Composite Score

Impact Rating

Companies Included

Credit Assessment / Intelligence

Key Drivers / Mitigants

using existing approved methodology.

No invented values.

If a required portfolio field genuinely does not exist:

N/A

rather than fabrication.

============================================================
23. V31 VISUAL TESTING
============================================================

After data execution works:

compare the served current app directly with v31 for:

Step 2.4
Step 2.5
Step 3.

Do not change working business logic merely for CSS.

Fix remaining genuine visual discrepancies.

============================================================
24. DO NOT PRODUCE ANOTHER INTERIM STATUS REPORT
============================================================

Your current report already identified the blockers.

Do not repeat them.

Continue resolving them.

Only produce a response if:

A. the complete live test succeeds,

or

B. one precise external blocker genuinely requires a user action.

============================================================
25. IF A USER ACTION IS REQUIRED
============================================================

Return ONLY:

USER ACTION REQUIRED

Blocker:
<one exact blocker>

Why:
<one concise explanation>

Exact action:
<exact local UI/command action>

Last verified checkpoint:
<exact checkpoint>

Do NOT provide a broad report.

Do NOT ask multiple questions.

============================================================
26. FINAL SUCCESS RESPONSE
============================================================

Only after real end-to-end completion return:

END-TO-END: PASS

RUNNER TOKEN: PASS

LIVE SEC NETWORK: PASS
SEC GROUNDING: PASS

STEP 2.4: PASS
STEP 2.5: PASS
STEP 3: PASS

10 ASSESSED ISSUERS:

Company | Ticker | CIK | Form | Filing Date | Accession

STEP 2.5:
10/10 evidence validated

STEP 3:
Total exposure
IG
NIG
Criticized
Classified
Weighted composite
Impact rating

V31 2.4: PASS
V31 2.5: PASS
V31 STEP 3: PASS

PRESET MANUAL CHANGE REQUIRED:
NO

or the one minimal required change.

REMAINING BLOCKER:
NONE

Begin with Runner token recovery and network-path tracing now.
