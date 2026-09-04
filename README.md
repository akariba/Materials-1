I need your help as the Stylus platform expert for a NON-PRODUCTION proof of concept.

Please treat this strictly as a local POC / demonstration environment.

IMPORTANT SCOPE:
- This is NOT production.
- Do NOT propose MCP.
- Do NOT propose a production deployment architecture.
- Do NOT propose production service accounts, enterprise production onboarding, Kubernetes, gateways, persistent orchestration infrastructure, or similar production engineering.
- Do NOT redesign the application.
- I need the smallest supported POC integration that allows my local Python application to invoke a Stylus preset, use the Stylus SEC Filings and Web Search integrations, receive the final structured response, and continue the workflow.
- Real data only. No fabricated SEC evidence.
- Windows local development environment.
- I am allowed to use Stylus manually in my browser and I have access to the Runner/Workspace environment used by Stylus.

I want you to analyze the exact situation below and tell me the simplest technically correct Stylus-supported solution.

============================================================
1. BUSINESS / POC PURPOSE
============================================================

The application is an AI-assisted Rapid Portfolio Review (RPR) proof of concept for credit-risk analysis.

The workflow is:

Step 2.1
Scenario and assumptions are generated and confirmed.

Step 2.2
A portfolio / sector and companies are selected and confirmed.

Step 2.3
Exactly 5 Event-Driven credit risk factors are generated and confirmed.

Step 2.4
Exactly 5 Sector-Inherent credit risk factors are generated and confirmed.

Step 2.5
For ONE selected company, perform a company-specific financial/credit assessment using:

- confirmed Step 2.1 scenario;
- confirmed Step 2.2 company identity/context;
- confirmed Step 2.3 Event-Driven factors;
- confirmed Step 2.4 Sector-Inherent factors;
- real SEC filing evidence;
- real web evidence where needed.

Step 2.5 produces, among other things:

- Event-Driven weighted score;
- Sector-Inherent weighted score;
- composite score;
- residual-risk rating;
- credit-impact rating;
- factor-level vulnerability/buffer assessments;
- evidence;
- credit assessment commentary.

The current product weighting is:

Composite Score =
80% × Event-Driven score
+
20% × Sector-Inherent score.

The completed Step 2.5 company results are later aggregated into Step 3 Portfolio Level Assessment.

Therefore Step 2.5 must be:
- deterministic with respect to supplied confirmed factors;
- company-specific;
- evidence grounded;
- machine readable;
- usable by downstream Step 3.

============================================================
2. CURRENT STYLUS PRESET
============================================================

I manually created a Stylus preset for Step 2.5.

Conceptually it is:

RPR Step 2.5 SEC + Web Financial Assessment

It uses Claude Sonnet 5.

Enabled Stylus integrations:

- SEC Filings
- Web Search

The preset currently receives approximately these input fields:

1. CompanyContextJSON
2. ScenarioContextJSON
3. EventDrivenFactorsJSON
4. SectorInherentFactorsJSON
5. AssessmentASOFDATE
6. UserFeedback (optional)

The preset also has Knowledge attachments containing:

- the Step 2.5 field dictionary / methodology;
- the required Step 2.5 output schema.

The prompt explicitly requires:

- exactly one company;
- use the supplied confirmed ED factors;
- use the supplied confirmed SI factors;
- do not create/rewrite/remove factors;
- preserve supplied factor weights;
- obtain real evidence;
- use SEC filings and Web Search;
- no invented values;
- unavailable evidence must be marked unavailable;
- output JSON only;
- output must conform to the attached schema;
- calculate ED score;
- calculate SI score;
- calculate composite score;
- derive residual risk / credit impact according to the supplied methodology;
- return a structured assessment consumable by the RPR application.

============================================================
3. IMPORTANT FACT: MANUAL STYLUS EXECUTION WORKS
============================================================

When I manually run this preset INSIDE Stylus, it works much better.

For example, I manually tested Apple.

Stylus visibly executed:

- SEC Filings
- Web Search

and generated a structured JSON artifact.

The manual execution took approximately 2 minutes.

The generated assessment contained:

- company identity;
- Event-Driven assessments;
- Sector-Inherent assessments;
- scores;
- evidence;
- commentary.

