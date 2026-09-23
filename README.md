Perform a READ-ONLY extraction coverage benchmark.

Do not modify code, databases, UI, prompts, taxonomies, or deployment.

PURPOSE

The reconciliation audit established that the Lending application currently has several different relationship universes:

- V3 strict portfolio artifact
- V2 candidate extraction
- normalized relationship store

The client has specifically questioned whether the current extraction is missing too many valid relationships.

We now need to determine where valid relationships are being lost.

Do not assume V3 is correct.
Do not assume V2 is correct.
Do not assume more relationships means better extraction.

==================================================
1. SELECT BENCHMARK DOCUMENTS
==================================================

Use a small representative benchmark set from the existing CAM source documents.

Include CoreWeave-related source documents if available.

Also identify any source documents involving entities such as NVIDIA or Anthropic if they actually exist in the repository.

Do not invent documents or expected relationships.

Use approximately 5-10 source documents, enough to represent different relationship families.

==================================================
2. BUILD A SOURCE-DOCUMENT RELATIONSHIP INVENTORY
==================================================

For each selected document, inspect the actual source content and identify relationship statements present in the document.

For every relationship record:

- subject entity
- related entity
- relationship wording
- relationship type suggested by the source
- direction if explicit
- state if explicit
- source document
- supporting text/reference
- whether an amount or commitment is stated

This is a benchmark inventory only.

Do not apply the current V3 relevance restrictions when constructing this inventory.

Do not create relationships that are not supported by the source.

==================================================
3. COMPARE AGAINST V3
==================================================

For every benchmark relationship determine:

- found in V3
- not found in V3
- partially represented
- represented under another relationship type
- entity resolution mismatch
- direction mismatch

Report V3 coverage per document and overall.

==================================================
4. COMPARE AGAINST V2
==================================================

For the same benchmark relationships determine:

- found in V2
- missing
- duplicate
- unresolved endpoint
- fragment endpoint
- relationship_key missing
- taxonomy mismatch
- review-required
- canonical
- rejected

==================================================
5. COMPARE AGAINST NORMALIZED STORE
==================================================

For the same benchmark determine whether each relationship exists in the normalized store and its final state:

- validated
- review-required
- rejected

For rejected benchmark relationships, identify the actual rejection reason(s).

Pay particular attention to:

- no strict narrative evidence
- low extraction confidence
- missing/conflicting state
- missing direction
- taxonomy mismatch
- entity-resolution problems

==================================================
6. TRACE LOSS THROUGH THE PIPELINE
==================================================

For every valid benchmark relationship that does not reach the final visible V3 portfolio view, classify where it was lost:

A. not extracted
B. extracted but entity resolution failed
C. extracted but taxonomy mapping failed
D. extracted but evidence gate failed
E. extracted but confidence gate failed
F. extracted but state/direction gate failed
G. extracted but deduplicated incorrectly
H. valid but outside V3 source/scope policy
I. valid in another store but excluded from global portfolio API
J. other — explain

==================================================
7. RELATIONSHIP FAMILY COVERAGE
==================================================

Compare benchmark coverage by family.

At minimum inspect where applicable:

- Commercial
- Financing
- Credit support
- Ownership / control
- Ownership / capital
- Concentration
- Operational dependency
- Supplier / supply-chain dependency
- Investment
- Off-taker / customer
- Guarantor
- Lender / agent bank

Identify relationships that the source clearly contains but the current taxonomy cannot represent cleanly.

==================================================
8. COREWEAVE / NVIDIA EXAMPLE
==================================================

If supported by repository sources, explicitly trace the relationships involving CoreWeave and NVIDIA.

If Anthropic is supported by repository sources, include it.

For each pair answer:

- Is there source evidence?
- Which source?
- Which relationship type?
- Was it extracted?
- Which store contains it?
- What state is it in?
- If rejected or absent from V3, why?

Do not use general market knowledge to create a relationship that is absent from the available sources.

==================================================
9. QUANTIFY COVERAGE
==================================================

Return benchmark metrics:

SOURCE-SUPPORTED RELATIONSHIPS
V3 FOUND
V3 MISSED
V2 FOUND
NORMALIZED FOUND
NORMALIZED VALIDATED
NORMALIZED REVIEW
NORMALIZED REJECTED

Calculate a simple benchmark recall for each extraction layer.

Also report precision problems found during manual inspection, but do not claim statistical portfolio-wide precision from this small benchmark.

==================================================
10. ANSWER THESE QUESTIONS DIRECTLY
==================================================

A. Is V3's strict source/scope policy materially suppressing legitimate relationships?

B. Are legitimate relationships being lost primarily during extraction, entity resolution, taxonomy mapping, or quality gating?

C. Does V2 provide useful high-recall candidate coverage that could feed a governed pipeline?

D. Are large numbers of normalized rejections actually valid relationships being rejected too aggressively?

E. Which current relationship families appear most under-extracted?

F. What specific changes should be tested next — without implementing them yet?

==================================================
OUTPUT
==================================================

Return:

1. EXECUTIVE FINDING
2. BENCHMARK DOCUMENT SET
3. SOURCE-SUPPORTED RELATIONSHIP INVENTORY
4. V3 COVERAGE
5. V2 COVERAGE
6. NORMALIZED STORE COVERAGE
7. LOSS-POINT ANALYSIS
8. TAXONOMY GAPS
9. COREWEAVE / NVIDIA TRACE
10. BENCHMARK METRICS
11. ROOT CAUSES OF MISSED RELATIONSHIPS
12. RECOMMENDED EXTRACTION EXPERIMENTS

Do not implement fixes.

Stop after the benchmark and diagnosis.
