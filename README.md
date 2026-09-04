STOP CODE CHANGES.

The Deutsche Bank SEC/FPI resolver fix is now proven:

SEC canonical name = DEUTSCHE BANK AKTIENGESELLSCHAFT
CIK = 0001159508
SEC registrant = YES
Foreign private issuer = YES
Annual form = 20-F
Current/interim form = 6-K

The current Step 2.1/2.3/2.4 zeros appeared after the code changes and
backend reload. This POC uses in-memory authoritative workflow state,
so treat those zeros as expected state loss after restart unless proven
otherwise.

Do NOT modify:
- Steps 2.1–2.4
- persistence wiring
- SEC resolver
- Stylus preset
- Step 2.5 scoring
- Step 3
- UI

I will now reconfirm the real workflow through Step 2.4 once.

Monitor only.

After I finish 2.1 → 2.2 → 2.3 → 2.4, verify:

STEP 2.1 SCENARIO PRESENT
STEP 2.2 PORTFOLIO PRESENT
STEP 2.3 CONFIRMED / FACTOR COUNT
STEP 2.4 CONFIRMED / FACTOR COUNT

Then, for the selected Deutsche Bank company only, separately check:

1. SEC identity resolution
2. actual verified SEC grounding construction
3. Runner authentication

Do not start /run.

Return only:

UPSTREAM STATE RESTORED: YES/NO
STEP 2.1 PRESENT: YES/NO
STEP 2.2 PRESENT: YES/NO
STEP 2.3 COUNT:
STEP 2.4 COUNT:

SEC REGISTRANT: YES/NO
SEC CIK:
SEC GROUNDING READY: YES/NO
VERIFIED SEC SOURCE COUNT:
VERIFIED FORMS:
VERIFIED ACCESSION NUMBERS PRESENT: YES/NO
VERIFIED EDGAR URLS PRESENT: YES/NO

RUNNER AUTH READY: YES/NO
TOKEN REFRESH/CAPTURE REQUIRED: YES/NO

SAFE FOR STEP 2.5 RUN: YES/NO

Do not modify anything during this verification.
