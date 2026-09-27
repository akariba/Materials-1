CCR V1 — STAGE 7
CONTROLLED REAL-WORLD ENRICHMENT PILOT

You are the implementation agent.

This stage begins the first controlled real factual-enrichment exercise after the approved CCR V1 identity, evidence, relationship, correlation, API, and UI foundations.

DO NOT redesign the architecture.

DO NOT broaden the product.

DO NOT manufacture correlation results.

The objective is to populate the existing governed factual graph with a small amount of high-quality real-world relationship data and determine whether meaningful correlations emerge naturally.

============================================================
1. APPROVED BASELINE
============================================================

Treat the following as frozen and authoritative:

- Client Universe:
  3,670,650 authoritative Client Records

- Client Record / Legal Entity separation

- identity eligibility:
  VERIFIED + EXACT

- no fuzzy identity merge

- no synthetic direct relationship

- factual network:
  ACCEPTED CCR V1 relationship versions only

- supporting evidence required

- Document -> Passage -> Atomic Claim -> Relationship model

- qualifier independence

- relationship-version history

- query-time derived correlations only

- no persisted derived-result rows

- six approved correlation definitions only:

  SHARED_CONTROLLER
  SHARED_SUPPLIER
  SHARED_CUSTOMER
  SUPPLY_CHAIN
  SHARED_LENDER
  SHARED_PRODUCT_DEPENDENCY

- maximum derived depth:
  exactly two relationship hops

- coverage independent from result count

- zero result is NOT a universal negative

- current Stage 5 / 5.1 / 6.1 API and UI contracts

Do not change these contracts unless an actual blocking implementation defect is proven.

============================================================
2. STAGE 7 PURPOSE
============================================================

Build a small real, evidence-backed factual graph around a controlled pilot.

The pilot must test whether the existing correlation engine produces useful derived correlations naturally once enough accepted factual relationships exist.

The pilot is NOT successful merely because a correlation is produced.

Zero correlations is a valid outcome.

Do not select evidence or weaken gates in order to force a correlation result.

============================================================
3. PRE-FLIGHT SAFETY AUDIT
============================================================

Before performing any external research or enrichment, confirm three things.

A. AMBIGUOUS EXTERNAL ENTITY SAFETY

Prove in code/tests that a discovered external Legal Entity whose provider identifier maps ambiguously to multiple Client Records cannot automatically become a VERIFIED+EXACT Client Record identity link.

This must be structurally prevented.

It must not merely happen to be absent in current data.

Explicit named-client queries may continue to use an already-persisted qualifying identity link.

Broad discovered-entity match-back must remain ambiguity-safe.

B. REJECTED / CONTEXT-ONLY OBSERVATION RETENTION

Determine where non-accepted observations are currently retained.

Examples:

- rejected evidence
- insufficient evidence
- context-only claims
- candidate relationship claims
- Cabot-shaped cases

They must remain distinguishable from:

"this relationship was never observed."

They do NOT need to appear in the factual relationship network.

Do not create a new major subsystem if an existing audit/candidate surface already provides this.

Document exactly where these observations remain accessible.

C. STALENESS POLICY

Inspect whether a governed platform-wide freshness/staleness policy already exists.

If it exists:
- identify it,
- use it unchanged.

If it does not exist:
- do NOT invent a broad new policy in this stage,
- record the absence as an explicit Stage 7 limitation,
- continue using existing governed temporal fields honestly.

Stop Stage 7 before enrichment if A is not structurally safe.

============================================================
4. PILOT SELECTION PRINCIPLE
============================================================

Start from the existing real 3M case.

The initial anchor remains:

Client Record:
GFCID 0000426083
client_id 437487
3M

Existing governed facts include:

- 3M -> 3M India: owns
- 3M -> Solventum: owns
- 3M -> Solventum: supplies

Use these as starting facts, NOT as a target pattern to manufacture.

Expand the pilot to a SMALL bounded real entity set.

Target size:

approximately 5–15 additional relevant entities / Client Records / discovered Legal Entities.

Selection must be plausibility-based, not correlation-result-based.

Reasonable selection rationales include:

- entities explicitly named in primary documents concerning pilot entities;
- real subsidiaries / controlled entities;
- significant disclosed customers or suppliers;
- financing counterparties explicitly disclosed;
- entities involved in disclosed product dependencies;
- industry peers selected BEFORE relationship research begins;
- entities naturally reached from documents already being researched.

