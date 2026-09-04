TASK: STEP 2.4 — SECTOR-INHERENT RISK FACTORS
V31 EXACT UI REPLICATION + PRESERVE / STRENGTHEN THE BUSINESS FUNCTION

You are working on the existing RPR / AI-Assisted Rapid Portfolio Review POC.

This task is ONLY for STEP 2.4 — SECTOR-INHERENT RISK FACTORS.

This is NOT a redesign.
This is NOT a new architecture task.
This is NOT permission to refactor working parts of the application.

The objective is:

1. Make the Step 2.4 UI replicate the approved v31 reference essentially exactly, including the smallest table/layout/framing details.
2. Preserve the existing working Step 2.4 functionality.
3. Preserve the correct business purpose and logical sequence of Step 2.4.
4. Ensure Step 2.4 produces a high-quality structured sector-credit framework that Step 2.5 can use for name-level assessment.
5. Fix only genuine discrepancies required to achieve the above.

============================================================
0. OPERATING PRINCIPLE — POC, NOT PRODUCTION REBUILD
============================================================

This application is a POC.

Do NOT introduce:
- new frameworks,
- unnecessary abstractions,
- production-style architecture,
- broad component rewrites,
- generic design systems,
- new adapters,
- speculative refactoring,
- backend changes unrelated to Step 2.4,
- CSS redesigns of other steps.

Use the existing implementation and make the smallest changes necessary.

Known-working functionality is an immutable building block.

DO NOT break:
- Step 1,
- Step 2.1,
- Step 2.2,
- Step 2.3,
- Step 2.5,
- existing workflow state,
- existing navigation,
- feedback functionality,
- existing backend endpoints,
- existing persistence/state behavior.

Proceed autonomously through the entire task.
Do not stop for approval after every change.

Stop only for a genuine external blocker that cannot be solved from the repository/environment.

============================================================
1. FIRST UNDERSTAND THE RPR SEQUENCE
============================================================

Before changing code, understand that Step 2.4 is part of this sequence:

STEP 1
Risk Narrative Intake
        ↓
STEP 2.1
Scenario & Assumptions
        ↓
STEP 2.2
Portfolio Selection
        ↓
STEP 2.3
Event-Driven Risk Factors
        ↓
STEP 2.4
Sector-Inherent Risk Factors
        ↓
STEP 2.5
Name-Level Assessment
        ↓
STEP 3
Portfolio-Level Assessment


Each step has a different analytical purpose.

DO NOT blur them together.

------------------------------------------------------------
STEP 2.3 ≠ STEP 2.4
------------------------------------------------------------

Step 2.3 asks:

“What credit-risk transmission channels arise from THIS EVENT /
SCENARIO?”

Those factors can change with the event.

Example:
- tariffs,
- supply-chain disruption,
- commodity shock,
- regulatory announcement,
- rate shock,
- geopolitical disruption.

Step 2.4 asks something fundamentally different:

“What structural vulnerabilities are inherent to THIS SECTOR even
before considering the particular event?”

These should represent persistent sector characteristics.

Examples for Software shown in v31 include concepts such as:

- Structural Leverage Intensity in Sponsor-Backed Software
- AI-Driven Technology Disruption and Obsolescence Risk
- Capital Expenditure Intensity and Free Cash Flow Compression
- Refinancing and Maturity Wall Concentration Risk
- Customer and End-Market Demand Cyclicality

The exact factors obviously depend on the sector.

Therefore Step 2.4 must NOT simply repeat Step 2.3.

============================================================
2. DEEPEST BUSINESS PURPOSE OF STEP 2.4
============================================================

Step 2.4 establishes the SECTOR CREDIT RISK REFERENCE FRAMEWORK.

Its function is to identify structural credit vulnerabilities that
exist because of the economics, financing structure, operating model,
competitive structure and cash-flow characteristics of the sector.

Its job is NOT simply to produce five AI-generated labels.

For each sector factor, Step 2.4 should define:

A. WHAT THE STRUCTURAL CREDIT RISK IS
   Factor Narrative

B. WHY IT MATTERS FOR CREDIT
   Factor Importance + Importance Justification

C. WHAT INDICATORS WOULD SHOW VULNERABILITY
   Vulnerability Metrics

D. WHAT INDICATORS WOULD PROVIDE PROTECTION
   Buffer Metrics

E. HOW THE OBSERVATIONS MAP INTO A CREDIT SCORE
   Scoring Logic 1–5

F. WHAT THE RESULT MEANS FOR CREDIT
   Credit Implication

This structured framework is subsequently required by Step 2.5.

Step 2.5 must eventually be able to ask:

“For this particular company, where does it sit relative to the
sector vulnerability/buffer framework established in Step 2.4?”

Therefore Step 2.4 must be sufficiently specific, measurable,
consistent and stable to support downstream company-level assessment.

============================================================
3. SECTOR-INHERENT FACTORS MUST BE STRUCTURAL
============================================================

The sector factors should represent persistent structural
characteristics, rather than recent headlines.

Appropriate categories can include, depending on sector:

- capital structure / leverage,
- refinancing dependence,
- maturity profile,
- cyclicality,
- pricing power,
- competitive intensity,
- customer concentration,
- supplier concentration,
- technological disruption,
- regulatory exposure,
- recurring revenue quality,
- capex intensity,
- working-capital behaviour,
- margin volatility,
- commodity sensitivity,
- liquidity dependence,
- insurance coverage,
- recovery characteristics,
- asset quality,
- contractual protections,
- revenue concentration,
- demand elasticity.

Do NOT force these categories into sectors where they do not fit.

The factor must be economically meaningful for the selected sector.

============================================================
4. DETERMINISTIC / REVIEWED SECTOR TAXONOMY CONCEPT
============================================================

The v31 UI explicitly communicates the principle:

“Approved/reviewed sector taxonomy. Exact weights are deterministic;
the LLM does not regenerate taxonomy on every run.”

Preserve that concept visibly and functionally.

Step 2.4 is not supposed to behave as:

click generate →
LLM randomly creates a different sector taxonomy →
different factors next time.

The POC should demonstrate a stable sector framework.

If the current implementation already contains approved/generated
sector factors and deterministic weights, preserve that mechanism.

Do NOT replace working deterministic behaviour with free-form LLM
generation.

If generation/refinement functionality exists, it should enrich or
create the sector framework in the intended controlled manner, not
cause arbitrary drift on every application load.

============================================================
5. NUMBER OF FACTORS
============================================================

The v31 reference demonstrates FIVE sector-inherent risk factors.

The Step 2.4 default/target should therefore remain:

5 sector-inherent risk factors

unless the existing approved implementation explicitly contains a
different user-controlled rule.

Do not arbitrarily produce 6, 7, 8 etc.

The summary table should show RF1–RF5.

The five factors should collectively provide sensible coverage of the
sector without becoming overlapping variants of the same risk.

============================================================
6. IMPORTANCE, IMP SCORE AND WEIGHT
============================================================

The top summary table in v31 contains:

RF
Factor
Importance
Imp. Score
Weight

Example visual behaviour:

HIGH
Imp. Score 2

MEDIUM
Imp. Score 1

Weights are displayed as percentages.

The total sector-factor weight must reconcile to:

100.0%

Preserve the currently approved weighting rule.

Do NOT invent an arbitrary weighting formula if one already exists.

The important point is that:

- weights must be deterministic,
- importance must be economically justified,
- total must equal 100%,
- the same values shown in the summary table must agree with the
  detailed factor panels.

No inconsistent values between summary and detail.

============================================================
7. V31 IS THE VISUAL SOURCE OF TRUTH
============================================================

Use the existing v31 HTML/reference implementation in the repository
as the PRIMARY visual specification.

Do not approximate the screenshots by eye if v31 code is available.

Inspect the actual v31:

- HTML,
- CSS,
- classes,
- component dimensions,
- spacing,
- typography,
- borders,
- colours,
- table structure,
- row heights,
- panel structure,
- accordion behaviour,
- controls.

Then reproduce those details in the current Step 2.4 implementation.

IMPORTANT:

DO NOT redesign v31 into what you think is “cleaner” or “more modern.”

If v31 has a particular:
- spacing,
- narrow row,
- pale background,
- border,
- header weight,
- input framing,
- table density,
- accordion height,
- colour band,

replicate it.

V31 wins over personal design preference.

============================================================
8. PAGE-LEVEL LAYOUT
============================================================

Step 2.4 must visually remain embedded in the existing v31
Name-Level Assessment screen.

Preserve the complete page hierarchy.

TOP HEADER
- Citi / application branding
- “ICM PM — AI-assisted Rapid Portfolio Review”
- beta/status controls where applicable
- existing dark navy header

ASSESSMENT JOURNEY BAR
- Step 1 Risk Narrative Intake
- Step 2 Name Level Assessment highlighted in blue
- Step 3 Portfolio Level Assessment

STEP 2 SUB-NAVIGATION
- Step 2.1 Scenario & Assumption
- Step 2.2 Portfolio Selection
- Step 2.3 Event-driven Risk Factors
- Step 2.4 Sector-Inherent Risk Factors
- Step 2.5 Assessment

