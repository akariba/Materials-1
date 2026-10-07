You are continuing work on the existing CCR Relationship Intelligence repository.

The CAM indexing phase is complete enough to proceed.

Current validated state:

- CAM_INDEX_READY_WITH_WARNINGS
- 66 CAM documents in scope
- 60 successfully parsed
- 6 PDF timeouts remain recorded as coverage warnings
- 3,565 indexed passages
- entity-mention resolution has been repaired
- NVIDIA Corporation exact-name resolution works
- bare NVIDIA remains ambiguous when appropriate
- NVIDIA reconciliation completed successfully
- 43 NVIDIA-related passages are available from the indexed CAM corpus
- source/document/page/section provenance is preserved

Do NOT repeat the indexing work.
Do NOT rebuild the canonical entity master.
Do NOT perform another architecture audit.

This is an EXECUTION task.

The objective is:

Take the existing retrieved NVIDIA CAM passages and determine which passages establish actual evidence-backed relationships between NVIDIA and another entity.

Use this pipeline:

RETRIEVED NVIDIA PASSAGES
→ MAP: relationship extraction
→ SEMANTIC LLM CHECKER
→ DETERMINISTIC CHECKER
→ REDUCE / DEDUPLICATE
→ FINAL VERIFIED NVIDIA CAM RELATIONSHIPS

Do not proceed to SEC or web enrichment yet.

==================================================
PHASE 1 — LOAD THE EXISTING NVIDIA RETRIEVAL SET
==================================================

Reuse the existing indexed artifacts.

Locate and load the NVIDIA retrieval results already produced from:

cam_passages
cam_entity_mentions
NVIDIA reconciliation artifacts
canonical entity data

Do not rescan the complete raw CAM folder unless needed to retrieve surrounding context for an already-selected passage.

Start from the existing approximately 43 NVIDIA-related passages.

For every input passage retain:

document_id
filename
source_folder
page
section
heading
passage_id
exact passage text
retrieval method
canonical NVIDIA seed identity

Do not modify the original evidence text.

==================================================
PHASE 2 — ADD ONLY NECESSARY SURROUNDING CONTEXT
==================================================

For each NVIDIA passage, retrieve limited neighboring context when required to interpret the relationship correctly.

Examples:

- previous paragraph
- next paragraph
- same section
- relevant table row/header

Do not send entire CAMs to the model unless the existing passage is impossible to interpret without broader context.

Record exactly which context was supplied.

==================================================
PHASE 3 — MAP: EVIDENCE-BASED RELATIONSHIP EXTRACTION
==================================================

Run relationship extraction independently across the retrieved evidence units.

This is the MAP stage.

The objective is to identify explicit relationships such as:

ownership
parent/subsidiary
guarantee
lender/borrower
customer/supplier
major customer
major supplier
commercial dependency
strategic partnership
joint venture
investment
sponsor/SPV
distribution
licensing
service provider
technology dependency
financing relationship
other explicitly evidenced relationships

Do not force findings into the example taxonomy if another legitimate relationship is explicitly supported.

For every proposed relationship return:

source_entity_name
target_entity_name
relationship_type
direction
relationship_details

source_document_id
source_filename
page
section
passage_id

exact_evidence_excerpt

maker_confidence
maker_model
extraction_version

IMPORTANT RULES:

1. A co-mention is NOT a relationship.
2. The relationship must be supported by exact text.
3. Direction must be explicit or strongly grounded.
4. If evidence is insufficient, return NO_RELATIONSHIP.
5. Do not use graph proximity, Jaccard, hop distance or existing network structure as evidence.
6. Do not infer a relationship merely because it is economically plausible.
7. Preserve exact CAM evidence.

==================================================
PHASE 4 — RESOLVE THE OTHER ENTITY
==================================================

For each proposed relationship, resolve the non-NVIDIA entity against the existing canonical entity universe.

Use the repaired precedence:

1. exact identifier
2. exact canonical legal name
3. exact validated alias
4. case-insensitive exact legal/alias
5. controlled normalized matching
6. existing conservative fuzzy fallback

Return:

extracted_entity_name
canonical_entity_id
CAGID
GFCID
CIK if available
LEI if available
resolution_method
resolution_status
ambiguity_reason

Allowed statuses:

MATCHED
AMBIGUOUS
UNRESOLVED

Do not force ambiguous entities.

A relationship with an ambiguous target may be retained as REVIEW_REQUIRED but must not silently become VERIFIED.

==================================================
PHASE 5 — SEMANTIC LLM CHECKER
==================================================

Add an independent semantic checker for each maker relationship.

This checker must receive:

- original source passage
- necessary surrounding context
- maker-proposed relationship
- resolved entity identities

The checker must independently decide whether the relationship is actually supported.

The checker should validate:

- source entity
- target entity
- relationship type
- direction
- exact evidence
- whether the claim is speculative
- whether the evidence merely co-mentions the entities
- whether the evidence refers to the correct legal entity

Return exactly one of:

ACCEPT
REJECT
CORRECT
NEEDS_REVIEW

If CORRECT, return the corrected relationship.

Also return:

checker_reason
checker_confidence
checker_model
evidence_supported = true/false

The semantic checker must not simply repeat the maker output.

==================================================
PHASE 6 — EXISTING DETERMINISTIC CHECKER
==================================================

After semantic validation, run the existing deterministic checker unchanged.

Validate:

schema
required fields
relationship taxonomy
evidence presence
document provenance
entity anchoring
identifier consistency
invalid self-links
missing source/target
direction requirements
confidence/status rules

Keep semantic and deterministic checker results separately.

Final status should conceptually be:

VERIFIED
REJECTED
REVIEW_REQUIRED

