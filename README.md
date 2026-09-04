FINAL RPR LIVE EXECUTION AND ACCEPTANCE
NO MORE STATIC CODE-ONLY PASS REPORTS

Continue from your current implementation.

IMPORTANT:
Your previous status report is NOT accepted as final completion.

You explicitly stated:

- Step 2.5 was not re-run live end-to-end.
- Step 3 was not executed in a browser.
- validation was based partly on source inspection/static analysis.

The current browser result also proves the end-to-end workflow is not
yet demonstrated:

Step 3 currently shows:

“No confirmed Step 2.4 sector yet”
0 entities
$0 exposure
empty segmentation
empty commentary

Therefore STOP doing further broad rewrites.

The task now is REAL EXECUTION, STATE WIRING, DEBUGGING AND ACCEPTANCE.

Do NOT produce another report until you have done everything possible
to make the actual running application work.

============================================================
1. CRITICAL TESTING CORRECTION — DO NOT TEST VIA file://
============================================================

The user has opened:

C:/.../UI Design/step23.html

directly as a local FILE page.

That is NOT a valid end-to-end runtime test if application state/API
access is normally provided by the local backend.

The system log from the application shows the backend at approximately:

http://127.0.0.1:8000

Determine the existing correct application URL/startup path.

Use the SAME served application/session for:

Step 1
Step 2.1
Step 2.2
Step 2.3
Step 2.4
Step 2.5
Step 3

Do not validate Step 3 by opening step23.html directly from disk.

Do not invent a new server.

Use the project's current working backend/startup mechanism.

============================================================
2. FIRST TRACE STATE STORAGE / STATE PROPAGATION
============================================================

Before changing code, trace exactly where these confirmed states live:

Step 2.2 confirmed portfolio
Step 2.3 confirmed event RFs
Step 2.4 confirmed sector RFs
Step 2.5 confirmed company assessments

Determine whether each is stored in:

- browser memory
- localStorage
- sessionStorage
- backend memory
- backend JSON
- server-side workflow state
- another existing mechanism

Then verify Step 3 is reading the SAME state source.

The current Step 3 showing:

“No confirmed Step 2.4 sector yet”

means either:

A. Step 2.4 was not confirmed in the same runtime session,

B. Step 3 is reading the wrong key/source,

C. direct file:// loading loses the state,

or

D. Step 2.4 confirmation is not persisting correctly.

Identify the actual cause.

Fix only if needed.

============================================================
3. DO NOT CONFUSE API FACTOR GENERATION WITH STEP 2.4 CONFIRMATION
============================================================

You reported that a real backend call returned:

FACTOR_COUNT = 5

Good.

But that is NOT enough.

We need:

backend generated 5
        ↓
Step 2.4 UI rendered those 5
        ↓
user/application confirms those 5
        ↓
confirmed Step 2.4 state persisted
        ↓
Step 2.5 reads the same exact five
        ↓
Step 3 knows the confirmed sector.

Verify the full sequence.

============================================================
4. STEP 2.4 LIVE TEST
============================================================

Using the served application, load the real workflow.

For Software verify live:

RF1
RF2
RF3
RF4
RF5

Exactly 5.

Verify:

Total Weight = 100.0%

Every RF has:

- narrative
- importance
- importance justification
- vulnerability metrics
- formulas
- thresholds
- critical threshold
- buffer metrics
- key principle
- scoring 5–1
- credit implication

Then compare rendered Step 2.4 directly to actual v31.

Do NOT declare visual parity by reading CSS.

Use the live rendered screen.

Fix remaining visual differences if they are visible.

Then confirm Step 2.4 through the actual application.

Verify confirmation persistence.

============================================================
5. STEP 2.5 POPULATION — PROVE THE FIX LIVE
============================================================

After Step 2.4 confirmation, open Step 2.5 in the SAME runtime session.

The Step 2.5 universe MUST come from the confirmed Step 2.2 Software
portfolio.

It must NOT display the old 226-company global population.

Verify the actual Step 2.2 Software count.

Then build the POC cohort from that population.

============================================================
6. EXACTLY 10 COMPANIES FOR THE POC
============================================================

We do NOT need to assess all Software companies.

Select exactly ten valid public issuers.

But do not select arbitrary ten names.

Preflight candidates using the identifiers now present in Step 2.2:

- company name
- ticker if present
- CUSIP
- ISIN
- SEDOL
- RIC
- country
- CAGID/internal ID

Preference:

1. known ticker / known CIK
2. strong RIC/ticker resolution
3. CUSIP/ISIN supported resolution
4. company-name resolution as fallback

Use existing CikResolver and existing identity logic.

Do NOT send CUSIP or ISIN to SEC pretending it is CIK.

Resolve:

Step 2.2 row
→ canonical issuer
→ ticker
→ CIK
→ SEC filing.

============================================================
7. PREFLIGHT BEFORE RUNNING EXPENSIVE ASSESSMENTS
============================================================

