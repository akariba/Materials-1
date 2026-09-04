RPR STEP 2.3 — DEEP FUNCTIONAL CORRECTION + EXACT V31 RECONSTRUCTION

IMPLEMENTATION TASK ONLY.

NO AUDIT REPORT.
NO DESIGN DOCUMENT.
NO PROGRESS REPORT.
NO APPROVAL QUESTIONS.
DO NOT ASK “SHOULD I PROCEED?”
DO NOT STOP AFTER DIAGNOSIS.

Everything required by this prompt is PRE-APPROVED.

Proceed autonomously:

READ AUTHORITATIVE SOURCES
→ UNDERSTAND BUSINESS PURPOSE
→ IMPLEMENT
→ RUN
→ COMPARE WITH V31
→ FIX
→ CONTINUE

until the acceptance criteria at the end are satisfied.

PROJECT ROOT:

C:\Users\ak54743\Downloads\OneDrive_2026-07-16\Rapid Portfolio Review_AI

ACTIVE APPLICATION:

UI Design\step23.html

AUTHORITATIVE VISUAL / BEHAVIORAL REFERENCE:

UI Design\icm-pm-rapid-portfolio-review-v31.html

============================================================
1. SCOPE — STEP 2.3 ONLY
============================================================

This task concerns:

STEP 2.3 — EVENT-DRIVEN RISK FACTORS

Do NOT redesign or refactor:

Step 1
Step 2.1
Step 2.2
Step 2.4
Step 2.5
Step 3

except for the minimum interface compatibility necessary for Step 2.3
confirmed output to continue flowing downstream.

Preserve all currently working functionality outside Step 2.3.

This remains a POC.

No production architecture.

============================================================
2. FIRST RULE — DO NOT IMPLEMENT BEFORE READING THE REAL SOURCES
============================================================

Before changing ANY Step 2.3 code:

READ the complete relevant implementation in:

UI Design\icm-pm-rapid-portfolio-review-v31.html

Do not skim.

Search the full file for everything related to:

Step 2.3
Event-driven Risk Factors
Event Factors
RF1
factor weights
importance
vulnerability metrics
buffer metrics
critical threshold
key principle
scoring logic
Net Score
Buffer Credit
Confirm All Risk Factors
Generate Event Factors
Save All Changes
Feedback to Risk Factor Agent

Read every associated:

HTML
CSS
JavaScript
data structure
render function
event handler
weight-calculation function
validation rule.

If Step 2.3 prompt files exist in the repository, read those FULLY too.

Search all prompt/preset/knowledge files for the original Step 2.3
business specification.

Do NOT infer business rules from the current implementation.

Do NOT use screenshots as the primary source when the actual source exists.

The authority order is:

1. original Step 2.3 business/prompt specification
2. actual v31 Step 2.3 implementation
3. manager/demo behavior
4. current Step 2.3 implementation

If current code conflicts with 1–3, current code loses.

============================================================
3. BUSINESS PURPOSE — UNDERSTAND THIS BEFORE CODING
============================================================

Step 2.3 is NOT a company assessment.

Step 2.3 is NOT supposed to search SEC filings for individual companies.

Step 2.3 is NOT supposed to decide company creditworthiness.

Step 2.3 is NOT supposed to generate a huge list of generic risks.

Its business purpose is:

TAKE THE CONFIRMED STEP 2.1 SCENARIO

and translate that scenario into a SMALL, COMPLETE, NON-OVERLAPPING SET
OF MATERIAL EVENT-DRIVEN CREDIT-RISK TRANSMISSION CHANNELS.

These factors explain:

HOW CAN THIS SPECIFIC SCENARIO DAMAGE OR SUPPORT A COMPANY'S CREDIT
PROFILE?

Each factor must later be measurable at company level in Step 2.5.

Therefore a good RF is not merely:

"Tariff Risk"

or:

"Macroeconomic Risk"

It should identify a concrete transmission mechanism such as:

scenario event
→ business/financial exposure
→ vulnerability metric
→ mitigating buffer
→ measurable company consequence.

Step 2.3 creates the analytical framework.

Step 2.5 later applies that framework to every portfolio company using
SEC/Web/company evidence.

That separation is fundamental.

============================================================
4. STEP 2.3 VS STEP 2.4 — DO NOT CONFUSE THEM
============================================================

