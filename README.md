RPR POC — STRICT FINAL END-TO-END IMPLEMENTATION
STEP 2.4 → STEP 2.5 REAL SEC + WEB → STEP 3

THIS SUPERSEDES THE PREVIOUS LIVE-ACCEPTANCE PROMPT.

You have now identified the actual Step 2.5 SEC problem.

Your own finding was:

- cik_resolver.py performs real SEC issuer resolution.
- sec_filings.py performs deterministic real SEC filing selection.
- evidence validation correctly rejects unverifiable/fabricated SEC
  citations.
- the existing hybrid path has previously produced validated real SEC
  evidence.
- BUT the currently-active Stylus path does NOT wire sec_filings.py
  into stylus_engine.py.
- Stylus therefore asks the model to discover / describe SEC evidence
  and self-report accession numbers/URLs.
- the model frequently fails to emit a parseable real EDGAR accession,
  so the evidence validator correctly removes the unsupported evidence.

THAT IS THE PRIMARY BLOCKER.

DO NOT merely report this again.

IMPLEMENT THE FIX.

============================================================
0. EXECUTION RULE
============================================================

Proceed autonomously through the complete approved scope.

DO NOT stop after:
- wiring SEC,
- one successful issuer,
- Step 2.5,
- static tests,
- API tests,
- Step 3 code changes.

Continue until the complete real workflow works:

Step 2.2
→ Step 2.3
→ Step 2.4
→ issuer preflight
→ deterministic SEC evidence
→ Stylus SEC + Web
→ validated Step 2.5
→ confirmed Step 2.5
→ populated Step 3
→ confirmed Step 3.

Do not ask for permission between phases.

Do not write interim reports.

Do not perform broad architectural refactoring.

This is a POC.

Use the existing code and make the smallest working changes.

============================================================
1. ABSOLUTE NO-FABRICATION RULE
============================================================

NO fabricated:

- CIK
- ticker
- CUSIP
- ISIN
- accession number
- filing URL
- SEC form
- filing date
- financial value
- exposure
- rating
- risk classification
- assessment score
- evidence source.

If data cannot be verified:

N/A
INSUFFICIENT EVIDENCE
NOT ASSESSED

must be used.

Technical failure is NEVER credit deterioration.

SEC FAILURE ≠ SUBSTANDARD.
WEB FAILURE ≠ HIGH IMPACT.
RUNNER FAILURE ≠ DOWNGRADE.
MISSING DATA ≠ BAD CREDIT.

============================================================
2. DO NOT CHANGE THE STYLUS PRESET FROM VS CODE
============================================================

IMPORTANT ARCHITECTURAL BOUNDARY:

The VS Code coding agent does NOT edit, recreate, configure or manage
the Stylus preset in the Stylus UI.

Do NOT:
- create a preset,
- alter preset knowledge,
- change preset UI fields,
- change preset UUIDs,
- configure Runner manually.

The user owns preset configuration manually.

Your code must work with the existing preset/Runner integration.

If a preset prompt adjustment is required for grounded SEC evidence,
implement the backend payload first and explicitly state the minimum
manual preset prompt change required at the very end.

Do NOT stop implementation waiting for the preset modification unless
the current preset literally cannot consume the supplied input.

============================================================
3. REQUIRED TARGET ARCHITECTURE
============================================================

Replace the current weak evidence chain:

company
→ Stylus
→ model searches SEC
→ model narrates filing
→ model self-reports accession
→ validator rejects citation

with:

Step 2.2 company
        ↓
canonical issuer resolution
        ↓
CIK resolution
        ↓
sec_filings.py
        ↓
REAL deterministic SEC filing package
        ↓
stylus_engine.py
        ↓
Stylus receives VERIFIED SEC evidence as grounding context
        +
Web tool for supplemental public evidence
        ↓
model assessment
        ↓
evidence validator
        ↓
normalized Step 2.5 result
        ↓
Step 3.

The deterministic backend must own SEC provenance.

The model must NOT be the authority for SEC provenance.

============================================================
4. REUSE sec_filings.py — DO NOT REBUILD SEC RETRIEVAL
============================================================

There is already:

sec_filings.py

which you identified as:

- deterministic,
- real,
- SEC metadata based,
- capable of selecting real filings,
- unit tested,
- already used in another existing path.

