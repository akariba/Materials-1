CLIENT DEMO MODE — USE ONLY PROVEN WORKING DIRECT SOURCES.

DIRECT_FETCH_WORKS has been validated.

For the demo, do NOT use native ADK grounding.

Do NOT use opaque Google redirect URLs.

Do NOT rely on search snippets as evidence.

Use only direct publisher/source pages that are already proven accessible in this CCR environment.

==================================================
APPROVED DEMO SOURCE TYPES
==================================================

Use this priority:

1. SEC / EDGAR direct filing URLs
2. Official company Investor Relations pages
3. Official company newsroom / press release pages
4. Official annual report pages
5. Other direct official corporate disclosure pages

Only use Yahoo Finance / Investing.com if a direct fetch has already been confirmed to work.

==================================================
DEMO RETRIEVAL RULE
==================================================

For every external evidence item:

DIRECT SOURCE URL
→ HTTP fetch
→ page text
→ publisher/title/date
→ exact excerpt
→ deterministic CCR validation
→ display

The source page itself is the evidence.

==================================================
FIVE-COMPANY DEMO
==================================================

Build the demo around:

1. NVIDIA Corporation
2. Intel Corporation
3. Hut 8 Corporation
4. one strong resolved NVIDIA-related entity from current CAM artifacts
5. one additional strong resolved NVIDIA-related entity from current CAM artifacts

Prefer CoreWeave and Cerebras only if they are already present and resolvable in the existing CAM artifacts.

Do not fabricate relationships.

==================================================
EXTERNAL EVIDENCE
==================================================

For NVIDIA / Intel, reuse the known working direct sources that already passed:

- NVIDIA official newsroom / IR
- Intel SEC filing
- Intel SEC exhibit

For the other entities:

First inspect existing CAM candidates.

Then use a maximum of 1–3 direct official sources per relationship.

Do not perform broad discovery.

If no working direct official URL is quickly available:
keep the CAM relationship status as-is.

Do not block the demo.

==================================================
FRONTEND
==================================================

Populate:

- identity
- verified relationships
- review-required relationships separately
- exact CAM excerpts
- direct-source corroboration where available
- final direct URL
- publisher
- date if available
- evidence status

Verified = solid edge.
Review Required = dashed edge.

==================================================
DEMO SAFETY
==================================================

Disable or bypass:
- native ADK grounded search
- generic web enrichment
- broken live investigation path

If the user clicks external enrichment, either:
- use the direct-source path only, or
- show "External enrichment limited to verified direct sources for demo"

Do not expose provider errors.

==================================================
STOP CONDITION
==================================================

STOP as soon as:

- five companies are selectable
- NVIDIA is populated
- graph works
- Intel/Hut 8 relationships are visible
- two additional companies are visible
- evidence can be opened
- direct-source corroboration works where available
- no ADK dependency is required

Return exactly:

FIVE_COMPANY_DIRECT_SOURCE_DEMO_READY

or

FIVE_COMPANY_DIRECT_SOURCE_DEMO_READY_WITH_WARNINGS