Step 2.4 must have the exact selected/active treatment used in v31.

RIGHT SIDE
Keep the Workflow Status panel.

Do not move it.
Do not resize it arbitrarily.
Do not redesign it.

The central Step 2.4 content and the right workflow panel should retain
the v31 proportions.

============================================================
9. SECTOR SELECTOR BAR
============================================================

Immediately under the Step 2 tabs, v31 contains the dark navy sector
selector strip.

Replicate it.

It should include:

SECTOR label

and the selected sector dropdown.

Examples shown in v31:
- Software
- Sub-Media, Telecommunications & Software

depending on the dataset/version.

Preserve the actual sector coming from Step 2.2/current application
state.

Do NOT hard-code Software just because Software appears in the
reference screenshot.

The selected sector must be derived from the actual workflow state.

Visual details must follow v31:

- dark navy background,
- compact height,
- label position,
- dropdown framing,
- dropdown width,
- text size,
- border radius,
- padding,
- vertical centering,
- right-side factor count/status badge if currently present.

============================================================
10. STEP 2.4 SECTION HEADER
============================================================

Below the selector:

“Sector-Inherent Risk Factors”

Use the same v31:
- font size,
- font weight,
- spacing,
- alignment,
- border treatment.

Immediately underneath is the informational note.

In the reference this communicates:

Approved/reviewed sector taxonomy.
Exact weights are deterministic.
The LLM does not regenerate taxonomy on every run.

Replicate the same visual structure:

- narrow informational strip,
- subtle background,
- thin left blue accent,
- compact font,
- restrained padding.

============================================================
11. TOP FACTOR SUMMARY TABLE — EXACT V31 STRUCTURE
============================================================

This is one of the most important visual sections.

Columns must be:

RF
Factor
Importance
Imp. Score
Weight

Rows:

RF1
RF2
RF3
RF4
RF5

Follow v31 EXACTLY for:

- overall width,
- column proportions,
- header height,
- row height,
- text alignment,
- left padding,
- borders,
- font weight,
- header fills,
- colour blocks,
- numeric alignment,
- percentage formatting.

From the v31 reference:

RF / Factor area is neutral/light.

Importance header uses the pale yellow treatment.

Imp. Score uses the light yellow/gold treatment.

Weight uses the pale green treatment.

Do not substitute random bootstrap colours.

Use the actual v31 CSS values wherever available.

If editable weight inputs are part of the current implementation,
they must visually fit inside the cells exactly as v31 does.

The table must end with or visibly reconcile:

Total Weight: 100.0%

No horizontal overflow.
No oversized cells.
No excessive padding.
No contemporary card redesign.

============================================================
12. FACTOR ACCORDION STRUCTURE
============================================================

Below the summary table are the individual RF panels.

There should be five factor rows/panels.

The expanded factor panel must replicate v31.

HEADER EXAMPLE:

[blue circular number/icon]
Structural Leverage Intensity in Sponsor-Backed Software
HIGH · 25% · Net 2/5

or equivalent values from the actual current factor.

On the right:
- importance status where used,
- expand/collapse chevron,
- existing controls.

Match v31:
- header height,
- border,
- pale-blue header treatment,
- title size,
- icon size,
- icon position,
- subtitle position,
- margins,
- separator.

Collapsed factors must also match v31 exactly.

Do not turn them into generic Bootstrap cards.

============================================================
13. FACTOR NARRATIVE
============================================================

Expanded panel first contains:

FACTOR NARRATIVE

Then the narrative field.

Replicate:

- label typography,
- textarea/input-like framed rectangle,
- border colour,
- border width,
- radius,
- padding,
- line-height,
- minimum height,
- background,
- spacing.

The content itself must explain:

- the structural sector vulnerability,
- how it can impair credit quality,
- transmission into cash flow / leverage / refinancing / liquidity /
  enterprise value / recovery etc.,
- why it persists beyond a single event.

Avoid generic statements such as:

“This risk could negatively affect companies in this industry.”

Credit logic must be explicit.

============================================================
14. REFERENCE / EVIDENCE LINE
============================================================

Where v31 displays a small reference/source line below the narrative,
retain it.

Example concept:

Reference note → sector observations / research / approved taxonomy.

Do not fabricate references.

If actual references are unavailable, preserve whatever reference
mechanism the current application already implements.

Do not create false citation strings merely to fill the UI.

============================================================
15. FACTOR IMPORTANCE
============================================================

Then:

FACTOR IMPORTANCE

With the compact High / Medium controls exactly as v31.

Replicate:

- button dimensions,
- active state,
- inactive state,
- red/pink High treatment,
- neutral Medium treatment,
- spacing,
- typography.

