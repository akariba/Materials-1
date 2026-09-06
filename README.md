STEP 2.5 — EXACT LIVE REQUEST DIFF ONLY

STRICT MODE.

NO CODE CHANGES YET.
NO REPORT.
NO REFACTOR.
NO APPROVAL QUESTIONS.
DO NOT ASK ME TO PROCEED.
DO NOT RUN ANOTHER SPECULATIVE TEST.

The previous hypotheses have already been disproven and reverted:

1. singular `message` vs `message` + `messages`
2. tool_config.integrations populated vs empty
3. CIK-specific failure

DO NOT RETEST THEM.

I have now captured a CURRENT SUCCESSFUL request body directly from
the Stylus browser UI:

working_stylus_request.json

This is the GOLDEN CONTRACT.

The backend's current failing outgoing request already exists in the
debug/request artifacts.

============================================================
TASK
============================================================

Compare:

A. working_stylus_request.json
   = CURRENT SUCCESSFUL HUMAN/STYLUS UI REQUEST

against

B. the exact backend request that produced the current HTTP 500:
   "messages: at least one message is required"

Do a deep structural diff.

Do NOT compare documentation.
Do NOT compare memory.
Do NOT compare intended architecture.

Compare the ACTUAL serialized request bodies.

Inspect every level, especially:

- top-level keys
- message
- role
- content
- parts
- part ordering
- part types
- preset invocation object
- saved preset / pinned preset wrapper
- preset_id
- integration_id
- tool_id
- answers
- six Step 2.5 input values
- content_type
- mime_type
- application
- mode
- invoker
- request_id
- session_id
- temperature
- tool_config
- nested message/conversation structures
- omitted vs null
- empty string vs absent
- object vs array
- scalar vs list
- any browser-generated metadata the backend currently omits
- any backend-only fields absent from the successful browser request

Normalize only volatile values such as:
request IDs
session IDs
timestamps

Do NOT normalize structural differences.

============================================================
IMPORTANT
============================================================

The successful browser request is now authoritative.

Do not defend the current backend architecture if its serialized request
differs from the successful browser request.

Likewise, do not redesign anything beyond the proven difference.

The exact question is:

WHAT IS THE FIRST MATERIAL REQUEST-CONTRACT DIFFERENCE BETWEEN THE
CURRENT SUCCESSFUL STYLUS BROWSER CALL AND THE CURRENT FAILING BACKEND
CALL?

============================================================
AFTER THE DIFF
============================================================

If a concrete material difference is proven:

1. change ONLY that difference in the backend request builder;
2. preserve every other byte/behavior possible;
3. run its existing offline tests;
4. execute ONE company only;
5. stop immediately after determining whether Runner accepts the request.

Do not make a second fix in the same pass.

If no material structural difference exists, make NO production change.

In that case test the conclusion:

BROWSER_REQUEST_SUCCEEDS_NOW = YES
BACKEND_EQUIVALENT_REQUEST_FAILS_NOW = YES

which indicates the remaining difference is likely outside the JSON body,
for example transport/session/header/service context.

Do not guess which one until proven.

============================================================
FINAL OUTPUT — MAXIMUM 10 LINES
============================================================

GOLDEN_BROWSER_REQUEST = FOUND/NOT_FOUND
FAILING_BACKEND_REQUEST = FOUND/NOT_FOUND
FIRST_MATERIAL_DIFFERENCE = <exact field/path/value difference or NONE>
FILE_CHANGED = <file or NONE>
RUNNER_HTTP = <status or NOT_RUN>
MESSAGES_REQUIRED_500 = YES/NO
REQUEST_ACCEPTED = YES/NO
CHANGE_RETAINED = YES/NO
NEXT_BLOCKER = <one exact line or NONE>

NO LONG REPORT.
NO HISTORY.
NO SECOND EXPERIMENT.