Step 2.3 = EVENT-DRIVEN.

Its factors must arise specifically because of the Step 2.1 scenario.

Step 2.4 = SECTOR-INHERENT.

Those are structural risks that exist because of the company's sector even
without the particular event.

Do not generate Step 2.3 RFs that are merely generic sector risks.

Before accepting a proposed RF ask internally:

WOULD THIS FACTOR STILL EXIST IN ESSENTIALLY THE SAME FORM IF THE STEP 2.1
EVENT DID NOT OCCUR?

If yes, it may belong in Step 2.4 rather than Step 2.3.

Avoid duplication across the two factor families.

============================================================
5. NUMBER OF EVENT-DRIVEN FACTORS — IMPORTANT DISCREPANCY
============================================================

The current Step 2.3 screenshot generates:

RF1
RF2
RF3
RF4
RF5
RF6

= SIX factors.

The v31 reference shown by the user contains:

RF1
RF2
RF3
RF4
RF5

= FIVE factors.

This discrepancy must be resolved from the AUTHORITATIVE original prompt
and v31 source.

Do not simply preserve 6 because the current implementation happens to
generate 6.

EXPECTED TARGET:

FIVE MATERIAL EVENT-DRIVEN FACTORS.

Unless the original authoritative Step 2.3 prompt explicitly and
unambiguously requires another number, implement:

TARGET_EVENT_FACTOR_COUNT = 5

The model must generate the FIVE most material, distinct and measurable
event-driven transmission channels.

Do NOT generate six and then arbitrarily delete one.

Prompt the model to prioritize and consolidate BEFORE returning the final
set.

If multiple candidate risks describe substantially the same transmission
channel, consolidate them.

Five is intended to provide:

materiality
coverage
clarity
non-overlap
manageable downstream analysis
high-quality Step 2.5 assessment.

Do not dilute the framework by generating marginal sixth/seventh factors.

============================================================
6. FACTOR QUALITY — EACH OF THE FIVE MUST BE MATERIAL
============================================================

Every RF must satisfy ALL of these:

A. DIRECT EVENT LINKAGE

There must be a clear causal link to Step 2.1.

B. COMPANY-LEVEL MEASURABILITY

Step 2.5 must be able to assess it using financial/company evidence.

C. CREDIT RELEVANCE

It must affect at least one meaningful credit dimension such as:

revenue
margin
cash flow
liquidity
leverage
debt-service capacity
refinancing
capital structure
customer concentration
supplier concentration
operational dependency
market access
working capital
funding access
business durability.

D. DISTINCTNESS

Avoid factors measuring essentially the same transmission mechanism.

E. ACTIONABLE METRICS

The RF needs useful vulnerability and buffer metrics.

F. MATERIALITY

Do not use one of five slots for a remote or speculative tail risk when a
more important scenario channel exists.

============================================================
7. EXAMPLE — DO NOT HARD-CODE THESE FACTORS
============================================================

The screenshots show scenario-specific factors such as:

Import-Cost Pass-Through & Margin Restoration

Export Market Access & Retaliatory Tariff Relief

Competitive Displacement from Tariff-Shield Removal

Customer-Base Tariff Sensitivity & Downstream Demand Transmission

Policy Uncertainty & Legislative Replacement Risk

Supply-Chain Reconfiguration Stranded-Cost & Transition Risk

and another scenario generates factors such as:

Revenue Model Obsolescence & ARR Durability

Gross Margin Compression from AI COGS

Competitive Moat Erosion & Market Position

R&D / AI Reinvestment Burden & FCF Sustainability

Capital Structure Stress & Refinancing Risk

These demonstrate that RFs are DYNAMIC.

DO NOT hard-code any of these factor names.

The scenario determines the five factors.

============================================================
8. FACTOR STRUCTURE — EACH RF MUST BE FULLY SPECIFIED
============================================================

For every generated RF, preserve the full analytical structure shown by
v31.

At minimum:

factor_id
factor_name
factor_narrative
importance
importance_score
weight

VULNERABILITY METRICS SET 1

Each vulnerability metric should include whatever the authoritative v31
source actually contains, likely equivalent to:

metric name
formula
Very High threshold
High threshold
Moderate threshold
Low threshold

CRITICAL THRESHOLD

BUFFER METRICS SET 2

Each buffer metric should include equivalent categories:

