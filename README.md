Good. The ADK runtime/interpreter issue is now resolved.

The CCR project is using the correct virtual environment and the bounded ADK request completes successfully.

Do NOT revisit package installation or interpreter configuration unless new evidence shows a regression.

The remaining blocker is now specifically the grounding/citation contract.

Current smoke-test result:

- ADK application status: OK
- Request completed successfully
- Attempts: 1
- Answer returned: ~1,526 characters
- Grounding events: 1
- External citations: 0
- Accepted evidence records: 0
- Rejected citations: 5
- Final evidence status: no_grounded_citations

The NVIDIA external-enrichment phase remains paused.

Yesterday this ADK/web-search pattern worked using the APR/RPR project implementation as the reference.

Your task is to determine why ADK is now returning an answer but CCR is not obtaining valid external URL/date/verbatim-excerpt citation records.

DO NOT redesign the solution.
DO NOT replace ADK.
DO NOT use public web search outside the approved ADK mechanism.
DO NOT rerun the full NVIDIA enrichment yet.

==================================================
1. COMPARE WITH THE APR/RPR KNOWN-WORKING IMPLEMENTATION
==================================================

Locate the APR/RPR implementation we used as the working reference yesterday.

Compare the complete ADK web-search path against the current CCR implementation.

Specifically compare:

- Agent/model construction
- model name
- tools configuration
- Google Search / enterprise search tool configuration
- Runner/session setup
- API/version configuration
- response/event streaming
- grounding metadata extraction
- citation extraction
- URL extraction
- title/source extraction
- publication date extraction
- text/snippet extraction
- final response serialization

Do not compare only prompts.

Trace the full working data path.

==================================================
2. INSPECT THE RAW ADK RESPONSE/EVENT OBJECT
==================================================

For one bounded smoke query, inspect the raw ADK response/events before CCR transforms them.

Do not expose secrets or tokens.

Determine whether the raw ADK result actually contains any of the following or SDK-equivalent structures:

- grounding metadata
- grounding chunks
- grounding supports
- web/source objects
- citation metadata
- retrieved context metadata
- URLs
- source titles
- snippets
- search-entry points

Record which fields are present.

The key question is:

A. ADK is not returning grounded sources at all

OR

B. ADK returns source metadata, but the CCR wrapper/parser is failing to extract it

Prove which one is true.

==================================================
3. TRACE THE 5 REJECTED CITATIONS
==================================================

The previous smoke run reported:

rejected citations = 5

Inspect each rejected item.

For each show:

- raw citation/source representation
- URL present? yes/no
- source title present? yes/no
- publication date present? yes/no
- source excerpt/snippet present? yes/no
- exact rejection reason

Determine whether they are being rejected because of:

- missing URL
- internal/non-external URL
- missing date
- missing verbatim source text
- malformed URL
- parser mismatch
- unsupported ADK response schema
- metadata lost during serialization
- other confirmed reason

Do not just report "failed grounding."

==================================================
4. CHECK SDK VERSION DIFFERENCE AGAINST APR/RPR
==================================================

Current CCR environment:

- google-adk 2.11.0
- google-genai 2.28.0

APR/RPR reference environment:

- google-adk 2.6.1
- google-genai 2.16.0

Determine whether the response/citation/grounding object schema changed between these versions in a way that affects the current parser.

Do NOT downgrade immediately.

First inspect actual runtime objects and the relevant installed SDK interfaces.

If CCR's parser expects the older APR/RPR response structure, identify the exact mismatch.

Prefer making the adapter version-tolerant rather than blindly downgrading, unless repository constraints clearly require exact version parity.

==================================================
5. VERIFY THE SEARCH TOOL IS ACTUALLY ENABLED
==================================================

Confirm that the working smoke test is not merely calling the LLM without an active search tool.

Verify at runtime:

- which agent is instantiated
- which tools are attached
- whether the approved search tool is present
- whether a search/grounding event actually executes
- whether source metadata returns from that tool

An answer generated from model knowledge alone is NOT a successful web-search test.

==================================================
6. CHECK THE CCR CITATION CONTRACT
==================================================

Trace the current CCR requirement for a web evidence record.

Current expected minimum appears to be:

- external URL
- source/publication date
- exact/verbatim excerpt or source text

Confirm the actual code contract.

Then determine whether ADK provides:

- all three directly
- some fields directly and some derivable from grounded source metadata
- or insufficient evidence

Do not weaken the contract merely to make the test pass.

==================================================
7. APPLY THE SMALLEST FIX
==================================================

Once the exact mismatch is proven, apply only the smallest necessary fix.

Examples of acceptable fixes:

- read grounding metadata from the correct ADK SDK field
- support both old and new ADK response schemas
- preserve grounding metadata before response serialization
- correctly extract external URLs from grounding chunks
- correctly map source title/snippet/date fields
- fix the CCR adapter dropping citation metadata

Do NOT fabricate missing dates/excerpts.

Do NOT treat internal gateway URLs as external citations.

Do NOT accept model-written URLs unless grounded metadata proves them.

==================================================
8. RUN A NEW BOUNDED SMOKE TEST
==================================================

Use one simple query involving NVIDIA and one known company.

The smoke test must prove the full path:

ADK search executes
→ grounded source returned
→ real external URL extracted
→ publisher/source extracted
→ date extracted when genuinely available
→ exact source excerpt/snippet retained
→ CCR evidence contract evaluates it

Report:

ADK request: PASS/FAIL
Search tool execution: PASS/FAIL
Grounding metadata present: YES/NO
External URLs: count
Accepted citations: count
Rejected citations: count
Evidence-contract result: PASS/FAIL

Show one accepted citation record if available.

==================================================
9. COMPARE APR/RPR VS CCR
==================================================

Produce a concise comparison:

APR/RPR known-working path:
- ADK version
- GenAI version
- search tool
- grounding response fields
- citation extraction path

CCR current path:
- ADK version
- GenAI version
- search tool
- grounding response fields
- citation extraction path

Exact difference:
- ...

==================================================
10. FINAL STATUS
==================================================

Return exactly one:

ADK_GROUNDED_SEARCH_READY

ADK_GROUNDED_SEARCH_READY_WITH_WARNING

BLOCKED_BY_SEARCH_TOOL_CONFIGURATION

BLOCKED_BY_ADK_GROUNDING_RESPONSE

BLOCKED_BY_CITATION_ADAPTER

BLOCKED_BY_EVIDENCE_CONTRACT

BLOCKED_BY_SDK_VERSION_MISMATCH

ROOT_CAUSE_NOT_PROVEN

STOP after the bounded grounded-search smoke test.

Do NOT resume full NVIDIA external enrichment automatically.
