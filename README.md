MASTER END-TO-END RPR POC FIX
STEP 2.4 + STEP 2.5 + STEP 3
V31 EXACT DESIGN + REAL DATA + SEC/WEB + CORRECT WORKFLOW LINEAGE

This supersedes the previous Step 2.4 acceptance prompt.

DO NOT execute the previous prompt separately.

You are now responsible for completing the remaining RPR POC from the
confirmed Step 2.2/2.3 state through:

STEP 2.4 — Sector-Inherent Risk Factors
STEP 2.5 — Name-Level Assessment
STEP 3   — Portfolio-Level Assessment

This is one continuous end-to-end implementation and acceptance task.

DO NOT stop after Step 2.4.
DO NOT stop after Step 2.5.
DO NOT write interim implementation reports.
DO NOT ask for approval between phases.
DO NOT present an audit and wait.
DO NOT merely describe what should be done.

Inspect → implement → run → debug → correct → rerun → visually compare
→ complete the full workflow.

Only stop before completion for a genuine EXTERNAL blocker that cannot
be solved from the repository/environment.

==============================================================
0. ABSOLUTE PROJECT RULES
==============================================================

This is a POC.

The objective is a real, accurate, demonstrable end-to-end result.

Do NOT introduce:
- production architecture,
- unnecessary frameworks,
- generic abstraction layers,
- broad refactoring,
- repository restructuring,
- new design systems,
- new orchestration frameworks,
- speculative future-proofing.

Preserve all known-working implementation.

Use the smallest changes necessary.

Do not damage:
- Step 1
- Step 2.1
- Step 2.2
- Step 2.3
- current Runner integration
- existing feedback controls
- workflow state
- right-side system/workflow panel
- working APIs

V31 is the immutable VISUAL reference.

Existing correct business functionality is the immutable FUNCTIONAL
reference.

The required final result is:

V31 PRESENTATION
+
CORRECT CURRENT BUSINESS LOGIC
+
REAL EVIDENCE
+
END-TO-END WORKFLOW.

==============================================================
1. STYLUS RULE — VERY IMPORTANT
==============================================================

The VS Code coding agent DOES NOT edit or configure Stylus presets.

The user manually owns Stylus preset configuration.

DO NOT:
- recreate the SEC + Web preset,
- edit its prompt,
- change its knowledge,
- change its input fields in Stylus,
- create a new preset,
- investigate preset UUID configuration again.

Use the currently configured working Stylus/Runner path from the
existing code.

If backend code invokes the preset inline through Runner, preserve that
working approach.

Your responsibility is:

application state
→ issuer identity
→ correct preset inputs
→ Runner invocation
→ bounded SSE completion
→ parse real response
→ validate response
→ render it correctly.

==============================================================
2. FIRST UNDERSTAND THE BUSINESS CHAIN
==============================================================

The workflow has distinct analytical stages:

STEP 1
Risk Narrative
       ↓
STEP 2.1
Scenario / Assumptions
       ↓
STEP 2.2
Portfolio + Sector + Company Selection
       ↓
STEP 2.3
EVENT-DRIVEN Risk Factors
       ↓
STEP 2.4
SECTOR-INHERENT Risk Factors
       ↓
STEP 2.5
NAME-LEVEL Assessment
       ↓
STEP 3
PORTFOLIO Assessment


DO NOT mix these responsibilities.

STEP 2.3 answers:

“What credit transmission channels arise because of THIS event or
scenario?”

STEP 2.4 answers:

“What structural credit vulnerabilities exist because this borrower
belongs to THIS sector?”

STEP 2.5 answers:

“How does THIS particular issuer behave against BOTH frameworks, using
real issuer evidence?”

STEP 3 answers:

“What does the assessed issuer population imply for portfolio risk,
exposure segmentation, concentrations and portfolio-level credit
judgment?”

==============================================================
3. CURRENT ACCEPTANCE TEST CONTEXT
==============================================================

Use the currently confirmed Software workflow as the acceptance case.

The screenshots/current state show:

Sector = Software

Step 2.2 Software population = approximately 42 companies.

Step 2.3 = already confirmed with 5 event-driven factors.

The current Step 2.5 displaying ~226 entities is therefore incorrect.

