LENDING — EXTERNAL RESEARCH OVERLAY BACKEND INTEGRATION

This is the next stage after successful V3 CAM extraction and successful
read-only population reconciliation.

Proceed autonomously through the full approved scope.
Do not stop for intermediate approval.
Stop only for a genuine external/environment blocker.

==================================================
1. OBJECTIVE
==================================================

Build the backend integration layer that combines:

A. authoritative internal V3 CAM relationship data

with

B. supplemental external relationship research returned by the existing
Stylus SEC/R2D2 preset

WITHOUT mutating CAM truth.

This stage is BACKEND ONLY.

Do NOT rebuild the UI yet.

==================================================
2. CURRENT TRUSTED STATE
==================================================

V3 is frozen and validated.

Current V3 status:

- 46 unique physical narrative contents
- 42 physical CAM subject clients
- 13 canonical relationships
- 28 review-required relationships
- 0 unresolved document subjects
- 0 fragment entities in canonical
- 0 duplicate canonical rows
- 0 missing hidden paths
- CCR contamination = 0

V3 artifacts include:

- backend/data/LENDING_CANONICAL_V3_CANDIDATE.json
- backend/data/LENDING_V3_EXTRACTION_REPORT.json
- backend/data/LENDING_V3_EXTRACTION_REPORT.md
- backend/data/LENDING_V3_EXCEPTION_REGISTER.csv
- backend/data/LENDING_V3_SUBJECT_RECONCILIATION.csv

Reconfirm actual paths before use.

Do not hardcode paths if the repository already has path/config conventions.

==================================================
3. GOLDEN EXTERNAL RESEARCH FIXTURE
==================================================

A controlled Stylus result exists at the project root:

CoreWeave_NVIDIA_Relationship_Research.json

Use this as the GOLDEN EXTERNAL RESEARCH TEST FIXTURE.

It is NOT CAM truth.

It must NOT be inserted directly into V3 canonical data.

It is used to validate:

- JSON parsing
- schema handling
- evidence normalization
- source-channel normalization
- evidence admissibility
- semantic relationship consolidation
- cross-source corroboration recomputation
- V3 comparison/classification
- caching behavior
- review state generation

After locating it, copy it into the repository's existing test-fixture
location if one exists.

If no existing fixture convention exists, use something like:

backend/tests/fixtures/CoreWeave_NVIDIA_Relationship_Research.json

Do not modify the original root file.

==================================================
4. HARD BOUNDARIES
==================================================

LENDING ONLY.

DO NOT:

- modify V1
- modify V2
- modify V3 source data
- modify any CAM/PDF/DOCX source file
- rerun V3 extraction
- change V3 thresholds
- change the Stylus preset
- call Stylus automatically
- call SEC automatically
- call R2D2 automatically
- call Web automatically
- modify CCR
- read CCR data into Lending
- modify RPR
- redesign frontend/UI
- create external relationships as CAM canonical truth

External research remains supplemental.

==================================================
5. ARCHITECTURAL RULE
==================================================

The architecture must be:

V3 CAM
  = authoritative internal relationship state

External SEC/R2D2 result
  = supplemental research result

Backend Overlay
  = governed comparison / normalization / review layer

Never:

External result
  -> overwrite CAM

Never:

External result
  -> automatically become CAM canonical

==================================================
6. EXTERNAL RESULT STATES
==================================================

The backend must map external research into governed states.

Use these canonical application-level states:

CAM_CORROBORATION

Meaning:
An existing V3 CAM relationship is supported by admissible external evidence.

EXTERNAL_PROPOSAL_PENDING_REVIEW

Meaning:
External evidence supports a relationship that is not present as a matching
V3 CAM relationship.

CONFLICT_REVIEW_REQUIRED

Meaning:
External evidence materially conflicts with CAM relationship type,
direction, state, connectivity, or entity interpretation.

NO_EXTERNAL_CORROBORATION

Meaning:
The requested CAM relationship exists internally but acceptable external
evidence was not found.

MENTION_ONLY

Meaning:
External source mentions relevant entities but does not establish a
relationship.

INSUFFICIENT_EVIDENCE

Meaning:
Research returned data but it does not satisfy the evidence standard.

Do not silently map all EXTERNAL_PROPOSAL values to canonical truth.

