Stop trying to make ADK grounding metadata itself satisfy the CCR evidence contract.

Implement a bounded direct-source fallback for CCR external enrichment.

The architecture should be:

SEARCH / DISCOVERY
→ RESOLVE REAL PUBLISHER URL
→ FETCH DIRECT SOURCE
→ EXTRACT GROUNDED EVIDENCE
→ CCR EVIDENCE VALIDATOR

The search provider is for discovery only.

==================================================
SOURCE PRIORITY
==================================================

Use sources in this order:

1. SEC / EDGAR
2. Official company investor-relations pages
3. Official annual reports
4. Official company press releases
5. Regulatory / exchange disclosures
6. Yahoo Finance
7. Investing.com
8. Other approved credible financial/business sources

Prefer primary sources whenever possible.

==================================================
GOOGLE SEARCH
==================================================

Google/simple search may be used to discover candidate URLs.

A Google search-result URL or Google redirect URL is NOT itself evidence.

Resolve/search for the actual publisher URL.

Examples:

sec.gov/...
investor.nvidia.com/...
intel.com/...
hut8.com/...
finance.yahoo.com/...
investing.com/...

Then fetch the publisher page directly.

==================================================
EVIDENCE CONTRACT
==================================================

A source can become accepted CCR evidence only after direct retrieval of the publisher/source page.

Capture:

- final resolved URL
- publisher/domain
- page/document title
- publication/filing date when available
- retrieval timestamp
- exact source excerpt
- entity pair
- relationship claim

Do not fabricate missing fields.

If publication date is genuinely unavailable, retain DATE_NOT_AVAILABLE rather than rejecting otherwise strong primary-source evidence solely because the page does not expose a date, unless existing governance explicitly requires a date.

==================================================
SEC
==================================================

For company relationships, search SEC directly wherever possible.

Use:

CIK
company name
10-K
10-Q
8-K
13D/G
S-1
424B
other relevant filings

Extract evidence directly from the SEC filing rather than from Google snippets.

==================================================
COMPANY ANNUAL REPORTS / IR
==================================================

Search official company domains for:

annual reports
investor-relations pages
press releases
partnership announcements
investment announcements
customer/supplier disclosures

Direct company disclosure should be treated as high-authority evidence.

==================================================
YAHOO FINANCE / INVESTING.COM
==================================================

These may be used as secondary sources for:

- market data
- financial metrics
- corporate events
- company profiles
- relationship/event discovery

Preserve the direct article/page URL and exact extracted text.

Do not use these to override contradictory SEC or official-company disclosures.

==================================================
BOUNDED SMOKE TEST
==================================================

Do not run the full NVIDIA universe yet.

Test only:

NVIDIA Corporation
+
Intel Corporation

Try to establish independently:

1. NVIDIA equity investment in Intel
2. NVIDIA / Intel strategic partnership

Use:

SEC
official NVIDIA/Intel sources
then Yahoo Finance / Investing.com only if useful.

Return for each evidence record:

source_type
publisher
final_url
title
publication_date
exact_excerpt
relationship_type
direction
evidence_status

Expected evidence_status:

SUPPORTS
CONTRADICTS
MENTIONS_ONLY
INSUFFICIENT

==================================================
IMPORTANT
==================================================

Do not depend on opaque Google redirect URLs.

Do not require ADK grounding metadata to contain the entire evidence record.

Google/search is discovery.
The directly retrieved publisher page is the evidence source.

Do not weaken source provenance.

==================================================
SUCCESS CRITERIA
==================================================

The smoke test passes if at least one direct source can be retrieved and produces:

- real publisher URL
- exact page text
- relationship evidence
- inspectable provenance

Return:

DIRECT_SOURCE_EVIDENCE_READY

or:

BLOCKED_BY_DIRECT_SOURCE_ACCESS

STOP after the NVIDIA/Intel smoke test.