DO NOT select an entity because:

"adding this entity will create SHARED_SUPPLIER"

or

"we need something to make SHARED_LENDER non-zero."

Persist an auditable pilot-selection manifest BEFORE relationship research begins.

For every selected entity record:

- selection reason
- source of selection
- whether selected before research
- known Client Record if any
- unresolved/discovered entity status if applicable

============================================================
5. ENTITY-CENTRIC / DOCUMENT-CENTRIC RESEARCH
============================================================

Research must be entity/document-centric.

Do NOT research pair-by-pair looking for a requested answer.

A document should be processed once and may generate multiple atomic claims concerning multiple entities.

Reuse:

- source documents
- passages
- extracted claims
- identity evidence
- provider results
- registry records

across all applicable Client Records and research scopes.

Avoid duplicated provider calls and duplicated evidence objects.

============================================================
6. RESEARCH SCOPE
============================================================

Use ONLY relationship families classified ACTIVE in the frozen CCR V1 research-scope policy.

Do not expand the ontology.

Do not activate previously deferred relationship types.

Do not introduce provides_professional_services_to if it remains deferred.

Do not introduce litigation unless already ACTIVE under the frozen approved policy.

Do not reinterpret historical Stage 2 relationship labels directly into CCR V1 truth.

Historical material may only be used through the governed evidence/claim acceptance pipeline.

============================================================
7. ACCEPTANCE RULES
============================================================

Use the frozen CCR V1 acceptance rules EXACTLY.

IMPORTANT:

Do not invent a new universal evidence threshold.

Use the approved per-relationship-type acceptance rules and evidence-basis requirements from the frozen V1 policy.

Every correlation-eligible factual hop must satisfy all existing gates, including:

- qualifying endpoint identity;
- approved relationship type;
- correct direction;
- required relationship acceptance state;
- admissible evidence;
- required source/evidence-basis standard for that relationship type;
- temporal validity;
- complete lineage.

No pilot exception.

No manual analyst override that bypasses the policy.

No lower identity gate because an entity "obviously" looks correct.

No model inference as evidence.

No co-mention-only relationship.

No fuzzy or name-only merge.

============================================================
8. PROVIDERS / SOURCES
============================================================

Use existing provider infrastructure only.

Permitted providers/sources should remain governed by the frozen source policy, including where applicable:

- GLEIF for Legal Entity identity
- SEC / regulatory filing retrieval
- official company / issuer sources
- approved Web retrieval
- approved secondary sources only according to policy

Remember:

retrieval mechanism != evidence source.

A Web provider retrieving an SEC filing does not turn the SEC filing into "Web evidence."

Preserve source class separately from retrieval mechanism.

All provider attempts must remain auditable.

============================================================
9. DOCUMENT AND PASSAGE RETENTION
============================================================

For newly researched material, improve replayability wherever licensing/source policy permits.

Persist:

- canonical source reference
- retrieval metadata
- document/source hash where available
- exact evidence passage
- passage locator / section / offsets where available
- extraction provenance
- policy version
- research run
- timestamps
- retention/replay capability

Do not falsely classify evidence as FULL_REPLAY when only a passage/reference is retained.

============================================================
10. IDENTITY RESOLUTION
============================================================

Resolve newly discovered entities through the existing governed identity pipeline.

Strong identifiers should be preferred where available.

Possible states remain governed.

Only qualifying VERIFIED + EXACT links may participate as Client Record endpoints under current correlation eligibility.

External Legal Entities may remain external.

It is valid for enrichment to discover a real Legal Entity that cannot be safely matched back to a Client Record.

Do not force match-back simply to increase internal network density.

============================================================
11. RELATIONSHIP INGESTION
============================================================

For every accepted relationship:

persist through the CCR V1 model:

Document
-> Passage
-> Atomic Claim
-> Relationship
-> Relationship Version
-> Relationship Support
-> independent Qualifiers

Do not write directly into graph/result structures.

Do not create a relationship merely because a graph path would be useful.

Do not modify historical Stage 2 rows.

============================================================
12. COVERAGE
============================================================

Track enrichment coverage for each researched:

- Legal Entity
- relationship family
- scope
- source set
- policy version
- as-of date

