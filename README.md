RPR STEP 2.5 — EXACT V31 FRONTEND RECONSTRUCTION
IMPLEMENTATION ONLY — NO REPORTS, NO APPROVAL QUESTIONS

THIS IS NOT A DESIGN EXERCISE.

THE REQUIRED RESULT IS:

STEP 2.5 IN THE ACTIVE step23.html MUST LOOK AND BEHAVE AS CLOSE TO
IDENTICAL TO v31 AS THE EXISTING SOURCE ALLOWS.

DO NOT "IMPROVE" v31.
DO NOT INTERPRET v31.
DO NOT MAKE SOMETHING "INSPIRED BY" v31.
DO NOT CREATE YOUR OWN UI.

READ THE ACTUAL v31 HTML + CSS + JAVASCRIPT AND REUSE ITS STRUCTURE.

============================================================
0. AUTONOMY / EXECUTION RULE
============================================================

Do not ask me:

- whether you should proceed;
- whether a CSS rule should be copied;
- whether an existing Step 2.5 component should be replaced;
- whether a small implementation decision is acceptable.

Everything required by this scope is PRE-APPROVED.

Proceed autonomously until the final manual-browser-test state is ready.

Do not stop for intermediate reports.

Do not give me a design analysis before implementation.

You may inspect as much source as necessary, regardless of file size.

The rule is:

READ FULL RELEVANT v31 IMPLEMENTATION
→ UNDERSTAND EXACT STRUCTURE
→ IMPLEMENT
→ TEST
→ FIX
→ CONTINUE.

Do not shortcut the source inspection because the file is large.

============================================================
1. AUTHORITATIVE FILES
============================================================

ACTIVE APPLICATION:

UI Design/step23.html

and its existing associated files such as:

UI Design/rpr_step25_append.js
UI Design/rpr_step25_append.css

or the actual current Step 2.5 JS/CSS files discovered in the project.

AUTHORITATIVE VISUAL/FUNCTIONAL REFERENCE:

UI Design/icm-pm-rapid-portfolio-review-v31.html

If v31 references external/local CSS or JS files, inspect those too.

Do not inspect only screenshots.

Before editing Step 2.5:

READ the entire relevant v31 Step 2.5 DOM subtree.

READ every CSS selector/classes/variables that affect that subtree.

READ every JS function/event handler responsible for:

- Step 2.5 rendering;
- row expansion;
- Factor Assessment Commentary expansion;
- Run Assessment;
- assessment-type selection;
- score/rating badges;
- commentary controls;
- impact override;
- confirm assessment;
- export;
- filters/table behavior.

Trace dependencies if the relevant functions live elsewhere in v31.

Do not begin visual implementation until this is understood.

============================================================
2. GOLDEN RULE — COPY v31, DO NOT RECREATE IT
============================================================

Where technically possible:

REUSE THE ACTUAL v31:

- HTML hierarchy;
- class names;
- CSS declarations;
- spacing;
- padding;
- borders;
- font sizes;
- font weights;
- line heights;
- table layout;
- column widths;
- header heights;
- badge shapes;
- border radii;
- background colors;
- text colors;
- button sizes;
- select/input styling;
- expand/collapse styling;
- hover states;
- section labels;
- alignment;
- responsive/horizontal-scroll behavior.

DO NOT eyeball values.

DO NOT invent approximations such as:

"similar blue"
"close green"
"roughly 12px"
"something like v31".

If v31 defines an exact value, COPY THAT VALUE.

If v31 uses an existing CSS class, use that class or copy the exact rule
into the current active stylesheet if required.

No new color palette.

No new design tokens unless technically unavoidable.

No large decorative gradients.

No giant colored status cards.

No random green/blue panels.

No newly invented Step 2.5 visual language.

============================================================
3. CURRENT step23 STEP 2.5 IS NOT THE BASELINE
============================================================

The current Step 2.5 rendering has drifted significantly.

Do NOT preserve current UI merely because code already exists.

Preserve the WORKING DATA/EXECUTION CONNECTIONS.