DO NOT assess the entire 226-name broader portfolio.

The test cohort MUST originate from the confirmed Step 2.2 Software
population.

==============================================================
4. FIX DATA LINEAGE BEFORE DOING ANY UI PATCHING
==============================================================

Trace actual runtime state.

Identify:

confirmed Step 2.2 sector
confirmed Step 2.2 company list
confirmed Step 2.3 RFs
confirmed Step 2.4 RFs
Step 2.5 company source
Step 3 source

Prove where the 226 companies currently shown in Step 2.5 originate.

Fix it.

For this acceptance run:

STEP 2.2 SOFTWARE COMPANIES
            ↓
10 ELIGIBLE PUBLIC ISSUERS
            ↓
STEP 2.5

Step 2.5 must NOT silently switch back to the whole portfolio.

==============================================================
5. POC ASSESSMENT COHORT = EXACTLY 10 COMPANIES
==============================================================

For this POC acceptance test, assess exactly TEN companies.

Do not start by manually hard-coding ten arbitrary names.

Build the cohort deterministically from the confirmed Step 2.2 Software
rows.

Rank candidates by issuer-identity quality.

Preferred evidence hierarchy:

1. existing explicit CIK, if any
2. reliable ticker
3. RIC from which a canonical ticker can be safely derived
4. US ISIN + CUSIP
5. other reliable identifier combination
6. company-name resolution only as last resort

Also use:
- company name,
- country,
- CAGID/internal company ID,
- sector,
- CUSIP,
- ISIN,
- SEDOL,
- RIC,
- any existing ticker fields

where available.

DO NOT mistake:

CUSIP
ISIN
SEDOL
RIC

for an SEC CIK.

They are identity anchors.

They must be resolved to a canonical public issuer and ultimately the
correct SEC identity where required.

==============================================================
6. PRE-FLIGHT THE 10 COMPANIES BEFORE RUNNING THE LLM
==============================================================

Do NOT start ten expensive assessments blindly.

First create a lightweight issuer-resolution preflight.

For each Step 2.2 Software candidate:

A. canonicalize the company name

B. inspect available identifiers

C. resolve ticker where possible

D. use the existing CikResolver / existing approved SEC identity path

E. resolve CIK

F. verify the CIK actually corresponds to the intended issuer

G. verify at least one suitable SEC filing exists before the assessment
   as-of date

Only after successful identity + filing verification may the company
enter the 10-company assessment cohort.

Continue through the Software population until TEN companies have
passed preflight.

This solves the current situation where the application is attempting
a name such as an LLC with:

“TICKER/ID — Not supplied by Step 2.2 portfolio source”

and then expecting SEC evidence to magically resolve.

==============================================================
7. SEC FORMS / EVIDENCE
==============================================================

Use the latest appropriate filing available on or before the selected
assessment as-of date.

Possible forms include, as appropriate:

10-K
10-Q
8-K
20-F
6-K

Do not force every issuer into the same filing type.

The evidence package should retain useful provenance such as:

canonical issuer
ticker
CIK
form type
filing date
accession / filing identifier
source type

Do not expose huge raw SEC payloads in the UI.

==============================================================
8. SEC IDENTITY SAFETY
==============================================================

Never attach a filing to a company merely because names look similar.

Identity verification should consider combinations of:

company name
ticker
CIK
CUSIP
ISIN
RIC
country

when available.

Avoid false matches.

A false SEC filing attached to the wrong borrower is worse than an
explicit missing-data result.

==============================================================
9. IF A PRE-FLIGHT CANDIDATE FAILS
==============================================================

Do NOT kill the whole assessment.

Do NOT wait forty minutes.

Do NOT include the failed candidate in the final 10-company cohort.

Move to the next eligible Software company.

Continue until ten verified candidates are available.

Only if the entire confirmed Software population contains fewer than
10 SEC-resolvable/public candidates should this be considered a genuine
external/data blocker.

==============================================================
10. PRESERVE BOUNDED RUNNER COMPLETION
==============================================================

The project previously established the required Runner behaviour:

- Runner stream opens
- SEC/Web tools execute
- assistant output is accumulated
- after tool execution, wait a bounded period for the genuine final
  model response
