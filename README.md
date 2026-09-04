STEP 2.4 FINAL ACCEPTANCE PASS — LIVE EXECUTION + V31 VISUAL PARITY

Continue from the Step 2.4 work you just completed.

DO NOT start another redesign.
DO NOT refactor.
DO NOT perform another broad audit.
DO NOT change backend/business logic unless a live test proves a concrete defect.

Your previous report is useful, but Step 2.4 is NOT yet accepted because you explicitly stated:

“Not yet exercised live in a browser…”

and you also identified at least one remaining potential v31 discrepancy:

“scoring-logic rows remain read-only in Step 2.4 while v31/Step2.3 render them as editable inputs/textareas.”

The purpose of this final pass is to EXECUTE the real workflow, compare the rendered Step 2.4 against the ACTUAL v31 Step 2.4 implementation, correct genuine visual discrepancies, and finish acceptance.

============================================================
1. ACTUAL V31 STEP 2.4 IS THE ONLY VISUAL AUTHORITY
============================================================

Do not use Step 2.3 as the visual authority.

Do not infer behaviour from another step.

Locate the actual v31 Step 2.4 code and compare CURRENT Step 2.4 against it directly.

The user requires replication at the smallest practical design-detail level.

Therefore determine definitively whether v31 Step 2.4 scoring-logic cells are:

- editable inputs/textareas,
or
- read-only presentation.

If v31 Step 2.4 uses editable controls, CURRENT Step 2.4 MUST use the same controls.

Replicate:
- control type,
- height,
- border,
- padding,
- font,
- width,
- row height,
- resize behaviour if applicable,
- focus state where applicable.

Do not leave the difference merely because data content is correct.

If v31 itself is read-only, leave current behaviour unchanged.

============================================================
2. VERIFY THE step23.html CHANGE
============================================================

You reported changing:

step23.html
- corrected the Step 2.4 formula banner text.

Verify why Step 2.4 requires this file modification.

If step23.html is genuinely the shared/current host containing the
Step 2.4 markup, retain the smallest necessary change.

If the modification accidentally changes Step 2.3 or is unnecessary
for Step 2.4:
REVERT IT.

Do not create regression in another step just to achieve Step 2.4
parity.

============================================================
3. RUN THE REAL APPLICATION
============================================================

Now actually run the backend/frontend using the project's existing
Windows execution method.

Do not create a new startup mechanism.

Use the current working application.

Navigate through the real workflow:

Step 1
→ Step 2.1
→ Step 2.2
→ Step 2.3
→ Step 2.4

Use an existing valid/confirmed workflow state if one is already
available.

If necessary, use the minimum existing actions needed to reach
Step 2.4.

DO NOT fabricate backend state.

============================================================
4. VERIFY SECTOR LINEAGE
============================================================

At Step 2.4 confirm that the sector displayed comes from the actual
Step 2.2 portfolio/sector selection.

Do not hard-code the sector shown in v31 screenshots.

Verify:

Step 2.2 selected sector
        ↓
Step 2.4 sector selector
        ↓
Step 2.4 generated/loaded sector factors

All three must agree.

============================================================
5. VERIFY EXACT FACTOR COUNT
============================================================

Rendered Step 2.4 must contain exactly:

RF1
RF2
RF3
RF4
RF5

Target = 5.

Verify visually and from application state.

No accidental sixth factor.
No hidden duplicate factor.
No stale factor from a previous sector.

============================================================
6. VERIFY TOP SUMMARY TABLE LIVE
============================================================

Check the rendered table against actual v31.

Columns:

RF
Factor
Importance
Imp. Score
Weight

Verify individually:

- complete table width
- each column width
- header height
- row height
- header background colours
- body backgrounds
- font size
- font weight
- vertical alignment
- horizontal alignment
- cell padding
- borders
- RF labels
- percentage formatting
- Importance values
- Imp. Score values
- weight values
- Total Weight presentation

Weights must reconcile to:

100.0%

Do not merely inspect the object in JavaScript.
Verify what the browser actually renders.

============================================================
7. VERIFY THE SECTOR HEADER STRIP
============================================================

Compare current rendered Step 2.4 to v31:

- navy sector strip height
- SECTOR label
- dropdown dimensions
- dropdown padding
- selected sector font
- factor-count chip
- chip position
- chip border/radius
- strip left/right margins

The factor count should visually follow the v31 convention.

============================================================
8. VERIFY INFORMATION / FORMULA BANNERS
============================================================

Confirm the Step 2.4 explanatory banner matches v31 visually and
semantically.

It must retain the correct Step 2.4 concept:

approved/reviewed sector taxonomy
+
deterministic importance/weights
+
issuer scoring downstream.

Do NOT restore inaccurate wording such as claiming the LLM regenerates
the taxonomy on every run if that contradicts the implemented design.

But visual dimensions must still follow v31:

- background
- left accent
- height
- padding
- font size
- margins

============================================================
9. VERIFY RF1 COMPLETELY
============================================================

Open RF1.

Compare every element against actual v31 Step 2.4.

HEADER:
- blue number/icon
- exact icon size
- title alignment
- title weight
- subtitle
- importance badge
- Net X/5 display if applicable
- expand/collapse chevron
- header height
- pale-blue treatment
- borders

FACTOR NARRATIVE:
- heading
- textarea/frame
- width
- height
- padding
- line-height
- borders

FACTOR IMPORTANCE:
- High/Medium controls
- active/inactive state
- dimensions
- spacing

IMPORTANCE JUSTIFICATION:
- green strip
- width
- border
- padding
- font

SET 1 — VULNERABILITY METRICS:
- Metric and Formula MUST be visibly separate columns if v31 does so.
- metric column width
- formula column width
- Very High
- High
- Moderate
- Low
- colour bands
- threshold cells
- row heights
- borders
- padding

CRITICAL THRESHOLD:
- position
- height
- background
- border
- typography

SET 2 — BUFFER METRICS:
- Metric
- Formula
- Strong
- Moderate
- Weak
- Negligible
- exact v31 colour treatments
- widths
- padding
- row heights

KEY PRINCIPLE:
- green strip
- border
- spacing

SCORING LOGIC:
- Score
- Vulnerability Profile
- Buffer Profile
- rows 5,4,3,2,1
- exact control/read-only behaviour from ACTUAL v31
- column widths
- row heights
- header fills
- cell borders

CREDIT IMPLICATION:
- heading
- green box
- spacing
- dimensions

Do not sign off RF1 until the browser result is visually aligned.

============================================================
10. VERIFY RF2–RF5 — DO NOT ASSUME RF1 REPRESENTS THEM
============================================================

Expand RF2.

Verify the full structure.

Repeat for:
RF3
RF4
RF5.

Each factor must contain the full 9-part analytical structure:

1. Factor Narrative
2. Factor Importance
3. Importance Justification
4. Vulnerability Metrics Set 1
5. Critical Threshold
6. Buffer Metrics Set 2
7. Key Principle
8. Scoring Logic 1–5
9. Credit Implication

No shallow/partial factors.

============================================================
11. BUSINESS CONTENT CHECK
============================================================

While testing, verify that the five factors are genuinely:

SECTOR-INHERENT

and are NOT simply repetitions of Step 2.3 event-driven factors.

Remember:

STEP 2.3:
What risks arise because of THIS scenario/event?

STEP 2.4:
What structural credit vulnerabilities already exist because of THIS
sector?

STEP 2.5:
How does THIS company perform against the event-driven and
sector-inherent frameworks?

Do not alter correct business content merely for wording preference.

Only flag/fix obvious contamination or structural errors.

============================================================
12. VULNERABILITY VS BUFFER LOGIC
============================================================

Confirm the rendered structure genuinely separates:

VULNERABILITY METRICS

from

BUFFER / MITIGANT METRICS.

Do not merge them.

This distinction is fundamental because Step 2.5 needs both:

risk severity
and
credit protection.

============================================================
13. SCORING LOGIC CHECK
============================================================

Verify browser rendering and data for scores:

5
4
3
2
1.

Ensure vulnerability profiles and buffer profiles are paired correctly.

Do not change the existing approved Net Score calculation.

The UI, formula banner and actual existing calculation must tell the
same story.

