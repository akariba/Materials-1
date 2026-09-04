Do not modify code.

I am about to click Run Assessment ONCE.

Monitor the backend logs.

The expected sequence is:

1. POST /api/v1/rpr/step25/context
2. Verify:
   company = Apple Inc.
   Step 2.1 scenario present = true
   Step 2.3 confirmed = true
   Step 2.3 factor count = 5
   Step 2.4 confirmed = true
   Step 2.4 factor count = 5
3. ONLY if all of the above pass, allow POST /step25/run.

If context registration returns anything other than real 5 ED + real 5 SI,
the frontend/backend gate must prevent Runner from starting.

Do not change code.
Just monitor this one click and report the context values.