- do not synthesize a fake final assessment
- do not wait forever

Preserve this.

No single issuer should block the complete POC indefinitely.

A technical timeout must produce a TECHNICAL failure state, never a
credit-risk judgment.

==============================================================
11. STEP 2.4 — EXACTLY FIVE STRUCTURAL FACTORS
==============================================================

The current screenshot shows:

4 factors

with weights:

28.57%
28.57%
28.57%
14.29%

This is NOT accepted.

For the POC target, Step 2.4 must contain exactly:

RF1
RF2
RF3
RF4
RF5

Five sector-inherent factors.

Do not accept 4.

Do not generate 6.

If the current service returns only four factors, use the existing
approved sector-factor generation/refinement mechanism to obtain a
fifth distinct valid structural factor BEFORE allowing Step 2.4 to be
confirmed.

==============================================================
12. STEP 2.4 FACTOR QUALITY
==============================================================

Each Step 2.4 factor must be:

- specific to Software
- structurally persistent
- relevant to credit
- distinct from the other four
- measurable
- suitable for issuer-level downstream assessment

Do not merely rewrite the current scenario.

Step 2.4 is not another event-generation step.

For Software, structural topics may relate to concepts such as:

recurring revenue quality
customer retention
leverage
refinancing
asset/recovery characteristics
technology disruption
business-model economics
free-cash-flow structure
customer concentration
cyclicality

but DO NOT hard-code this example list blindly.

Use the actual approved taxonomy/generation logic.

==============================================================
13. STEP 2.4 WEIGHTING
==============================================================

Five factors must reconcile to:

100.0%

Preserve deterministic importance-weight mapping.

If the five importance values are for example:

HIGH
HIGH
HIGH
MEDIUM
MEDIUM

with scores:

2
2
2
1
1

the normalized result naturally becomes:

25%
25%
25%
12.5%
12.5%

This is the type of deterministic logic reflected in v31.

Use actual approved importance values.

Do not arbitrarily assign weights to imitate screenshots.

==============================================================
14. STEP 2.4 COMPLETE ANALYTICAL SCHEMA
==============================================================

EVERY RF must contain the complete framework:

Factor Narrative

Factor Importance

Importance Justification

Vulnerability Metrics — Set 1

Metric + Formula

Very High / High / Moderate / Low thresholds

Critical Threshold

Buffer Metrics — Set 2

Metric + Formula

Strong / Moderate / Weak / Negligible thresholds

Key Principle

Scoring Logic 1–5

Vulnerability Profile

Buffer Profile

Credit Implication

RF1 cannot be rich while RF2–RF5 are shallow.

All five need the same complete schema.

==============================================================
15. STEP 2.4 VISUAL REQUIREMENT — CURRENT VERSION STILL FAILS
==============================================================

The latest implementation is still visibly different from v31.

Do NOT claim parity because the same sections exist.

Use the ACTUAL v31 HTML/CSS implementation as source of truth.

Do not recreate it by eye from screenshots when source code exists.

Compare DOM and CSS.

Match at component level:

overall content width
right sidebar width
sector strip height
sector dropdown width
factor-count chip
information banner
summary-table frame
summary-table column widths
header heights
row heights
header fills
cell padding
text size
text weight
border colour
border thickness
accordion spacing
accordion header height
number-circle dimensions
importance badge
chevron
narrative box
importance controls
green justification strip
metric tables
critical-threshold strip
buffer table
key-principle strip
scoring table
credit-implication box
collapsed RF rows
bottom buttons
feedback panel

Do not use “similar”.

Replicate v31.

==============================================================
16. PARTICULAR STEP 2.4 TABLE REQUIREMENTS
==============================================================

Top table:

RF
Factor
Importance
Imp. Score
Weight

Exactly v31 framing.

Metric tables:

Metric
Formula

must remain visibly separate columns.

Do NOT merge them.

Severity headers must use v31 colour bands.

Scoring table:

Score
Vulnerability Profile
Buffer Profile

Rows:

5
4
3
2
1

Match v31 cell framing, width and control/read-only behaviour.

Determine behaviour from ACTUAL v31 Step 2.4, not from Step 2.3.