REUSE IT.

Do NOT build a parallel SEC crawler.

Do NOT create another SEC abstraction.

Do NOT rely on LLM web search to identify filings when deterministic
SEC metadata already exists.

Inspect the existing interface and reuse it with the smallest adapter
necessary.

============================================================
5. WIRE sec_filings.py INTO stylus_engine.py
============================================================

This is the critical implementation.

Before invoking Stylus for a Step 2.5 company:

1. resolve canonical company identity;

2. obtain/confirm CIK;

3. invoke the existing deterministic filing-selection logic;

4. obtain the appropriate real filing(s);

5. construct an evidence package;

6. inject that package into the context passed to Stylus.

Do this in the existing Stylus execution path.

Do not redirect Step 2.5 to the old hybrid engine merely because hybrid
once worked.

The approved POC path remains Stylus.

Reuse the good SEC component from the hybrid/orchestrated path inside
the Stylus path.

============================================================
6. SEC FILING PACKAGE
============================================================

Build a compact structured grounding package from existing real SEC
data.

Conceptually it should contain fields equivalent to:

issuer_name
ticker
cik

filing_id
form
filing_date
accession_number
filing_url

source = SEC_EDGAR

selected_sections / extracted_content
or
filing_text excerpts/content

The exact field names should follow existing repository structures.

DO NOT unnecessarily introduce a new schema if an existing SEC evidence
model already exists.

Prefer existing models.

Every filing/evidence item should have an internal deterministic
evidence ID such as:

SEC_1
SEC_2

or the repository's existing identifier.

============================================================
7. ACTUAL FILING CONTENT MUST REACH THE MODEL
============================================================

Do NOT pass only:

“10-K found.”

Stylus must receive useful verified filing content sufficient to assess
the issuer.

Inspect the existing sec_filings.py / orchestration implementation and
determine how filing text or relevant filing sections are already
retrieved.

Reuse the existing implementation.

The model needs enough real evidence for credit assessment such as
where available:

- debt
- liquidity
- interest expense
- cash flow
- revenue
- business risks
- maturity/refinancing information
- financial condition
- risk factors

depending on the filing.

Do NOT dump an enormous raw filing into the prompt unnecessarily.

Use the existing relevant extraction strategy if one already exists.

============================================================
8. SEC AS-OF DATE
============================================================

Respect the selected Step 2.5 assessment as-of date.

Select an appropriate filing available ON OR BEFORE that date.

Do not use future information.

Possible forms include:

10-K
10-Q
8-K
20-F
6-K

as appropriate to the issuer.

Reuse the existing filing-selection rules in sec_filings.py.

============================================================
9. SEC PROVENANCE MUST BE DETERMINISTIC
============================================================

The model does NOT need to manufacture:

accession number
EDGAR URL
form
filing date.

These are already supplied in the SEC evidence package.

When the model refers to SEC evidence, require it to reference the
provided evidence ID.

Example concept:

evidence_ids: ["SEC_1"]

NOT:

“I found this filing at some SEC URL…”

The backend then maps:

SEC_1
→ known accession
→ known form
→ known filing date
→ known EDGAR URL.

============================================================
10. EVIDENCE VALIDATION
============================================================

KEEP the existing strict evidence validator.

Do NOT weaken validation to make Stylus output pass.

Do NOT accept model-created URLs.

Do NOT accept malformed accession numbers.

Instead make Stylus produce evidence references that the validator can
prove.

Preferred validation:

Model returns:
SEC_1

Backend already knows:
SEC_1 =
real verified SEC filing.

Therefore SEC evidence passes deterministically.

For web evidence:

retain existing approved URL/source validation.

============================================================
11. DO NOT TRUST FREE-FORM CITATIONS
============================================================

If Stylus includes prose such as:

“According to the company's 10-K…”

that text alone is NOT provenance.

The assessment must link that claim to a valid supplied SEC evidence ID.

If the model outputs unsupported SEC claims:

remove/reject those claims according to existing validation logic.

Do not invent provenance after generation.

============================================================
12. WEB EVIDENCE
============================================================

The current SEC + Web path may continue to use the approved Web
capability.

Web serves a different purpose.

SEC:
deterministic first-party filing evidence supplied by backend.

WEB:
supplemental current/public evidence discovered through approved
enterprise web search.

