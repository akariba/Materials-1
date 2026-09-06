STEP 2.5 — FIND THE REQUEST REGRESSION FROM THE LAST PROVEN SUCCESS

IMPLEMENTATION TASK.
NO GENERAL REPORT.
NO APPROVAL QUESTIONS.
DO NOT ASK ME WHETHER TO PROCEED.
ALL ACTIONS INSIDE THIS SCOPE ARE PRE-APPROVED.
CONTINUE AUTONOMOUSLY UNTIL THE SINGLE-COMPANY ACCEPTANCE TEST PASSES
OR UNTIL A GENUINE EXTERNAL RUNNER BLOCKER IS PROVEN.

IMPORTANT CURRENT STATE

The previous isolated experiment is finished and reverted.

PROVEN:

SINGULAR_MESSAGE_ONLY = FAIL
RUNNER_HTTP = 500
MESSAGES_REQUIRED_500 = YES

Therefore:

DO NOT retry message-vs-messages experiments.
DO NOT change parser/SSE framing.
DO NOT change Step 2.3.
DO NOT change Step 2.4.
DO NOT change Step 2.5 UI.
DO NOT change weighting.
DO NOT change SEC/CIK behavior.
DO NOT change token logic.
DO NOT change the Stylus live preset.
DO NOT revert the saved/pinned-preset architecture.

The current saved/pinned-preset six-input architecture had successful
Step 2.5 live runs previously.

Known successful run IDs include:

step25stylus_af7dfb79753c4410
step25stylus_a83c86e280b84626

Use the repository's persisted run/debug/request artifacts for those
successful runs as the GOLDEN BASELINE.

============================================================
1. DO NOT MODIFY CODE YET
============================================================

Before changing runtime code, locate the actual persisted request/raw
Runner artifacts belonging to at least one successful run above.

Also locate the current failing run's exact outgoing Runner request.

Do not reconstruct either request from memory.

Do not use repo documentation as a substitute when raw request artifacts
exist.

The goal is an EXACT structural comparison:

SUCCESSFUL_REQUEST
versus
CURRENT_FAILING_REQUEST

============================================================
2. COMPARE THE COMPLETE OUTGOING REQUEST CONTRACT
============================================================

Compare every relevant field, including nesting and value type:

top-level keys
application
invoker
mode
request_id
session_id
temperature
tool_config
message
messages, if historically present
message.role
message.content
message.parts
part data/content
preset/tool invocation object
integration_id
tool_id
preset_id
preset version/config
answers/input mapping
CompanyConte
ScenarioCont
EventDrivenF
SectorInhere
AssessmentAS
UserFeedback

Also compare:

null versus omitted
empty string versus populated value
object versus array
string versus JSON object
field casing
field order only if the receiving API historically depends on it
content_type / mime_type
nested `messages` or conversation fields inside the preset/tool payload
rather than only top-level fields.

The current Runner error is:

HTTP 500
UPSTREAM_SERVER_ERROR
"messages: at least one message is required"

Do not assume this refers to the top-level request field.

Identify which exact successful-vs-failing structural difference can make
the downstream saved-preset execution believe no conversation message was
provided.

============================================================
3. PAY PARTICULAR ATTENTION TO RECENT REQUEST-BUILDER CHANGES
============================================================

Inspect recent changes around:

stylus_runner_client.py
stylus_engine.py
stylus_preset_config.py

and any request/preset serialization helper.

Determine whether the successful September 2 request had:

- a different `message.parts` structure;
- preset invocation in a different part;
- a text/content part accompanying the preset invocation;
- different answer placement;
- different content_type;
- different integration/tool wrapper;
- different nested conversation structure;
- a non-empty field that is now empty/omitted.

Do not infer. Prove it from the successful request.

============================================================
4. MAKE ONLY THE SMALLEST PROVEN FIX
============================================================

Once the exact regression is found:

make ONLY the minimum change required to restore the successful request
shape.

Do not perform cleanup/refactoring around it.

Do not change unrelated request fields.

Add a focused regression test that compares the current request builder
against the relevant shape of the known successful request.

============================================================
5. ONE LIVE TEST ONLY
============================================================

After the exact request-shape regression is fixed:

run ONE company only.

Do not run a batch.

Acceptance milestone:

Runner must no longer immediately return:

"messages: at least one message is required"

If Runner accepts the request and opens normal execution/tool activity,
allow that single run to continue.

Do not introduce a second speculative fix during the same test.

============================================================
6. IF NO RAW SUCCESSFUL REQUEST EXISTS
============================================================

Only if no historical outgoing request artifact exists:

use the closest actual raw successful Runner SSE/request capture and the
known-working saved-preset code state to reconstruct the request shape.

But do not change runtime code until you can state one concrete structural
difference supported by repository evidence.

============================================================
7. FINAL RESPONSE — SHORT ONLY
============================================================

Return only:

GOLDEN_SUCCESS_REQUEST_FOUND = YES/NO
CURRENT_FAILING_REQUEST_FOUND = YES/NO

FIRST_PROVEN_REQUEST_DIFFERENCE =
<one concise line>

FILE_CHANGED =
<file or NONE>

RUNNER_HTTP =
<status or NOT_RUN>

MESSAGES_REQUIRED_500 =
YES/NO

REQUEST_ACCEPTED_BY_RUNNER =
YES/NO

READY_FOR_ONE_COMPANY_UI_TEST =
YES/NO

If NO:

FIRST_REMAINING_BLOCKER =
<one exact line>

NO HISTORY.
NO LONG REPORT.
NO SECOND SPECULATIVE FIX.