==================================================
7. PARSE THE GOLDEN JSON SAFELY
==================================================

Validate the fixture before interpretation.

Required controls:

- syntactically valid JSON
- required root structure
- research_context
- result_summary
- findings[]
- unresolved_items[]

Do not assume all optional fields exist.

Do not crash if:
- CAGID is null
- entity_id is null
- evidence list is empty
- published_at is null
- filing_type is null
- conflict description is null

Return explicit validation errors for malformed payloads.

Do not silently repair materially malformed structures.

==================================================
8. EXTERNAL FINDING NORMALIZATION
==================================================

Normalize each finding into a backend model.

At minimum persist:

- external_result_id
- subject_name
- subject_entity_id if available
- subject_cagid if available
- related_name
- related_entity_id if available
- related_cagid if available
- relationship_type
- finding_type_raw
- relationship_supported
- mention_only
- relationship_status
- connectivity
- direction
- confidence_raw
- normalized_confidence
- credit_materiality classification
- claim
- rationale
- credit_relevance
- evidence[]
- conflict
- analyst_review_required
- unresolved_items
- research as-of date
- source channels requested
- request key
- payload hash
- created/received timestamp

Do not invent missing values.

==================================================
9. SEMANTIC RELATIONSHIP IDENTITY
==================================================

For comparison and deduplication, define semantic identity using:

- normalized subject entity
- normalized related entity
- relationship type
- direction

State may be compared separately.

Do not duplicate the same semantic relationship merely because:

- SEC and Web both found it
- several SEC filings support it
- multiple excerpts support it

One semantic external relationship can contain multiple evidence objects.

==================================================
10. ENTITY MATCHING
==================================================

Compare external entities to V3 entities conservatively.

Priority:

1. exact CAGID
2. exact internal entity_id
3. exact normalized legal name
4. validated alias if already present locally
5. otherwise unresolved

Do NOT perform broad fuzzy matching.

Do NOT manufacture CAGIDs.

Do NOT automatically match similar names where ambiguity exists.

If unresolved:
preserve external finding,
but set entity-match state to REVIEW_REQUIRED.

For the golden fixture:
CoreWeave and NVIDIA may have null CAGIDs in the Stylus JSON.

Use local V3/entity registry only if deterministic matching exists.

==================================================
11. SOURCE CHANNEL NORMALIZATION
==================================================

The backend must enforce the preset governance rules even if model output
does not fully comply.

source_channel represents the UNDERLYING SOURCE.

Rules:

- SEC 10-K, 10-Q, 8-K, S-1, proxy, exhibit, or other SEC filing
  -> SEC_FILING

- genuine company website, Reuters, Bloomberg, FT, etc.
  -> R2D2_WEB

If R2D2 retrieved an SEC filing:
normalize to SEC_FILING.

Do not keep the same SEC filing once as SEC_FILING and again as R2D2_WEB.

==================================================
12. EVIDENCE DEDUPLICATION
==================================================

Deduplicate evidence by stable normalized key using, where available:

- source channel
- normalized source reference / URL
- filing type
- publication date
- normalized excerpt

Avoid duplicate evidence objects from:
- repeated model output
- same filing returned by multiple tools
- same excerpt with trivial whitespace/case differences

Keep provenance of merged duplicates.

==================================================
13. EVIDENCE ADMISSIBILITY FILTER
==================================================

This is critical.

The backend must not blindly trust model-assigned HIGH confidence.

For every evidence object determine:

ADMISSIBLE
or
NOT_ADMISSIBLE

Evidence should be admissible only when:

1. source type is allowed;
2. source is not a prohibited low-quality source;
3. evidence excerpt materially supports the claimed relationship;
4. entity identity is sufficiently clear;
5. relationship semantics are sufficiently clear;
6. source provenance/reference is usable;
7. evidence is not merely a generic statement.

Examples of evidence that must NOT independently support a relationship:

- generic supplier commentary
- generic advanced-hardware commentary
- generic collaboration language
- generic market commentary
- generic semiconductor supply-chain text
- co-mention only
- unrelated upstream supplier discussion

For POC scope, implement deterministic structural and source-quality checks.

Do NOT attempt to build a new LLM adjudicator.