Do not use Web as a replacement for deterministic SEC filing retrieval
for SEC issuers.

Keep provenance separated internally:

SEC_*
WEB_*

or the existing equivalent.

============================================================
13. STEP 2.2 COMPANY UNIVERSE
============================================================

Use the confirmed Step 2.2 sector population.

Current POC sector:

Software.

Do not assess the global ~226-name population.

The screenshots show the Software portfolio contains a much smaller
confirmed sector population.

Use that sector-scoped population only.

============================================================
14. USE IDENTIFIERS NOW AVAILABLE IN STEP 2.2
============================================================

Step 2.2 contains useful identifiers for some companies such as:

CUSIP
ISIN
SEDOL
RIC
company name
country
internal company ID / CAGID

and potentially ticker.

Use them to improve issuer resolution.

But NEVER confuse:

CUSIP
ISIN
SEDOL
RIC

with CIK.

They are identity anchors.

Use the existing resolver to map the intended issuer to the correct SEC
identity.

============================================================
15. PRE-FLIGHT BEFORE EXPENSIVE STYLUS EXECUTION
============================================================

Do not repeat the previous 40-minute failure pattern.

Before invoking Stylus, preflight candidate companies.

For each candidate:

A. confirm it belongs to the confirmed Software Step 2.2 population;

B. canonicalize identity;

C. resolve ticker if possible;

D. resolve CIK;

E. call deterministic SEC filing selector;

F. confirm suitable filing exists;

G. confirm accession number is real;

H. confirm SEC URL/metadata is valid.

Only then is the candidate eligible for Step 2.5 execution.

============================================================
16. TARGET EXACTLY 10 SUCCESSFUL POC COMPANIES
============================================================

For the acceptance run select:

10 companies

from the confirmed Software population.

Do not hard-code arbitrary famous companies.

Use deterministic preflight quality.

Prefer candidates with:

strong identifier coverage
+
successful CIK resolution
+
real SEC filing availability.

Continue through candidates until 10 companies pass preflight.

Do NOT count failed/unresolved names in the 10.

============================================================
17. ISSUER PREFLIGHT OUTPUT
============================================================

For each accepted company the backend must know before Stylus runs:

canonical_company_name
ticker
CIK
filing form
filing date
accession number
SEC evidence ID.

This does not all have to clutter the user-facing table.

It must exist internally for evidence provenance.

============================================================
18. STEP 2.4 MUST REMAIN EXACTLY 5 FACTORS
============================================================

Before Step 2.5 execution verify confirmed Step 2.4 contains:

RF1
RF2
RF3
RF4
RF5

exactly 5.

Total weight:

100.0%.

Do not use stale 4-factor state.

Use the actual confirmed five-factor object produced by the live Step
2.4 workflow.

Step 2.5 must consume those exact factors.

============================================================
19. STEP 2.5 MODEL CONTEXT
============================================================

For each issuer, Stylus must receive a complete assessment context.

It should contain:

COMPANY IDENTITY
- canonical name
- ticker
- CIK
- country
- sector

SCENARIO
- confirmed Step 2.1 scenario/assumptions

EVENT-DRIVEN FRAMEWORK
- confirmed Step 2.3 five RFs

SECTOR-INHERENT FRAMEWORK
- confirmed Step 2.4 five RFs

SEC GROUNDING
- deterministic verified filing evidence package

WEB CAPABILITY
- supplemental approved web evidence

AS-OF DATE
- selected assessment date.

Do not make Stylus rediscover upstream workflow state.

Pass it explicitly.

============================================================
20. STEP 2.5 BUSINESS PURPOSE
============================================================

For each issuer determine:

How this specific issuer behaves under the confirmed scenario,
considering BOTH:

Step 2.3 event-driven vulnerabilities

and

Step 2.4 sector-inherent vulnerabilities.

The assessment must remain issuer-specific.

Do not simply repeat sector commentary.

============================================================
21. CREDIT ASSESSMENT MUST BE EVIDENCE-DRIVEN
============================================================

A score/classification may only come from:

real evidence
+
approved RF framework
+
existing scoring methodology.

No evidence:
no score where a score cannot be justified.

Do not infer missing financial metrics.

Use:

N/A

when unavailable.