Therefore:

THE CORE PRESET + MODEL + STYLUS INTEGRATIONS ARE CAPABLE OF EXECUTING THE USE CASE.

The problem is primarily the integration between my local RPR backend and Stylus/Runner, not that Stylus is incapable of doing the assessment.

============================================================
4. CURRENT LOCAL RPR ARCHITECTURE
============================================================

The local application is:

Browser UI
    ↓
Local FastAPI Python backend
    ↓
Step 2.5 Runner client
    ↓
Stylus / Runner
    ↓
Stylus preset
    ↓
SEC Filings + Web Search
    ↓
structured final JSON
    ↓
FastAPI
    ↓
RPR Step 2.5 UI
    ↓
Step 3 aggregation

This is strictly a POC.

I do NOT need production architecture.

============================================================
5. WHAT ALREADY WORKS
============================================================

We have now verified that the upstream RPR workflow can persist server-side.

For a controlled live test we confirmed:

Step 2.1:
Scenario present = YES

Step 2.2:
Portfolio present = YES

Step 2.3:
Confirmed = YES
Real factor count = 5
Weights total = 100%

Step 2.4:
Confirmed = YES
Real factor count = 5
Weights total = 100%

Therefore the authoritative upstream state is ready for Step 2.5.

We also implemented a SINGLE-COMPANY selector so that Step 2.5 does not accidentally run 30+ companies concurrently.

The backend constructs a compact payload rather than sending enormous UI objects.

============================================================
6. COMPANY IDENTITY / SEC RESOLUTION
============================================================

One of our controlled test companies is:

Deutsche Bank AG [DE Frankfurt am Main]

Internal company ID:
9000008998

Our identity resolver successfully maps this to:

SEC canonical name:
DEUTSCHE BANK AKTIENGESELLSCHAFT

CIK:
0001159508

SEC registrant:
YES

Foreign Private Issuer:
YES

Relevant forms include:
20-F
6-K

So company/CIK resolution itself is not the primary problem.

============================================================
7. THE SEC PROBLEM
============================================================

Our Python backend contains a deterministic SEC lookup implementation which attempts to reach URLs such as:

https://data.sec.gov/submissions/CIK0001159508.json

However, from this local corporate development environment, direct Python access to:

data.sec.gov
www.sec.gov

is not reliably reachable.

We have seen DNS/network/proxy related failures.

Therefore a backend preflight that requires Python itself to successfully download SEC filings can block Step 2.5 even though the Stylus SEC Filings integration is available and works from inside Stylus.

This creates the current architectural question.

Should the POC architecture be:

A)

Python backend
→ direct data.sec.gov
→ obtain filings
→ send filings to Stylus

OR

B)

Python backend
→ send company identity/context to Stylus
→ Stylus SEC Filings integration retrieves the real filing evidence
→ Stylus returns evidence + assessment

For this POC, B appears much more appropriate because the approved Stylus SEC integration already works.

Please explicitly confirm whether this is the correct supported POC pattern.

============================================================
8. IMPORTANT DATA-INTEGRITY REQUIREMENT
============================================================

We absolutely do NOT want the model merely to SAY:

“According to the company's 20-F…”

unless that filing genuinely came from the SEC Filings integration.

Our backend previously attempted to validate evidence by looking for:

- accession number;
- filing URL;
- SEC source reference;
- tool-origin metadata.

In some manual Stylus output, the model produced reasonable SEC-derived facts but fields such as:

accession_number
url

were null.

Therefore please explain:

WHAT EXACTLY DOES THE STYLUS SEC FILINGS INTEGRATION RETURN TO THE MODEL/RUNNER?

For example, does the tool result expose:

- company/registrant?
- CIK?
- filing type?
- filing date?
- accession number?
- SEC filing URL?
- document URL?
- filing text?
- source identifier?
- integration/tool-call metadata?

Which fields can we reliably use to prove that evidence really came from the Stylus SEC Filings integration?

If the SEC integration does not expose accession_number or URL for every result, we should NOT invent them.

Please tell us the appropriate validation rule.

============================================================
9. RUNNER / SSE ISSUE
============================================================

