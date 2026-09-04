STOP THE CURRENT >30-MINUTE APPLE RUN.

We now have the root cause sufficiently isolated.

DO NOT produce another diagnostic report.
IMPLEMENT THE FIX.

VERIFIED:

- Manual Stylus Apple run completes in approximately 2 minutes.
- Same preset.
- Same model.
- Same tool configuration.
- Runner itself works.
- Job/poll mechanism works.
- Backend run is materially larger than manual run.
- Backend currently supplies:
    * real company context
    * Step 2.1 scenario
    * Step 2.3 factors
    * all 5 Step 2.4 factors
    * additional deterministic SEC grounding
- Stylus also has SEC/Web tools available.
- Current backend-driven Apple run has exceeded 30 minutes without a
  final response.

The Step 2.5 input contract must now be corrected.

============================================================
1. DO NOT REMOVE THE REAL BUSINESS CONTEXT
============================================================

Do NOT solve performance by going back to the small synthetic manual
test.

The real assessment MUST retain:

- actual company identity
- actual Step 2.1 scenario
- exactly 5 confirmed Step 2.3 event-driven factors
- exactly 5 confirmed Step 2.4 sector-inherent factors
- assessment as-of date
- verified SEC grounding
- supplemental Web capability.

The goal is COMPACTION + DE-DUPLICATION, not loss of analytical
content.

============================================================
2. MAKE THE BACKEND PAYLOAD MATCH THE MANUAL PRESET CONTRACT
============================================================

Use exactly the same preset, model and Runner invocation structure as
the successful manual Stylus call.

Do not add separate backend-only prose/prompts unless genuinely needed.

The only difference should be that the backend supplies REAL values to
the preset's existing inputs.

============================================================
3. COMPANY CONTEXT MUST BE SMALL
============================================================

CompanyContextJSON should contain only fields needed for assessment.

For Apple conceptually:

company_name
ticker
CIK
sector
country
internal company identifier where useful

Do NOT include the entire Step 2.2 row or unrelated portfolio metadata.

============================================================
4. COMPACT STEP 2.1
============================================================

ScenarioContextJSON should contain only the confirmed assessment
scenario required by Step 2.5:

- scenario name
- horizon
- major assumptions/shocks
- relevant stress narrative.

Do not pass the complete raw Step 2.1 application state.

============================================================
5. KEEP ALL FIVE STEP 2.3 FACTORS, BUT COMPACT THEM
============================================================

EventDrivenFactorsJSON must contain exactly the 5 confirmed Step 2.3
factors.

For each factor keep only what Step 2.5 genuinely needs, such as:

factor_id
factor_name
weight
credit transmission / concise rationale
relevant scoring information if required by approved methodology.

Do not send UI metadata, workflow fields, feedback history or other
irrelevant state.

============================================================
6. KEEP ALL FIVE STEP 2.4 FACTORS
============================================================

SectorInherentFactorsJSON must contain exactly the 5 confirmed Step 2.4
factors.

Do NOT reduce this to one factor merely to match the manual smoke test.

For each RF keep only fields required to score a company:

factor_id
factor_name
weight
importance

relevant vulnerability metrics / thresholds

relevant buffer metrics / thresholds

scoring rule necessary for Step 2.5.

Do NOT pass visual/UI content or redundant long narratives when the
structured metric/scoring framework already expresses the same logic.

============================================================
7. COMPACT SEC GROUNDING AGGRESSIVELY
============================================================

This is critical.

Do NOT attach entire SEC filings or very large filing text to the
Stylus input.

The backend already deterministically knows:

evidence ID
CIK
form
filing date
accession
EDGAR URL.

For grounding, supply a SMALL set of relevant verified excerpts/facts
from the latest appropriate filing(s).

Prefer approximately:

1–3 relevant SEC filing sources

with only credit-relevant excerpts needed for the Step 2.3/2.4
assessment.

For example where available:

debt/leverage
liquidity/cash
interest coverage
cash flow
maturities/refinancing
revenue/retention
material risk disclosures

depending on the actual RFs.

