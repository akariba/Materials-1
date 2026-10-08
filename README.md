CLEANUP PHASE IS COMPLETE.

Now implement ONE bounded NVIDIA end-to-end backend integration.

Do NOT redesign the frontend yet.
Do NOT create new storage technology.
Do NOT create SQLite.
Do NOT restore demo-only paths.

Use the cleaned current architecture:

Parquet = persistent analytical artifacts
DuckDB = analytical/query layer
API = application access layer

==================================================
1. NVIDIA CAM FACTS
==================================================

Using the existing CAM index and canonical entity data, extract all available
NVIDIA-related facts already present in CAM.

Populate where available:

- Citi EXP
- TFA
- facilities
- lending exposure
- RLR
- FORR
- country of risk
- industry/sector
- parent/subsidiary hierarchy
- ownership
- guarantor
- collateral
- maturity
- customer/supplier relationships
- investment
- strategic partnership
- contractual relationship
- lease/offtake
- other explicit relationship facts

Every value must retain provenance.

Do not fabricate missing values.

==================================================
2. CANONICAL RELATIONSHIP STORAGE
==================================================

Use the current canonical relationship schema.

Verified DIRECT relationships must live in the current persistent
relationship artifact, preferably the existing Parquet equivalent.

Preserve separately:

- source_entity_id
- target_entity_id
- relationship_type
- subtype
- direction
- fact_class
- source_type
- source_document/url
- source_excerpt
- source_date
- confidence
- evidence_status
- relationship_strength
- provenance

Do not collapse multiple relationship types for the same entity pair.

Example:

NVIDIA ↔ Intel strategic partnership

and

NVIDIA → Intel equity investment

must remain separate relationship records.

==================================================
3. FACT CLASSIFICATION
==================================================

Maintain:

FACT
DERIVED
EXPOSURE
AI_CANDIDATE

FACT:
explicit CAM or validated external evidence

DERIVED:
deterministic result from verified facts

EXPOSURE:
Citi internal exposure data such as Citi EXP/TFA

AI_CANDIDATE:
AI-proposed relationship requiring evidence/review

Do not mix these classes.

==================================================
4. R2D2 ENRICHMENT
==================================================

Use the existing approved R2D2 adapter.

Generate targeted retrieval tasks for current NVIDIA relationship candidates:

- ownership
- hierarchy
- investment
- supplier/customer
- strategic partnership
- financing
- guarantee
- collateral
- lease/offtake
- shared project
- SPV
- commercial dependency

R2D2 output is supporting evidence/context only.

It does not automatically create VERIFIED relationships.

==================================================
5. OPUS REFINEMENT
==================================================

Use the existing Opus integration after CAM + R2D2 evidence exists.

Input:

- canonical entities
- CAM facts
- CAM relationship candidates
- R2D2 evidence
- existing direct-source evidence
- current verified relationship graph

Opus may:

- reconcile entities
- normalize relationship type
- determine direction
- identify contradictions
- deduplicate
- rank candidates
- identify possible hidden relationships

Opus may NOT:

- invent Citi EXP/TFA
- fabricate relationship evidence
- promote unsupported candidates to FACT

Require schema-valid JSON.

==================================================
6. DIRECT SOURCE VALIDATION
==================================================

Reuse the already working direct-source pipeline:

real URL
→ fetch
→ source text
→ publisher/title/date
→ exact excerpt
→ deterministic validator

Priority:

SEC / EDGAR
official investor relations
official company newsroom
annual report
approved direct publisher

Do not return to ADK grounding debugging.

==================================================
7. INDIRECT RELATIONSHIPS
==================================================

Generate indirect relationships ONLY from verified graph edges.

Example:

NVIDIA → A
A → B

produces:

NVIDIA → A → B

Store:

- origin
- destination
- path entity IDs
- hop_count
- relationship types
- path strength
- evidence references for every underlying edge

Use the recovered typed-path implementation if available.

Do not ask the LLM to invent indirect paths.

==================================================
8. HIDDEN RELATIONSHIPS
==================================================

R2D2/Opus may identify hidden dependencies.

Initially store these as:

AI_CANDIDATE
REVIEW_REQUIRED

Examples:

- common supplier
- common customer
- shared project
- common SPV
- shared guarantor
- shared financing source
- infrastructure dependency

Only promote after independent supporting evidence is validated.

==================================================
9. DUCKDB VIEWS
==================================================

Expose the canonical data through DuckDB views.

At minimum confirm readable views for:

- canonical entities
- CAM facts
- exposures
- direct relationships
- relationship candidates
- indirect paths
- evidence/provenance

No duplicate source-of-truth database.

==================================================
10. NVIDIA ACCEPTANCE TEST
==================================================

Confirm:

[ ] NVIDIA canonical identity resolves
[ ] CAM Citi EXP populated where present
[ ] CAM TFA populated where present
[ ] RLR/FORR populated where present
[ ] hierarchy/ownership facts extracted
[ ] direct relationships persisted
[ ] multiple edges between same pair preserved
[ ] R2D2 executes
[ ] Opus returns valid structured output
[ ] direct-source validator works
[ ] indirect paths generated from verified edges
[ ] hidden candidates remain review-required
[ ] provenance retained
[ ] no SQLite production dependency
[ ] no RPR dependency
[ ] no demo data dependency
[ ] tests pass

STOP before frontend integration.

Report:

NVIDIA FACTS:
<count>

DIRECT RELATIONSHIPS:
<count>

INDIRECT PATHS:
<count>

HIDDEN / AI CANDIDATES:
<count>

CITI EXP:
POPULATED / NOT_PRESENT_IN_CAM

TFA:
POPULATED / NOT_PRESENT_IN_CAM

R2D2:
WORKING / BLOCKED

OPUS:
WORKING / BLOCKED

DIRECT SOURCE:
WORKING / BLOCKED

DUCKDB VIEWS:
<list>

TESTS:
<passed>/<total>

Return:

NVIDIA_BACKEND_READY

or

NVIDIA_BACKEND_READY_WITH_WARNINGS

or

NVIDIA_BACKEND_BLOCKED