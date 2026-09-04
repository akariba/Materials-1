Take ONE public company from the confirmed Step 2.2 Software population.

I do NOT have CIK in Step 2.2 and I do not want to enter it manually.

Use the identifiers already available in Step 2.2, such as:

- company name
- RIC
- CUSIP
- ISIN
- SEDOL
- country
- internal company ID

to identify the public issuer.

Then use the existing cik_resolver.py / SEC company mapping logic to
derive the REAL CIK automatically.

Do NOT treat CUSIP, ISIN, SEDOL or RIC as a CIK.

After resolving the CIK, verify it against SEC by checking that the
returned SEC company name/ticker corresponds to the Step 2.2 company.

DO NOT call Stylus.
DO NOT retrieve Step 2.5 assessment yet.

Return only:

STEP 2.2 COMPANY:
IDENTIFIERS AVAILABLE:
RESOLVED TICKER:
RESOLVED CIK:
SEC VERIFIED COMPANY NAME:
MATCH: YES / NO
RESULT: PASS / FAIL