metric
formula
Strong
Moderate
Weak
Negligible

KEY PRINCIPLE

SCORING LOGIC 1–5

For scores:

5
4
3
2
1

include:

Vulnerability Profile
Buffer Profile

and the exact Net Score / Buffer Credit methodology used by v31.

Do not simplify this structure to:

name
description
weight.

The depth of the factor definition is what makes Step 2.5 analytically
useful.

============================================================
9. CREDIT-ANALYSIS DESIGN OF VULNERABILITY METRICS
============================================================

Vulnerability metrics identify:

HOW EXPOSED IS THIS COMPANY TO THIS EVENT TRANSMISSION CHANNEL?

Metrics should be company-observable where reasonably possible.

Examples of metric families:

revenue concentration
geographic exposure
COGS exposure
margin sensitivity
customer concentration
supplier concentration
working-capital dependence
debt maturity profile
leverage
interest coverage
ARR/NRR/churn
capex intensity
R&D intensity
funding dependence
contract duration
pricing power
market-share concentration.

Do not use abstract metrics that Step 2.5 cannot reasonably evidence.

============================================================
10. BUFFER METRICS — EQUALLY IMPORTANT
============================================================

Step 2.3 must not model only downside exposure.

The Step 3a methodology explicitly requires:

VULNERABILITY

versus:

BUFFER / MITIGANT.

Buffer metrics should capture real resilience such as:

pricing power
gross-margin headroom
liquidity
cash balance
low leverage
strong interest coverage
contractual protection
short procurement cycles
geographic diversification
supplier diversification
recurring revenue
customer stickiness
asset-light operations
access to funding
parent support
capital flexibility.

The final score is therefore not:

raw exposure = final score.

It should reflect:

raw vulnerability
adjusted by
credible buffers.

============================================================
11. CRITICAL THRESHOLD
============================================================

Each factor should contain a meaningful critical-threshold rule where the
authoritative v31 methodology requires it.

A critical threshold is not arbitrary explanatory prose.

It defines a combination of conditions sufficiently severe to justify an
override/high vulnerability treatment.

Read the exact v31 implementation and preserve its role.

Do not invent mandatory overrides unrelated to the original methodology.

============================================================
12. KEY PRINCIPLE
============================================================

Each RF should state the analytical principle explaining what combination
of business characteristics creates the strongest resilience or greatest
exposure.

This is useful downstream because Step 2.5 can compare actual company
evidence against that principle.

Keep it concise but analytically meaningful.

============================================================
13. SCORING LOGIC — DO NOT INVENT A NEW ONE
============================================================

Read v31's actual Step 2.3 scoring logic.

The screenshots indicate a 1–5 structure with:

Score
Vulnerability Profile
Buffer Profile

and a Net Score / Buffer Credit methodology.

The visual screenshot includes language equivalent to:

Buffer Credit:
Strong = -2
Moderate = -1
Weak = 0

Floor = 1
Ceiling = 5

DO NOT use this text merely because it appears in the screenshot.

Find the actual source implementation and reproduce the authoritative
calculation exactly.

There must be ONE clear methodology.

Do not let the frontend calculate one formula and Step 2.5 interpret
another.

============================================================
14. FACTOR IMPORTANCE
============================================================

Use the authoritative Step 2.3 importance vocabulary.

The screenshots show:

HIGH
MEDIUM

Do not introduce LOW importance unless the original prompt/v31 explicitly
supports it.

This step should contain the most material factors; a factor that is only
low importance probably should not occupy one of the five slots.

============================================================
15. WEIGHTING — CURRENT 6-FACTOR VERSION VS V31
============================================================

The current six-factor example shows:

HIGH
HIGH
HIGH
HIGH
MEDIUM
MEDIUM

and weights:

20%
20%
20%
20%
10%
10%

= 100%.

The v31 five-factor example shows approximately:

HIGH
HIGH
HIGH
HIGH
MEDIUM

with displayed weights:

22.2%
22.2%
22.2%
22.2%
11.1%

display total approximately:

99.9%

because of decimal display rounding.

This is consistent with deterministic importance weighting:

HIGH = 2 units
MEDIUM = 1 unit

Total units:

2+2+2+2+1 = 9

Therefore:

HIGH = 2/9 = 22.222...%

MEDIUM = 1/9 = 11.111...%

Internally:

weights must normalize mathematically to 100%.