============================================================
22. DO NOT CHANGE APPROVED SCORING FORMULA
============================================================

Inspect v31/current approved Step 2.5 scoring logic.

Reuse it.

Do not invent another composite score methodology.

Step 2.3 and Step 2.4 scores must feed the existing approved name-level
calculation.

============================================================
23. STRICT OUTPUT NORMALIZATION
============================================================

Before rendering an assessment:

parse
validate
normalize.

Business cells must contain clean values.

Never display:

raw JSON
Markdown fences
tool events
SSE payloads
Python exceptions
backend warnings
prompt text
long technical errors.

If output schema is invalid:

mark the run technical failure and retry/fallback according to existing
bounded logic.

Do not convert it into credit output.

============================================================
24. TECHNICAL FAILURE ≠ CREDIT ASSESSMENT
============================================================

This rule is non-negotiable.

If one issuer's assessment fails technically:

do NOT publish:

Substandard
Continue Review
Low Impact
High Impact
rating downgrade
composite risk score

as a consequence of the failure.

Use:

NOT ASSESSED / TECHNICAL FAILURE

internally.

For the final 10-company POC acceptance cohort, replace the failed
candidate with another successfully preflighted Software company.

============================================================
25. RUNNER BOUNDED COMPLETION
============================================================

Preserve the bounded SSE completion fix.

Expected sequence:

Runner stream opens
→ tools execute
→ SEC/Web tool events occur
→ assistant content accumulates
→ wait bounded grace period
→ genuine final model response received
→ parse
→ validate
→ return.

Do not wait indefinitely.

Do not synthesize a final model assessment yourself.

============================================================
26. STEP 2.5 UI
============================================================

Use actual v31 Step 2.5 as the visual source of truth.

The final POC screen must show only the 10 assessment cohort companies.

Do NOT display the old 226-name global table.

Do not make the table an enormous raw-data browser.

Replicate v31:

- header framing
- column proportions
- row height
- dark headers
- filter row
- score badges
- impact rating badges
- horizontal scrolling
- compact readable rows
- company identity presentation
- action buttons.

Long rationale belongs in the existing detail/expanded mechanism, not
inside a narrow giant cell.

============================================================
27. HIDE DEBUG NOISE IN NORMAL DEMO MODE
============================================================

Preserve technical diagnostics for development.

But normal Step 2.5 demo mode must not be dominated by:

Local PoC Readiness
auth flags
SEC readiness strings
internal error dumps
environment variables.

Collapse/hide them behind the existing diagnostic pattern.

Do not delete useful diagnostics.

============================================================
28. CONFIRM STEP 2.5 ONLY AFTER VALID RESULTS
============================================================

Confirmation should require the actual valid assessed cohort.

For this acceptance run:

10/10 successful assessments required.

When confirmed:

persist the exact assessment results.

Step 3 must read that confirmed object.

============================================================
29. STEP 3 — NO STATIC DEMO DATA
============================================================

Step 3 must be generated from the current live confirmed results.

Do NOT copy the v31 example values such as:

Salesforce
SAP
Autodesk
Open Text

unless those companies genuinely happen to be part of this live
10-company cohort.

V31 provides the DESIGN and approved methodology.

It is not a data source.

============================================================
30. STEP 3 DATA LINEAGE
============================================================

Step 3 inputs:

confirmed Step 2.2 portfolio/exposures
+
confirmed Step 2.3 event RFs
+
confirmed Step 2.4 sector RFs
+
confirmed Step 2.5 assessment results.

Trace this explicitly.

The current state must not show:

“No confirmed Step 2.4 sector yet”

once Step 2.4 has been confirmed in the same served application
session.

============================================================
31. STEP 3 ASSESSMENT COHORT
============================================================

For the POC acceptance run, Step 3 must clearly operate on the confirmed
10-company assessment cohort.

Do not mix:

10 assessed companies

with

226 global companies.

If Step 2.2 contains exposure for a larger sector population but only
10 were assessed, explicitly keep:

assessed population
and
portfolio population

conceptually distinct.

For this demonstration, aggregate the confirmed assessment cohort
unless existing approved v31 logic explicitly requires another scope.

No misleading denominator.

============================================================
32. STEP 3 EXPOSURE
============================================================

Reuse real Step 2.2 exposure fields where present.

