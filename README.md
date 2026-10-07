You are continuing work on the existing CCR Relationship Intelligence repository.

The NVIDIA CAM-only phase is complete.

Current validated CAM-only state:

- Status: NVIDIA_CAM_PHASE_COMPLETE_WITH_WARNINGS
- Retrieved passages: 43
- Documents represented: 15
- Relationship candidates: 63
- Semantic checker decisions:
  - 23 accepted
  - 12 corrected
  - 28 rejected
- Verified candidate records before deduplication: 8
- Final verified relationships: 3
- Review-required records: 31
- NO_RELATIONSHIP passages: 15
- Deterministic checks:
  - 42 passed
  - 21 review-required
- Semantic errors: 0
- Focused tests: 18 passed
- Full regression: 447 passed, with 2 failures outside the NVIDIA CAM scope
- CAM provenance validation passed

The three current CAM-verified relationships are:

1. NVIDIA Corporation ↔ Hut 8 Corporation
   Relationship: contracted_customer
   CAM evidence includes the 15-year 100% NNN lease with NVIDIA.

2. NVIDIA Corporation ↔ Intel Corporation
   Relationship: strategic_partner
   CAM evidence includes Intel strengthening its balance sheet through a strategic partnership involving NVIDIA's approximately $5bn contribution.

3. NVIDIA Corporation → Intel Corporation
   Relationship: equity_investor
   CAM evidence includes the approximately $5bn NVIDIA equity investment.

Do NOT rerun the CAM extraction pipeline.
Do NOT rebuild the CAM index.
Do NOT modify canonical entity source-of-truth data.
Do NOT overwrite CAM-only relationship artifacts.
Do NOT perform graph proximity/Jaccard/hidden-link analysis yet.

This is an EXECUTION task.

The objective is:

Use independent SEC and approved web evidence to corroborate, contradict, resolve, or leave unresolved the existing NVIDIA CAM relationships and review-required candidates.

The required architecture is:

CAM EVIDENCE
      +
SEC EVIDENCE
      +
APPROVED WEB EVIDENCE
      ↓
SOURCE-SEPARATED RECONCILIATION
      ↓
FINAL EVIDENCE-BACKED NVIDIA RELATIONSHIP SET

==================================================
PHASE 1 — LOAD EXISTING NVIDIA CAM RESULTS
==================================================

Reuse the existing artifacts, including repository-equivalent files such as:

nvidia_cam_relationships.parquet
nvidia_cam_relationship_candidates.jsonl
nvidia_cam_review_required.jsonl
nvidia_cam_no_relationship.jsonl
nvidia_cam_relationship_metrics.json

Load the existing:

- 3 CAM-verified relationships
- 31 review-required records
- CAM evidence/citations
- canonical NVIDIA identity
- resolved target identities
- unresolved/ambiguous target identities

Do not regenerate CAM findings.

Separate the population into:

A. CAM_VERIFIED
B. CAM_REVIEW_REQUIRED
C. CAM_REJECTED / NO_RELATIONSHIP

Only A and B require external enrichment.

==================================================
PHASE 2 — PRESERVE SOURCE INDEPENDENCE
==================================================

CAM, SEC and WEB evidence must remain independent source layers.

For every evidence record preserve:

source_type
source_entity
target_entity
relationship_type_candidate
direction
document/filing/page/source
publication or filing date
URL where applicable
exact excerpt
retrieval timestamp
confidence
evidence status

Never replace CAM evidence with SEC/web evidence.

Never rewrite or paraphrase the original CAM excerpt in storage.

The final relationship record may aggregate evidence, but each source citation must remain separately inspectable.

==================================================
PHASE 3 — SEC ENRICHMENT
==================================================

Perform SEC enrichment before general web enrichment.

Use the existing SEC/EDGAR integration and approved enterprise mechanisms.

For NVIDIA and each relevant target entity:

1. Resolve CIK using existing canonical identity data where available.
2. Retrieve relevant real SEC filings.
3. Search only for evidence relevant to the proposed entity pair / relationship.

Potential filing types may include:

10-K
10-Q
8-K
DEF 14A
13D
13G
S-1
424B / prospectus filings
other relevant SEC filings

Do not search SEC blindly across unrelated entities.

For every SEC finding return:

source_entity
target_entity
relationship_type_candidate
direction

filing_entity
CIK
filing_type
filing_date
filing_url

exact_evidence_excerpt
evidence_status
confidence

Allowed evidence statuses:

SUPPORTS
CONTRADICTS
MENTIONS_ONLY
INSUFFICIENT
NOT_FOUND

CRITICAL:

A SEC relationship finding may only be accepted if its quoted/extracted evidence can be grounded back to the retrieved SEC filing text.

If the excerpt does not exist in the filing, reject the finding.

Do not allow model memory/knowledge to substitute for filing evidence.

==================================================
PHASE 4 — APPROVED WEB ENRICHMENT
==================================================

