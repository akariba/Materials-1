IMPLEMENT WITH LUNA

CCR — CLIENT CORRELATION
V1 FOUNDATION — STAGE 1.1 COMPLIANCE AND CONSISTENCY PATCH

This is a narrow corrective stage following the successful CCR V1 Foundation Stage 1 implementation.

Do NOT begin 3M V1 relationship reclassification or replay yet.

Do NOT perform new research.

Do NOT call SEC, GLEIF, Web, Stylus, recovery, frontier research, or any external provider.

Do NOT implement Stage 2A.8.

Do NOT modify the frontend.

The purpose of this stage is to close the remaining implementation gaps identified by reviewing:

backend/data/CCR_V1_FOUNDATION_STAGE_1_REPORT.md

against the approved CCR V1 architecture.

--------------------------------------------------
1. CURRENT VERIFIED BASELINE
--------------------------------------------------

Current relationship schema:

v9

Current Client Universe:

3,670,650 rows

Current backend tests:

57 passed
0 failed
0 skipped

Current CCR V1 tables:

ccr_v1_identity_links
ccr_v1_documents
ccr_v1_passages
ccr_v1_claims
ccr_v1_identity_link_support
ccr_v1_relationships
ccr_v1_relationship_versions
ccr_v1_relationship_support
ccr_v1_qualifiers
ccr_v1_enrichment_coverage

These tables are currently empty.

Historical Stage 2 rows remain preserved.

Current historical 3M state remains:

4 accepted observations
3 graph-visible accepted edges

No fuzzy merges.

No synthetic direct edges.

No source-master changes.

No Client Universe changes.

Preserve all of these invariants.

--------------------------------------------------
2. IMPORTANT: STAGE 1 PASSED, BUT IT DID NOT COMPLETE ALL REQUESTED WORK
--------------------------------------------------

Do not roll back Stage 1.

The additive CCR V1 foundation is accepted.

However, the Stage 1 report explicitly records that the historical ordinary-evidence-link / graph-predicate discrepancy remains unchanged.

This is a required correction before any V1 migration/replay.

The Stage 1 implementation also omitted the minimal event foundation and introduced two semantic differences from the approved model that should be corrected while the CCR V1 tables remain empty:

1. coverage representation of identity-unresolved research;
2. legacy evidence retention mode.

This stage addresses those items only.

--------------------------------------------------
3. FIX THE CANONICAL EVIDENCE RESOLUTION DEFECT
--------------------------------------------------

This is the highest-priority change.

The historical relationship store currently has:

4 accepted 3M observations

but:

3 graph-visible accepted edges.

The architecture reconciliation audit established the exact reason.

Observation 2 — Cabot Corporation — is ACCEPTED and has admissible ordinary evidence.

Its valid normalized lineage is:

relationship observation 2
    ->
relationship_observation_evidence
    ->
relationship_evidence row 13

But relationship_evidence row 13 originated from a candidate and therefore has:

candidate_id populated

and:

observation_id NULL

The current graph predicate checks:

1. direct relationship_evidence.observation_id;
2. recovery evidence associations;

but it does NOT correctly inspect the normalized:

relationship_observation_evidence

association.

Therefore different consumers disagree about the same accepted observation:

relationship evidence API can see the Cabot evidence

while:

graph/neighbour/traversal eligibility cannot.

This must be corrected.

--------------------------------------------------
4. IMPLEMENT ONE CANONICAL HISTORICAL EVIDENCE RESOLVER
--------------------------------------------------

Create one shared repository/domain-level evidence-resolution mechanism for historical accepted observations.

Do NOT repair this by changing historical evidence rows.

Do NOT populate missing observation_id values.

Do NOT duplicate evidence.

Do NOT manufacture new evidence.

The canonical resolver must recognize all currently valid evidence paths:

A. DIRECT ORDINARY EVIDENCE

relationship_evidence.observation_id
    ->
relationship observation

B. NORMALIZED ORDINARY EVIDENCE

relationship_observation_evidence
    ->
relationship_evidence

C. RECOVERY EVIDENCE