Where semantic admissibility cannot be deterministically established from
structured fields:
preserve the model result but mark it for analyst review rather than
automatically treating it as trusted.

==================================================
14. SOURCE QUALITY POLICY
==================================================

Allowed / preferred:

Tier 1:
- SEC filings
- official company IR
- official company press releases
- exchange filings
- regulators/government
- official transaction disclosures
- rating agencies

Tier 2:
- Reuters
- Bloomberg
- Financial Times
- Wall Street Journal
- S&P
- Moody's
- Fitch
- other established institutional sources

Tier 3:
- reputable specialist/trade sources
- supplemental only

Do not allow as relationship proof:

- blogs
- anonymous blogs
- SEO/content farms
- aggregators
- repost/scrape sites
- forums
- social media
- AI-generated summaries
- generic company-profile sites
- Wikipedia as final evidence
- unsourced claims

Persist source tier.

==================================================
15. RECOMPUTE CROSS-SOURCE CORROBORATION
==================================================

Do NOT trust:

cross_source_corroboration

from the model output.

Recompute it.

Set TRUE only if retained admissible evidence represents at least two
genuinely independent underlying sources.

Examples:

Same SEC filing, 3 excerpts:
FALSE

Two sections of same 10-K:
FALSE

10-K + same 10-K discovered through R2D2:
FALSE

10-K + Reuters:
TRUE

Company press release + Reuters:
TRUE

Different SEC filings by same registrant:
multiple-document support, but not automatically Web+SEC independent
cross-source corroboration.

Persist:

- model_cross_source_corroboration
- backend_cross_source_corroboration
- independent_source_count

==================================================
16. CONFIDENCE NORMALIZATION
==================================================

Recompute a normalized backend evidence confidence.

Do not automatically copy model HIGH.

Use:

HIGH
MEDIUM
INSUFFICIENT

HIGH requires:
- admissible evidence
- strong entity identification
- explicit relationship semantics
- strong source quality
- no material conflict

MEDIUM:
- admissible evidence exists
- relationship is defensible
- one important confirmation element is missing

INSUFFICIENT:
- no admissible evidence
- weak/ambiguous source
- co-mention
- unresolved identity affecting the relationship materially
- unsupported direction/type
- material contradiction

Persist both:
- model confidence
- backend normalized confidence

==================================================
17. V3 COMPARISON
==================================================

For every external semantic relationship:

Compare against V3 canonical relationships first.

Then inspect V3 review-required relationships separately.

Do NOT treat review-required as canonical truth.

Comparison dimensions:

- entity pair
- relationship type
- direction
- state
- connectivity

Possible outcomes:

MATCHES_CANONICAL_CAM
MATCHES_REVIEW_REQUIRED_CAM
NEW_EXTERNAL_RELATIONSHIP
CONFLICTS_CANONICAL_CAM
UNRESOLVED_ENTITY_MATCH

==================================================
18. GOVERNED CLASSIFICATION
==================================================

Derive final application classification.

If external finding matches canonical V3 and evidence is admissible:

CAM_CORROBORATION

If V3 canonical exists but admissible external evidence is absent:

NO_EXTERNAL_CORROBORATION

If external finding is not present in V3 and evidence is HIGH/MEDIUM:

EXTERNAL_PROPOSAL_PENDING_REVIEW

If external finding conflicts materially with canonical V3:

CONFLICT_REVIEW_REQUIRED

If only co-mention:

MENTION_ONLY

If no admissible evidence:

INSUFFICIENT_EVIDENCE

Never mutate V3 as part of classification.

==================================================
19. GOLDEN FIXTURE EXPECTATIONS
==================================================

The CoreWeave/NVIDIA golden fixture currently contains two semantic findings:

1. supplier
2. technology_dependency

Expected directional semantics:

supplier:
NVIDIA -> CoreWeave
B_TO_A relative to SubjectEntity CoreWeave / RelatedEntity NVIDIA

technology_dependency:
CoreWeave -> NVIDIA
A_TO_B

The backend test must verify these remain separate semantic findings.

Do not expect CAGIDs to be supplied by the fixture.

Do not invent them.

If deterministic local entity matching exists, record the match separately.

==================================================
20. CACHE DESIGN
==================================================

External research can be slow.