Use the governed outcomes unchanged.

Do not translate PARTIAL into RESEARCHED_NONE_FOUND.

Do not translate NOT_RESEARCHED into negative evidence.

A completed provider call does not imply complete real-world coverage.

============================================================
13. CORRELATION EVALUATION
============================================================

After sufficient accepted factual relationships have been created, run the existing six Stage 4/5 correlation definitions unchanged.

Do not create new definitions.

Do not increase depth.

Do not persist derived results.

Evaluate correlations naturally from the newly enriched accepted graph.

For each returned derived result record:

- definition
- source Client Record
- target Client Record
- intermediate Legal Entity
- exact qualifying relationship/version hops
- relationship directions
- evidence lineage
- identity lineage
- qualifiers
- temporal validity
- coverage
- warnings
- visibility/suppression metadata
- deterministic explanation

If result count is zero, preserve zero_is_not_universal_negative semantics.

============================================================
14. UI VALIDATION
============================================================

Do NOT redesign or materially expand the frontend.

Only use the existing Stage 6.1 workspace to validate real pilot outputs.

If the pilot naturally produces a non-zero derived correlation:

verify that the current UI correctly renders:

- factual network edges
- derived correlation overlay / halo
- correlation definition
- intermediate Legal Entity
- two underlying factual hops
- evidence drilldown
- identity lineage
- qualifiers
- coverage
- warnings
- query-time / non-persisted state

If the pilot produces zero derived correlations:

do NOT fabricate a UI demo.

Show the honest zero-result state.

============================================================
15. DO NOT IMPLEMENT
============================================================

Absolutely do NOT implement:

- new correlation definitions
- depth > 2
- recursive traversal
- portfolio-wide graph mining
- AI Analyst
- AI Create Correlation
- correlation authoring
- user-defined correlation configuration
- fuzzy identity matching
- synthetic relationships
- synthetic correlation fixtures in production data
- statistical / market correlation
- exposure logic
- old 16K / thousandClients priority cohort
- PostgreSQL migration
- graph database
- broad 3.67M enrichment
- major UI redesign

============================================================
16. SUCCESS CRITERIA
============================================================

Report the pilot against these dimensions.

Do NOT collapse them into a composite score.

A. Identity precision
- every VERIFIED+EXACT link reviewed
- no unsupported merge

B. Relationship precision
- accepted facts manually spot-checkable against exact evidence

C. Evidence replayability
- every accepted claim traceable to retained passage and source reference
- replay limitations explicitly identified

D. Coverage honesty
- PARTIAL / NOT_RESEARCHED / UNAVAILABLE preserved correctly

E. Relationship reuse
- evidence/documents reused instead of duplicated client-by-client retrieval

F. Naturally discovered correlations
- report any real non-zero matches
- zero remains acceptable

G. Analyst usability
- existing workspace can explain why a factual or derived result exists

H. Determinism
- rerun does not duplicate facts, claims, identities, relationships, versions, or qualifiers

I. Source / Client Universe safety
- source parquet unchanged
- Client Universe unchanged
- historical Stage 2 records unchanged

============================================================
17. REQUIRED REPORT
============================================================

Create:

backend/data/CCR_V1_STAGE_7_CONTROLLED_ENRICHMENT_PILOT_REPORT.md

The report must contain:

1. Executive result
2. Pre-flight safety audit
3. Pilot selection manifest
4. Research scope
5. Provider/source activity
6. Documents retrieved
7. Evidence/passages retained
8. Entity identities discovered
9. Client Record match-backs
10. Ambiguous/unresolved identities
11. Atomic claims
12. Accepted relationships
13. Candidate/rejected/context-only observations
14. Qualifiers
15. Coverage by entity/family
16. Correlation evaluation for all six definitions
17. Any naturally discovered correlations
18. Exact relationship hops for every derived result
19. UI positive/zero-result validation
20. Replay/idempotence
21. Database integrity
22. Client Universe integrity
23. Source-master integrity
24. Remaining limitations
25. Recommendation for next stage

Also produce a machine-readable run manifest.

============================================================
18. STOP CONDITION
============================================================

When Stage 7 completes:

STOP.

Do not automatically continue into:

- AI Analyst
- AI Create Correlation
- configurable authoring
- broader enrichment
- recursive graph expansion
- UI redesign

Return the report and wait for senior review.
