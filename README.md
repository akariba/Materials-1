The previous live retest was invalid for the Apple acceptance case.

The browser was actually showing TWO Banks companies:
- COMMERZBANK AG
- DEUTSCHE BANK AG

while the backend verification was still looking for Apple company_id
0000014508.

I have now redone the controlled acceptance workflow correctly:

- Step 2.2 = Software
- exactly ONE company selected = Apple Inc.
- Step 2.2 confirmed
- Step 2.3 real factors confirmed
- Step 2.4 real factors confirmed
- now on Step 2.5
- I have NOT clicked Run Assessment

Do NOT modify code.
Do NOT start Stylus.

Check the authoritative backend persisted state for the CURRENT workflow.

Return only:

COMPANY:
COMPANY ID:
PORTFOLIO/SECTOR:

SELECTED COMPANY COUNT:

STEP 2.1 SCENARIO PRESENT: YES/NO

STEP 2.3 CONFIRMED: YES/NO
REAL STEP 2.3 FACTOR COUNT:

STEP 2.4 CONFIRMED: YES/NO
REAL STEP 2.4 FACTOR COUNT:

SAFE TO RUN STEP 2.5: YES/NO
