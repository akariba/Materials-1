All RPR browser tabs/windows are now CLOSED.

Do not modify any code.

Do this sequence exactly:

1. Restart the existing backend cleanly.

2. With NO RPR browser open, monitor the backend for 90 seconds.

During those 90 seconds there must be ZERO new requests for:

- Step 1 market-event/discovery
- Step 2.1
- Step 2.2
- Step 2.3
- Step 2.4
- Step 2.5 /run

3. If the backend remains idle for 90 seconds, immediately run the
isolated Apple Step 2.5 test FROM THE TERMINAL ONLY.

Use:

Company: Apple Inc.
Ticker: AAPL
CIK: 0000320193

Do not open the browser.
Do not run Quick Setup.
Do not run another company.
Do not modify code.
Do not change the Stylus preset.
Do not work on Step 3.

Apple test hard maximum: 6 minutes.

Return only:

90-SECOND BACKEND IDLE TEST: PASS / FAIL

UNEXPECTED REQUESTS DURING IDLE:
<number and endpoint, or NONE>

APPLE TEST: PASS / FAIL
RUNNER TIME:
FINAL RESPONSE RECEIVED: YES / NO
ARTIFACT PARSED: YES / NO
EVIDENCE VALIDATED: YES / NO
SCORING CREATED: YES / NO
JOB COMPLETED: YES / NO

FAILURE POINT:
NONE or exact checkpoint
