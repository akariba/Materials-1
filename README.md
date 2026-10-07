Continue from the current CCR ADK self-containment task.

Current state:

- CCR runtime dependency audit complete.
- Isolated dependency lock added.
- CCR interpreter authority enforced.
- Stale runtime assumptions removed.
- Deterministic smoke coverage added.
- Clean candidate runtime validated.
- The current remaining blocker is:

BLOCKED_BY_GROUNDING

Do NOT revisit environment recreation, interpreter selection, package installation, RPR migration, CAM extraction, SEC enrichment, or NVIDIA enrichment unless the grounding investigation proves one of those is directly responsible.

This is now a targeted grounding-debug task.

==================================================
1. TRACE THE STRICT EVIDENCE PATH END TO END
==================================================

Run exactly one bounded ADK grounded-search smoke test.

Trace:

query
→ ADK agent
→ search tool
→ raw ADK events
→ grounding metadata
→ citation/source extraction
→ CCR normalization
→ strict evidence validator
→ final evidence status

Capture the state at every boundary.

Do not summarize prematurely.

==================================================
2. INSPECT RAW ADK GROUNDING OBJECTS
==================================================

Before CCR transforms the response, inspect the raw runtime objects.

Determine whether ADK returns any of:

- grounding_metadata
- grounding_chunks
- grounding_supports
- web sources
- source URLs
- source titles
- retrieved snippets
- search entry points
- citation metadata
- publication dates

Do not expose secrets.

Report the actual object field names present in the installed ADK/GenAI versions.

The key question is:

A. the provider returned no usable grounding

OR

B. grounding exists but CCR failed to extract it

Prove which one.

==================================================
3. TRACE EVERY REJECTED CITATION
==================================================

For every candidate citation rejected by the strict evidence layer, report:

- raw provider object
- extracted URL
- extracted title/publisher
- extracted date
- extracted snippet/excerpt
- grounding/support reference
- exact rejection reason

Classify each rejection as:

MISSING_URL
MISSING_GROUNDING
MISSING_EXCERPT
MISSING_DATE
NON_EXTERNAL_URL
UNSUPPORTED_SCHEMA
SERIALIZATION_LOSS
PARSER_BUG
OTHER_CONFIRMED_REASON

Do not simply report "no grounded citations."

==================================================
4. VERIFY THE SEARCH TOOL REALLY EXECUTED
==================================================

Confirm at runtime:

- the approved search tool is attached to the ADK agent;
- the tool actually executed;
- the answer was not generated only from model knowledge;
- grounding/search events were emitted.

If no search tool execution occurred, return:

BLOCKED_BY_SEARCH_TOOL_CONFIGURATION

==================================================
5. COMPARE RAW PROVIDER OUTPUT TO CCR EXPECTATIONS
==================================================

Document the exact CCR strict evidence contract.

For example:

URL required?
publisher/title required?
publication date required?
verbatim snippet required?
grounding support ID required?

Then compare that contract field-by-field with what ADK actually returns.

Do NOT weaken the evidence contract yet.

First determine exactly which required field is failing.

==================================================
6. CHECK SDK-SCHEMA COMPATIBILITY
==================================================

The current CCR environment may use a newer ADK/GenAI version than the older reference implementation.

Inspect whether CCR's citation parser expects an older object schema.

Check for renamed/moved fields such as:

grounding_metadata
grounding_chunks
grounding_supports
web
uri/url
title
segment/text

If the data exists under a new schema, make the CCR adapter version-tolerant.

Do not blindly downgrade packages.

==================================================
7. APPLY THE SMALLEST VERIFIED FIX
==================================================

Only after root cause is proven, apply the smallest fix.

Acceptable fixes include:

- extract grounding from the correct current SDK field;
- preserve grounding metadata before serialization;
- correctly map grounding chunks/supports;
- correctly extract real external URLs;
- correctly associate grounded snippets with URLs;
- support both known ADK response schemas.

Do NOT:

- fabricate URLs;
- fabricate publication dates;
- use model-written citations as grounded evidence;
- accept internal gateway URLs as external sources;
- weaken fail-closed behavior.

==================================================
8. RUN ONE STRICT GROUNDED-SMOKE TEST
==================================================

After the fix, run one fresh-process smoke test.

Require:

search tool executed = YES
grounding metadata present = YES
external URL count >= 1
grounded excerpt count >= 1
accepted strict evidence records >= 1

Report:

simple_answer_status
strict_evidence_status
search_tool_execution
grounding_metadata_present
external_urls
accepted_citations
rejected_citations

Show one accepted evidence record.

==================================================
9. DO NOT CONTINUE TO NVIDIA YET
==================================================

Even if the grounding smoke test passes, STOP.

Do not rerun:
- NVIDIA enrichment
- CAM
- SEC
- reconciliation
- graph analytics

The infrastructure must be proven first.

==================================================
FINAL STATUS
==================================================

Return exactly one:

CCR_ADK_GROUNDING_READY

BLOCKED_BY_SEARCH_TOOL_CONFIGURATION

BLOCKED_BY_PROVIDER_GROUNDING

BLOCKED_BY_CITATION_ADAPTER

BLOCKED_BY_EVIDENCE_CONTRACT

BLOCKED_BY_SDK_SCHEMA_MISMATCH

ROOT_CAUSE_NOT_PROVEN
