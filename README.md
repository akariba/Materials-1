STOP ALL BROAD CHANGES.

No report.
No approval questions.
No refactor.
One isolated experiment only.

Keep the current proven SAVED_PRESET_REQUEST / pinned-preset architecture.
Do NOT revert to inline preset.

The live Runner failure is:

HTTP 500
"messages: at least one message is required"

You have now verified that the proven reference
pe-sponsor-search/app 1.py sends only the singular:

"message": runner_message

while the current Step 2.5 runner client sends both:

"message": runner_message,
"messages": [runner_message]

Do ONE isolated reversible experiment:

1. Preserve everything else byte-for-byte.
2. Remove only the redundant plural `messages` field from the outgoing
   Runner request.
3. Keep only the proven singular `message` field.
4. Do not modify preset architecture, six-key answers, SEC logic, UI,
   batching, Step 2.3, Step 2.4, token logic, or parser.
5. Run one company only.
6. If the request no longer returns the immediate
   "messages: at least one message is required" 500, stop and report success.
7. If the same error remains, immediately revert this one change and stop.

Do not make a second fix.

Return only:

SINGULAR_MESSAGE_ONLY = PASS/FAIL
RUNNER_HTTP = <status>
MESSAGES_REQUIRED_500 = YES/NO
CHANGE_RETAINED_OR_REVERTED = <value>
