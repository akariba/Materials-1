STRICT STEP 2.5 PREFLIGHT FIX — DEUTSCHE BANK

Do not modify Steps 2.1–2.4.
Their live backend persistence is now proven and frozen:

Step 2.1 = persisted
Step 2.2 = persisted
Step 2.3 = 5 real factors persisted
Step 2.4 = 5 real factors persisted

Current Step 2.5 preflight for exactly one company:

COMPANY:
DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

COMPANY ID:
9000008998

COMPANY NAME RESOLVED:
YES

STEP 2.1:
YES

STEP 2.3:
5 real factors / confirmed

STEP 2.4:
5 real factors / confirmed

SELECTED COMPANY COUNT:
1

COMPACT PAYLOAD:
READY

But:

SEC REGISTRANT / SEC-ELIGIBLE RESOLUTION:
NO

REAL SEC GROUNDING READY:
NO

RUNNER AUTH READY:
NO

SAFE TO RUN:
NO


============================================================
A. FIX THE SEC FALSE NEGATIVE
============================================================

Deutsche Bank is a real SEC registrant.

Known authoritative SEC identity:

Canonical registrant:
DEUTSCHE BANK AKTIENGESELLSCHAFT

CIK:
0001159508

It is a FOREIGN PRIVATE ISSUER.

Its relevant filing family includes:

20-F = annual report
6-K  = interim/current foreign issuer reports

Do NOT hard-code Deutsche Bank as a one-off exception.

Fix the generic SEC resolver / eligibility logic so that:

1. SEC registrant status is determined from a successful canonical
   SEC identity/CIK resolution, NOT from the existence of a 10-K or
   10-Q.

2. Foreign private issuers are supported.

3. Accepted credit-relevant annual/current filing families include:

   US domestic:
   - 10-K
   - 10-Q
   - 8-K where useful

   Foreign private issuer:
   - 20-F
   - 6-K

   If the existing architecture already supports 40-F, preserve it.
   Do not expand scope unnecessarily otherwise.

4. Normalize legal-name variations generically.

For example the portfolio display name:

DEUTSCHE BANK AG [DE FRANKFURT AM MAIN]

must be capable of matching the SEC registrant:

DEUTSCHE BANK AKTIENGESELLSCHAFT

Generic normalization may remove:
- bracketed geographic/legal annotations
- punctuation/casing differences
- standard corporate suffix variations

Do NOT rely solely on fuzzy company-name similarity when a genuine
identifier is available.

5. Use existing portfolio identifiers where useful, but do not
fabricate CIK/CUSIP/ISIN mappings.

6. For this Deutsche Bank test, prove resolution results in:

CIK = 0001159508
SEC registrant = YES
filing family = foreign private issuer
annual filing type = 20-F

7. SEC grounding for the assessment as-of date should select a small,
credit-relevant verified set, for example:

- latest eligible 20-F at or before the assessment date
- one or two relevant recent 6-K filings where useful

Do NOT load the entire filing corpus.

Maintain accession number, filing date and EDGAR URL provenance.


============================================================
B. DO NOT CHANGE THE COMPACT-PAYLOAD DESIGN
============================================================

Keep:

5 real Step 2.3 factors
5 real Step 2.4 factors
real Step 2.1 scenario
one selected company
compact SEC evidence

Do not re-expand the payload.

Do not use synthetic factors.


============================================================
C. VERIFY RUNNER AUTH SEPARATELY
============================================================

Current preflight says:

RUNNER AUTH READY = NO

Check the existing Runner token status only.

Do not redesign authentication.

Use the existing approved token mechanism.

If a fresh user-side browser token capture is genuinely required,
stop and return the exact local action required.

Do NOT ask the user to paste a token into chat.

If the token can be refreshed using the existing mechanism, do so.


============================================================
D. DO NOT START THE ASSESSMENT
============================================================

After fixing/verifying these two preflight blockers:

Do NOT call /run.
Do NOT start Stylus.

Return only:

COMPANY:
DEUTSCHE BANK AG

COMPANY ID:
9000008998

SEC CANONICAL NAME:
SEC CIK:

SEC REGISTRANT:
YES / NO

FOREIGN PRIVATE ISSUER:
YES / NO

SUPPORTED ANNUAL FORM:
SUPPORTED CURRENT/INTERIM FORM:

REAL SEC GROUNDING READY:
YES / NO

SEC SOURCE COUNT:

RUNNER AUTH READY:
YES / NO

STEP 2.1 PRESENT:
YES / NO

REAL STEP 2.3 FACTOR COUNT:
REAL STEP 2.4 FACTOR COUNT:

SELECTED COMPANY COUNT:

COMPACT PAYLOAD READY:
YES / NO

SAFE TO CLICK RUN ASSESSMENT:
YES / NO

FILES CHANGED:
exact paths

Do not continue beyond preflight.