==============================================================
17. STEP 2.4 CONFIRMATION
==============================================================

Do not allow confirmation with:

4 factors
invalid weights
incomplete metrics
missing scoring logic

Confirmation requires five valid factors and 100% total weight.

After confirmation, persist the exact Step 2.4 dataset for Step 2.5.

==============================================================
18. STEP 2.5 — DO NOT DISPLAY THE RAW 226-NAME PORTFOLIO
==============================================================

This is one of the biggest current defects.

The v31 Step 2.5 table is an ASSESSMENT OUTCOME.

It is not a raw portfolio-browser table.

For the POC acceptance run:

show only the 10 verified assessed companies.

Do not populate 226 rows.

Do not show unrelated sectors.

Do not mix raw Step 2.2 portfolio inventory with assessment output.

==============================================================
19. STEP 2.5 ASSESSMENT INPUT PER COMPANY
==============================================================

For each of the ten verified issuers, pass the assessment enough context
to understand:

COMPANY:
canonical company identity

SECTOR:
Software

SCENARIO:
confirmed Step 2.1 scenario/assumptions

EVENT-DRIVEN FRAMEWORK:
confirmed five Step 2.3 RFs

SECTOR-INHERENT FRAMEWORK:
confirmed five Step 2.4 RFs

PUBLIC EVIDENCE:
verified SEC filing evidence

WEB EVIDENCE:
approved SEC + Web preset path

AS-OF DATE:
current selected assessment date

The model must assess the actual issuer, not merely the sector.

==============================================================
20. STEP 2.5 EVIDENCE STANDARD
==============================================================

Use real evidence.

Never invent:

revenue
leverage
interest coverage
cash
debt
maturity
customer concentration
growth
retention
ratings
filing values
exposure
financial metrics

If a particular required metric genuinely cannot be obtained:

show N/A / unavailable.

Do not create a plausible-looking number.

==============================================================
21. APPLY BOTH RF SETS
==============================================================

Step 2.5 must not ignore upstream analytical work.

For every company, evaluate:

5 Step 2.3 event-driven factors

AND

5 Step 2.4 sector-inherent factors.

Where the current approved scoring methodology produces separate
event and sector scores, preserve it.

Do not invent a new formula.

Use the scoring/composite methodology already present in v31/current
approved implementation.

==============================================================
22. DO NOT CONVERT TECHNICAL FAILURE INTO CREDIT FAILURE
==============================================================

This is an absolute rule.

The current output shows technical/evidence failure being mixed with
business classifications.

That must stop.

If:

SEC resolution fails
Runner fails
web retrieval fails
response parsing fails
required evidence is missing

then the correct assessment status is something like:

NOT ASSESSED
INSUFFICIENT EVIDENCE
TECHNICAL FAILURE

according to existing UI terminology.

It is NOT automatically:

Substandard
High Risk
Continue Review
Low Impact
Medium Impact
rating downgrade

Technical failure contains ZERO credit information.

Do not assign a credit score from it.

==============================================================
23. NO GARBAGE TEXT IN BUSINESS CELLS
==============================================================

Never put raw backend errors into:

Key Risk Driver
Recommended Class
Credit Commentary
Rating Impact
Score
Business Rationale

Examples of unacceptable cell content:

“SEC registration identity unresolved...”

followed by internal exception details.

Internal diagnostic information belongs in:

system log
or
collapsed technical diagnostics.

The business table must stay business-readable.

==============================================================
24. STEP 2.5 OUTPUT NORMALIZATION
==============================================================

Before a model result enters the table:

validate the response against the expected schema.

Normalize:

numbers
scores
enums
missing values
text length

Reject malformed model fragments.

Never render:

raw JSON
markdown fences
tool traces
SSE events
stack traces
internal prompts
backend exception text

inside the business assessment grid.

==============================================================
25. STEP 2.5 READABILITY
==============================================================

The current table is too wide, too dense and visually chaotic.

Use actual v31 Step 2.5 as the visual specification.

Replicate:

column order
column widths
header height
dark-navy header styling
filter-row height
row height
score badges
rating-impact badges
horizontal scrolling behaviour
vertical scrolling behaviour
text alignment
number formatting
company-name treatment
expand/collapse behaviour if present