For candidate companies, before Runner/model assessment:

verify:

canonical company
ticker
CIK
latest suitable SEC filing on/before as-of date.

Use appropriate filings such as:

10-K
10-Q
8-K
20-F
6-K

depending on issuer.

If a candidate cannot be reliably resolved:

skip it.

Take the next candidate.

Do not waste a 40-minute Runner attempt on an unresolved company.

Continue until ten companies pass preflight.

============================================================
8. SHOW ME THE PREFLIGHT RESULT INTERNALLY BEFORE RUNNING
============================================================

The application/code should internally have for each selected issuer:

company
ticker
CIK
filing form
filing date
filing/accession identity

Do not fabricate any of these.

Do not publish a company into the 10-company assessment cohort unless
identity verification succeeds.

============================================================
9. RUN REAL SEC + WEB
============================================================

Now run the actual SEC + Web assessment through the existing Stylus
Runner path.

Do NOT modify the Stylus preset.

The user owns the preset manually.

Use the currently existing Runner integration.

For each company supply:

- canonical issuer identity
- Step 2.1 scenario
- Step 2.3 five event RFs
- Step 2.4 five sector RFs
- SEC evidence
- Web evidence
- assessment as-of date

Use the existing bounded Runner completion handling.

No infinite waits.

============================================================
10. RUNNER FAILURE HANDLING
============================================================

If Runner/auth fails:

trace whether it is:

A. authentication/token
B. Runner endpoint
C. issuer identity
D. SEC retrieval
E. web retrieval
F. final-model completion
G. response parsing

Do not label everything “SEC failed.”

Fix the actual active cause where possible.

If the Runner credential/token needs refreshing through the existing
project mechanism, use that existing mechanism.

Do not redesign authentication.

============================================================
11. ABSOLUTE CREDIT SAFETY RULE
============================================================

Technical failure must NEVER create a credit assessment.

SEC failure ≠ Substandard.

Runner timeout ≠ High Impact.

Web failure ≠ downgrade.

Missing data ≠ poor credit quality.

If evidence is insufficient, use:

NOT ASSESSED
or
INSUFFICIENT EVIDENCE

according to existing vocabulary.

Do not generate a business rating from a technical exception.

============================================================
12. STEP 2.5 RESULT QUALITY
============================================================

For each successful issuer result, validate before rendering.

No:

- raw JSON
- markdown fences
- SSE messages
- tool traces
- stack traces
- backend exceptions
- gigantic diagnostic paragraphs
- fabricated financial values

inside the assessment table.

The result must be concise and readable.

Use actual v31 Step 2.5 as presentation authority.

============================================================
13. STEP 2.5 VISUAL TARGET
============================================================

The live Step 2.5 must look like an assessment application, not a raw
database dump.

Use v31 exact structure for:

- table framing
- headers
- row density
- score badges
- impact/rating badges
- filters
- scrolling
- company name
- ticker/id
- score presentation
- classification presentation
- button layout

The POC table should contain only the ten assessed companies.

Do not show 226 names.

Do not expose giant technical diagnostics by default.

Keep technical diagnostics collapsed/secondary.

============================================================
14. STEP 2.5 COMPLETION GATE
============================================================

Do not proceed to portfolio assessment until:

10 companies are selected
10 identities are verified
10 assessments have completed successfully
10 outputs validate
10 rows render cleanly.

If one issuer-specific run fails:

use another already-preflighted Software candidate.

Target remains 10 successful results.

============================================================
15. CONFIRM STEP 2.5 FOR REAL
============================================================

After the ten results are valid:

Confirm Assessment

through the actual UI/state mechanism.

Verify persisted confirmed assessment state.

Then navigate to Step 3 WITHOUT opening a separate local HTML file.

Use the same served application and same workflow/session.

============================================================
16. STEP 3 CURRENT EMPTY SCREEN IS A FAILURE
============================================================

The current live/static screenshot showing:

No confirmed Step 2.4 sector yet
0 entities
$0
0.0%
empty tables

is NOT an acceptable result.

Step 3 must receive the confirmed upstream state.

Trace and fix the handoff if it does not.

============================================================
17. STEP 3 INPUT
============================================================

Step 3 must use:

confirmed Software sector

confirmed Step 2.3 RFs

confirmed Step 2.4 RFs

confirmed Step 2.5 ten-company assessments

actual Step 2.2 exposure/limit values where available.

No v31 demonstration numbers.

No hard-coded Salesforce/SAP/Autodesk values unless those are genuinely
among the real current assessed companies.

============================================================
18. STEP 3 REAL AGGREGATION
============================================================

Populate the v31 portfolio-level framework from actual data.

Portfolio Exposure Summary:

Total Exposure
IG Exposure
NIG Exposure
Criticized Exposure
Classified Exposure

Exposure Segmentation:

Overall Portfolio
Investment Grade
Non-Investment Grade
Criticized
Classified

Use real classification logic already approved in v31/current code.

Use actual OSUC/exposure values.