Do not fabricate:

OSUC
limit
IG exposure
NIG exposure
criticized exposure
classified exposure.

If exposure is unavailable:

N/A.

If the underlying real data genuinely supports 0:

0 is valid.

Do not replace missing values with 0 just to populate cards.

============================================================
33. STEP 3 CLASSIFICATION RULES
============================================================

Reuse the existing approved v31/current classification mappings.

Examples conceptually include:

IG
NIG
Criticized
Classified.

Do not invent a new classification taxonomy.

Make sure classification comes from valid name-level results and/or
real portfolio fields, not technical execution state.

============================================================
34. STEP 3 WEIGHTED COMPOSITE
============================================================

Reuse the existing v31/current approved calculation.

If exposure weights exist:
use actual exposure.

Do not invent exposure just to calculate a weighted score.

The final number must be mathematically traceable.

============================================================
35. STEP 3 CREDIT INTELLIGENCE
============================================================

Populate the portfolio commentary using actual current outputs.

It should explain:

- confirmed scenario;
- Software sector exposure;
- assessed company distribution;
- dominant Step 2.3 event-driven risks;
- dominant Step 2.4 structural risks;
- largest name-level contributors;
- major mitigants/buffers;
- overall composite result;
- impact conclusion.

No unsupported metrics.

No static v31 narrative.

============================================================
36. STEP 3 V31 DESIGN
============================================================

Replicate the real v31 Step 3 DOM/CSS.

Required information architecture includes:

Sector strip

Portfolio Assessment Outcome

Portfolio Exposure Summary

5 KPI cards:
- Total
- IG
- NIG
- Criticized
- Classified

Exposure Segmentation

Weighted Composite Score

Impact Rating

Companies Included

Credit Assessment / Credit Intelligence

Export Report

Confirm Portfolio Assessment

Feedback

Workflow Status.

Match:

dimensions
spacing
table layout
header colors
border treatment
card geometry
font hierarchy
badges
density.

Do not leave the simplified empty Step 3 currently shown.

============================================================
37. LIVE APPLICATION TEST ONLY
============================================================

Do not use direct:

file://.../step23.html

for functional acceptance.

Reference v31 can be opened through file://.

The current application must be tested from its actual served runtime,
using the same workflow/session.

Start the current backend/frontend with the existing Windows project
startup method.

Do not create another server architecture.

============================================================
38. TEST IN THIS EXACT ORDER
============================================================

1. Start real application.

2. Confirm Step 2.2 Software population.

3. Verify Step 2.3 = 5 confirmed event-driven RFs.

4. Run/verify Step 2.4:
   - 5 RFs
   - 100%
   - complete schema
   - confirm.

5. Verify Step 2.4 confirmation persists.

6. Enter Step 2.5 in SAME session.

7. Preflight Software population.

8. Produce 10 verified issuers.

9. For each verify:
   company
   ticker
   CIK
   filing
   accession
   SEC URL.

10. Run real Stylus SEC + Web assessment.

11. Verify real deterministic SEC evidence reaches Stylus.

12. Verify model references supplied evidence IDs.

13. Verify evidence validator accepts them.

14. Obtain 10 successful clean assessments.

15. Compare Step 2.5 live UI against v31.

16. Confirm Step 2.5.

17. Open Step 3 in SAME session.

18. Verify real Step 2.5 results appear automatically.

19. Verify real exposure calculations.

20. Verify aggregation.

21. Verify commentary.

22. Compare Step 3 against v31.

23. Confirm Step 3.

============================================================
39. PROVE THAT THE SEC FIX ACTUALLY WORKS
============================================================

For at least each of the 10 assessment cohort issuers, record internally:

Company
Ticker
CIK
SEC form
Filing date
Accession number
EDGAR URL
Evidence ID used by model.

The final validation must demonstrate that the model assessment's SEC
evidence maps to these deterministic records.

It is NOT enough for the model to mention:

“10-K”
or
“SEC filing.”

============================================================
40. DO NOT WEAKEN HONESTY CHECKS
============================================================

The current backend correctly drops unverifiable model citations.

KEEP THAT.

The solution is not:

make validator less strict.

The solution is:

provide verified evidence BEFORE generation so the model can cite it.

============================================================
41. PRESET INPUT COMPATIBILITY
============================================================