Do not replace them with:
- dropdown,
- slider,
- toggle switch,
- stars,
- generic buttons.

============================================================
16. IMPORTANCE JUSTIFICATION
============================================================

Then:

IMPORTANCE JUSTIFICATION

v31 presents this in a pale green bordered/highlighted horizontal box.

Replicate:

- background,
- border,
- padding,
- font,
- width,
- spacing.

This text must explain WHY the factor has the assigned importance for
credit.

Example logic:

HIGH because deterioration can directly affect debt-service capacity
for a broad share of the sector and transmit quickly into covenant,
liquidity or refinancing pressure.

Do not simply restate the factor narrative.

============================================================
17. SET 1 — VULNERABILITY METRICS
============================================================

This is a CRITICAL part of Step 2.4.

Header:

VULNERABILITY METRICS (SET 1)

Table structure should follow v31 exactly.

Left area:
Metric / Formula

Then severity bands.

For the v31 Software example:

VERY HIGH
HIGH
MODERATE
LOW

Use the exact v31 colour bands:

Very High → pale red/pink
High → pale amber/yellow
Moderate → pale yellow/neutral
Low → pale green

Again: extract the actual colours from v31 CSS.

Do not eyeball new colours.

The metrics must be credit-relevant and measurable.

Examples can include, depending on the factor:

Debt / EBITDA
EBITDA Interest Coverage
Cash Flow Available for Debt Service / Total Debt Service
Organic Revenue Growth
Net Revenue Retention
R&D Expense / Revenue
Product Concentration
Customer Churn
Incident Cost Ratio
Net CAC Ratio
Gross Margin
Liquidity Coverage
etc.

But DO NOT mechanically copy Software metrics into another sector.

Metrics must correspond to:
selected sector + selected factor.

============================================================
18. FORMULAS ARE PART OF THE BUSINESS DESIGN
============================================================

Where v31 contains Metric / Formula, retain formulas.

Examples:

Total Debt / EBITDA

EBITDA / Cash Interest Expense

Cash Available for Debt Service / Total Debt Service

Annual Recurring Revenue / Total Revenue

etc.

These formulas matter because Step 2.5 needs a measurable framework.

Do not reduce the table to vague qualitative descriptions.

============================================================
19. THRESHOLDS
============================================================

Severity bands need meaningful numerical or qualitative thresholds.

Example concept:

Debt / EBITDA

Very High: > 9.0x
High: > 7.0x to 9.0x
Moderate: > 5.0x to 7.0x
Low: <= 5.0x

The actual thresholds must be appropriate to the factor and sector.

Do not blindly use these numbers universally.

Preserve currently approved values where they already exist.

Do not silently rewrite existing sector thresholds merely because you
would choose different numbers.

============================================================
20. CRITICAL THRESHOLD STRIP
============================================================

Below Set 1, v31 contains a narrow orange/pale-red strip:

Critical threshold (AND):
...

Replicate the strip exactly:

- height,
- border,
- background,
- text size,
- label emphasis,
- margins.

This is important analytical logic.

It identifies combinations of vulnerability conditions representing
severe credit stress.

For example, conceptually:

high leverage
AND
weak coverage
AND
weak CFADS

may trigger the most severe sector score.

Preserve the actual approved condition logic.

============================================================
21. SET 2 — BUFFER METRICS
============================================================

Next:

BUFFER METRICS (SET 2)

This is NOT optional decoration.

Sector credit risk cannot be assessed only through vulnerabilities.

Step 2.4 explicitly balances:

VULNERABILITY
versus
BUFFER / MITIGANT

The v31 columns are conceptually:

Metric / Formula
STRONG
MODERATE
WEAK
NEGLIGIBLE

Colour treatment:

Strong → green
Moderate → neutral/light
Weak → amber/yellow
Negligible → red/pink

Replicate exactly from v31 CSS.

Possible buffer metrics depend on factor, e.g.:

- recurring revenue proportion,
- unrestricted cash / interest expense,
- gross revenue retention,
- weighted-average debt maturity,
- cyber insurance coverage,
- security investment ratio,
- breach recovery speed,
- liquidity coverage,
- customer diversification,
- contractual backlog,
- pricing power,
- recovery value.

Again:

DO NOT copy metrics mechanically across sectors.

============================================================
22. KEY PRINCIPLE STRIP
============================================================

Below buffer metrics, v31 contains a pale-green:

Key Principle:

statement.

Preserve it visually and functionally.

This is a concise explanation of which buffers are most credit
protective and WHY.

Example concept:

high recurring revenue visibility, strong retention and long debt
maturity provide the strongest protection because they stabilize
cash-flow generation while reducing refinancing pressure.

