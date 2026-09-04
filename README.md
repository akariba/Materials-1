STOP. Do not make any further payload, preset, SEC, UI or Step 3 changes yet.

The latest result gives us a clear checkpoint.

VERIFIED:

- payload compaction succeeded;
- compact input size is approximately 2,521 chars;
- 5 ED factors and 5 SI factors were supplied;
- SEC grounding was reduced to 2 sources;
- Runner execution failed after ~52 seconds because authentication
  failed;
- the preset/model/tool phase was therefore NOT reached;
- this test does NOT prove whether the compact payload solves the
  previous long-runtime issue.

The ONLY immediate blocker is Runner authentication.

Also, the current diagnostic script added 5 SYNTHETIC Step 2.3 factors.
That is not acceptable for the real POC acceptance run.

Do the following only.

============================================================
1. PRESERVE THE PAYLOAD COMPACTION
============================================================

Keep the current compaction changes in:

stylus_engine.py
stylus_sec_grounding.py

Do not redesign them again.

Do not expand the payload.

============================================================
2. REMOVE SYNTHETIC ED FACTORS FROM THE REAL ACCEPTANCE TEST
============================================================

The temporary synthetic ED factors added to:

_step25_ui_route_single_company_diag.py

must NOT be treated as the final test inputs.

For the next Apple acceptance run, use the ACTUAL five confirmed
Step 2.3 Event-Driven factors from the real workflow state.

Also use the ACTUAL five confirmed Step 2.4 Sector-Inherent factors.

Acceptance requires:

ED FACTORS = real confirmed 5
SI FACTORS = real confirmed 5

No fabricated/synthetic upstream factors.

If the diagnostic helper needs temporary fixture support for unit
testing, keep that clearly isolated from the real acceptance path.

============================================================
3. FIX RUNNER AUTHENTICATION ONLY
============================================================

Latest failure:

HTTP 401 TOKEN_EXPIRED

and the automatic refresh attempt itself failed with HTTP 400.

Do not touch Stylus payload logic to solve this.

Inspect the EXISTING Runner token mechanism and determine why the
refresh request is failing now.

Reuse the existing approved authentication mechanism.

Do NOT:
- create another token system;
- hard-code a bearer token;
- print secrets;
- ask me to paste a secret into chat;
- change Runner API architecture.

Check:

- current cached Runner token
- expiry
- current refresh-token state
- canonical refreshed-token source
- existing refresh script / endpoint
- why the refresh endpoint returned HTTP 400.

If the project already contains the previously implemented secure token
refresh script/process, use it.

============================================================
4. VERIFY AUTH BEFORE RUNNING APPLE
============================================================

Do NOT launch another Apple assessment until auth is proven.

Required preflight:

RUNNER TOKEN PRESENT: YES
RUNNER TOKEN EXPIRED: NO
REFRESH MECHANISM: PASS
TOKEN REMAINING TIME: sufficient for one assessment

Then perform a lightweight authenticated Runner connectivity check
using the existing safe mechanism.

Do not launch the full preset merely to test auth.

============================================================
5. IF USER INTERACTION IS GENUINELY REQUIRED
============================================================

If the corporate authentication system requires me to perform an
interactive login or securely refresh the token myself, STOP there.

Return only:

USER ACTION REQUIRED

EXACT ACTION:
<the exact local command/UI action I must perform>

Do NOT ask me to send the bearer token or refresh token in chat.

Otherwise continue automatically.

============================================================
6. THEN RUN ONE REAL APPLE ACCEPTANCE TEST
============================================================

Only after authentication passes, run:

Apple Inc.
AAPL
CIK 0000320193

with:

- real Step 2.1 scenario
- REAL five confirmed Step 2.3 ED factors
- REAL five confirmed Step 2.4 SI factors
- compact verified SEC grounding
- current assessment as-of date

Apple only.

No second company.
No 32-company batch.
No Step 3.

============================================================
7. DO NOT CHANGE THE PRESET DURING THIS TASK
============================================================

Do not modify the Stylus preset yourself.

We already know a potential preset optimisation may be useful, but this
latest run never reached the preset.

First prove the compact real payload can execute with valid auth.

============================================================
8. FINAL OUTPUT
============================================================

Return only:

RUNNER AUTH: PASS / FAIL

REFRESH: PASS / FAIL

APPLE REAL-INPUT TEST: PASS / FAIL

ED FACTORS:
5 REAL / NOT REAL

SI FACTORS:
5 REAL / NOT REAL

INPUT SIZE:
<chars>

SEC SOURCES:
<count>

RUNNER TIME:

FINAL RESPONSE:
YES / NO

EVIDENCE VALIDATED:
YES / NO

ED SCORE:
SI SCORE:
COMPOSITE:
RESIDUAL RATING:
IMPACT RATING:

JOB COMPLETED:
YES / NO

NEXT FAILURE:
NONE or exact checkpoint

Do not continue to Step 3.