The ten-company grid must be readable at normal desktop zoom.

==============================================================
26. LONG TEXT
==============================================================

Do not allow multi-paragraph analysis to make a row hundreds of pixels
high.

Where v31 uses compact content, keep it compact.

Long rationale belongs in an expanded detail region / existing detail
mechanism, not a narrow score table cell.

If there is no existing expanded-detail component, use the smallest
existing v31-compatible pattern rather than inventing a new complex UI.

==============================================================
27. STEP 2.5 IDENTIFIER PRESENTATION
==============================================================

Display canonical issuer identity cleanly.

Where v31 has TICKER / ID, show a useful resolved value.

Do not repeat:

“Not supplied by Step 2.2 portfolio source”

across many rows.

If unavailable, use:

—

or

N/A

according to v31 convention.

==============================================================
28. STEP 2.5 DATA PROVENANCE
==============================================================

The assessment must internally retain enough evidence lineage to answer:

Which issuer?
Which CIK?
Which filing?
Which filing date?
Which evidence supported the score?
Which factors came from Step 2.3?
Which factors came from Step 2.4?

Do not necessarily expose all metadata as columns.

Keep the primary assessment table readable.

==============================================================
29. STEP 2.5 SUCCESS CONDITION
==============================================================

The acceptance cohort is successful only when the application has:

10 selected Software companies

10 verified issuer identities

10 successful assessments

10 valid normalized results

and no technical-failure rows.

If one selected company fails after preflight for an issuer-specific
reason:

use the next eligible preflight candidate and complete the cohort.

==============================================================
30. STEP 2.5 CURRENT LARGE TECHNICAL-DIAGNOSTIC PANEL
==============================================================

The current screen exposes a very large:

“Step 2.5 — Local PoC Readiness”

diagnostics region.

That may be useful during debugging, but it damages the business demo.

Preserve diagnostic capability, but compare to v31.

For normal demo mode it should be:

collapsed
or
hidden behind an existing debug/technical toggle

unless v31 explicitly shows it.

Do not delete useful diagnostics.

Do not allow them to dominate the normal Step 2.5 business screen.

==============================================================
31. LEGACY READINESS FLAGS
==============================================================

The current diagnostics still display items such as:

SEC ACCESS NOT APPROVED
WEB PROVIDER NOT READY

Trace whether these flags are actually blocking the currently intended
Stylus POC path.

The agreed POC architecture previously bypassed legacy SEC/Web readiness
checks for the Stylus Runner mode while leaving legacy routes unchanged.

If these old checks have accidentally re-entered the active Stylus
path, correct the routing using the smallest existing POC-specific fix.

Do NOT globally disable security/readiness checks.

Do NOT alter unrelated legacy modes.

Only ensure the approved existing POC Runner path behaves as intended.

==============================================================
32. DISTINGUISH THREE DIFFERENT FAILURE TYPES
==============================================================

When debugging SEC + Web, determine which one is actually failing:

A. ENVIRONMENT / ROUTE
   Runner/auth/readiness problem

B. IDENTITY
   company cannot be mapped to correct ticker/CIK

C. MODEL COMPLETION
   tools finish but final model response never arrives

Do not treat all three as “SEC failed”.

Trace each layer independently and fix the real cause.

==============================================================
33. STEP 2.5 BUTTON / WORKFLOW BEHAVIOUR
==============================================================

Run assessment should actually initiate the selected 10-company cohort.

While running, show controlled status.

Do not leave indefinite “Running...” if the backend has completed or
failed.

When all ten are valid:

enable confirmation.

Confirm Assessment must persist the ten valid results.

Workflow sidebar then moves Step 2.5 from:

In Progress

to:

Confirmed / Completed.

==============================================================
34. STEP 3 MUST USE REAL STEP 2.5 OUTPUT
==============================================================

Do not hard-code the rich v31 Step 3 demo values.

The current Step 3 is blank because upstream assessment is invalid.

Fix the handoff.

Step 3 input must be:

confirmed Step 2.5 ten-company cohort
+
Step 2.2 actual exposure / portfolio fields
+
Step 2.3 event RFs
+
Step 2.4 sector RFs.

