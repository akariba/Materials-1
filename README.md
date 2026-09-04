STOP ALL TESTING.

The Apple 6-minute test is NOT conclusive because you confirmed the old
32-company UI batch was still running concurrently on the same
single-worker FastAPI backend.

I want a completely clean backend before any further diagnosis.

Do NOT modify code.
Do NOT modify Stylus.
Do NOT modify the preset.
Do NOT start Apple.
Do NOT run Step 2.5.
Do NOT work on Step 3.

1. Stop/terminate all stale Step 2.5 test jobs and old in-flight Runner
   calls from this local development session.

2. Gracefully restart the existing local backend using the normal
   project startup method if that is the safest way to clear them.

3. After restart, verify there are ZERO active Step 2.5 assessment
   requests.

4. Verify the backend is healthy.

Return ONLY:

OLD 32-COMPANY BATCH: STOPPED / ACTIVE
OLD RUNNER CALLS: 0 / <number>
BACKEND RESTARTED: YES / NO
BACKEND HEALTH: PASS / FAIL
ACTIVE STEP 2.5 JOBS: <number>
READY FOR CLEAN APPLE TEST: YES / NO

DO NOT start Apple yet.