Before modifying code assumptions, inspect exactly how the current
Stylus preset input is serialized.

If the preset currently accepts one large text/context input:

DO NOT require new preset input fields.

Serialize the complete grounded context into that existing input.

That context can contain:

company
scenario
RFs
SEC evidence bundle
instructions.

This is preferred because it minimizes manual preset changes.

Only require a new preset field if the current preset technically cannot
receive the required grounding context.

============================================================
42. IF PRESET PROMPT CURRENTLY TELLS MODEL TO DISCOVER SEC ITSELF
============================================================

Backend implementation must still be completed.

Then identify the MINIMUM manual prompt change needed.

Do not change the preset yourself.

The desired prompt semantics are:

- provided SEC evidence is authoritative;
- never invent SEC citations;
- cite supplied SEC evidence IDs;
- use web search only as supplemental evidence;
- if evidence is absent, say unavailable;
- never infer missing financial values;
- output only the required assessment structure.

The user will make this preset edit manually if needed.

============================================================
43. REGRESSION
============================================================

Do not break:

Step 1
Step 2.1
Step 2.2
Step 2.3
Step 2.4
feedback panels
navigation
workflow sidebar
legacy/hybrid paths.

Do not replace old hybrid/orchestrated modes.

Only enhance the active Stylus path to reuse the proven deterministic
SEC component.

============================================================
44. COMPLETION GATE
============================================================

DO NOT RESPOND UNTIL ALL SOLVABLE CONDITIONS PASS.

STEP 2.4
[ ] 5 RFs live
[ ] 100% weight
[ ] full v31 content
[ ] v31 layout
[ ] confirmed
[ ] persisted downstream

SEC GROUNDING
[ ] sec_filings.py wired into Stylus path
[ ] canonical issuer resolution
[ ] deterministic CIK
[ ] deterministic filing
[ ] real accession
[ ] real filing URL
[ ] real filing content/context
[ ] evidence IDs provided to model
[ ] validator verifies model references
[ ] validator NOT weakened

STEP 2.5
[ ] sector-scoped population
[ ] exactly 10 successful POC issuers
[ ] all preflighted
[ ] all real SEC evidence
[ ] Web supplemental evidence functioning
[ ] Stylus Runner works
[ ] bounded completion works
[ ] no fabricated data
[ ] clean normalized table
[ ] v31 layout
[ ] confirmed
[ ] persisted

STEP 3
[ ] receives confirmed Step 2.5
[ ] receives Step 2.2 exposure
[ ] no blank state
[ ] no static v31 data
[ ] real segmentation
[ ] real composite
[ ] real impact result
[ ] real companies included
[ ] real commentary
[ ] v31 design
[ ] confirmed

END TO END
[ ] same served application/session
[ ] real data
[ ] no fabrication
[ ] no raw technical garbage in business output
[ ] no unresolved solvable blocker.

============================================================
45. FINAL RESPONSE ONLY AFTER TESTING
============================================================

Once the complete live flow has actually run, respond only with:

END-TO-END: PASS / FAIL

SEC GROUNDING INTO STYLUS: PASS / FAIL
STEP 2.4: PASS / FAIL
STEP 2.5 SEC+WEB: PASS / FAIL
STEP 3: PASS / FAIL

TEN ASSESSED ISSUERS:

Company | Ticker | CIK | Form | Filing Date | Accession

For each issuer also confirm:
SEC evidence validated: YES/NO

STEP 2.4 RF1–RF5:
names

STEP 3:
Assessed companies
Total exposure
IG
NIG
Criticized
Classified
Weighted composite
Impact rating

V31 2.4:
PASS / FAIL

V31 2.5:
PASS / FAIL

V31 STEP 3:
PASS / FAIL

FILES CHANGED:
exact paths only

PRESET MANUAL CHANGE REQUIRED:
YES / NO

If YES:
give ONLY the exact minimal manual change required.

REMAINING BLOCKER:
NONE

or exact genuine external blocker.

DO NOT CALL STATIC SOURCE INSPECTION A PASS.
DO NOT CALL UNIT TESTS AN END-TO-END PASS.
DO NOT STOP AFTER ONE COMPANY.

IMPLEMENT THE SEC GROUNDING FIX AND COMPLETE THE REAL WORKFLOW NOW.