existing observation-to-recovery-evidence linkage

The resolver must deduplicate evidence if the same evidence is reachable through more than one path.

The resolver should return enough metadata to identify:

evidence identifier
evidence source
linkage mechanism
admissibility
source reference
content/reference hash where present

Do not alter acceptance criteria.

This resolver answers:

"What admissible evidence supports this accepted historical observation?"

It does not decide whether an unaccepted observation should become accepted.

--------------------------------------------------
5. USE THE CANONICAL RESOLVER CONSISTENTLY
--------------------------------------------------

Inspect all current code paths that determine evidence-backed relationship visibility.

At minimum reconcile:

accepted observation detail
evidence listing
graph edge eligibility
neighbour calculation
network calculation
traversal hop eligibility
graph fingerprints/counting where applicable

Do not create several slightly different resolver implementations.

All relevant consumers should use the same canonical evidence meaning.

The invariant must become:

the same accepted observation must not be evidence-backed in one API and evidence-unbacked in another because of storage-link shape.

--------------------------------------------------
6. CABOT REGRESSION TEST
--------------------------------------------------

Create a focused regression fixture reproducing the historical Cabot structure:

candidate-originated evidence
+
relationship_evidence.observation_id = NULL
+
normalized relationship_observation_evidence link
+
accepted relationship observation

Verify:

canonical evidence resolver finds the evidence

and, if all existing historical graph eligibility rules are satisfied:

the accepted observation becomes graph-visible.

Do NOT weaken any other eligibility rule to achieve this.

--------------------------------------------------
7. VERIFY THE FOUR 3M HISTORICAL OBSERVATIONS
--------------------------------------------------

Using current persisted data only, evaluate:

Observation 1
3M -> 3M India Ltd
historical type: subsidiary

Observation 2
3M <-> Cabot Corporation
historical type: legal_counterparty

Observation 3
3M -> Solventum Corporation
historical type: equity_investor

Observation 4
3M <-> Solventum Corporation
historical type: strategic_partner

Do not reclassify these relationship types yet.

Report for each:

acceptance state
resolved evidence count
evidence linkage path(s)
graph eligibility
reason

Historical accepted observation count must remain:

4

Expected graph-visible edge result after the canonical evidence fix:

4

ONLY if all four meet the existing historical eligibility rules.

If the result remains 3, identify the exact remaining rule.

Do not force 4.

--------------------------------------------------
8. COVERAGE SEMANTICS CORRECTION
--------------------------------------------------

The approved CCR V1 enrichment coverage outcomes are:

NOT_ELIGIBLE
NOT_RESEARCHED
RESEARCHED_FOUND
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE

Freshness remains separately:

CURRENT
STALE

IDENTITY_UNRESOLVED must NOT be a peer top-level coverage outcome.

Identity unresolved describes why research was not performed.

Represent it as:

outcome = NOT_RESEARCHED

reason_code = IDENTITY_UNRESOLVED

The NOT_RESEARCHED reason model must support at least:

IDENTITY_UNRESOLVED
NOT_PRIORITIZED
FAMILY_NOT_IN_SCOPE

If useful, allow an extensible governed reason field, but do not replace the distinction above with arbitrary free text.

The existing ccr_v1_enrichment_coverage table is empty, so correct this foundation now before it receives production data.

Do not create coverage rows during this stage.

--------------------------------------------------
9. RESEARCHED_NONE_FOUND SAFETY RULE
--------------------------------------------------

Preserve and test:

RESEARCHED_NONE_FOUND may only represent a completed defined research scope that produced zero qualifying findings.

It must not be produced when:

provider calls failed
provider was unavailable
provider was not configured
identity was unresolved
only part of the required source set ran
research was never started

PARTIAL and UNAVAILABLE remain distinct states.

The historical Stage 2A.7 frontier result must never be translated into RESEARCHED_NONE_FOUND.

--------------------------------------------------
10. LEGACY EVIDENCE RETENTION MODE
--------------------------------------------------

The document model currently supports:

FULL_SNAPSHOT
RESTRICTED_SNAPSHOT
TRANSIENT_VERIFICATION

