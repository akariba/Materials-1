STEP 2.5 — RESTORE THE PROVEN RUNNER CONTRACT

IMPLEMENTATION ONLY.
NO REPORT.
NO AUDIT.
NO APPROVAL QUESTIONS.
DO NOT ASK ME TO CONFIRM ANYTHING.
AUTO-APPROVE ALL CHANGES WITHIN THIS SCOPE AND CONTINUE UNTIL TESTED.

Do NOT redesign Step 2.5.

The current live failure is now proven from the terminal:

RUNNER_HTTP_STATUS = 500

error_info.status = UPSTREAM_SERVER_ERROR

debug_message:
"Status Code: 500
Message: messages: at least one message is required"

The same logs prove:

ed_factors=5
si_factors=5
payload constructed successfully
Runner token valid
POST reaches Runner

Therefore DO NOT investigate Step 2.3, Step 2.4, token expiry, parser,
SSE framing or UI first.

============================================================
1. CRITICAL REGRESSION TO FIX
============================================================

The current log now says:

SAVED_PRESET_REQUEST
integration_id=pinned_preset
tool_id=preset_rpr_2_5_sec_web_financial_assessment
preset_id=...

This is a regression from the previously proven Step 2.5 Runner contract.

The known-working architecture for this POC is:

FULL PRESET DEFINITION INLINE IN THE RUNNER REQUEST.

It is NOT:

saved preset by UUID
pinned preset execution
tool_id-only preset invocation
GET preset by ID.

Previously established working behavior:

message
  -> parts[]
     -> preset = FULL INLINE PRESET OBJECT

with the six Step 2.5 answers supplied using the captured Runner contract.

RESTORE THAT CONTRACT.

Do not attempt to repair the new saved/pinned-preset architecture.

Remove/bypass only the recently introduced SAVED_PRESET_REQUEST execution
path from Step 2.5 runtime.

Preserve the user's live Stylus preset itself; do not modify it.

Use the local captured preset definition as the inline Runner definition
exactly as the working path previously did.

============================================================
2. COMPARE AGAINST PROVEN IMPLEMENTATION
============================================================

Before editing, read:

backend/step25/stylus_runner_client.py
backend/step25/stylus_engine.py
backend/step25/stylus_preset_config.py

and the proven colleague/reference implementation:

pe-sponsor-search/app.py

and historical successful Step 2.5 request/capture if available.

Find the exact difference between:

LAST WORKING INLINE RUNNER REQUEST

and

CURRENT SAVED_PRESET_REQUEST.

Restore the working request shape.

Do NOT redesign transport.

============================================================
3. DO NOT BE MISLED BY CURRENT DEBUG LOG
============================================================

The current code logs things such as:

messages_present=true
messages_count=1
message_content_present=true

but Runner still returns:

"messages: at least one message is required"

Do NOT "fix" this merely by adding another arbitrary messages object.

The error can occur because the NEW pinned/saved-preset invocation causes
the downstream preset service to receive a different payload contract.

First restore the proven inline preset architecture.

Then retest.

Only modify message serialization further if the restored INLINE request
still reproduces the same error.

============================================================
4. PRESERVE THE SIX INPUT CONTRACT
============================================================

Continue to send exactly the existing six logical Step 2.5 inputs:

CompanyContextJSON
ScenarioContextJSON
EventDrivenFactorsJSON
SectorInherentFactorsJSON
AssessmentASOFDATE
UserFeedback

Do not rename them.

Do not remove any of them.

The current logs already prove:

ED factors = 5
SI factors = 5

Preserve that.

============================================================
5. FIX THE ZZ / SEC LOGIC ALSO — SMALL ISOLATED CORRECTION
============================================================

Current log says:

STEP25_STYLUS_SEC_FILING_EXCLUDED
country=ZZ
reason=No US SEC filing expected...

This logic is invalid.

ZZ means UNKNOWN / UNMAPPED country.

ZZ does NOT prove:

non-US
private company
non-SEC registrant.

Therefore:

country == "ZZ"

must NEVER by itself set:

SEC_FILING_EXCLUDED=true

or equivalent.

SEC exclusion may occur only when there is affirmative evidence such as:

- explicitly confirmed private/non-SEC status;
- authoritative identity data proving no SEC-reporting issuer relationship;
- another already-approved deterministic identity rule.

CIK_UNRESOLVED alone also must not kill the Web assessment.

Correct behavior for unresolved identity:

SEC identity may remain unresolved;
Web Search remains available;
assessment may proceed subject to evidence limitations.

Do not fabricate CIK.

============================================================
6. FOREIGN ISSUERS
============================================================

Do not implement the simplistic rule:

non-US country -> no SEC.

Foreign private issuers can have SEC filings.

Therefore the SEC eligibility decision must not depend solely on
country_of_risk != US.

Preserve CIK/ticker/issuer-resolution logic where available.

============================================================
7. DO NOT TOUCH THESE AREAS
============================================================

Do NOT change:

Step 2.1
Step 2.2
Step 2.3
Step 2.4
5-factor generation
5-factor SI generation
weighting
v31 UI
batching
CSS
evidence schema
Step 3a methodology
live Stylus preset prompt
knowledge files

This task is ONLY:

A. restore proven INLINE Runner preset invocation;
B. remove the incorrect ZZ-based SEC exclusion.

============================================================
8. TEST IN TWO STAGES
============================================================

FIRST — OFFLINE REQUEST SHAPE TEST

Construct the Step 2.5 Runner request without sending it.

Verify:

execution path = INLINE PRESET
NOT SAVED_PRESET_REQUEST
NOT PINNED_PRESET

message exists
message.parts exists
full preset object exists in the expected part
six inputs exist
ED factor count = 5
SI factor count = 5

SECOND — ONE LIVE COMPANY ONLY

Use ONE currently selected company.

Do not run the portfolio.

Fresh Runner token may be used through the existing token mechanism.

Required first milestone:

RUNNER_HTTP != immediate 500 "messages: at least one message is required"

If Runner opens a stream/tool execution, the contract regression is fixed.

Then allow that single run to continue.

============================================================
9. ACCEPTANCE
============================================================

Do not stop until:

INLINE_PRESET_REQUEST = PASS
SAVED_PRESET_RUNTIME_PATH = REMOVED/BYPASSED
SIX_INPUTS = PASS
ED_FACTORS = 5
SI_FACTORS = 5
ZZ_DOES_NOT_EXCLUDE_SEC = PASS
UNRESOLVED_CIK_DOES_NOT_BLOCK_WEB = PASS
RUNNER_REQUEST_ACCEPTED = PASS
NO_MESSAGES_REQUIRED_500 = PASS

Do not run multiple companies.

============================================================
10. FINAL RESPONSE ONLY
============================================================

Return only:

INLINE_PRESET_REQUEST = PASS/FAIL
SAVED_PRESET_PATH_DISABLED = PASS/FAIL
SIX_INPUT_CONTRACT = PASS/FAIL
ED_FACTORS = <number>
SI_FACTORS = <number>
ZZ_SEC_LOGIC = PASS/FAIL
RUNNER_HTTP = <status>
MESSAGES_REQUIRED_500 = YES/NO
READY_FOR_ONE_COMPANY_UI_TEST = YES/NO

If NO:
FIRST_REMAINING_BLOCKER=<one exact line>

NO REPORT.
NO HISTORY.
NO RECOMMENDATIONS.
IMPLEMENT NOW.