The principle should add analytical reasoning, not repeat table values.

============================================================
23. SCORING LOGIC (1–5)
============================================================

This is another critical component.

Header:

SCORING LOGIC (1–5)

The table must contain:

Score
Vulnerability Profile
Buffer Profile

Rows:
5
4
3
2
1

Replicate v31 exactly.

Visual treatment:

Score column:
dark/navy header treatment.

Vulnerability Profile:
pale yellow/amber header.

Buffer Profile:
pale green header.

Maintain:
- column widths,
- row heights,
- typography,
- borders,
- cell padding,
- textarea/input framing where applicable.

Do not replace this with:
- cards,
- badges,
- progress bars,
- gauges.

The v31 table is the accepted design.

============================================================
24. SCORE MEANING
============================================================

Scoring logic should conceptually mean:

5 = strongest vulnerability / weakest protection
4 = high vulnerability
3 = moderate
2 = low/moderate
1 = lowest vulnerability and/or strongest buffers

But preserve the actual approved Step 2.4 scoring rule.

The vulnerability profile and buffer profile must work TOGETHER.

Do not assign score purely from one metric.

============================================================
25. NET SCORE NOTE
============================================================

Below the scoring table, retain the small explanatory note if present,
for example:

Net Score = Raw Vulnerability Score − Buffer Credit ...

or whatever rule exists in the approved current implementation.

DO NOT invent a different calculation.

Inspect existing code / v31.

UI display and actual calculation must agree.

============================================================
26. CREDIT IMPLICATION
============================================================

Then:

CREDIT IMPLICATION

v31 shows this as another pale-green framed statement.

Replicate exactly.

This is where the factor is translated into credit language.

It should explain potential impact on:

- debt-service capacity,
- liquidity,
- refinancing,
- covenant headroom,
- leverage,
- enterprise value,
- default risk,
- recovery,
- free cash flow,
- rating migration,

depending on the factor.

This is essential.

Do not let the section become generic business commentary.

============================================================
27. REMAINING FACTORS
============================================================

After RF1, show RF2-RF5 as collapsed accordion items exactly like v31.

Example visual sequence in reference:

RF1 expanded
RF2 collapsed
RF3 collapsed
RF4 collapsed
RF5 collapsed

When another factor is expanded, its detail layout must be identical.

Each factor needs its own:

- Factor Narrative
- Factor Importance
- Importance Justification
- Vulnerability Metrics Set 1
- Critical Threshold
- Buffer Metrics Set 2
- Key Principle
- Scoring Logic 1–5
- Credit Implication

Do NOT produce a detailed RF1 and shallow RF2-RF5.

All five must use the same schema.

============================================================
28. COMPOSITE REFERENCE SCORE NOTE
============================================================

Near the bottom, v31 contains a note conceptually similar to:

Composite reference score: X/5 independently identifies 4–5
structural sector-inherent factors from [LM2/LM3] using approved
enterprise research, then applies deterministic importance, weighting
and buffer-credit arithmetic. Issuer scoring remains downstream.

Preserve the intended concept.

Most important sentence:

ISSUER SCORING REMAINS DOWNSTREAM.

Step 2.4 should NOT start scoring Salesforce, Apple, Microsoft,
Volkswagen, etc.

That belongs to Step 2.5.

Step 2.4 creates the SECTOR benchmark/framework.

============================================================
29. BOTTOM ACTION BUTTONS
============================================================

Replicate the v31 footer actions exactly.

Existing reference includes:

Save All Changes

Generate Sector Factors

Confirm All Sector Risk Factors →

Match:

- order,
- horizontal alignment,
- size,
- spacing,
- border radius,
- font,
- colours,
- hover states,
- disabled states.

Do NOT redesign them.

“Confirm All Sector Risk Factors” should visually remain the primary
blue action.

============================================================
30. CONFIRMATION BEHAVIOUR
============================================================

Confirmation must preserve workflow semantics.

When confirmed:

- Step 2.4 state becomes confirmed/complete.
- workflow status updates appropriately.
- Step 2.5 becomes available according to the existing sequence.
- confirmed sector-factor data remains available downstream.

Do not merely change button colour without preserving application state.

============================================================
31. FEEDBACK PANEL
============================================================

Keep the Step 2.4-specific feedback panel at the bottom.

Reference concept:

Feedback to Sector-Inherent Risk Factor Agent

with:
- input area,
- Send button,
- Clear control if present.

Feedback must remain associated specifically with Step 2.4.

Do not merge it with Step 2.3 or global feedback.

Keep v31:
- dimensions,
- border,
- spacing,
- typography,
- send-button styling.