The second problem is execution through Runner.

We have observed this pattern:

HTTP request accepted
→ Runner request starts
→ HTTP 200
→ SSE stream opens
→ FIRST_SSE_EVENT received
→ Stylus continues processing
→ sometimes SEC/Web tool execution occurs
→ backend continues waiting
→ final model response sometimes arrives very late or is not recognized correctly.

At times a manual Stylus execution finishes in approximately 2 minutes while the backend-driven execution can continue for 6, 10, 20 or even 30+ minutes.

We have already found one major cause:

Previously the backend supplied a much larger payload than the manual Stylus execution.

We reduced this to a compact payload.

The approximate compact payload is now only a few KB rather than a huge company/portfolio object.

But I need to know the correct Runner completion contract.

PLEASE EXPLAIN PRECISELY:

When invoking Stylus through Runner/SSE:

1. What event means the Runner request has been accepted?
2. What event means model generation has started?
3. How are integration/tool calls represented?
4. How are SEC Filings tool results represented?
5. How are Web Search tool results represented?
6. What event represents the genuine FINAL assistant/model response?
7. Is there a dedicated completion/end event?
8. Is an artifact emitted separately from the assistant final message?
9. Can an artifact arrive before/after the final assistant event?
10. When is it safe for the Python client to close the SSE stream?
11. Should the client continue reading after tool completion until a final model message is received?
12. What is the recommended timeout for a POC?
13. Is there a supported polling/job-status pattern that is better than holding one long HTTP request?

We need the smallest robust client implementation.

============================================================
10. TOKEN / AUTHENTICATION ISSUE
============================================================

We also periodically encounter Runner authentication expiration.

Symptoms have included:

HTTP 401
expired token
refresh attempt returning HTTP 400
Runner auth not ready

Our current POC has experimented with:

- storing a current Runner bearer token locally;
- refreshing cached credentials;
- manually obtaining a new token from an authenticated browser session.

This is becoming brittle.

I need the SUPPORTED POC METHOD.

Again:

NO MCP.
NO PRODUCTION TRACK.
NO production service account design.

For a developer running a local Python FastAPI POC while logged into Stylus in the browser:

What is the simplest supported authentication mechanism for invoking Runner?

Please answer specifically:

1. Should a local POC use a bearer token?
2. How is that bearer token supposed to be obtained?
3. What is its normal lifetime?
4. Is there a real supported refresh-token mechanism?
5. If yes, what endpoint/workflow should refresh it?
6. If no, should the user simply re-authenticate through SSO when expired?
7. Is there a local developer/Runner SDK that manages authentication automatically?
8. Is there a supported CLI login/session mechanism?
9. Should we avoid copying browser network tokens entirely?
10. Is there a standard POC example for local Python → Runner?

Please distinguish clearly between:
- what is officially supported;
- what merely happens to work temporarily;
- what we should NOT do.

============================================================
11. SAVED PRESET VS INLINE PRESET
============================================================

Another question:

Our backend has experimented with supplying an inline preset definition to Runner.

But the user also has the preset saved manually in Stylus.

For this POC, which approach is simpler and more reliable?

OPTION A
Invoke the saved Stylus preset by an identifier/reference.

OPTION B
Send the entire inline preset definition from Python on every run.

Please explain the supported pattern and trade-offs.

If a saved preset can be invoked directly, tell us what identifier the backend needs and where the user can obtain it.

Do not propose changing the preset unless actually necessary.

============================================================
12. DUPLICATE SEC RETRIEVAL
============================================================

We also identified an efficiency problem.

If Python obtains deterministic SEC evidence first AND the Stylus preset independently executes SEC Filings again, we duplicate retrieval.

That increases:

- execution time;
- context size;
- tool calls;
- complexity.

For the POC I want ONE authoritative SEC retrieval path.

My preference is:

Stylus SEC Filings integration = authoritative filing retrieval.

Python backend = orchestration + validation + persistence.

Please tell me whether you agree.

If so, the backend should NOT fail preflight simply because local Python cannot reach data.sec.gov.

Instead:

- verify company identity;
- invoke Stylus;
- require genuine SEC Filings tool activity/result where applicable;
- validate the returned provenance;
- reject fabricated SEC claims;
- continue to scoring/UI.

