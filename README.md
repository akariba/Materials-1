STOP ALL FURTHER UI WORK.

The actual browser runtime has exposed a compile failure that your previous
source-inspection validation did not catch.

CURRENT REAL ERROR:

[plugin:vite:oxc] Transform failed
[PARSE_ERROR] Expected '}' but found 'Identifier'
'}' expected

File:
frontend/src/pages/PortfolioAnalytics.tsx

The browser points approximately to:
122364..122370

TASK:

Fix ONLY the syntax / TSX parse error preventing the Lending application
from compiling.

Do not redesign anything further.
Do not add features.
Do not change backend.
Do not change APIs.
Do not modify V1/V2/V3.
Do not modify relationship data.
Do not modify portfolio calculations.
Do not touch external-overlay logic.
Do not touch Stylus/R2D2/SEC.
Do not touch CCR.

Inspect the code around the reported location and also inspect the immediately
surrounding JSX/TSX blocks for:

- missing }
- missing )
- missing >
- malformed JSX attribute
- incorrectly nested JSX
- unterminated template literal
- malformed object literal
- malformed conditional rendering
- accidental text/identifier inside JSX or JavaScript expression

Fix the smallest possible scope.

After fixing:

1. Save the file.
2. Let the existing Vite dev server recompile.
3. Open:
   http://127.0.0.1:5174/lending
4. Confirm the Vite red error overlay is gone.
5. Confirm the Lending page actually renders.
6. Check browser console for runtime errors.
7. Navigate Overview -> Clients -> Network and confirm each route renders.

Do NOT claim PASS based only on code inspection.

The browser rendering is the acceptance test.

Final response only:

TSX PARSE ERROR FIXED: YES / NO
VITE COMPILE: PASS / FAIL
/lending RENDERS: PASS / FAIL
OVERVIEW: PASS / FAIL
CLIENTS: PASS / FAIL
NETWORK: PASS / FAIL
BROWSER CONSOLE ERRORS: <count>

FILES MODIFIED:
<files>

DATA/BACKEND/V3 CHANGED: YES / NO

Then STOP.
