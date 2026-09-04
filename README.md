STEP 2.5 — FINAL SEC + RUNNER PREFLIGHT FOR DEUTSCHE BANK

The Step 2.5 single-company selection defect is now LIVE-PROVEN and CLOSED.

Freeze the following working state:

Selected company:
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

Internal company ID:
9000008998

Selected company count for /run:
1

Stale company ID:
CLEARED

Step 2.1 present:
YES

Step 2.3:
CONFIRMED
5 REAL FACTORS

Step 2.4:
CONFIRMED
5 REAL FACTORS

Backend context registration:
PASS

Run-button company-selection gate:
PASS

READY FOR SEC + RUNNER PREFLIGHT:
YES


============================================================
STRICT SCOPE
============================================================

Do NOT modify:

- Step 2.1
- Step 2.2
- Step 2.3
- Step 2.4
- Step 2.5 company selector
- upstream persistence
- Step 2.5 scoring methodology
- 80/20 ED/SI weighting
- Step 3
- v31 UI
- Stylus preset
- Stylus preset prompt
- output schema

Do NOT restart the backend unless absolutely required for an auth action.

Do NOT call /run yet.

Do NOT start a Step 2.5 assessment.

We are checking exactly TWO remaining preconditions:

A. VERIFIED REAL SEC GROUNDING
B. RUNNER AUTHENTICATION


============================================================
A. VERIFY REAL SEC GROUNDING
============================================================

The Deutsche Bank SEC identity resolver has already been fixed and must
not be reimplemented.

Expected canonical identity:

Portfolio company:
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

SEC canonical registrant:
DEUTSCHE BANK AKTIENGESELLSCHAFT

CIK:
0001159508

SEC registrant:
YES

Foreign private issuer:
YES

Relevant filing families:
20-F
6-K

Now verify the actual deterministic SEC grounding that will be passed to
Step 2.5.

This is NOT satisfied merely because CIK resolution succeeds.

REAL SEC GROUNDING READY requires genuine SEC filing metadata/evidence.

For the assessment as-of date, verify a small credit-relevant filing set.

Prefer:

1. latest eligible 20-F at or before the assessment date
2. one or two relevant recent 6-K filings where useful

Every accepted SEC source must have genuine provenance including:

- filing form
- filing date
- accession number
- real EDGAR source URL/reference
- company/CIK identity correspondence

No fabricated accession number.
No fabricated URL.
No model-invented filing metadata.
No evidence accepted merely because the model says "SEC".

Do not load excessive filing content.

Use the deterministic SEC grounding path already implemented.


============================================================
B. VERIFY RUNNER AUTH
============================================================

Check the current Runner authentication state using the existing approved
Runner/token implementation.

Do not redesign authentication.

Do not implement a new auth framework.

Check:

- token currently available
- token currently valid
- expiry
- refresh mechanism status
- Runner preflight/auth endpoint

If existing automatic refresh succeeds, use it.

If the credential genuinely requires manual browser-side recapture,
DO NOT ask me to paste the token into chat.

Instead return the exact local browser action required.

Do not start the assessment merely to test auth.


============================================================
C. VERIFY FINAL PAYLOAD READINESS
============================================================

Without calling /run, verify that the exact payload that would be used for
Deutsche Bank contains:

CompanyContextJSON:
- Deutsche Bank only
- internal company ID 9000008998
- correct available real Step 2.2 fields
- canonical SEC identity / grounding where expected

ScenarioContextJSON:
- real confirmed Step 2.1 scenario

EventDrivenFactorsJSON:
- exactly 5 confirmed real Step 2.3 factors

SectorInherentFactorsJSON:
- exactly 5 confirmed real Step 2.4 factors

AssessmentAsOfDate:
- current selected assessment date

Do not print the entire large payload.
Report only field presence/counts and approximate payload size.

No synthetic factors.
No fixture factors.
No stale companies.
No second portfolio company.


============================================================
STOPPING CONDITION
============================================================

Do not make unrelated fixes.

Do not run Step 2.5.

Return only:

SELECTED COMPANY:
SELECTED COMPANY ID:
SELECTED COMPANY COUNT:

SEC CANONICAL NAME:
SEC CIK:
SEC REGISTRANT: YES / NO
FOREIGN PRIVATE ISSUER: YES / NO

REAL SEC GROUNDING READY: YES / NO
VERIFIED SEC SOURCE COUNT:
FORM 1:
FILING DATE:
ACCESSION NUMBER PRESENT: YES / NO
EDGAR URL PRESENT: YES / NO

FORM 2:
FILING DATE:
ACCESSION NUMBER PRESENT: YES / NO
EDGAR URL PRESENT: YES / NO

FORM 3:
FILING DATE:
ACCESSION NUMBER PRESENT: YES / NO
EDGAR URL PRESENT: YES / NO

RUNNER TOKEN PRESENT: YES / NO
RUNNER TOKEN VALID: YES / NO
RUNNER AUTH READY: YES / NO
MANUAL TOKEN ACTION REQUIRED: YES / NO

STEP 2.1 PAYLOAD PRESENT: YES / NO
STEP 2.3 PAYLOAD FACTORS:
STEP 2.4 PAYLOAD FACTORS:
COMPANY PAYLOAD COUNT:
APPROX PAYLOAD SIZE:

COMPACT PAYLOAD READY: YES / NO

SAFE TO CLICK RUN ASSESSMENT: YES / NO

FAILURE POINT:
NONE or exact remaining blocker

FILES CHANGED:
NONE — this is verification only.