Add an explicit:

LEGACY_REFERENCE

retention mode.

Purpose:

represent historical evidence for which CCR possesses references/excerpts/metadata but does NOT possess a first-class retained source document sufficient for deterministic full replay.

LEGACY_REFERENCE must support cases like the historical 3M evidence:

source reference known
excerpt known
some metadata known
full source body absent
passage offsets unavailable
content hash possibly absent
full replay impossible

LEGACY_REFERENCE must never imply:

FULL_REPLAY

A legacy-reference document may have replay capability such as:

PASSAGE_REPLAY
PARTIAL_REPLAY
NO_REPLAY

depending on what is actually retained.

Do not backfill historical evidence yet.

This stage only ensures the schema/domain model can represent it correctly.

--------------------------------------------------
11. MINIMAL EVENT FOUNDATION
--------------------------------------------------

Stage 1 explicitly chose not to introduce an event object.

The approved CCR model requires events to remain conceptually separate from persistent relationships.

Create a minimal additive event foundation now.

Do NOT create a large event taxonomy.

Do NOT populate historical events.

At minimum introduce:

ccr_v1_events

with a domain/repository contract capable of representing:

event_id
event_type
event state/status if required
effective/announced/observed dates where known
date precision
subject Legal Entity
optional related Legal Entity
optional unresolved counterparty/reference
source/policy provenance
stable fingerprint
created timestamp

Examples of future event types include:

ACQUISITION
DIVESTITURE
SPIN_OFF
FACILITY_SIGNING
FACILITY_TERMINATION
LITIGATION_SETTLEMENT
JV_FORMATION

These examples do not need to become a complete closed taxonomy during this stage.

If event evidence/claim support requires a separate small association table, add it only if necessary.

Prefer reuse of the existing:

document
passage
atomic claim

foundation.

Important:

an event must NOT automatically create a persistent relationship.

Example:

announced acquisition

does not automatically mean:

owns

until the relevant relationship acceptance conditions are satisfied.

--------------------------------------------------
12. EVENT VS RELATIONSHIP INVARIANT
--------------------------------------------------

Add tests demonstrating that:

creating or representing an event does not automatically create:

ccr_v1_relationships

or:

ccr_v1_relationship_versions

Examples:

FACILITY_SIGNING event
does not automatically create lends_to

ACQUISITION announcement
does not automatically create owns or controls

LITIGATION_SETTLEMENT event
does not automatically create litigates_against

Relationship creation remains governed separately.

--------------------------------------------------
13. VERIFY SOURCE CLASS VS RETRIEVAL MECHANISM
--------------------------------------------------

Preserve Stage 1's correct separation between:

underlying source class

and:

retrieval mechanism/provider.

Example:

retrieval mechanism = WEB

underlying source class = REGULATORY_FILING

must remain possible.

Do not treat retrieval provider as independent corroboration.

No external retrieval occurs during this stage.

--------------------------------------------------
14. DO NOT CHANGE THE V1 RELATIONSHIP ONTOLOGY
--------------------------------------------------

Keep the current approved ACTIVE types:

owns
controls
lends_to
provides_credit_support
supplies
depends_on_products_of

Keep passive/opportunistic metadata support:

manages
licenses_to
partners_with
litigates_against

Do not activate:

provides_professional_services_to
broad passive ownership harvesting
regulatory relationships
natural-person external enrichment
organisation-grain relationships

Do not migrate the 23 historical Stage 2 relationship labels yet.

--------------------------------------------------
15. DO NOT POPULATE THE CCR V1 TABLES WITH 3M YET
--------------------------------------------------

This remains a foundation-compliance patch.

Do not migrate:

3M India
Cabot
Solventum

into V1 relationship rows yet.

Do not create V1 accepted relationships from the old four observations.

Do not create identity links for them merely because historical resolution exists.

Do not backfill documents/passages/claims yet.

That is the next controlled stage after this patch is verified.

--------------------------------------------------
16. IDENTITY FOUNDATION — NO CHANGE IN AUTHORITY
--------------------------------------------------