Implement a simple POC cache.

Cache key must include at least:

- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- AsOfDate

Normalize ordering where appropriate.

For empty RelatedEntity discovery mode, key must still be deterministic.

Persist:

- cache key
- request inputs
- result payload
- normalized result
- created_at
- payload hash
- status

Do not overengineer.

Use the repository's existing storage convention where possible.

==================================================
21. ON-DEMAND ONLY — CRITICAL
==================================================

External research MUST NEVER run automatically.

It must NOT trigger from:

- application startup
- backend startup
- page load
- entity selection
- graph node click
- graph edge click
- route change
- refresh
- reconnect
- websocket reconnect
- browser reload
- cache miss during a normal read endpoint
- background worker
- polling
- scheduled job

Execution is allowed ONLY after an explicit user research action.

Backend read endpoints must NEVER trigger external research.

==================================================
22. EXECUTION ENDPOINT / SERVICE
==================================================

Create a clear backend service boundary.

Conceptually:

POST /lending/external-research/run

or follow the repository's existing API conventions.

It must require explicit invocation.

Inputs must remain aligned with the existing six Stylus runtime keys:

- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- ResearchInstruction
- AsOfDate

Do not invent required runtime keys.

Before remote execution:

1. validate inputs
2. check cache
3. if successful cached result exists:
   return cache unless explicit supported refresh mode exists
4. otherwise invoke existing external-runner integration

Do NOT build a new Stylus authentication architecture.

Reuse the proven existing runner/preset invocation mechanism if present.

==================================================
23. IMPORTANT — DO NOT CALL LIVE STYLUS UNNECESSARILY
==================================================

For this implementation stage:

FIRST validate the complete normalization/comparison pipeline using the local
golden fixture.

Do not make a live Stylus call merely to prove parsing logic.

Only perform ONE live controlled execution at the end if:

- the existing runner integration is already configured,
- credentials/auth are available,
- and it is required for end-to-end acceptance.

If live execution is unavailable:
the local golden-fixture acceptance test is sufficient for this stage and
report the live-run blocker separately.

==================================================
24. READ ENDPOINTS
==================================================

Provide read-only backend access to normalized external results.

At minimum support:

- external result for request/entity pair
- cached status
- governed classification
- evidence
- unresolved items
- V3 comparison state

Read endpoints must never trigger research.

==================================================
25. EXTERNAL RESULT STORAGE
==================================================

Do NOT store external results inside V3 relationship tables/artifacts.

Keep external overlay data logically separate.

Example conceptual storage:

external_research_runs
external_findings
external_evidence
external_cache

or repository-equivalent.

POC scope:
keep implementation simple.

Do not introduce unnecessary enterprise architecture.

==================================================
26. HIDDEN / INDIRECT EXTERNAL PATHS
==================================================

Support the schema/logic for hidden relationships, but do not manufacture
paths from the golden fixture.

A hidden external relationship is valid only when every hop has admissible
evidence.

Persist:

- path length
- intermediate entities
- relationship type per hop
- evidence per hop
- weakest-hop confidence

If any hop = INSUFFICIENT:
do not promote the hidden path.

==================================================
27. REVIEW MODEL
==================================================

External proposals and conflicts should have a simple review state:

PENDING_REVIEW
ACCEPTED_AS_EXTERNAL
REJECTED
NEEDS_MORE_EVIDENCE

IMPORTANT:

ACCEPTED_AS_EXTERNAL does NOT mean CAM canonical.

It remains external intelligence.

Do not implement CAM mutation.

==================================================
28. TESTS
==================================================

Create focused tests for:

A. fixture parsing
B. schema validation
C. supplier direction
D. technology_dependency direction
E. duplicate evidence removal
F. SEC source normalization
G. no SEC evidence duplicated as Web
H. cross-source corroboration recomputation
I. null CAGID handling
J. entity matching without fuzzy guessing
K. V3 CAM comparison
L. external proposal classification
M. CAM corroboration classification
N. conflict classification
O. insufficient evidence handling
P. cache hit
Q. cache key stability
R. normal GET/read does not trigger research
S. application startup does not trigger research
T. refresh/reconnect does not trigger research

==================================================
29. REGRESSION PROTECTION
==================================================

Verify after implementation:

V1 unchanged
V2 unchanged
V3 unchanged

Specifically verify:

- V3 canonical relationships still 13
- V3 review-required still 28
- unresolved document subjects still 0
- V3 artifact hash/digest unchanged where previously recorded

Do not modify the new 2,484 population workbook.

Do not modify population-analysis source files.

Do not modify Stylus preset files.

Do not modify frontend.

==================================================
30. REQUIRED STATISTICS / REPORT
==================================================

Produce an implementation/validation report containing:

Golden fixture:
- findings received
- semantic findings after dedupe
- evidence received
- evidence retained
- evidence removed/flagged
- SEC evidence count
- Web evidence count
- independent source count
- model cross-source values
- backend recomputed cross-source values

Entity matching:
- matched by CAGID
- matched by entity_id
- matched by exact legal name
- unresolved

V3 comparison:
- CAM corroborations
- external proposals
- conflicts
- no corroboration
- mention only
- insufficient evidence

Cache:
- cache key
- cache write PASS/FAIL
- cache read PASS/FAIL
- duplicate execution prevented PASS/FAIL

Execution safety:
- startup auto-trigger = 0
- page/read endpoint auto-trigger = 0
- reconnect trigger = 0
- explicit-run-only control = PASS/FAIL

Regression:
- V1 unchanged PASS/FAIL
- V2 unchanged PASS/FAIL
- V3 unchanged PASS/FAIL
- Stylus preset unchanged PASS/FAIL
- CCR untouched PASS/FAIL
- frontend untouched PASS/FAIL

==================================================
31. ACCEPTANCE CRITERIA
==================================================

This stage passes only if:

- golden fixture parses successfully
- exactly 2 semantic CoreWeave/NVIDIA findings remain
- supplier direction remains correct
- technology_dependency direction remains correct
- external data remains separate from V3
- SEC/Web channels are normalized correctly
- duplicate evidence is controlled
- backend recomputes cross-source corroboration
- null CAGIDs do not cause invented identities
- no broad fuzzy matching
- governed classification works
- cache works
- external execution is explicit-user-action only
- no automatic execution path exists
- V1/V2/V3 unchanged
- frontend unchanged
- CCR untouched

==================================================
32. OUTPUT ARTIFACTS
==================================================

Use repository conventions.

At minimum create/update:

- external research normalization/service code
- external overlay models/schema
- cache implementation
- tests
- human-readable validation report

Suggested report:

backend/data/LENDING_EXTERNAL_OVERLAY_VALIDATION_REPORT.md

and optionally:

backend/data/LENDING_EXTERNAL_OVERLAY_VALIDATION_REPORT.json

Do not create unnecessary files.

==================================================
33. FINAL RESPONSE
==================================================

Return:

LENDING EXTERNAL OVERLAY BACKEND: PASS / FAIL

Golden fixture parsed:
PASS / FAIL

Fixture findings received:
X

Semantic findings retained:
X

Supplier direction:
PASS / FAIL

Technology dependency direction:
PASS / FAIL

Evidence received:
X

Evidence retained:
X

Evidence filtered/flagged:
X

SEC evidence normalized:
PASS / FAIL

SEC duplicated as Web:
0 / X

Backend cross-source corroboration recomputed:
PASS / FAIL

Entity matches:
X

Unresolved entity matches:
X

CAM_CORROBORATION:
X

EXTERNAL_PROPOSAL_PENDING_REVIEW:
X

CONFLICT_REVIEW_REQUIRED:
X

NO_EXTERNAL_CORROBORATION:
X

MENTION_ONLY:
X

INSUFFICIENT_EVIDENCE:
X

Cache write:
PASS / FAIL

Cache read:
PASS / FAIL

Explicit-run-only:
PASS / FAIL

Automatic startup executions:
0 / X

Automatic read/page executions:
0 / X

V1 unchanged:
PASS / FAIL

V2 unchanged:
PASS / FAIL

V3 unchanged:
PASS / FAIL

Stylus preset unchanged:
PASS / FAIL

Frontend unchanged:
PASS / FAIL

CCR untouched:
PASS / FAIL

Validation report:
<path>

READY FOR PORTFOLIO API + UI INTEGRATION:
YES / NO

If NO:
list only blockers.

Then STOP.
