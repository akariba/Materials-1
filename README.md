STEP 2.5 — FIX THE REAL SINGLE-COMPANY SELECTION BUG END TO END

We have now isolated the actual Step 2.5 frontend blocker.

This is NOT an SEC problem.
This is NOT a Step 2.1–2.4 persistence problem.
This is NOT a Runner problem yet.

The authoritative upstream workflow is already LIVE-PROVEN and FROZEN:

Step 2.1 scenario persisted = YES
Step 2.2 portfolio persisted = YES
Sector/L3 = Banks - Major

Confirmed Step 2.2 companies:
1. COMMERZBANK AG
   company/CAGID = 9000024985

2. DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]
   company/CAGID = 9000008998

Step 2.3 confirmed = YES
Step 2.3 real factors = 5
Step 2.3 weights = 100%

Step 2.4 confirmed = YES
Step 2.4 real factors = 5
Step 2.4 weights = 100%

DO NOT modify any of that.

============================================================
CONFIRMED LIVE DEFECT
============================================================

Current Step 2.5 frontend state reports:

S25.selectedCompanyId = 1019556006

but 1019556006 is NOT in the currently confirmed Step 2.2 portfolio.

As a result:

selected company name = none
selected-company count for /run = 0
backend company context = missing
Run Assessment = disabled

Claude also confirmed:

THE DEUTSCHE BANK ROW IS NOT CURRENTLY A SELECTION CONTROL.

There is currently NO visible Step 2.5 company selector.

Therefore the user has no legitimate UI action that can satisfy the
existing gate:

"select exactly one eligible company from the confirmed Step 2.2
portfolio before running."

This is the defect to fix.

============================================================
OBJECTIVE
============================================================

Implement the smallest correct POC solution that allows the analyst to
select exactly ONE company from the confirmed Step 2.2 portfolio directly
inside Step 2.5 and then run the assessment for that company only.

Do not redesign Step 2.5.

Preserve the v31 visual baseline and current table layout.

============================================================
1. REMOVE STALE COMPANY SELECTION
============================================================

On Step 2.5 initialization / refresh:

Read the authoritative currently confirmed Step 2.2 company list.

Validate S25.selectedCompanyId against those current company IDs.

If the persisted/current selectedCompanyId is NOT present in the confirmed
portfolio:

CLEAR IT IMMEDIATELY.

For this current case:

1019556006 must be discarded.

Do NOT attempt to resolve it.
Do NOT preserve it.
Do NOT use it as a fallback.

The Step 2.5 assessment target must always belong to the CURRENT confirmed
Step 2.2 portfolio.

If Step 2.2 is reconfirmed with a different company universe, invalidate
any Step 2.5 selected company that is no longer part of that universe.

============================================================
2. ADD A REAL SINGLE-COMPANY SELECTOR
============================================================

The Step 2.5 portfolio table currently has two rows:

COMMERZBANK AG
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

Implement an explicit SINGLE-SELECTION mechanism.

Preferred minimal design:

Use the existing narrow left-most table control area and add a small radio
selection control for each company.

Do NOT add a large new panel.
Do NOT redesign the table.
Do NOT change existing column widths unnecessarily.
Do NOT replace the table.
Do NOT remove the existing row expansion behavior.

The analyst must be able to clearly select:

( ) COMMERZBANK AG
( ) DEUTSCHE BANK AG

Only one company can be selected at a time.

If using native radio inputs would visually damage v31 parity, implement
an equivalent compact single-select control, but it must be visually
obvious and accessible.

Use the existing v31/Citi styling:
- same typography
- same spacing
- same border treatment
- same row height as far as possible
- same navy/blue accent
- no new design system
- no oversized controls

Optional but useful:
when selected, apply the existing subtle selected-row visual treatment.
Do not invent a radically different highlight.

============================================================
3. USE THE REAL STEP 2.2 COMPANY ID
============================================================

When Deutsche Bank is selected:

S25.selectedCompanyId MUST become:

9000008998

When Commerzbank is selected:

S25.selectedCompanyId MUST become:

9000024985

Use the exact identifier from the authoritative confirmed Step 2.2 record.

Do NOT substitute:
- ticker
- CIK
- CUSIP
- ISIN
- old cached ID
- row index

Those can remain supplementary identity fields, but the Step 2.5 target
identity must remain tied to the confirmed Step 2.2 company record.

============================================================
4. SELECTION MUST BUILD THE REAL COMPANY OBJECT
============================================================

Selecting a row/company must resolve the complete current Step 2.2 company
object already held by the authoritative upstream state.

The selected Step 2.5 company object should preserve available real fields,
for example:

company_id / cagid
company_name
ticker if available
country
MLE
limit industry L1
limit industry L2
limit industry L3
CUSIP if available
ISIN if available
SEDOL if available
GTCX if available
RIC if available
current RRR where genuinely supplied
OSUC/exposure where genuinely supplied
other existing real Step 2.2 fields already consumed downstream

Do NOT fabricate missing values.

============================================================
5. REGISTER THE SELECTED COMPANY WITH BACKEND
============================================================

After a legitimate company selection, use the EXISTING context-registration
path.

Do not invent another state store.

Use the existing Step 2.5 context handoff / registerContextAndVerifyForRun
logic or its current equivalent.

The backend must receive the selected company together with the already
persisted upstream state.

After selecting Deutsche Bank, backend authoritative Step 2.5 context must
show:

company name =
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

company ID =
9000008998

Step 2.1 scenario present = true

Step 2.3 confirmed = true
Step 2.3 factor count = 5

Step 2.4 confirmed = true
Step 2.4 factor count = 5

selected company count for /run = 1

Do not duplicate or reconstruct the ED/SI factors from displayed DOM text.
Use the authoritative persisted objects.

============================================================
6. RUN BUTTON GATING
============================================================

Keep Run Assessment fail-closed.

It may only become executable when:

- exactly one CURRENT Step 2.2 company is selected
- selected company identity matches the authoritative portfolio record
- Step 2.1 scenario is present
- Step 2.3 confirmed = true
- Step 2.3 factor count = expected real count
- Step 2.4 confirmed = true
- Step 2.4 factor count = expected real count
- required Step 2.5 context registration succeeds

Do NOT weaken these gates.

Do NOT make the button clickable merely to make the demo work.

But the UI must now provide the legitimate action necessary to satisfy the
single-company gate.

============================================================
7. DO NOT MIX SEC/RUNNER INTO THIS FIX
============================================================

Do NOT start Stylus.

Do NOT call /run.

Do NOT troubleshoot Runner authentication yet.

Do NOT change the SEC resolver.

Do NOT fetch SEC evidence during this implementation test.

We are fixing ONLY the missing single-company selection / stale selection
handoff.

SEC and Runner readiness will be checked immediately AFTER this selection
path is proven.

============================================================
8. PRESERVE ALL EXISTING WORK
============================================================

DO NOT modify:

Step 2.1 generation/business logic
Step 2.2 portfolio business logic
Step 2.3 generation/business logic
Step 2.4 generation/business logic
Step 2.3/2.4 confirmed factors
Stylus preset
Stylus prompt
output schema
Step 2.5 scoring methodology
80/20 ED/SI weighting
SEC evidence methodology
Runner SSE handling
Step 3
v31 overall layout

Avoid new architecture.
Avoid new framework.
Avoid broad refactoring.

POC implementation only.

============================================================
9. LIVE ACCEPTANCE TEST
============================================================

After implementation:

DO NOT restart/rebuild Steps 2.1–2.4 unnecessarily.

Open Step 2.5 using the existing current confirmed Banks-Major workflow.

Verify the table contains:

COMMERZBANK AG
DEUTSCHE BANK AG

Verify no company is falsely selected from stale state.

Then select:

DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

through the NEW real UI selector.

Do NOT invoke Run Assessment.

Verify from frontend AND backend:

selected company name =
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

selected company ID =
9000008998

selected company count for /run =
1

Step 2.1 scenario present =
YES

Step 2.3 confirmed =
YES

Step 2.3 factor count =
5

Step 2.4 confirmed =
YES

Step 2.4 factor count =
5

stale selected ID 1019556006 present =
NO

context registration =
PASS

============================================================
10. STOPPING CONDITION
============================================================

Do not stop to write diagnostic reports while implementing.

Proceed autonomously through this entire approved scope.

Do not ask me for confirmation during implementation.

Stop only if a genuine external blocker prevents implementation.

Do not start Step 2.5 assessment itself.

Final response only after implementation and validation, using exactly:

STEP 2.5 SINGLE-COMPANY SELECTOR: PASS / FAIL

STALE COMPANY ID CLEARED: YES / NO
OLD ID:
CURRENT SELECTED COMPANY:
CURRENT SELECTED COMPANY ID:
SELECTED COMPANY COUNT FOR /run:

STEP 2.1 PRESENT: YES / NO
STEP 2.3 CONFIRMED: YES / NO
STEP 2.3 FACTOR COUNT:
STEP 2.4 CONFIRMED: YES / NO
STEP 2.4 FACTOR COUNT:

BACKEND CONTEXT REGISTRATION: PASS / FAIL

RUN BUTTON COMPANY-SELECTION GATE: PASS / FAIL

READY FOR SEC + RUNNER PREFLIGHT: YES / NO

FILES CHANGED:
<exact paths>