Do not dump the filing.

Preserve deterministic provenance for every excerpt.

============================================================
8. REMOVE DUPLICATE SEC DISCOVERY
============================================================

If verified SEC grounding has already been supplied by the backend,
Stylus should NOT spend time rediscovering the same SEC filing.

The backend owns SEC provenance.

The preset should consume supplied verified SEC evidence.

Web remains supplemental.

DO NOT modify the Stylus preset yourself.

Implement backend payload support first.

At the end, if the current preset prompt explicitly tells the model to
always perform its own SEC filing lookup even when verified SEC
evidence is supplied, flag the minimal manual preset change for the
user.

============================================================
9. BOUND WEB RESEARCH
============================================================

Web search is supplemental.

Do not allow open-ended research.

The Step 2.5 purpose is an issuer credit assessment, not a research
project.

Use Web only where needed for current information not adequately
covered by SEC evidence.

The successful manual Apple run used a small number of targeted
searches.

The real backend run should behave similarly.

Do not introduce a generic research loop.

============================================================
10. DO NOT CHANGE SCORING
============================================================

Do not modify the approved:

ED score
SI score
Composite score
Residual rating
Credit impact rating

methodology.

This task only fixes how evidence/context reaches the existing
assessment.

============================================================
11. DO NOT CHANGE RUNNER
============================================================

Runner has now been proven to:

HTTP 200
open stream
receive SSE events
produce final output in previous runs.

Do not rewrite Runner again.

Do not touch Step 3.

Do not touch UI styling.

============================================================
12. ADD ONE USEFUL PAYLOAD SIZE CHECK
============================================================

Before calling Runner, log safe summary information only:

company
ED factor count
SI factor count
SEC evidence count
approximate serialized input size

Do not log secrets or huge evidence text.

This is only to prevent accidental payload growth.

============================================================
13. APPLE ACCEPTANCE TEST
============================================================

After implementing payload compaction:

restart backend cleanly.

Run Apple ONLY.

Use:

Apple Inc.
AAPL
CIK 0000320193

Exactly:

5 Step 2.3 factors
5 Step 2.4 factors
real Step 2.1 scenario
compact verified SEC evidence.

No 32-company batch.

No second company.

============================================================
14. PERFORMANCE ACCEPTANCE
============================================================

This POC cannot accept another 30–40 minute name assessment.

Target should be reasonably comparable to the manual Stylus run.

Do not impose an unrealistically strict 2-minute requirement because
the real assessment has richer context.

But one issuer should normally complete in minutes, not tens of
minutes.

Use a bounded maximum for the Apple acceptance run.

If the model performs repeated unnecessary tool searches despite the
compact context, inspect the preset instruction once and request the
minimal manual change.

============================================================
15. SUCCESS
============================================================

Apple must reach:

FINAL RESPONSE RECEIVED
ARTIFACT PARSED
EVIDENCE VALIDATED
ED SCORE POPULATED
SI SCORE POPULATED
COMPOSITE SCORE POPULATED
RESIDUAL RATING POPULATED
CREDIT IMPACT RATING POPULATED
JOB COMPLETED

No fabrication.

============================================================
16. STOP AFTER APPLE
============================================================

Do not run 10 companies yet.
Do not execute Step 3 yet.

Return only:

APPLE COMPACT-PAYLOAD TEST: PASS / FAIL

INPUT SIZE BEFORE:
INPUT SIZE AFTER:

ED FACTORS: 5
SI FACTORS: 5
SEC SOURCES:
WEB SEARCHES PERFORMED:
RUNNER EXECUTION TIME:

FINAL RESPONSE: YES / NO
EVIDENCE VALIDATED: YES / NO
ED SCORE:
SI SCORE:
COMPOSITE:
RESIDUAL RATING:
IMPACT RATING:
JOB COMPLETED: YES / NO

ROOT CAUSE FIXED:
one sentence

FILES CHANGED:
exact paths

PRESET MANUAL CHANGE REQUIRED:
YES / NO

If YES:
give only the exact minimal prompt change required.

Do not continue to another task.
