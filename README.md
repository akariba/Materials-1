The previous result BLOCKED_BY_DIRECT_SOURCE_ACCESS is not yet proven.

The run shows:

- SEC discovery candidates: 0
- ADK discovery: no_grounded_citations
- direct fetches: 0
- validation attempts: 0
- direct fetch errors: []

Therefore no direct publisher URL was actually fetched.

Do NOT run another discovery loop.

For this smoke test, BYPASS discovery and seed known authoritative direct URLs explicitly.

Test these NVIDIA / Intel sources:

1. NVIDIA official newsroom:
https://nvidianews.nvidia.com/news/nvidia-and-intel-to-develop-ai-infrastructure-and-personal-computing-products

2. NVIDIA Investor Relations:
https://investor.nvidia.com/news/press-release-details/2025/NVIDIA-and-Intel-to-Develop-AI-Infrastructure-and-Personal-Computing-Products/default.aspx

3. Intel SEC filing:
https://www.sec.gov/Archives/edgar/data/50863/000005086325000155/intc-20250915.htm

4. Intel SEC exhibit / announcement:
https://www.sec.gov/Archives/edgar/data/50863/000005086325000155/a09152025form8-kex991.htm

The expected facts are:

A. NVIDIA and Intel announced a collaboration to jointly develop data-center and PC products.

B. NVIDIA agreed to invest approximately $5 billion in Intel common stock.

==================================================
TEST ONLY DIRECT FETCH
==================================================

For each seeded URL:

1. Fetch the URL directly.
2. Report HTTP/result status.
3. Extract:
   - final URL
   - publisher
   - title
   - publication/filing date
   - source text
4. Search the returned source text for evidence relevant to:
   - NVIDIA / Intel strategic collaboration
   - NVIDIA $5bn Intel investment
5. Preserve an exact source excerpt.
6. Run the existing deterministic evidence validator.

Do NOT call ADK.
Do NOT use Google discovery.
Do NOT use SEC discovery.
Do NOT run CAM.
Do NOT run broader enrichment.

==================================================
IMPORTANT DIAGNOSTIC
==================================================

We need to distinguish:

A. DIRECT_FETCH_WORKS
   URLs can be retrieved and evidence extracted.

B. DIRECT_FETCH_NETWORK_BLOCKED
   Direct outbound retrieval itself is prohibited.

C. DIRECT_FETCH_PARSER_FAILED
   Page retrieved but parser cannot extract usable content.

D. EVIDENCE_VALIDATOR_FAILED
   Page and text retrieved, but CCR rejects otherwise valid evidence.

The previous status BLOCKED_BY_DIRECT_SOURCE_ACCESS must NOT be returned simply because discovery produced zero URLs.

==================================================
SUCCESS CONDITION
==================================================

At least one seeded direct source must produce:

- real publisher URL
- real source text
- source date
- exact evidence excerpt
- validated NVIDIA/Intel relationship evidence

Expected examples include:

NVIDIA ↔ Intel
relationship: strategic_partner / strategic_collaboration

NVIDIA → Intel
relationship: equity_investor / investor_in

==================================================
FINAL STATUS
==================================================

Return exactly one:

DIRECT_FETCH_WORKS

DIRECT_FETCH_NETWORK_BLOCKED

DIRECT_FETCH_PARSER_FAILED

EVIDENCE_VALIDATOR_FAILED

STOP after this test.