Do not hide intermediate decisions.

==================================================
PHASE 7 — REDUCE / DEDUPLICATE
==================================================

Now REDUCE the accepted relationship findings.

The purpose is NOT to summarize them into prose.

The reducer must:

- group duplicate relationship claims
- preserve every contributing citation
- preserve every source passage
- preserve source document/page/section
- preserve differing dates where available
- retain disagreement instead of overwriting it
- retain multiple supporting CAMs

Conceptually group by:

source canonical entity
target canonical entity
normalized relationship type
direction

Do NOT collapse materially different relationships.

For example:

NVIDIA → supplier_to → Company A

must remain separate from:

NVIDIA → strategic_partner_of → Company A

unless business rules explicitly define them as equivalent.

==================================================
PHASE 8 — BUILD FINAL RELATIONSHIP RECORDS
==================================================

Create a structured relationship artifact.

Prefer Parquet and/or JSONL consistent with the repository.

Suggested fields:

relationship_id

source_entity_id
source_entity_name
source_CAGID
source_GFCID

target_entity_id
target_entity_name
target_CAGID
target_GFCID

relationship_type
direction

source_type = CAM

evidence_count
supporting_document_count

evidence_records [
    document_id
    filename
    page
    section
    passage_id
    exact_excerpt
]

maker_confidence
semantic_checker_status
semantic_checker_confidence
deterministic_checker_status
final_status

entity_resolution_status

valid_from if explicitly known
valid_to if explicitly known

maker_model
semantic_checker_model
pipeline_version
created_at

Do not invent valid_from/valid_to if the CAM does not provide them.

==================================================
PHASE 9 — KEEP NO-RELATIONSHIP RESULTS
==================================================

Do not discard negative examples.

For passages where NVIDIA is mentioned but no relationship is established, record:

passage_id
document_id
reason = NO_RELATIONSHIP
checker confirmation if applicable

This is important for measuring false positives later.

==================================================
PHASE 10 — HUMAN-READABLE NVIDIA REVIEW REPORT
==================================================

Produce a review report containing:

A. NVIDIA seed identity

B. Input retrieval summary
- passages reviewed
- documents represented

C. Maker results
- relationships proposed
- no-relationship results

D. Semantic checker
- accepted
- corrected
- rejected
- needs review

E. Deterministic checker
- passed
- rejected
- warnings

F. Final verified relationships

For each final relationship show:

Source Entity
Relationship Type
Target Entity
Direction
Canonical IDs
CAM Filename
Page
Section
Exact Evidence
Maker Confidence
Semantic Checker Result
Deterministic Checker Result
Final Status

G. Review-required cases

H. Rejected cases

I. No-relationship examples

==================================================
PHASE 11 — QUALITY METRICS
==================================================

Report:

NVIDIA passages processed
documents represented

maker relationships proposed
maker NO_RELATIONSHIP results

semantic checker:
ACCEPT
CORRECT
REJECT
NEEDS_REVIEW

deterministic checker:
passed
rejected
warnings

final:
VERIFIED relationships
REVIEW_REQUIRED relationships
REJECTED relationships

canonical target entities:
MATCHED
AMBIGUOUS
UNRESOLVED

relationships with:
exact evidence
missing evidence
multiple supporting passages
multiple supporting CAMs

Do NOT claim precision/recall yet unless human gold labels exist.

==================================================
PHASE 12 — DO NOT DO THESE THINGS
==================================================

Do NOT:

- run SEC enrichment
- run web enrichment
- use market data
- use Jaccard as evidence
- use hop distance as evidence
- use weighted path distance as evidence
- infer hidden relationships
- redesign the frontend
- rebuild the CAM index
- rebuild canonical entities
- change CAGID/GFCID source data
- migrate database technology
- process unrelated seed entities
- produce portfolio-level executive summaries
- overwrite original CAM evidence

This phase is strictly:

RETRIEVE EXISTING NVIDIA PASSAGES
→ EXTRACT
→ SEMANTIC CHECK
→ DETERMINISTIC CHECK
→ REDUCE
→ PERSIST VERIFIED RELATIONSHIPS

==================================================
PHASE 13 — REQUIRED ARTIFACTS
==================================================

Create repository-consistent equivalents of:

nvidia_cam_relationship_candidates.jsonl
nvidia_cam_relationships.parquet
nvidia_cam_no_relationship.jsonl
nvidia_cam_review_required.jsonl
nvidia_cam_relationship_report.xlsx or equivalent
nvidia_cam_relationship_metrics.json

Do not overwrite unrelated production artifacts.

==================================================
PHASE 14 — FINAL STATUS
==================================================

Return exactly one of:

NVIDIA_CAM_RELATIONSHIPS_READY

NVIDIA_CAM_RELATIONSHIPS_READY_WITH_WARNINGS

BLOCKED_BY_LLM_EXTRACTION

BLOCKED_BY_SEMANTIC_CHECKER

BLOCKED_BY_ENTITY_RESOLUTION

BLOCKED_BY_DETERMINISTIC_CHECKER

BLOCKED_BY_PIPELINE_ERROR

Also report the reason.

==================================================
STOP CONDITION
==================================================

STOP once:

1. all currently retrieved NVIDIA CAM passages have been processed,
2. maker relationship candidates exist,
3. independent semantic checking is complete,
4. deterministic checking is complete,
5. duplicate findings are consolidated without losing citations,
6. final verified/rejected/review-required relationship artifacts exist,
7. a human-readable NVIDIA relationship report exists.

Do NOT proceed to SEC or web enrichment.

The next phase will independently enrich and validate the resulting NVIDIA CAM relationship set using SEC filings and approved web evidence, while preserving each source separately.