Preserve the Stage 1 identity model:

link_type:
EXACT
ASSOCIATED

link_state:
VERIFIED
PROBABLE
UNVERIFIED
REJECTED

Do not infer identity from:

name similarity
CAGID
CAGID_NAME
beneficial_owner_gfcid
legal_entity_id without semantic validation
lei_legal_name alone

No fuzzy merge.

Do not bulk-map the 3.67M Client Universe.

--------------------------------------------------
17. CLIENT UNIVERSE AND SOURCE MASTER
--------------------------------------------------

The authoritative Client Universe remains:

backend/Customer_latest.parquet

Expected:

3,670,650 rows
3,670,650 unique GFCIDs

Runtime Client Universe remains:

backend/data/client_universe.sqlite3

Do not modify either source.

No CCR V1 migration should copy the entire Client Universe into the relationship database.

Client Record identifiers remain validated through the existing read-only repository boundary.

--------------------------------------------------
18. STATUS ENDPOINT
--------------------------------------------------

Inspect:

GET /api/status

If it still advertises Stage 2A.6 as the active product readiness state, update the wording to accurately describe current state.

It should communicate approximately:

CCR_V1_FOUNDATION_READY

or an equivalent existing status convention.

Do not claim:

CCR V1 enrichment complete

because no V1 data migration/research has occurred.

Do not advertise Stage 2A.7 frontier research as an active production capability.

Preserve backwards-compatible fields where possible.

--------------------------------------------------
19. SCHEMA MIGRATION
--------------------------------------------------

The current schema is v9.

Implement the smallest safe schema migration required for these corrections.

Expected next schema version:

v10

unless repository conventions provide a compelling reason otherwise.

The migration may include:

coverage reason-code correction
LEGACY_REFERENCE retention mode support
minimal ccr_v1_events table
minimal event support association if required

Do not redesign unrelated Stage 1 tables.

Do not drop Stage 2 tables.

Do not delete Stage 2 rows.

Do not destructively rename historical structures.

Because current CCR V1 tables are empty, normalize these semantics now rather than preserving an incorrect empty contract for compatibility.

Migration must be:

deterministic
idempotent
replay-safe
foreign-key safe

--------------------------------------------------
20. REQUIRED TESTS
--------------------------------------------------

Preserve all existing tests.

Add focused tests for:

CANONICAL HISTORICAL EVIDENCE

1. direct ordinary evidence resolves.

2. normalized relationship_observation_evidence resolves.

3. recovery evidence resolves.

4. duplicate reachability does not double-count evidence.

5. Cabot candidate-originated normalized evidence resolves.

6. candidate evidence alone does not create an accepted edge.

7. rejected/inadmissible evidence remains ineligible.

GRAPH/API CONSISTENCY

8. accepted relationship detail and graph eligibility see the same admissible evidence set.

9. neighbor calculation uses canonical evidence resolution.

10. network calculation uses canonical evidence resolution.

11. traversal hop eligibility uses canonical evidence resolution.

COVERAGE

12. IDENTITY_UNRESOLVED is represented as:
NOT_RESEARCHED + IDENTITY_UNRESOLVED reason.

13. NOT_PRIORITIZED is represented as NOT_RESEARCHED reason.

14. FAMILY_NOT_IN_SCOPE is represented as NOT_RESEARCHED reason.

15. provider failure cannot become RESEARCHED_NONE_FOUND.

16. PARTIAL remains distinct from RESEARCHED_NONE_FOUND.

17. UNAVAILABLE remains distinct from RESEARCHED_NONE_FOUND.

RETENTION

18. LEGACY_REFERENCE can be persisted.

19. LEGACY_REFERENCE cannot imply FULL_REPLAY.

20. FULL_SNAPSHOT consistency rules remain valid.

EVENTS

21. event can be persisted without a relationship.

22. acquisition event does not automatically create owns.

23. facility-signing event does not automatically create lends_to.

24. litigation-settlement event does not automatically create a persistent relationship.

INVARIANTS

25. fuzzy merge count remains zero.