==============================================================
35. STEP 3 SCOPE CONSISTENCY
==============================================================

Do not combine:

10 assessed companies

with:

226-company exposure totals

unless the product explicitly says the aggregation is for the broader
portfolio and has a mathematically valid coverage mechanism.

For this acceptance POC, keep scope internally consistent.

The portfolio-level assessment should clearly reflect the actual
confirmed assessment cohort.

If the design has a concept of “assessed population / portfolio
population”, show it explicitly.

No misleading denominators.

==============================================================
36. STEP 3 EXPOSURE DATA
==============================================================

Use actual Step 2.2 exposure fields where available.

Do not invent:

GSUC
limits
exposure
IG percentage
NIG percentage
criticized percentage
classified percentage
concentration

If a field is unavailable:

N/A

is preferable to fabrication.

However, inspect the Step 2.2 source carefully because many exposure
fields already exist in the data.

Reuse them.

==============================================================
37. STEP 3 BUSINESS PURPOSE
==============================================================

Step 3 should answer:

What is the portfolio-level outcome after the issuer assessments?

It should communicate:

total assessed exposure

risk segmentation

weighted composite risk

impact/rating distribution

largest contributors

concentrations

key event-driven drivers

key sector-inherent drivers

portfolio credit interpretation

and final portfolio assessment.

This is aggregation and interpretation.

It is not another independent LLM analysis disconnected from the ten
company results.

==============================================================
38. STEP 3 WEIGHTED AGGREGATION
==============================================================

Use the existing approved v31/current aggregation methodology.

Do not invent a new score formula.

Where exposure weighting exists, use real exposure.

Where exposure is unavailable, do not silently replace it with an
invented exposure.

Any equal-weight fallback already supported by the POC must be clearly
identified by the existing logic.

==============================================================
39. STEP 3 EXACT V31 DESIGN
==============================================================

The supplied v31 reference is the target.

Replicate actual v31 source code for:

Portfolio Level Assessment heading

sector selector bar

Portfolio Assessment Outcome

Portfolio Exposure Summary

KPI/exposure cards

Exposure Segmentation table

rating/impact colour badges

Credit Assessment / Credit Intelligence section

risk-driver cards

source labels

portfolio commentary

Export Report

Confirm Portfolio Assessment

feedback section

right Workflow Status panel.

Do NOT create a simplified empty five-card page like the current
implementation.

The current blank Step 3 is NOT acceptable.

==============================================================
40. STEP 3 EXPOSURE SUMMARY
==============================================================

Use the v31 framing for cards such as:

Total Exposure

IG Exposure

NIG Exposure

Criticized Exposure

Classified Exposure

but populate them from REAL current data.

If classifications required for a card genuinely do not exist, display
a correct 0 only when the underlying data genuinely supports zero.

Otherwise display N/A.

Do not use v31 demonstration values.

==============================================================
41. STEP 3 EXPOSURE SEGMENTATION TABLE
==============================================================

Recreate v31's actual table structure.

Use the same:

header colours
column order
column widths
row heights
badge treatment
border treatment
spacing
font hierarchy

Populate it with real computed results from the accepted ten-company
cohort.

==============================================================
42. STEP 3 CREDIT ASSESSMENT CARDS
==============================================================

The v31 Step 3 contains dense but readable credit assessment sections.

These must not become generic AI paragraphs.

The cards should reflect actual:

scenario
event-driven RFs
sector RFs
assessed company results
portfolio contributors.

Preserve the existing approved Step 3 structure.

Do not invent unsupported claims.

==============================================================
43. NO STALE DEMO DATA
==============================================================

Before the final test, ensure no old failed Step 2.5 / Step 3 objects
are contaminating the run.

Clear/reset ONLY the appropriate current workflow state using existing
mechanisms.

Do NOT delete unrelated project data.

Do NOT hard-code values from screenshots.

==============================================================
44. V31 IMPLEMENTATION METHOD
==============================================================

For Step 2.4, Step 2.5 and Step 3:

locate actual v31 HTML/CSS/JS.

Do not approximate.

Extract and compare:

DOM hierarchy
classes
CSS rules
dimensions
padding
margin
grid widths
table column widths
font sizes
font weights
border colours
background colours
button geometry
accordion structure
scroll behaviour.