The rendering structure may be replaced with the exact v31 structure.

Separate:

BACKEND / DATA WIRING = preserve.

CURRENT STEP23 VISUAL STRUCTURE = not authoritative.

v31 VISUAL STRUCTURE = authoritative.

============================================================
4. REMOVE NON-v31 BUSINESS UI
============================================================

The following current inventions must NOT remain as primary Step 2.5
workflow elements unless they actually exist in v31.

A. COMPANY DROPDOWN

The normal Step 2.5 workflow must NOT ask the analyst to choose one
company again.

Step 2.5 automatically inherits the CONFIRMED Step 2.2 portfolio.

Do not require a second company selection.

A company-specific developer/debug control may remain hidden behind
technical diagnostics if genuinely necessary, but it must not appear as
normal business workflow.

B. QUICK SEC SCAN

The visible "Quick SEC Scan" column/workflow was introduced as a token /
execution workaround.

It is NOT part of the v31 business design.

Remove it from the normal Step 2.5 table/UI.

If an identity/preflight check is technically useful, perform it
internally in the backend/orchestration layer.

The user should not have to understand or operate "Quick Scan."

C. EXTRA STATUS CARDS / COLORFUL PANELS

If they are not in v31, remove them from the normal Step 2.5 presentation.

Technical diagnostics may remain collapsed and unobtrusive.

============================================================
5. PORTFOLIO WORKFLOW MUST MATCH THE ORIGINAL FUNCTIONAL DESIGN
============================================================

Step 2.2 determines the portfolio.

Therefore:

Step 2.2 confirmed portfolio
→ same companies automatically appear in Step 2.5.

No reselection.

If Step 2.2 selected:

7 companies

Step 2.5 shows those same 7 companies.

If Step 2.2 selected:

27 companies

Step 2.5 shows those same 27 companies.

The user clicks ONE portfolio-level:

RUN ASSESSMENT

button as in v31.

============================================================
6. MAXIMUM 10-COMPANY RULE — INTERNAL EXECUTION ONLY
============================================================

Leslie's requirement:

SEC assessment quality deteriorates if too many companies are handled
together.

Therefore the POC must process a MAXIMUM OF 10 companies per logical
execution batch.

This is NOT a UI portfolio limit.

This is NOT a company-picker requirement.

Example:

27 selected companies:

batch 1 = companies 1–10
batch 2 = companies 11–20
batch 3 = companies 21–27

The Step 2.5 UI continues to display all 27 portfolio rows.

Execution orchestration handles batching behind the scenes.

Do not display a new "batch configuration" interface.

A small non-intrusive running status may say:

Assessing companies 1–10 of 27

if useful.

Do not transform the page around batching.

============================================================
7. MAIN STEP 2.5 COMPANY TABLE — USE v31 EXACTLY
============================================================

Locate the exact v31 Step 2.5 table.

Reuse its:

- table element/container;
- header structure;
- column sequence;
- widths;
- sticky/horizontal behavior;
- filters;
- row height;
- company expansion control;
- colors;
- typography;
- borders.

Do NOT redesign the table.

Populate it from REAL data.

Use the EXACT v31 column names/order discovered from the source.

The screenshots indicate fields equivalent to:

COMPANY NAME
CAGID
TICKER / ID
REL COUNTRY OF RISK
LIMIT INDUSTRY L1
LIMIT INDUSTRY L2
LIMIT INDUSTRY L3
TOTAL OSUC
OSUC-P
OSUC-PWL
OSUC-SM
OSUC-SS
OSUC-D/L
ED SCORE (80%)
SI SCORE (20%)
COMPOSITE SCORE
RESIDUAL RATING
CREDIT IMPACT RATING
CURRENT RRR
REC. RRR ACTION
CURRENT CLASS
REC. CLASS ACTION
KEY RISK DRIVER
IMPACT RATING OVERRIDE
USER CREDIT COMMENTARY

BUT:

DO NOT use this list as authority if the actual v31 source differs.

The ACTUAL v31 markup is authoritative.