26. synthetic direct edge count remains zero.

27. historical Stage 2 rows remain unchanged.

28. Client Universe remains unchanged.

29. source master remains unchanged.

30. CCR V1 relationship tables remain unpopulated unless a test transaction uses temporary/test storage.

--------------------------------------------------
21. VALIDATE CURRENT 3M GRAPH CONSISTENCY
--------------------------------------------------

After implementing the canonical evidence resolver, inspect the existing production-like local relationship database read-only.

Report:

historical accepted observations:
expected 4

graph-visible accepted edges before patch:
3

graph-visible accepted edges after patch:
expected investigation result, not forced

For every historical observation report:

observation ID
endpoint
historical type
resolved admissible evidence count
evidence linkage mechanisms
graph-visible yes/no
reason

Particularly confirm:

Cabot normalized ordinary evidence recognized:
YES / NO

Do not alter the historical rows.

--------------------------------------------------
22. NO EXTERNAL ACTIVITY
--------------------------------------------------

During this stage:

SEC calls = 0
GLEIF calls = 0
Web calls = 0
Stylus calls = 0
provider recovery calls = 0
frontier research calls = 0

new research findings = 0
new research candidates = 0
new accepted research relationships = 0

Do not rerun 3M research.

--------------------------------------------------
23. NO FRONTEND
--------------------------------------------------

Frontend modifications:

0

Do not work on:

network map
dashboard
search UI
evidence UI
relationship UI
design/styling

Backend consistency only.

--------------------------------------------------
24. CREATE REPORT
--------------------------------------------------

Create:

backend/data/CCR_V1_FOUNDATION_STAGE_1_1_REPORT.md

The report must include:

1. Executive result
2. Stage 1 baseline
3. Files changed
4. Schema v9 -> v10 changes
5. Canonical evidence resolver
6. Direct ordinary evidence handling
7. Normalized ordinary evidence handling
8. Recovery evidence handling
9. Evidence deduplication
10. Cabot consistency repair
11. 3M graph validation
12. Coverage semantic correction
13. NOT_RESEARCHED reason model
14. LEGACY_REFERENCE retention model
15. Minimal event foundation
16. Event/relationship separation
17. Status endpoint result
18. Historical compatibility
19. Test results
20. SQLite integrity
21. Client Universe integrity
22. Source-master integrity
23. External-call verification
24. Remaining V1 unknowns
25. Recommended next action

--------------------------------------------------
25. FINAL STATUS FORMAT
--------------------------------------------------

At completion output exactly:

CCR V1 FOUNDATION — STAGE 1.1

Status: PASS / PARTIAL / FAIL

Schema before:
Schema after:

Historical Stage 2 tables deleted:
Historical Stage 2 rows modified:

Client Universe rows:
Client Universe modifications:
Source-master modifications:

Historical 3M accepted observations:

Graph-visible accepted 3M edges before:
Graph-visible accepted 3M edges after:

Cabot normalized ordinary evidence recognized:

Canonical evidence resolver:
PASS / PARTIAL / FAIL

Direct ordinary evidence:
PASS / FAIL

Normalized ordinary evidence:
PASS / FAIL

Recovery evidence:
PASS / FAIL

Evidence deduplication:
PASS / FAIL

Graph/API evidence semantics aligned:
YES / NO

Coverage outcome model:
PASS / PARTIAL / FAIL

NOT_RESEARCHED reason codes:
PASS / PARTIAL / FAIL

LEGACY_REFERENCE retention:
PASS / FAIL

Event foundation:
PASS / PARTIAL / FAIL

Event does not automatically create relationship:
PASS / FAIL

Identity foundation unchanged:
YES / NO

CCR V1 relationship rows migrated from historical 3M:
0

External provider calls:
0

New research findings:
0

New accepted research relationships:
0

Fuzzy merges:
0

Synthetic direct edges:
0

Frontend files modified:
0

Backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Migration replay:

Report:
backend/data/CCR_V1_FOUNDATION_STAGE_1_1_REPORT.md

Recommended next action:

Do not begin the next stage automatically.