Do not fabricate missing exposure.

If genuinely unavailable, show N/A.

============================================================
19. STEP 3 SCORING
============================================================

Use existing approved methodology only.

Do not invent a new weighted composite formula.

The aggregation must be mathematically traceable to the confirmed
Step 2.5 results and real exposure data.

Where exposure weighting is available, use it.

============================================================
20. STEP 3 COMMENTARY
============================================================

Populate the v31 Credit Assessment / Credit Intelligence sections from
the real current run.

The commentary should explain:

- scenario
- sector/exposure profile
- event-driven vulnerabilities
- sector-inherent vulnerabilities
- dominant assessed companies
- largest exposure contributors
- aggregate impact
- key mitigants / buffers

Do not create unrelated generic AI commentary.

Do not insert unsupported metrics.

============================================================
21. STEP 3 VISUAL PARITY
============================================================

Use ACTUAL v31 code as source of truth.

The reference screenshot contains:

- dark sector selector strip
- five exposure/KPI cards
- exposure segmentation table
- weighted composite scores
- impact rating badges
- companies included
- large Credit Assessment / Credit Intelligence region
- export control
- confirm portfolio assessment

Replicate the actual v31 DOM/CSS geometry.

The currently blank/simple screen is not sufficient.

Do not merely create sections with similar names.

Match:

width
height
padding
border
font
column proportions
header colours
row heights
badge styles
card layout
content density.

============================================================
22. DO NOT TEST STEP 3 BY OPENING step23.html DIRECTLY
============================================================

This is important enough to repeat.

The reference v31 can be opened from file:// because it is static.

The current functional application must be tested through its served
runtime because it depends on live workflow state.

So:

V31 reference:
file:// is fine.

CURRENT APPLICATION:
use actual backend-served URL/session.

============================================================
23. IF YOU HAVE NO BROWSER AUTOMATION TOOL
============================================================

Lack of browser automation is NOT permission to declare PASS.

Do everything you can from the repository:

- start backend
- execute APIs
- inspect workflow state
- verify saved JSON/state
- test Runner
- test all ten companies
- verify Step 3 aggregation output

Then, if ONE purely visual click-through remains impossible because your
environment truly has no browser-driving capability, do NOT claim full
PASS.

Instead leave the server running and give the user only the exact
minimal URL/click sequence required for the final visual verification.

But all backend/state/data execution must already have succeeded.

============================================================
24. DO NOT WRITE ANOTHER STATUS REPORT WHILE WORK IS REMAINING
============================================================

Do not stop after:

“code fix complete”

“source inspection clean”

“get_errors clean”

“API returns five factors”

“Step 3 rewrite complete.”

Those are intermediate conditions.

Continue.

============================================================
25. ACCEPTANCE CRITERIA
============================================================

STEP 2.4

[ ] served UI works
[ ] exactly 5 factors rendered
[ ] 100% weights
[ ] all detail structures populated
[ ] v31 layout replicated
[ ] confirmation persists
[ ] sector state available downstream

STEP 2.5

[ ] reads Software population from confirmed Step 2.2
[ ] no 226-company wrong population
[ ] 10-company preflight cohort
[ ] canonical issuer for all 10
[ ] ticker for all 10 where applicable
[ ] CIK resolved for SEC issuers
[ ] real filing located
[ ] SEC+Web successfully runs
[ ] 10 valid assessments
[ ] clean readable business output
[ ] no fabricated data
[ ] no technical failure translated into credit judgment
[ ] v31 UI replicated
[ ] confirmation persists

STEP 3

[ ] same live session receives upstream state
[ ] confirmed Software sector visible
[ ] ten assessed companies available
[ ] real exposure aggregation
[ ] IG/NIG/Criticized/Classified logic
[ ] weighted composite scores
[ ] companies included
[ ] real portfolio commentary
[ ] v31 dashboard structure
[ ] not blank
[ ] confirmation works

============================================================
26. FINAL RESPONSE ONLY WHEN EXECUTION IS COMPLETE
============================================================

Only after real execution, respond with:

END-TO-END: PASS / FAIL

STEP 2.4 LIVE: PASS / FAIL
STEP 2.4 V31: PASS / FAIL

STEP 2.5 LIVE SEC+WEB: PASS / FAIL
STEP 2.5 V31: PASS / FAIL

STEP 3 LIVE: PASS / FAIL
STEP 3 V31: PASS / FAIL

SOFTWARE POPULATION:
actual number

TEN ASSESSED ISSUERS:
company | ticker | CIK | SEC form | filing date

STEP 2.4 RF1–RF5:
names

STEP 3:
total exposure
IG
NIG
criticized
classified
weighted composite score
impact rating

FILES CHANGED:
exact paths

REMAINING BLOCKER:
NONE

If there is a genuine external blocker, state the EXACT blocker and
the exact last successful checkpoint.

DO NOT call source inspection alone a PASS.

START THE REAL RUNTIME VALIDATION NOW.