Is that the appropriate architecture?

============================================================
13. DESIRED MINIMAL POC ARCHITECTURE
============================================================

My preferred architecture is:

CONFIRMED STEP 2.1
+
CONFIRMED STEP 2.2 COMPANY
+
5 CONFIRMED STEP 2.3 FACTORS
+
5 CONFIRMED STEP 2.4 FACTORS
        ↓
small JSON payload
        ↓
Runner
        ↓
existing Stylus Step 2.5 preset
        ↓
SEC Filings integration
+
Web Search integration
        ↓
Claude Sonnet assessment
        ↓
schema-conformant JSON
        ↓
Runner final response
        ↓
Python validation
        ↓
Step 2.5 score/UI
        ↓
Step 3 portfolio aggregation

NOT:

Python
→ direct sec.gov requirement
→ network blocked
→ fail
→ retry
→ timeout
→ restart
→ repeat.

============================================================
14. WHAT I NEED FROM YOU
============================================================

Please act as the Stylus platform/integration expert and give me a concrete recommendation.

Do NOT give me generic architecture advice.

Do NOT recommend productionization.

Do NOT recommend MCP.

Do NOT recommend a redesign.

Do NOT tell me merely to “check networking.”

I want you to determine the smallest supported POC solution using capabilities already available in Stylus.

Please answer in this exact structure:

A. RECOMMENDED POC ARCHITECTURE

Show the exact call flow.

B. SEC FILINGS

Explain who should retrieve the filing:
Python or Stylus.

Explain exactly how the model receives SEC evidence.

Explain what evidence/provenance fields Runner exposes and what our backend should validate.

C. PRESET INVOCATION

Saved preset vs inline preset.

Give the recommended option.

If saved preset is supported, explain how to obtain/use its identifier.

D. RUNNER REQUEST

Describe the minimum request payload required.

Do NOT ask us to send unnecessary portfolio data.

E. RUNNER SSE RESPONSE

List the exact event types/state transitions we should expect.

Explain exactly how to identify the genuine final output.

F. ARTIFACT HANDLING

Explain whether the structured JSON artifact is available through Runner and how we retrieve it.

G. AUTHENTICATION

Give the simplest supported POC authentication procedure.

Explain token acquisition, expiration and refresh/re-authentication.

H. TIMEOUT

Given that the exact preset finishes manually in approximately 2 minutes, recommend reasonable:
- connection timeout;
- total execution timeout;
- final-response grace period.

I. WHAT TO REMOVE FROM OUR CURRENT IMPLEMENTATION

Identify only the things that should be removed/bypassed because they conflict with the proper Stylus POC integration.

For example, whether local Python SEC preflight should be removed from the Stylus path.

J. WHAT NOT TO CHANGE

Identify the working pieces we should keep:
- Step 2.1–2.4 confirmation;
- 5 ED factors;
- 5 SI factors;
- single-company selection;
- compact payload;
- Step 2.5 methodology;
- output JSON/schema;
- Step 3 downstream aggregation.

K. EXACT POC IMPLEMENTATION SEQUENCE

Give us a short numbered implementation sequence that a Python developer can follow.

L. ACCEPTANCE TEST

Define ONE controlled end-to-end test for one company.

The test succeeds only if:

1. exactly one company is sent;
2. the correct company identity is used;
3. 5 real confirmed ED factors are supplied;
4. 5 real confirmed SI factors are supplied;
5. SEC Filings integration genuinely executes;
6. real SEC evidence is returned;
7. Web Search executes only as needed;
8. the final model response is received;
9. schema-conformant JSON is obtained;
10. evidence provenance is validated;
11. ED score is populated;
12. SI score is populated;
13. composite score is populated;
14. residual rating is populated;
15. credit-impact rating is populated;
16. the Step 2.5 job completes;
17. the output can be consumed by Step 3.

If any of these are NOT possible through the current Stylus/Runner POC interface, say exactly which one and why.

Most importantly:

Please tell me whether we can solve this using the existing Stylus preset + SEC Filings + Web Search + Runner without relying on direct Python access to data.sec.gov.

I want a POC solution, not a production solution.