Where possible reuse the actual v31 CSS/classes rather than manually
recreating slightly different copies.

But DO NOT replace current business event handlers or API wiring with
static v31 mock logic.

The final combination is:

v31 DOM/CSS presentation
+
current live backend/state.

==============================================================
45. CSS SCOPING
==============================================================

Avoid broad CSS selectors that regress other steps.

Step 2.4 fixes must not change Step 2.3.

Step 2.5 fixes must not change Step 2.2.

Step 3 fixes must not alter Name-Level Assessment.

Scope selectors carefully.

==============================================================
46. BUSINESS OUTPUT QUALITY GATE
==============================================================

A successful issuer result must pass all of these checks:

real canonical issuer

verified identity

real SEC evidence

valid model output

no raw JSON

no tool trace

no technical error in business fields

no invented financial values

valid factor scores

valid composite score

valid rating/impact output according to existing methodology

concise credit rationale

clear source/evidence lineage

If it fails validation:

do not publish it to the assessment table.

==============================================================
47. MISSING DATA IS NOT BAD CREDIT
==============================================================

Repeat this rule throughout the implementation:

MISSING DATA ≠ CREDIT DETERIORATION

SEC FAILURE ≠ SUBSTANDARD

WEB FAILURE ≠ DOWNGRADE

PARSER FAILURE ≠ HIGH IMPACT

RUNNER TIMEOUT ≠ CREDIT RISK

Only actual issuer evidence and approved scoring logic may produce a
credit-risk result.

==============================================================
48. FINAL END-TO-END TEST — DO THIS YOURSELF
==============================================================

Run the REAL application.

Do not stop at unit tests.

Execute the workflow.

TEST CASE:

Sector = Software

Step 2.2:
confirmed Software population

Verify actual count and identifiers.

Step 2.3:
5 confirmed event-driven RFs.

Step 2.4:
generate/load exactly 5 structural RFs.

Verify:

5 factors
100% weights
complete schema
v31 rendering.

Confirm Step 2.4.

Then Step 2.5:

preflight Step 2.2 Software companies

select exactly ten verified SEC-resolvable issuers

run SEC + Web assessment

obtain ten successful model results

render ten readable rows

verify no technical garbage

verify scores and evidence

confirm Step 2.5.

Then Step 3:

open Step 3

verify data automatically exists

verify exposure calculations

verify segmentation

verify portfolio score/output

verify commentary

verify v31 design

confirm portfolio assessment.

==============================================================
49. DO NOT DECLARE SUCCESS AFTER STATIC FIXES
==============================================================

These do NOT count as completion:

HTML looks correct

CSS compiles

JSON fixture passes

unit test passes

mock data renders

preset auth passes

SEC endpoint answers once

one issuer succeeds

Step 2.4 alone succeeds

Step 2.5 alone succeeds.

Completion means the actual workflow reaches Step 3 with real accepted
results.

==============================================================
50. VISUAL ACCEPTANCE — STEP 2.4
==============================================================

Compare live current Step 2.4 directly against v31.

At normal desktop zoom, no obvious differences should remain in:

sector strip
summary table
factor cards
accordion rows
metrics
severity bands
scoring table
green/orange information strips
button layout
feedback panel
sidebar proportions.

==============================================================
51. VISUAL ACCEPTANCE — STEP 2.5
==============================================================

Compare live current Step 2.5 against v31.

It should look like a professional assessment outcome.

It must NOT look like:

a raw 226-row database dump

a debug console

a collection of giant wrapped error cells

or a backend diagnostic page.

==============================================================
52. VISUAL ACCEPTANCE — STEP 3
==============================================================

Compare live Step 3 to actual v31.

The current mostly-empty page is not accepted.

It must have the full v31 portfolio-assessment information architecture
populated with real current results.

==============================================================
53. REGRESSION CHECK
==============================================================

Before completion verify:

Step 1 still loads

Step 2.1 still loads

Step 2.2 still shows confirmed Software portfolio

Step 2.3 still shows its five confirmed event-driven RFs

Step 2.4 works

Step 2.5 works

Step 3 works

navigation works

workflow sidebar works

feedback panels remain step-specific.