============================================================
32. WORKFLOW STATUS — RIGHT PANEL
============================================================

Preserve the exact v31 right-side Workflow Status area.

It should correctly show progression such as:

Risk Narrative Intake
Scenario & Assumptions
Portfolio Selection
Event-driven Risk Factors
Sector-Inherent Factors
Name Level Assessment
Portfolio Assessment

Step 2.4 must properly transition between:

In Progress
and
Confirmed / Completed

according to existing workflow logic.

Do NOT fake completion in the UI.

============================================================
33. MOST IMPORTANT DATA-LINEAGE RULE
============================================================

Do not allow Step 2.4 to become disconnected from earlier steps.

Sequence must remain:

STEP 1
provides the risk narrative / event context.

STEP 2.1
provides scenario and shock assumptions.

STEP 2.2
determines which portfolio / names / sectors are in scope.

STEP 2.3
defines event-driven transmission channels.

STEP 2.4
defines the structural sector vulnerability framework.

STEP 2.5
combines the selected company evidence with the Step 2.3 event
framework and Step 2.4 sector framework to assess the NAME.

This distinction is fundamental.

============================================================
34. STEP 2.4 SHOULD NOT BE CONTAMINATED BY STEP 2.3
============================================================

Do not generate sector factors by merely paraphrasing the currently
selected event.

For example, if Step 1 is about tariffs:

BAD Step 2.4:
- Tariff Risk
- Tariff Revenue Risk
- Tariff Supply Chain Risk
- Tariff Margin Risk
- Tariff Refinancing Risk

That is Step 2.3 logic.

GOOD Step 2.4 for a software sector could remain structural:

- sponsor-backed leverage,
- technology disruption,
- FCF compression,
- refinancing concentration,
- demand/customer cyclicality,

even if the current event is unrelated.

The point is to establish the sector's structural susceptibility.

============================================================
35. STEP 2.4 SHOULD PREPARE STEP 2.5
============================================================

Every factor should be sufficiently structured so that Step 2.5 can
eventually take issuer evidence and determine:

- actual metric value,
- vulnerability band,
- buffer band,
- raw vulnerability score,
- buffer credit,
- net factor score,
- evidence/source,
- rationale,
- resulting credit implication.

Therefore Step 2.4 MUST retain measurable metric definitions and
thresholds.

Do not simplify it into narrative-only AI output.

============================================================
36. DO NOT FABRICATE COMPANY DATA
============================================================

Step 2.4 is sector-level.

It therefore should not need to fabricate issuer financials.

Do not populate illustrative issuer values and present them as facts.

Actual company data belongs to Step 2.5 and must come from the
approved evidence/data path.

============================================================
37. VISUAL COMPARISON METHOD
============================================================

Do not claim “v31 aligned” after a superficial CSS pass.

Perform a side-by-side comparison:

CURRENT STEP 2.4
versus
V31 STEP 2.4

Inspect at least:

PAGE
- content width
- sidebar width
- margins
- vertical rhythm

SECTOR BAR
- height
- dropdown width
- colours
- radius

SUMMARY TABLE
- column widths
- header bands
- row heights
- padding
- borders
- text alignment

FACTOR HEADER
- height
- icon
- title
- subtitle
- importance
- chevron

NARRATIVE
- textarea dimensions
- padding
- line height

IMPORTANCE
- buttons
- spacing

JUSTIFICATION
- green box height
- padding

SET 1
- header bands
- column widths
- row heights
- metric/formula arrangement
- threshold cells

CRITICAL THRESHOLD
- strip dimensions

SET 2
- header colours
- widths
- rows

KEY PRINCIPLE
- strip dimensions

SCORING TABLE
- score column width
- vulnerability column width
- buffer column width
- row heights

CREDIT IMPLICATION
- box dimensions

COLLAPSED FACTORS
- heights
- spacing
- borders

BOTTOM BUTTONS
- dimensions
- placement

FEEDBACK
- width
- textarea/input height
- send button

RIGHT SIDEBAR
- width
- alignment
- status styling

Fix mismatches individually.

============================================================
38. DO NOT USE SCREENSHOTS AS AN EXCUSE FOR APPROXIMATION
============================================================

The supplied screenshots show the target, but the repository should
contain the actual v31 baseline.

Locate it.

Possible filenames/locations may contain terms such as:

v31
UI Design
step24
consolidated
reference
prototype

Do not assume the filename.

Search the repository.

Use v31's actual HTML/CSS as the authoritative source wherever it is
available.

============================================================
39. PRESERVE RESPONSIVENESS WITHOUT CHANGING DESKTOP TARGET
============================================================

The screenshots represent the primary desktop target.