============================================================
8. ED 80% AND SI 20% MUST BE VISIBLE EXACTLY LIKE v31
============================================================

This is currently badly represented in step23.

Restore the v31 information hierarchy.

Inside the expanded company row there must be a compact factor-summary
area corresponding to:

EVENT-DRIVEN FACTORS (80%)

and

SECTOR-INHERENT FACTORS (20%)

These are separate factor families.

Do NOT merge them.

Do NOT hide the 80% / 20% meaning.

Do NOT dump detailed narratives here.

This layer should be compact.

Each factor should show the information v31 shows at this level:

- factor identifier/name;
- compact score;
- impact/risk indicator where v31 has one.

Use the exact v31 design and classes.

============================================================
9. FACTOR WEIGHTING
============================================================

The business methodology is:

Within EVENT-DRIVEN factors:

preserve the confirmed Step 2.3 individual weights.

Within SECTOR-INHERENT factors:

preserve the confirmed Step 2.4 individual weights.

Each complete factor family should normally represent its full 100%
allocation according to the upstream methodology.

Do not invent weights to force 100%.

Use normalized weighted scoring if needed:

ED_SCORE =
SUM(ED factor score × ED supplied weight)
/
SUM(ED supplied weights)

SI_SCORE =
SUM(SI factor score × SI supplied weight)
/
SUM(SI supplied weights)

THEN:

COMPOSITE_SCORE =
ED_SCORE × 0.80
+
SI_SCORE × 0.20

Do NOT incorrectly treat all ED + SI individual factors as one combined
100% factor basket.

============================================================
10. OVERALL COMPOSITE SCORE DETAILS — RESTORE IT
============================================================

This is an important v31 feature currently missing/wrong in step23.

Find the exact v31 component/markup that displays the overall/composite
assessment explanation.

Restore it EXACTLY.

Its job is to explain the combined Step 2.5 assessment at company level,
including whatever v31 presents such as:

- Overall assessment;
- Composite Score;
- overall impact/rating;
- concise synthesis;
- key driver / why the final outcome is what it is.

DO NOT replace this with generic raw:

Narrative
Risk Direction
Supporting Evidence
Disconfirming Evidence
Evidence Gaps
Analyst Questions

cards.

Map the available real Step 2.5 fields into the exact v31 Overall /
Composite Score Details presentation.

If one model field has no exact v31 location:

do not invent a new large panel.

Place it only in the most appropriate existing v31 commentary/evidence
area.

============================================================
11. FACTOR ASSESSMENT COMMENTARY — COLLAPSED BY DEFAULT
============================================================

This is another critical v31 behavior.

The detailed factor narratives must NOT be permanently dumped into the
expanded company row.

Restore the exact v31:

FACTOR ASSESSMENT COMMENTARY

control.

By default:

DETAILED FACTOR COMMENTARY IS COLLAPSED.

The user clicks:

Factor Assessment Commentary

to expand it.

Use the exact v31:

- label;
- icon/chevron;
- border;
- background;
- typography;
- padding;
- expand/collapse animation/behavior if present;
- open/closed state styling.

Do not invent a new accordion.

Reuse v31.

============================================================
12. CONTENT INSIDE FACTOR ASSESSMENT COMMENTARY
============================================================

When expanded, reproduce the exact v31 hierarchy.

First:

EVENT-DRIVEN FACTORS

Then:

SECTOR-INHERENT FACTORS

For each factor, render the detailed Step 2.5 content in the same pattern
as v31.

The screenshots show a structure similar to:

RF / SI-RF factor name
Score
Impact

Vulnerability:
<detailed explanation>

Buffer:
<mitigants / strengths / offsetting factors>

then compact status badges/labels where v31 provides them.

DO NOT dump one giant JSON rationale string.

Map the real Step 2.5 factor fields into:

FACTOR TITLE
SCORE
IMPACT
VULNERABILITY
BUFFER / MITIGANT
COMMENTARY / SUPPORTING DETAIL

according to the actual v31 source.

If the current backend factor output does not separately provide
Vulnerability and Buffer but the Step 3a methodology/prompt produces
them inside structured assessment content:

