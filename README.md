LIVE RETEST ONLY — NO MORE CODE CHANGES

The live upstream wiring fix has been implemented.

Do NOT modify any code.
Do NOT start Stylus.
Do NOT work on Step 2.5.
Do NOT work on Step 3.

I am going to reopen/reload the actual RPR application and perform the
real workflow again.

Monitor the backend logs/state while I do it.

I will execute:

1. Step 2.1 — confirm scenario
2. Step 2.2 — confirm portfolio/company selection
3. Step 2.3 — confirm the real Event-Driven factors
4. Step 2.4 — confirm the real Sector-Inherent factors

After EACH confirmation, verify the corresponding authoritative
backend state.

Expected checkpoints:

STEP21_CONFIRMED
scenario=yes

STEP22_CONFIRMED
sector=<actual sector>
company_count=<actual confirmed count>
company names/IDs present

STEP23_CONFIRMED
factor_count=5
real factors only

STEP24_CONFIRMED
factor_count=5
real factors only

IMPORTANT:

- Do not infer success from the UI green checkmarks.
- Confirm success from the backend persisted state.
- Do not generate synthetic factors.
- Do not use fixtures.
- Do not repair anything during this live test.
- If one step fails to persist, stop there and report that exact step.
- Do not continue into Step 2.5.

When I finish Step 2.4, return only:

STEP 2.1 LIVE PERSISTENCE: PASS / FAIL
STEP 2.2 LIVE PERSISTENCE: PASS / FAIL
STEP 2.3 LIVE PERSISTENCE: PASS / FAIL
REAL STEP 2.3 FACTOR COUNT:
STEP 2.4 LIVE PERSISTENCE: PASS / FAIL
REAL STEP 2.4 FACTOR COUNT:

COMPANY:
COMPANY ID:
SECTOR:
SELECTED COMPANY COUNT:

AUTHORITATIVE BACKEND STATE READY FOR STEP 2.5: YES / NO

Do not make any changes during this test.