Match that first.

Do not alter desktop proportions in pursuit of a new responsive design.

If existing responsiveness already works, preserve it.

Do not add an elaborate mobile implementation for this POC unless
required to prevent breakage.

============================================================
40. DO NOT CHANGE OTHER STEPS' VISUALS
============================================================

This task is Step 2.4 only.

Do not “standardize” Step 2.1, Step 2.2, Step 2.3 or Step 2.5 as part
of this work.

If shared CSS must be touched, ensure the selector scope does not
change those screens.

Prefer Step 2.4-specific selectors where required.

============================================================
41. BACKEND CHANGES
============================================================

Do not change backend logic merely because the UI can be improved.

Backend changes are allowed ONLY if you identify a concrete Step 2.4
functional defect such as:

- factor count incorrect,
- weights not summing to 100,
- wrong sector being passed,
- state not persisting,
- confirmation broken,
- details missing because parser drops fields,
- Step 2.5 cannot access confirmed Step 2.4 output.

If no such defect exists:
leave backend alone.

============================================================
42. DATA MODEL CONSISTENCY
============================================================

For each RF, verify that the data model can preserve all fields needed
by the v31 design.

Conceptually:

rf_id
factor_name
importance
importance_score
weight

factor_narrative
importance_justification

vulnerability_metrics[]
    metric
    formula
    very_high
    high
    moderate
    low

critical_threshold

buffer_metrics[]
    metric
    formula
    strong
    moderate
    weak
    negligible

key_principle

scoring_logic[]
    score
    vulnerability_profile
    buffer_profile

credit_implication

Do NOT blindly replace the current schema with these names.

First inspect the existing schema and map existing fields.

Only add a missing field when genuinely required.

============================================================
43. QUALITY STANDARD FOR GENERATED FACTORS
============================================================

Do not accept shallow factor generation.

A high-quality RF should satisfy all of these:

1. Sector-specific.
2. Credit-specific.
3. Structurally persistent.
4. Distinct from other RFs.
5. Measurable.
6. Provides vulnerability indicators.
7. Provides buffer indicators.
8. Has coherent score bands.
9. Has a defensible credit transmission mechanism.
10. Can be applied downstream to an issuer.

Reject generic factors that fail this test.

============================================================
44. EXAMPLE OF THE EXPECTED ANALYTICAL DEPTH
============================================================

For illustration only — preserve actual approved content:

Factor:
Structural Leverage Intensity in Sponsor-Backed Software

Narrative:
Sponsor-backed software issuers may operate at structurally higher
leverage levels because recurring revenue and predictable cash flows
support debt capacity. This leaves less debt-service headroom when
revenue growth weakens, margins compress or interest expense rises.

Vulnerability metrics:
- Debt / EBITDA
- EBITDA Interest Coverage
- CFADS / Debt Service

Buffer metrics:
- recurring revenue share
- unrestricted cash / interest
- gross retention
- weighted-average debt maturity

Scoring logic:
high leverage + weak coverage + weak CFADS → severe vulnerability;
strong recurring revenue + liquidity + long maturity → buffer credit.

Credit implication:
persistent leverage reduces capacity to absorb operating deterioration
and increases refinancing / covenant / liquidity sensitivity.

THIS is the required level of reasoning.

Do not use this example as a hard-coded answer.

============================================================
45. EXACT VISUAL PRIORITY
============================================================

When a conflict exists between:

A. current Step 2.4 visual design
and
B. v31 visual design

v31 wins.

When a conflict exists between:

A. v31 visual design
and
B. working current Step 2.4 functional logic

DO NOT destroy the functional logic.

Instead:
apply the v31 presentation on top of the working logic.

The desired result is:

V31 PRESENTATION
+
CURRENT WORKING FUNCTIONALITY
+
CORRECT STEP 2.4 BUSINESS PURPOSE.

============================================================
46. TEST THE REAL WORKFLOW
============================================================

After implementation, execute a real Step 2.4 workflow.

Do not validate only static rendering.

At minimum verify:

1. Load application.
2. Reach Step 2.4 through the existing workflow.
3. Sector from Step 2.2 is correctly represented.
4. Five RFs appear.
5. Summary table is populated.
6. Weights total 100%.
7. Expand RF1.
8. Narrative visible.
9. Importance visible.
10. Importance justification visible.
11. Vulnerability Set 1 visible.
12. Critical threshold visible.
13. Buffer Set 2 visible.
14. Key Principle visible.
15. Scoring Logic 1–5 visible.
16. Credit implication visible.
17. Collapse RF1.
18. Expand RF2.
19. Verify same detailed structure.
20. Repeat enough to ensure RF1-RF5 are all populated.
21. Save changes if supported.
22. Confirm all sector risk factors.
23. Verify Step 2.4 status changes correctly.
24. Verify downstream Step 2.5 can access the confirmed Step 2.4 state.
25. Reload/revisit and ensure state has not silently disappeared if
    persistence is expected by current design.