After SEC enrichment, use the existing approved enterprise web-search mechanism.

Prioritize sources in this order where possible:

1. official company investor-relations pages
2. official company press releases
3. regulatory or exchange announcements
4. official corporate disclosures
5. highly credible financial/business news
6. other approved sources

Do not use low-authority sources when authoritative evidence exists.

For every web finding preserve:

source_entity
target_entity
relationship_type_candidate
direction

URL
publisher
publication_date
retrieval_date
exact excerpt/snippet
authority_tier
evidence_status
confidence

Allowed evidence statuses:

SUPPORTS
CONTRADICTS
MENTIONS_ONLY
INSUFFICIENT

Do not promote a relationship because the search result merely associates two names.

==================================================
PHASE 5 — HANDLE THE THREE CAM-VERIFIED RELATIONSHIPS
==================================================

Process the three CAM-verified relationships independently.

Do NOT require SEC or web corroboration for them to remain CAM_VERIFIED.

For each one, external evidence should be classified as:

CORROBORATES
CONTRADICTS
NO_EXTERNAL_EVIDENCE
AMBIGUOUS

Specifically evaluate:

1. NVIDIA ↔ Hut 8
   contracted_customer

2. NVIDIA ↔ Intel
   strategic_partner

3. NVIDIA → Intel
   equity_investor

Do not merge the two Intel relationship types.

If external evidence contradicts CAM evidence:

- preserve the CAM relationship
- preserve the external evidence
- create SOURCE_CONFLICT
- mark for review

Do not overwrite either side.

==================================================
PHASE 6 — PROCESS THE 31 REVIEW-REQUIRED RECORDS
==================================================

For each review-required CAM candidate, use SEC/web evidence to attempt resolution.

Determine whether external evidence:

A. confirms the relationship
B. contradicts the relationship
C. resolves entity identity
D. corrects relationship type
E. corrects direction
F. provides insufficient evidence

Return one reconciliation status per candidate:

EXTERNALLY_CORROBORATED
EXTERNALLY_CONTRADICTED
IDENTITY_RESOLVED
RELATIONSHIP_CORRECTED
STILL_REVIEW_REQUIRED
REJECTED_NO_EVIDENCE

Do NOT promote a review candidate merely because:

- both companies appear in the same article
- they operate in the same sector
- one is a competitor
- one uses similar technology
- graph proximity is high
- market commentary associates them

There must be explicit relationship evidence.

==================================================
PHASE 7 — EXTERNAL ENTITY RESOLUTION
==================================================

For unresolved or ambiguous target entities, external evidence may be used to propose identity resolution.

Return:

raw_target_name
proposed_legal_name
proposed_canonical_entity_id
proposed_CAGID
proposed_GFCID
CIK
LEI if available

resolution_source
resolution_evidence
resolution_confidence

Do not automatically mutate canonical entity data.

Store external identity fixes as proposals unless existing governance explicitly allows promotion.

==================================================
PHASE 8 — RELATIONSHIP TAXONOMY AND DIRECTION
==================================================

Ensure every surviving relationship has an unambiguous semantic direction.

Where possible prefer directional semantics such as:

customer_of
supplier_to
investor_in
subsidiary_of
parent_of
guarantor_of
borrower_from
lender_to

For symmetric relationships, such as strategic partnership, explicitly mark:

directionality = SYMMETRIC

Do not silently change production taxonomy in this phase.

If the existing label is ambiguous, preserve the existing label and additionally flag:

TAXONOMY_REVIEW_REQUIRED

For example, determine whether:

contracted_customer

means:

NVIDIA --customer_of--> Hut 8

or:

Hut 8 --has_customer--> NVIDIA

Do not guess.

Use source evidence and existing taxonomy definitions.

==================================================
PHASE 9 — CROSS-SOURCE RECONCILIATION
==================================================

Build a reconciliation record per entity-pair / relationship-type combination.

Include:

source_entity_id
source_entity_name
target_entity_id
target_entity_name

relationship_type
direction

CAM_status
CAM_evidence_count

SEC_status
SEC_evidence_count

WEB_status
WEB_evidence_count

identity_status
taxonomy_status

cross_source_status

Allowed cross_source_status values:

MULTI_SOURCE_CONFIRMED
CAM_ONLY_VERIFIED
SEC_ONLY_VERIFIED
WEB_ONLY_VERIFIED
SOURCE_CONFLICT
STILL_REVIEW_REQUIRED
REJECTED

Do not merge different relationship types merely because the entity pair is identical.

For example:

NVIDIA ↔ Intel strategic partnership

and:

NVIDIA → Intel equity investment

must remain separate relationship records.

==================================================
PHASE 10 — EVIDENCE PRECEDENCE
==================================================

Do not use one source type to automatically override another.

Use evidence quality and explicit contradiction.

Suggested source trust handling:

- CAM: internal analyst-reviewed credit evidence
- SEC: authoritative regulatory disclosure
- official company disclosure: high authority
- high-quality news: secondary corroboration

Preserve disagreement when sources conflict.

Do not invent a single global "truth" when evidence genuinely conflicts.

==================================================
PHASE 11 — DO NOT USE GRAPH ANALYTICS YET
==================================================

Do NOT use:

Jaccard
hop distance
weighted path distance
common neighbors
graph proximity
hidden-link scores
co-exposure similarity

as evidence for any relationship.

Graph analytics belongs after evidence reconciliation.

==================================================
PHASE 12 — QUALITY CONTROLS
==================================================

For every externally supported relationship validate:

- target identity
- source identity
- relationship type
- direction
- exact source evidence
- URL
- publication/filing date
- evidence source authority
- source excerpt grounding
- duplicate handling

Reject unsupported model-generated statements.

Do not allow:

"According to available information..."

without an exact source.

==================================================
PHASE 13 — OUTPUT ARTIFACTS
==================================================

Create repository-consistent equivalents of:

nvidia_sec_evidence.jsonl
nvidia_web_evidence.jsonl

nvidia_external_identity_proposals.jsonl

nvidia_cross_source_reconciliation.parquet

nvidia_external_review_required.jsonl
nvidia_external_rejected.jsonl

nvidia_cross_source_review.xlsx

nvidia_external_enrichment_metrics.json

Do NOT overwrite:

nvidia_cam_relationships.parquet
nvidia_cam_relationship_candidates.jsonl
nvidia_cam_review_required.jsonl
nvidia_cam_no_relationship.jsonl

==================================================
PHASE 14 — FINAL METRICS
==================================================

Report:

CAM verified relationships: 3
CAM review-required records: 31

SEC:
- evidence records found
- supporting
- contradicting
- mention-only
- not found

WEB:
- evidence records found
- supporting
- contradicting
- mention-only

Review candidates:
- externally corroborated
- externally contradicted
- identity resolved
- relationship corrected
- still review-required
- rejected

Final relationship statuses:

MULTI_SOURCE_CONFIRMED
CAM_ONLY_VERIFIED
SEC_ONLY_VERIFIED
WEB_ONLY_VERIFIED
SOURCE_CONFLICT
STILL_REVIEW_REQUIRED
REJECTED

==================================================
PHASE 15 — HUMAN-READABLE REPORT
==================================================

Create a concise review report.

For every surviving relationship show:

Source Entity
Relationship Type
Target Entity
Direction

CAM Evidence
SEC Evidence
Web Evidence

CAM Status
SEC Status
Web Status

Identity Status
Cross-Source Status

Evidence Sources / URLs

Also separately list:

- conflicts
- unresolved identity cases
- rejected candidates
- candidates still requiring review

==================================================
PHASE 16 — VALIDATE THE THREE CAM-VERIFIED RELATIONSHIPS
==================================================

Provide an explicit external-evidence result for each:

1. NVIDIA / Hut 8 — contracted_customer
2. NVIDIA / Intel — strategic_partner
3. NVIDIA / Intel — equity_investor

For each return exactly one external status:

CORROBORATES
CONTRADICTS
NO_EXTERNAL_EVIDENCE
AMBIGUOUS

Do not change its existing CAM_VERIFIED status unless a governance rule specifically requires that.

==================================================
PHASE 17 — TESTING
==================================================

Run focused tests for:

SEC grounding
web grounding
source separation
cross-source reconciliation
identity proposals
relationship-type separation
conflict handling

Then run the relevant regression suite.

Do not fix unrelated existing failures unless this implementation caused them.

Report:

tests passed
tests failed
warnings
whether failures are in scope

==================================================
PHASE 18 — FINAL STATUS
==================================================

Return exactly one of:

NVIDIA_EXTERNAL_ENRICHMENT_READY

NVIDIA_EXTERNAL_ENRICHMENT_READY_WITH_REVIEW

BLOCKED_BY_SEC

BLOCKED_BY_WEB

BLOCKED_BY_ENTITY_RESOLUTION

BLOCKED_BY_RECONCILIATION

BLOCKED_BY_PIPELINE_ERROR

==================================================
STOP CONDITION
==================================================

STOP after:

1. SEC enrichment is complete,
2. approved web enrichment is complete,
3. CAM / SEC / WEB evidence remains source-separated,
4. all 3 CAM-verified relationships have an external corroboration status,
5. all 31 review-required CAM records have reconciliation statuses,
6. unresolved external identity findings remain proposals rather than silently modifying canonical identity,
7. final cross-source reconciliation artifacts exist,
8. the human-readable review report exists,
9. focused validation is complete.

Do NOT proceed automatically to:

- graph construction
- Jaccard
- hop distance
- weighted path distance
- hidden relationships
- portfolio-level aggregation
- executive summary generation

The next phase will construct the evidence-backed NVIDIA relationship graph using only reconciled relationship records.