map them correctly.

If the current schema genuinely lacks required v31 fields:

make the MINIMUM additive backend/schema mapping necessary to preserve
those already-produced model fields.

Do NOT redesign the analytical methodology.

============================================================
13. STEP 3a FINANCIAL FACTOR CONTENT
============================================================

The final Step 2.5 details should reflect the real original
Factor Analysis — Financials methodology.

Relevant categories observed in v31/demo include concepts such as:

- Earnings & Cash Flow Resilience;
- Liquidity & Short-Term Funding;
- Leverage & Debt Service Capacity;
- Capital / tangible-equity resilience;
- refinancing / maturity pressure;
- other confirmed Event-Driven/Sector-Inherent factors.

Do NOT hardcode those example factor names.

Use the actual confirmed Step 2.3 and Step 2.4 factors.

The UI layout is static v31.

The factor content is dynamic RPR data.

============================================================
14. COLORS — COPY v31 EXACTLY
============================================================

The current Step 2.5 color treatment is unacceptable.

Do NOT manually pick colors based on interpretation.

Read the actual v31 CSS.

Identify exact styles for:

- table header background;
- table header text;
- normal body text;
- muted text;
- row backgrounds;
- expanded row;
- section headings;
- green / low badges;
- amber / medium badges;
- red / high badges;
- score cells;
- credit impact cells;
- RRR action labels;
- class action labels;
- analyst override select;
- buttons;
- borders;
- hover states;
- disabled states;
- commentary expansion.

COPY those exact declarations.

If v31 uses CSS variables, reuse them.

If it uses hex/rgb values, copy them.

Do not create:

new teal
new blue
new bright green
new gradients
new shadows
new badge palette.

No visual experimentation.

============================================================
15. TYPOGRAPHY / SPACING — COPY v31
============================================================

Read exact v31 values for:

font-family
font-size
font-weight
line-height
letter spacing if any
text-transform
padding
margin
row height
section gap
cell padding
border widths
radius
button height
select height.

Use them.

Do not estimate from screenshot.

============================================================
16. IMPACT RATING OVERRIDE
============================================================

Restore the exact v31 analyst control.

The screenshots show options equivalent to:

Low Impact
Medium Impact
High Impact

Use the exact options/labels found in v31.

This is ANALYST OWNED.

Do not automatically overwrite this field with the model's
credit_impact_rating.

The model result may provide the AI assessment.

Impact Rating Override remains human input.

============================================================
17. USER CREDIT COMMENTARY
============================================================

Restore the exact v31 field.

Keep it editable by the analyst.

Do not automatically replace analyst commentary with model narrative.

Persist/reuse existing value according to the existing application logic.

============================================================
18. RRR / CLASSIFICATION / CREDIT ACTION
============================================================

Populate the corresponding v31 columns from REAL Step 2.2 + Step 2.5
data.

Where Step 2.2 supplies:

Current RRR
Current Class

display them.

Where Step 2.5 legitimately returns:

Recommended RRR Action
Recommended Class Action

display them.

Do not fabricate missing current values.

Do not hide available values because current mapping forgot them.

============================================================
19. OSUC / PORTFOLIO INFORMATION
============================================================

Step 2.5 should retain the portfolio information the manager showed.

Inspect actual Step 2.2 source fields.

Map real available:

CAGID
company name
country/full country name
industry L1/L2/L3
Total OSUC
OSUC-P
OSUC-PWL
OSUC-SM
OSUC-SS
OSUC-D/L
MLE if present
RRR
classification
other real relevant fields.

Do not manufacture unavailable data.

Do not add huge textual "Not supplied by Step 2.2..." blocks that distort
the table.

Use the same compact blank/unavailable presentation convention as v31.

============================================================
20. RUN ASSESSMENT — EXACT USER EXPERIENCE
============================================================

There is ONE normal portfolio-level:

RUN ASSESSMENT

button in the v31 location.

No normal company dropdown.

No normal Quick Scan control.

Clicking Run Assessment:

1. reads confirmed Step 2.2 portfolio;
2. validates confirmed 2.3/2.4;
3. builds mini-batches max 10;
4. executes the already-working company-level Step 2.5 unit;
5. persists results independently;
6. progressively populates the existing table rows;
7. continues automatically until all selected companies are completed or
   individually failed.

No user confirmation between companies/batches.

No approval prompts.

No manual company reselection.

============================================================
21. RUNNING STATE
============================================================

Do not transform the UI during execution.

The table remains visible.

Each company may show a compact v31-consistent state such as:

Queued
Running
Complete
Failed

only if necessary and styled consistently with v31.

Do NOT add huge progress cards.

If showing batch status:

keep it subtle.

Example:

Assessing 11–20 of 27

No new visual workflow.

============================================================
22. PERFORMANCE — DO NOT SACRIFICE QUALITY
============================================================

Do not bring back a visible Quick Scan merely to avoid token expiry.

The maximum-10 batching is the manager-approved quality control.

Use existing bounded token/retry mechanisms invisibly.

Do NOT lower SEC/Web evidence quality merely to make the page finish fast.

But also do not unnecessarily serialize every internal operation if safe
bounded concurrency already exists or can be implemented minimally.

Any concurrency change must preserve:

- one independent company assessment;
- max-10 logical batch;
- evidence quality;
- Runner stability;
- deterministic persistence.

Do NOT make 10 uncontrolled concurrent Runner calls.

For this POC, correctness and demonstrability come before aggressive
performance optimization.

============================================================
23. PRESERVE ALL REAL STEP 2.5 RESULT DATA
============================================================

Do not throw away model output just because v31 displays it more compactly.

Persist:

factor assessments
weights
scores
impact
directions
vulnerability/buffer content where available
rationale
evidence
evidence gaps
analyst questions
credit conclusion
ED/SI/composite
ratings/actions.

DISPLAY only according to the v31 hierarchy.

Persistence richness != visual clutter.

============================================================
24. NO RAW MODEL-DUMP UI
============================================================

The following current pattern must disappear from the normal expanded row
unless v31 explicitly places it there:

NARRATIVE
RISK DIRECTION
SUPPORTING EVIDENCE
DISCONFIRMING EVIDENCE
EVIDENCE GAPS
ANALYST QUESTIONS

as giant always-visible blocks.

Do not delete underlying data.

Relocate it into the appropriate v31 commentary/detail/evidence section.

============================================================
25. STEP 2.4 VISUAL CONSISTENCY
============================================================

While touching shared styles, ensure Step 2.4 remains visually aligned with
v31.

Do NOT redesign Step 2.4.

Do not spend this task rebuilding it.

Only avoid introducing styles that make Step 2.4 diverge further.

============================================================
26. STRICT SOURCE-READ REQUIREMENT
============================================================

Before writing any Step 2.5 HTML/CSS/JS:

you MUST have inspected the relevant v31 implementation.

Do not write a replacement from memory.

Do not rely only on screenshots.

If an exact visual/detail question arises:

ANSWER IT BY READING v31 SOURCE.

Do not ask me.

Do not guess.

This includes tiny details such as:

which border color
which padding
which text size
whether a heading is uppercase
where chevrons sit
which side a score badge appears
whether a section starts collapsed
column widths
alignment
control heights
hover states.

READ THE SOURCE.

============================================================
27. IMPLEMENTATION STRATEGY
============================================================

Use this order:

PHASE 1
Read v31 Step 2.5 HTML/CSS/JS completely.

PHASE 2
Make a temporary internal structural map of:
- table;
- columns;
- expanded row;
- ED panel;
- SI panel;
- Overall Composite Details;
- Factor Assessment Commentary;
- detailed factors;
- controls;
- buttons.

Do not report it to me.

PHASE 3
Replace/refactor ONLY the current Step 2.5 presentation renderer to use
that v31 structure.

PHASE 4
Wire existing real backend Step 2.5 fields into it.

PHASE 5
Remove visible Quick Scan / company dropdown dependency.