============================================================
14. EDIT / SAVE BEHAVIOUR
============================================================

If actual v31 Step 2.4 supports editable fields:

test one harmless change in the real UI.

Verify:

edit
→ Save All Changes
→ rendered state
→ underlying Step 2.4 state

then restore the original value if required.

If v31 does NOT permit editing that field, do not introduce editing.

============================================================
15. CONFIRM STEP 2.4
============================================================

Use:

Confirm All Sector Risk Factors

and verify real behaviour.

Expected:

Step 2.4 status
In Progress
        ↓
Confirmed / Complete

Workflow sidebar updates.

Step 2.5 becomes available according to existing workflow rules.

Do NOT fake confirmation through DOM/CSS.

Use actual application behaviour.

============================================================
16. VERIFY STEP 2.5 HANDOFF
============================================================

After confirmation, verify that Step 2.5 receives the confirmed Step
2.4 factor state through the existing handoff path you identified:

confirmStep24()
→ finalizeV6
→ RPR_STEP25_REFRESH_WORKFLOW_STATE

or whatever the actual runtime path is.

Do NOT modify Step 2.5 during this task.

Only prove the Step 2.4 output reaches it.

============================================================
17. VISUAL SIDE-BY-SIDE
============================================================

At desktop zoom, compare:

ACTUAL V31 STEP 2.4
vs
CURRENT LIVE STEP 2.4.

Do not compare from memory.

Check:

- page width
- right sidebar width
- content/sidebar gap
- sector bar
- summary table
- RF cards
- RF header
- text fields
- information boxes
- metric tables
- scoring tables
- button positions
- footer
- feedback panel
- overall vertical density

Correct remaining visible discrepancies individually.

============================================================
18. CSS RULE
============================================================

Do not solve individual differences with broad global CSS.

Keep Step 2.4 styling scoped.

Avoid regressions to:
Step 1
Step 2.1
Step 2.2
Step 2.3
Step 2.5.

Use actual v31 CSS values when available.

Do not approximate colours/dimensions unnecessarily.

============================================================
19. DO NOT REWRITE BUSINESS FUNCTIONALITY
============================================================

If the live test shows the current backend/data works:

LEAVE IT ALONE.

This final pass is primarily:

runtime validation
+
visual correction.

No architecture change.

============================================================
20. ACCEPTANCE TEST
============================================================

Do not finish until all are true:

[ ] Real application started successfully.
[ ] Real workflow reaches Step 2.4.
[ ] Sector comes from Step 2.2 correctly.
[ ] Exactly 5 RFs rendered.
[ ] Weights = 100.0%.
[ ] RF1–RF5 all have the complete 9-part schema.
[ ] Vulnerability and buffer tables are distinct.
[ ] Metric and Formula columns match v31.
[ ] Severity colours match v31.
[ ] Critical threshold matches v31.
[ ] Key Principle matches v31.
[ ] Scoring 5→1 matches v31.
[ ] Editable/read-only behaviour matches ACTUAL v31 Step 2.4.
[ ] Credit implication matches v31 structure.
[ ] Accordion behaviour works.
[ ] Save works where applicable.
[ ] Confirmation works.
[ ] Workflow sidebar updates.
[ ] Step 2.5 receives confirmed Step 2.4 state.
[ ] No Step 2.3 regression from step23.html modification.
[ ] Live visual result has been compared directly against v31.

============================================================
21. FINAL RESPONSE — KEEP IT SHORT
============================================================

Do not provide another long design report.

Give me:

1. LIVE TEST: PASS / FAIL

2. V31 VISUAL PARITY:
   PASS / FAIL

3. FUNCTIONAL STEP 2.4:
   PASS / FAIL

4. STEP 2.5 HANDOFF:
   PASS / FAIL

5. FILES CHANGED:
   exact paths only

6. REMAINING DIFFERENCES:
   every known difference, even minor

7. TESTED SECTOR:
   actual sector used in the live workflow

8. TESTED FACTORS:
   RF1–RF5 names

If a test fails, continue fixing it before reporting.

Only stop without completion for a genuine external blocker that cannot
be solved from the repository/environment.

EXECUTE THE LIVE ACCEPTANCE TEST NOW.