==============================================================
54. PERFORMANCE / FAILURE BEHAVIOUR
==============================================================

Do not allow another 40+ minute silent failure.

Every external/model operation must use the existing bounded completion
behaviour.

Display useful running state.

On issuer-specific failure, handle it and continue with the next
eligible candidate where appropriate.

The entire browser must remain responsive.

==============================================================
55. WHAT YOU MUST NOT DO
==============================================================

Do NOT:

create fake Salesforce/Apple demo substitutions

hard-code the v31 example numbers

hard-code ten arbitrary company results

fabricate SEC data

fabricate exposure

change Stylus preset configuration

create a new model/preset

replace current Runner architecture

use static JSON as the final assessment

show 226 companies in the 10-company acceptance run

accept four Step 2.4 factors

convert missing evidence into a credit downgrade

leave Step 3 blank

hide errors by inventing results

declare visual parity without a live comparison.

==============================================================
56. IMPLEMENTATION BEHAVIOUR
==============================================================

Proceed autonomously.

You have approval to make the smallest code changes needed throughout
Step 2.4, Step 2.5 and Step 3.

Do not stop and ask:

“Should I continue?”

“Would you like me to fix Step 2.5?”

“Should I now work on Step 3?”

Continue automatically.

Do not write progress essays while working.

Use terminal output/tests internally.

Fix problems as you encounter them.

==============================================================
57. ACCEPTANCE GATE
==============================================================

Do not finish until ALL are true:

STEP 2.4

[ ] Software sector inherited correctly
[ ] exactly five RFs
[ ] no duplicate RFs
[ ] 100.0% total weight
[ ] complete vulnerability framework
[ ] complete buffer framework
[ ] complete scoring 1–5
[ ] all five RF cards complete
[ ] v31 visual parity
[ ] confirmation persists

STEP 2.5

[ ] population comes from confirmed Step 2.2 Software selection
[ ] no 226-name wrong-universe table
[ ] 10-company acceptance cohort
[ ] all ten preflighted before model execution
[ ] all ten canonical identities resolved
[ ] all ten have verified SEC evidence
[ ] SEC + Web route works
[ ] bounded Runner completion works
[ ] ten successful assessments
[ ] no fabricated evidence
[ ] no technical errors in business cells
[ ] no technical failure converted to credit classification
[ ] table readable
[ ] v31 visual parity
[ ] Step 2.5 confirmation persists

STEP 3

[ ] automatically receives confirmed Step 2.5 results
[ ] scope matches assessed population
[ ] actual exposure data reused
[ ] real segmentation calculated
[ ] real aggregate scoring calculated
[ ] full v31 information architecture rendered
[ ] no blank placeholder output
[ ] no static demo values
[ ] portfolio confirmation works
[ ] workflow reaches completion

REGRESSION

[ ] Steps 1–2.3 still work
[ ] no shared-CSS regression
[ ] no unrelated backend regression.

==============================================================
58. ONLY AFTER EVERYTHING ABOVE PASSES
==============================================================

Only after the complete live end-to-end test succeeds may you respond.

Do NOT give me a long report.

Return only:

END-TO-END: PASS or FAIL

STEP 2.4: PASS or FAIL
STEP 2.5 SEC+WEB: PASS or FAIL
STEP 3: PASS or FAIL
V31 VISUAL PARITY 2.4: PASS or FAIL
V31 VISUAL PARITY 2.5: PASS or FAIL
V31 VISUAL PARITY STEP 3: PASS or FAIL

TEST SECTOR:
actual value

STEP 2.2 SECTOR POPULATION:
actual count

ASSESSED COMPANIES:
the ten canonical company names + ticker + CIK

SEC EVIDENCE:
filing form/date used for each company

STEP 2.4 FACTORS:
RF1–RF5 names

STEP 2.5:
10/10 success required

STEP 3:
confirmed aggregation result

FILES CHANGED:
exact paths

REMAINING DIFFERENCES FROM V31:
NONE if genuinely none;
otherwise list every remaining difference.

If any acceptance condition fails and it is solvable from the
repository/environment, DO NOT REPORT YET.

FIX IT AND RETEST.

BEGIN IMPLEMENTATION NOW.
