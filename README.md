FIX THE CURRENT STEP 2.5 BACKEND FAILURE NOW.

NO REPORT.
NO AUDIT.
NO APPROVAL QUESTION.
IMPLEMENT, TEST, CONTINUE AUTONOMOUSLY.

The exact live error is:

call_stylus_preset() got an unexpected keyword argument 'sec_filing_excluded'

The new SEC identity short-circuit is conceptually correct and MUST be
preserved.

Find the caller that passes:

sec_filing_excluded=...

into call_stylus_preset().

Then inspect the ACTUAL call_stylus_preset() signature and current inline
preset/tool-config construction.

Fix the interface mismatch minimally.

IMPORTANT:

- Do NOT remove SEC Identity Short-Circuit.
- Do NOT change the live Stylus preset.
- Do NOT change Step 2.3/2.4.
- Do NOT fabricate SEC evidence.
- Do NOT broadly refactor Runner code.
- Do NOT add an unused parameter merely to silence Python unless that
  parameter genuinely belongs in the function contract.

Correct behavior:

If SEC is excluded for a company:
  - Runner request still executes;
  - Web Search remains available;
  - SEC tool is not invoked for that company;
  - the assessment receives the SEC-unavailable/excluded state through the
    appropriate context/prompt/tool configuration;
  - Step 2.5 continues normally.

If SEC is allowed:
  - existing SEC + Web behavior remains intact.

After fixing:

1. py_compile/lint affected files.
2. Run one NON-SEC Step 2.5 company.
3. Confirm the job gets past call_stylus_preset().
4. Confirm Web Search executes.
5. Confirm SEC is skipped.
6. Confirm no `unexpected keyword argument` remains.
7. Do NOT run a portfolio batch.

Return only:

SEC_SHORT_CIRCUIT_WIRING = PASS/FAIL
CALL_STYLUS_PRESET = PASS/FAIL
NON_SEC_RUN_REACHED_RUNNER = PASS/FAIL
WEB_AVAILABLE = PASS/FAIL
SEC_SKIPPED = PASS/FAIL
FIRST_REMAINING_BLOCKER=<only if any>