Display:

must follow v31's actual decimal precision.

Do NOT alter a displayed 99.9% caused solely by rounding if that is exactly
what v31 displays.

Do not change weighting merely to make the displayed number say 100.0%.

Use full precision for downstream calculations.

============================================================
16. WEIGHTING MUST BE BACKEND-CONTROLLED
============================================================

Factor importance may be AI-proposed.

Weight arithmetic must be deterministic.

The model must NOT be trusted to perform weighting calculations.

Implement one authoritative backend weight function.

Conceptually:

importance → numeric unit
normalize units
store full precision
display v31 rounded precision.

Step 2.5 must receive the original full-precision Step 2.3 weights.

Do not recalculate different weights in Step 2.5.

============================================================
17. EXACT FIVE-FACTOR OUTPUT CONTRACT
============================================================

After generation and before rendering/confirmation:

validate:

factor count = 5

IDs exactly:

RF1
RF2
RF3
RF4
RF5

No RF6.

No missing ID.

No duplicate ID.

No duplicate/synonymous factor concepts.

Each factor has:

name
narrative
importance
weight
vulnerability metrics
buffer metrics
scoring logic

and all other mandatory v31 fields.

If generation returns >5:

DO NOT silently truncate.

Use the existing AI refinement path to consolidate/rank to the five most
material factors.

If generation returns <5:

use the approved generation/refinement path to complete the missing
material channel.

Do not fabricate empty placeholder factors.

============================================================
18. CONFIRMATION CONTRACT TO STEP 2.5
============================================================

When the analyst presses:

CONFIRM ALL RISK FACTORS

persist the EXACT confirmed set.

Step 2.5 must later receive:

exactly RF1–RF5
confirmed names
confirmed narratives
confirmed weights
confirmed vulnerability metrics
confirmed buffer metrics
critical thresholds
key principles
scoring logic
industry sensitivity/context if Step 2.3 actually supports it
analyst edits.

Do not reduce confirmed factors to name + weight downstream.

============================================================
19. ANALYST EDITABILITY
============================================================

Preserve v31 behavior allowing the analyst to review and edit the factor
definition before confirmation.

Where v31 supports editing:

factor name
factor narrative
importance
vulnerability metrics
thresholds
buffer metrics
critical threshold
key principle
scoring logic

preserve the same behavior.

"Save All Changes" should actually persist the edited draft.

"Confirm All Risk Factors" should freeze/confirm the final Step 2.3
version used downstream.

Do not lose analyst edits when switching sections.

============================================================
20. ADD FACTOR / REMOVE FACTOR
============================================================

Read v31's exact behavior.

If v31 permits:

+ Add Factor
Remove Factor

preserve the UI controls.

But distinguish:

AI DEFAULT GENERATED SET

from:

ANALYST MANUAL OVERRIDE.

Default AI generation should return FIVE.

If the analyst manually adds/removes a factor, preserve the explicit
analyst action according to v31 behavior.

Do not automatically force the analyst's manually edited count back to
five after an intentional change unless the original business rule
requires exactly five even after manual edit.

Document this distinction in code, not a report.

============================================================
21. GENERATE EVENT FACTORS BUTTON
============================================================

Use v31's exact button:

label
location
height
width
color
padding
font
hover
disabled state.

Functionally:

generation must use the confirmed current Step 2.1 scenario.

Do not use stale previous scenario factors.

If Step 2.1 changes:

the old Step 2.3 generated set must be marked stale/unconfirmed.

Do not silently keep scenario-incompatible factors.

============================================================
22. STEP 2.3 FEEDBACK
============================================================

Preserve:

Feedback to Risk Factor Agent

exactly as v31 implements it.

Feedback should refine the Step 2.3 factor generation/definition.

It should not modify unrelated steps.

It should respect confirmed scenario context.

Do not rebuild the whole page from scratch when feedback is applied if
v31 doesn't.

============================================================
23. V31 VISUAL PARITY — ZERO DESIGN FREEDOM
============================================================

The user explicitly requires:

STEP 2.3 IN step23 MUST LOOK LIKE v31.

Do not "improve" it.

Do not modernize it.

Do not approximate it.

Do not create your own design.

READ THE REAL v31 SOURCE.

For every component copy/reuse exact:

DOM hierarchy
class names where practical
CSS declarations
colors
font family
font size
font weight
line height
padding
margin
border width
border color
background
header height
row height
input height
textarea height
button height
button colors
badge colors
accordion height
accordion background
hover behavior
selected behavior
disabled behavior
scroll behavior.

No guessing.

============================================================
24. TOP STEP 2.3 FACTOR SUMMARY TABLE — EXACT V31
============================================================

Reproduce the exact v31 table.

Inspect and copy exact:

container width
table width
header background
header text colors
header height
header font size
body row height
cell alignment
grid borders
top/bottom padding.

The screenshots show columns conceptually equivalent to:

RF
FACTOR
IMPORTANCE
IMP. SCORE
WEIGHT

but the actual v31 source is authoritative.

Do not rely on screenshot wording if source differs.

============================================================
25. HEADER COLOR BANDS
============================================================

The current implementation and v31 differ in some styling.

Read v31 CSS and reproduce the exact header color segmentation.

For example if v31 uses:

neutral RF/FATOR cells
yellow importance area
green weight area

use the exact actual v31:

hex/rgb values
border treatment
font weight
cell dimensions.

Do NOT choose "similar" colors.

============================================================
26. FACTOR ACCORDION HEADER — EXACT V31
============================================================

Each factor row/card must use the exact v31 accordion design.

Copy:

factor number circle
circle size
circle color
RF label
factor name
weight text
importance text/badge
right-side controls
chevron
expanded background
collapsed background
border
spacing
padding
height.

The current Step 2.3 should not simply be "close."

It must be source-derived.

============================================================
27. FACTOR NARRATIVE AREA
============================================================

Copy exact v31:

section label
textarea dimensions
font
border
background
padding
line height
resize behavior
minimum/maximum height.

Do not let narratives create unnecessary giant whitespace.

============================================================
28. FACTOR IMPORTANCE CONTROL
============================================================

Copy v31 exact:

High
Medium

button/toggle styling.

Include:

selected colors
unselected colors
border
radius
font
spacing.

If v31 uses a badge elsewhere for the accordion summary, copy that too.

============================================================
29. VULNERABILITY METRICS TABLE — PIXEL-LEVEL PARITY
============================================================

This is one of the most important UI components.

Read the exact v31 structure.

Copy:

section heading
"SET 1" wording
column sequence
Metric width
Formula width
Very High width
High width
Moderate width
Low width
delete control width
header colors
input sizes
row heights
borders
cell spacing.

Copy exact colors for:

VERY HIGH
HIGH
MODERATE
LOW

Do NOT substitute the Step 2.5 score colors.

These are Step 2.3 vulnerability-threshold colors.

Use v31 exact values.

============================================================
30. CRITICAL THRESHOLD BLOCK — EXACT
============================================================

Copy exact:

border color
background
label color
input/textarea height
padding
spacing.

Do not invent a different warning card.

============================================================
31. BUFFER METRICS TABLE — PIXEL-LEVEL PARITY
============================================================

Copy exact v31:

SET 2 heading
Metric
Formula
Strong
Moderate
Weak
Negligible

and exact:

column sizes
header colors
input sizes
row heights
borders
padding.

Copy v31 exact colors for:

STRONG
MODERATE
WEAK
NEGLIGIBLE.

Do not use approximated greens/yellows/reds.

============================================================
32. KEY PRINCIPLE BLOCK
============================================================

Copy exact v31:

green-tinted container
border
label
textarea
text size
padding
margin.

No approximation.

============================================================
33. SCORING LOGIC TABLE — EXACT
============================================================

Copy v31 exactly.

Columns should follow actual source.

Screenshots show:

SCORE
VULNERABILITY PROFILE
BUFFER PROFILE

Rows:

5
4
3
2
1.

Copy:

score-column width
profile widths
header colors
row heights
textarea dimensions
font
borders
padding.

Do not compress it differently from v31.

Do not increase table height arbitrarily.

============================================================
34. NET SCORE FOOTER
============================================================

Copy the exact v31 methodology/footer text and style from SOURCE.

Do not rewrite the sentence.

Do not change:

font size
italicization
padding
border
color

unless source itself requires it.

============================================================
35. BOTTOM CONTROLS — EXACT V31
============================================================

Copy exact v31 position, size and order for:

+ Add Factor
Save All Changes
Confirm All Risk Factors

and any generate/regenerate control.

Exact:

button height
background
border
font size
font weight
spacing
alignment.

============================================================
36. NO UNNECESSARY SCROLL / PAGE DISTORTION
============================================================

Current screenshots show very long pages.

The expanded first factor will naturally be large, but dimensions must
match v31.

Do not create larger:

textarea heights
rows
gaps
margins
padding

than v31.

Collapsed RF2–RF5 should remain compact exactly like v31.

============================================================
37. CURRENT SCREENSHOT DISCREPANCIES TO ADDRESS
============================================================

Do not produce a report on these.

Fix them.

Observed discrepancies include:

A. current AI-generated count = 6 whereas v31 reference = 5;

B. current six-factor weighting is therefore structurally different from
the v31 five-factor weighting pattern;

C. current table/accordion dimensions are not proven source-identical;

D. current color blocks need exact source verification;

E. current factor cards need exact v31 header/spacing verification;

F. v31 appears to present a five-factor compact risk framework, whereas
current generation can create a broader six-factor catalogue;

G. downstream Step 2.5 requires the COMPLETE confirmed factor objects, not
merely names/weights.

Address all of these through source-based implementation.

============================================================
38. SCENARIO-SPECIFIC QUALITY GATE
============================================================

Before accepting generated RFs, implement a lightweight quality check.

For the five factors verify:

1. direct scenario linkage;
2. distinct transmission mechanism;
3. credit relevance;
4. measurable company-level metrics;
5. actionable buffers;
6. no obvious duplication;
7. no sector-inherent factor masquerading as event-driven;
8. complete analytical fields.

This should be bounded.

Do not add another expensive LLM loop if deterministic checks plus the
existing generation/refinement mechanism suffice.

POC efficiency matters.

============================================================
39. DO NOT FABRICATE INDUSTRY SENSITIVITY
============================================================

The manager previously highlighted industry sensitivity.

Inspect actual Step 2.3 prompt/data structures.

If Step 2.3 already generates:

industry sensitivity
sector sensitivity
industry impact modifier
or equivalent

preserve and pass it downstream.

If it does not exist in the authoritative Step 2.3 design:

do NOT invent a new field merely because it sounds useful.

Use the actual methodology.

============================================================
40. TESTING — NO REPORT FIRST
============================================================

After implementation:

A. Run syntax/lint checks.

B. Load step23.html.

C. Generate Step 2.3 from a confirmed Step 2.1 scenario.

D. Verify AI default returns:

RF1
RF2
RF3
RF4
RF5

and NO RF6.

E. Verify internal weight sum = 100%.

F. Verify display rounding matches v31.

G. Verify each factor contains complete:

narrative
importance
vulnerability metrics
critical threshold
buffer metrics
key principle
scoring logic.

H. Confirm factors.

I. Verify persisted confirmed Step 2.3 object contains all five complete
objects.

J. Verify Step 2.5 receives those complete objects.

Do NOT run an expensive full Step 2.5 SEC/Web portfolio assessment merely
to test this Step 2.3 task.

Inspect payload construction or use existing non-Runner test mechanisms.

============================================================
41. VISUAL SIDE-BY-SIDE ACCEPTANCE
============================================================

Open:

A.
icm-pm-rapid-portfolio-review-v31.html
→ Step 2.3

B.
step23.html
→ Step 2.3

Compare at the SAME browser zoom and viewport.

Check one component at a time:

page title
tabs
summary table
table header
table rows
weights
factor accordion
expanded header
factor narrative
importance controls
vulnerability table
critical threshold
buffer table
key principle
scoring logic
footer methodology text
collapsed factors
bottom buttons
feedback section.

If a visual difference exists and v31 provides the source values:

FIX IT.

Do not declare “close enough.”

============================================================
42. IMPORTANT: DO NOT HARD-CODE THE DEMO
============================================================

v31's SaaS example is a DEMONSTRATION OF STRUCTURE.

Do not hard-code:

SaaSpocalypse
Revenue Model Obsolescence
AI COGS
Competitive Moat
R&D Reinvestment
Capital Structure Stress

into production POC logic.

The content must come from the current Step 2.1 scenario.

What is fixed:

the analytical structure.

What is dynamic:

the factor content.

============================================================
43. IMPORTANT: STEP 2.3 OUTPUT SHOULD SUPPORT STEP 2.5
============================================================