PHASE 6
Connect portfolio-level Run Assessment batching.

PHASE 7
Test with static existing persisted assessment first to verify exact layout
without spending Runner tokens.

PHASE 8
Then execute ONE real SEC+Web UI test.

PHASE 9
Fix any actual render/data defects.

PHASE 10
Leave application ready for my manual test.

============================================================
28. VISUAL ACCEPTANCE — SCREENSHOT COMPARISON
============================================================

Before declaring completion:

open/render:

A. v31 Step 2.5
B. current step23 Step 2.5

Compare them side-by-side.

Check:

section positioning
table structure
header styling
column ordering
ED/SI summary
80/20 labels
Overall Composite Score Details
Factor Assessment Commentary
collapsed state
expanded state
factor-detail hierarchy
Vulnerability
Buffer
score badges
credit impact badges
RRR/classification/action controls
override select
commentary input
Run Assessment
Confirm Assessment
Export
feedback section
spacing
colors
borders
typography.

If a meaningful difference remains and v31 source provides the solution:

FIX IT.

Do not declare "close enough".

============================================================
29. BACKEND RULE
============================================================

The existing working SEC+Web backend / Stylus execution remains the
backbone.

Do not redesign it merely to implement frontend parity.

Only add mappings/fields where the real model already produces data needed
by the v31 structure.

No new assessment methodology.

No fake output.

============================================================
30. NO REPORTING / NO APPROVAL
============================================================

During implementation:

DO NOT stop for approval.

DO NOT send progress reports.

DO NOT produce design documents.

DO NOT ask me which style I prefer.

v31 answers the style question.

Continue autonomously.

============================================================
31. SUCCESS CONDITION
============================================================

Do not stop until:

STEP23_STEP25_STRUCTURE_MATCHES_V31 = PASS
STEP23_STEP25_COLORS_MATCH_V31 = PASS
STEP23_STEP25_TABLE_MATCHES_V31 = PASS
ED_80_PANEL = PASS
SI_20_PANEL = PASS
OVERALL_COMPOSITE_DETAILS = PASS
FACTOR_ASSESSMENT_COMMENTARY_COLLAPSED = PASS
FACTOR_ASSESSMENT_COMMENTARY_EXPANDED = PASS
VULNERABILITY_BUFFER_LAYOUT = PASS
RRR_CLASSIFICATION_CONTROLS = PASS
IMPACT_OVERRIDE = PASS
USER_COMMENTARY = PASS
NO_COMPANY_DROPDOWN_DEPENDENCY = PASS
NO_VISIBLE_QUICK_SCAN_WORKFLOW = PASS
PORTFOLIO_INHERITED_FROM_STEP22 = PASS
MAX_10_INTERNAL_BATCHING = PASS
REAL_STEP25_RESULT_RENDERING = PASS
RUN_ASSESSMENT = PASS

and:

READY_FOR_USER_UI_TEST = YES

============================================================
32. FINAL RESPONSE — MINIMAL ONLY
============================================================

When finished, do not write a long report.

Return only:

IMPLEMENTATION = PASS/FAIL
V31_VISUAL_PARITY = PASS/FAIL
ED_80_SI_20 = PASS/FAIL
OVERALL_COMPOSITE_DETAILS = PASS/FAIL
FACTOR_ASSESSMENT_COMMENTARY = PASS/FAIL
PORTFOLIO_AUTO_INHERIT = PASS/FAIL
QUICK_SCAN_REMOVED_FROM_UI = PASS/FAIL
COMPANY_DROPDOWN_REMOVED = PASS/FAIL
BATCHING_MAX_10 = PASS/FAIL
REAL_RESULT_MAPPING = PASS/FAIL
RUN_ASSESSMENT = PASS/FAIL
READY_FOR_USER_UI_TEST = YES/NO

If NO:
FIRST_REMAINING_BLOCKER=<one line>

No additional report.

START BY READING THE ACTUAL v31 STEP 2.5 SOURCE.
DO NOT WRITE ANY UI CODE UNTIL THAT SOURCE INSPECTION IS COMPLETE.