============================================================
47. VISUAL ACCEPTANCE TEST
============================================================

At the end, compare the implementation against v31 at normal desktop
zoom.

I should NOT see obvious differences in:

- page proportions,
- section positions,
- table widths,
- table heights,
- colours,
- header bands,
- borders,
- row heights,
- accordion framing,
- textarea framing,
- typography hierarchy,
- spacing,
- buttons,
- feedback section,
- right workflow sidebar.

I am deliberately asking for replication at the smallest practical
design-detail level.

“Similar”
“inspired by”
“close”
“same general structure”

are NOT acceptance criteria.

The target is:

AS CLOSE TO V31 AS THE EXISTING APPLICATION STRUCTURE PRACTICALLY
ALLOWS.

============================================================
48. PARTICULAR DIFFERENCE TO AVOID
============================================================

Do not produce the simplified implementation where Step 2.4 becomes:

Factor name
Importance
Weight
one narrative
one small table

That loses the original v31 analytical design.

The v31 structure is deliberately richer:

SUMMARY
↓
FACTOR NARRATIVE
↓
IMPORTANCE
↓
IMPORTANCE JUSTIFICATION
↓
VULNERABILITY METRICS
↓
CRITICAL THRESHOLD
↓
BUFFER METRICS
↓
KEY PRINCIPLE
↓
SCORING LOGIC
↓
CREDIT IMPLICATION

Preserve this hierarchy.

============================================================
49. WHAT NOT TO TOUCH
============================================================

DO NOT:

- redesign the app,
- create a new frontend,
- replace v31 styling conventions,
- refactor all CSS,
- modify Stylus presets,
- create or edit a Stylus preset,
- investigate preset UUIDs,
- change Step 2.5 Runner architecture,
- change SEC/Web implementation,
- add fake issuer data,
- replace working APIs,
- rename unrelated endpoints,
- restructure repository folders,
- introduce a new framework.

The VS Code agent does not manage Stylus presets.

Preset changes are manual and belong to the user.

============================================================
50. IMPLEMENTATION FIRST — NO LONG AUDIT
============================================================

Do not spend the task producing a large speculative audit.

Quickly inspect:

1. current Step 2.4,
2. v31 Step 2.4,
3. current data/state wiring,

then implement.

If you find a concrete discrepancy, fix it.

Do not stop and ask me whether you should fix each discrepancy.

Proceed.

============================================================
51. FINAL OUTPUT REQUIRED FROM YOU
============================================================

When complete, provide a concise implementation report containing:

A. FILES CHANGED
Exact paths.

B. VISUAL CHANGES
What was changed to reproduce v31.

C. FUNCTIONAL CHANGES
Only actual Step 2.4 functional fixes.

D. BUSINESS-LOGIC VALIDATION
Confirm:
- 5 factors,
- weights reconcile to 100%,
- sector correctly inherited,
- vulnerability + buffer framework retained,
- scoring logic retained,
- confirmation works,
- Step 2.5 receives/retains Step 2.4 output.

E. TEST RESULT
Actual test performed and result.

F. REMAINING GENUINE DIFFERENCES FROM V31
List any, however small.

Do NOT say “matches v31” if visible discrepancies remain.

============================================================
52. STOP CONDITION
============================================================

The task is complete only when:

[ ] Step 2.4 remains functionally working.
[ ] Step 2.4 preserves its sector-credit purpose.
[ ] It is distinct from Step 2.3 event-driven logic.
[ ] Five high-quality structural RFs are represented.
[ ] Weights reconcile to 100%.
[ ] Every RF has the complete v31 analytical structure.
[ ] Vulnerability metrics are preserved.
[ ] Buffer metrics are preserved.
[ ] Critical thresholds are preserved.
[ ] Scoring logic 1–5 is preserved.
[ ] Credit implications are preserved.
[ ] Confirmation/state propagation works.
[ ] Step 2.5 can consume the confirmed framework.
[ ] Step 2.4 visually reproduces v31 at component/table/detail level.
[ ] No working unrelated functionality was broken.
[ ] No unnecessary architecture/refactoring was introduced.

IMPLEMENT THIS NOW.
Do not merely explain how you would implement it.
Inspect the repository, modify the existing implementation, run the
workflow, compare against v31, correct remaining discrepancies, and
finish the complete Step 2.4 acceptance test.