The ultimate purpose of Step 2.3 is downstream name-level assessment.

A Step 2.3 factor is only useful if Step 2.5 can answer:

How vulnerable is THIS company to the factor?

What evidence supports the vulnerability?

What buffer offsets it?

What score 1–5 results?

Therefore do not create RFs so vague that no company-level evidence can
answer them.

Step 2.3 must produce a reusable scoring framework.

Step 2.5 applies it.

============================================================
44. DO NOT TOUCH THE CURRENT STEP 2.5 STABILIZATION WORK
============================================================

Another implementation stream may be working on Step 2.5.

Do not overwrite or roll back:

Step 2.5 Runner
token
evidence
batching
v31 rendering
context fingerprint
runtime fixes.

This task is Step 2.3.

Only ensure Step 2.3's confirmed output remains compatible with the
existing Step 2.5 input assembler.

============================================================
45. FILE CHANGE DISCIPLINE
============================================================

Change only files genuinely required for Step 2.3.

Do not create:

new UI framework
new CSS framework
generic component library
new state-management framework
new backend architecture.

Reuse existing project patterns.

============================================================
46. AUTONOMY
============================================================

Do not ask me:

whether five factors are okay;
whether to change the CSS;
whether to update the prompt;
whether to modify factor validation;
whether to proceed;
whether to test.

The bounded implementation described here is approved.

If you encounter ambiguity:

read the authoritative original Step 2.3 prompt and v31 source.

Make the minimal evidence-based decision.

Continue.

============================================================
47. ACCEPTANCE CRITERIA
============================================================

Do not stop until:

STEP23_STEP23_V31_STRUCTURE = PASS
STEP23_STEP23_V31_COLORS = PASS
STEP23_STEP23_V31_TABLE_DIMENSIONS = PASS
STEP23_STEP23_V31_ACCORDIONS = PASS
STEP23_STEP23_V31_VULNERABILITY_TABLE = PASS
STEP23_STEP23_V31_BUFFER_TABLE = PASS
STEP23_STEP23_V31_SCORING_TABLE = PASS

DEFAULT_RF_COUNT = 5
RF_IDS = RF1-RF5
NO_DEFAULT_RF6 = PASS

FACTOR_QUALITY_GATE = PASS
EVENT_VS_SECTOR_SEPARATION = PASS

INTERNAL_WEIGHT_SUM = 100%
DISPLAY_WEIGHTING_MATCHES_V31 = PASS
WEIGHT_CALC_BACKEND_CONTROLLED = PASS

FULL_FACTOR_NARRATIVE = PASS
VULNERABILITY_METRICS = PASS
CRITICAL_THRESHOLD = PASS
BUFFER_METRICS = PASS
KEY_PRINCIPLE = PASS
SCORING_LOGIC_1_5 = PASS

ANALYST_EDITABILITY = PASS
SAVE_ALL_CHANGES = PASS
CONFIRM_ALL_RISK_FACTORS = PASS

CONFIRMED_STEP23_FULL_OBJECT_PERSISTED = PASS
STEP25_RECEIVES_COMPLETE_STEP23_FACTORS = PASS

READY_FOR_USER_STEP23_TEST = YES

============================================================
48. FINAL RESPONSE — VERY SHORT
============================================================

Do NOT return another long report.

Return only:

IMPLEMENTATION = PASS/FAIL

V31_VISUAL_PARITY = PASS/FAIL
DEFAULT_RF_COUNT = <number>
RF_IDS = <value>
INTERNAL_WEIGHT_SUM = <value>
DISPLAY_WEIGHT_SUM = <value>

Event Factor Quality — PASS/FAIL
Event/Sector Separation — PASS/FAIL
Weighting — PASS/FAIL
Vulnerability Metrics — PASS/FAIL
Buffer Metrics — PASS/FAIL
Critical Threshold — PASS/FAIL
Scoring Logic — PASS/FAIL
Analyst Editing — PASS/FAIL
Step 2.3 Persistence — PASS/FAIL
Step 2.5 Handoff — PASS/FAIL

READY_FOR_USER_STEP23_TEST = YES/NO

If NO:

FIRST_REMAINING_BLOCKER=<one line>

NO EXTRA REPORT.

START BY READING THE COMPLETE AUTHORITATIVE STEP 2.3 IMPLEMENTATION AND
PROMPTS NOW.
