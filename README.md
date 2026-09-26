Claude’s review is constructive and confirms the direction. The important point is that Stage 5 architecture is approved; the remaining issues are API-contract completeness, not a redesign. Claude explicitly says there is no reason to change the evaluator, identity model, or the six correlation definitions themselves.   Pasted markdown
I would therefore not start the UI quite yet. Insert one small checkpoint: Stage 5.1 — UI Contract Hardening. Claude identified five things that should be proven or patched before the UI binds itself to these payloads: per-definition coverage/status, complete per-hop derived lineage, related-client navigation metadata, structured coverage on zero results, and consistent schemas between list and pairwise endpoints.   Pasted markdown
Importantly, Claude agrees that the lack of a real positive two-hop correlation does not block the UI. We can validate positive rendering using fixture-generated real contract payloads while separately increasing the real relationship graph later.   Pasted markdown Claude also agrees that we should use the existing six routes and /summary as the workspace bootstrap rather than inventing another aggregate API now.   Pasted markdown
Implement with Luna — Stage 5.1
Give Luna this prompt before any frontend work:
CCR V1 — STAGE 5.1: UI CONTRACT HARDENING
We have completed and validated CCR V1 Stage 5.
A senior architecture review returned:
Stage 5 verdict: APPROVE WITH PATCH
This is a narrow API/read-model contract hardening stage before Stage 6 UI.
Do NOT redesign the correlation engine.
Do NOT begin frontend development.
Do NOT perform enrichment or research.
Do NOT call SEC, GLEIF, Web, Stylus, or any external provider.
Do NOT modify the Client Universe or authoritative source parquet.
Do NOT create synthetic relationships.
Do NOT create fuzzy identity merges.
Do NOT persist derived correlation results.
Do NOT expand traversal beyond the approved Stage 4.1 two-hop patterns.
Preserve the approved architecture:
- DIRECT_RELATIONSHIP = factual accepted relationship projection.
- DERIVED_CORRELATION = governed query-time structural match.
- endpoint identity gate = VERIFIED + EXACT.
- relationship-version gate = ACCEPTED.
- supporting evidence lineage mandatory.
- derived depth exactly two relationship hops.
- derived pattern kinds limited to SHARED_INTERMEDIATE and DIRECTED_CHAIN.
- derived results query-time only.
- execution status and research/enrichment coverage remain independent.
- zero result is not proof of real-world non-existence.
Existing Stage 5 public routes must remain:
1. GET /api/ccr/correlation-definitions
2. GET /api/ccr/clients/{client_id}/summary
3. GET /api/ccr/clients/{client_id}/relationships
4. GET /api/ccr/clients/{client_id}/correlations
5. GET /api/ccr/clients/{source_client_id}/relationships/{target_client_id}
6. GET /api/ccr/clients/{source_client_id}/correlations/{target_client_id}
Do not replace these with a new aggregate/bootstrap endpoint.
1. AUDIT FIRST
Before changing code, inspect the actual Stage 5 response models and actual serialized payloads.
For every requirement below classify it:
- ALREADY_PRESENT_AND_CORRECT
- PRESENT_BUT_INCOMPLETE
- MISSING
Only patch what is actually missing or inconsistent.
Produce this audit in the Stage 5.1 report.
2. MULTI-DEFINITION CORRELATION STATUS
Inspect:
GET /api/ccr/clients/{client_id}/correlations
The response must make it possible for the UI to distinguish each correlation definition independently.
Each definition/result group must expose its own:
- definition_id
- definition_code
- definition_version
- category
- execution_status
- research_coverage
- result_count
- zero_is_not_universal_negative
- applicable warnings
Do not return only one shared execution status or one shared coverage value for all six definitions if the underlying coverage differs by relationship family/scope.
Example conceptual distinction:
- SHARED_SUPPLIER → execution COMPLETE, supply coverage PARTIAL
- SHARED_LENDER → execution COMPLETE, financing coverage NOT_RESEARCHED
Do not fabricate coverage where no coverage record exists.
3. STRUCTURED COVERAGE MUST ACCOMPANY ZERO RESULTS
A zero-match correlation response must not rely only on:
zero_is_not_universal_negative = true
The UI must also receive the governed structured coverage records that explain the research/enrichment state relevant to that definition.
Preserve:
- outcome
- freshness
- as-of date
- relationship family
- scope
- source set
- policy version
- available lifecycle/count metadata
A zero result therefore means:
no qualifying match was found in the currently available eligible graph under the stated coverage
It must never silently mean:
the relationship/correlation does not exist in the real world.
Add regression tests.
4. DERIVED CORRELATION EXPLANATION CONTRACT
Inspect the positive fixture payload for a derived correlation.
Each returned two-hop derived correlation must expose enough information for a Stage 6 analyst to answer:
“Why are these two clients connected?”
For every hop, expose or confirm:
- relationship ID
- relationship-version ID/version
- factual relationship type
- canonical relationship direction
- path-relative/query-relative direction
- relationship acceptance state
- evidence basis
- freshness / relevant temporal state
- supporting evidence lineage
- source Legal Entity
- target Legal Entity
- relevant endpoint identity-link ID
- identity-link type (EXACT / etc.)
- identity-link state
For the intermediate entity expose:
- Legal Entity ID
- display/legal name where stored
- its role in this correlation pattern
- role-specific known degree/count used for hub logic, if available
- whether it resolves to a Client Universe Client Record
- resolved client_id when uniquely eligible
- hub/visibility state
- suppression reason if applicable
Never fabricate missing metadata.
If a requested field cannot be supported from stored Stage 1–5 data, expose it as null/absent according to the existing serialization convention and document why.
5. RELATED-CLIENT NAVIGATION METADATA
Every factual relationship item returned to the future workspace must distinguish:
1. counterparty Legal Entity exists but is not resolved to a Client Record;
2. counterparty resolves uniquely to a Client Record;
3. counterparty-to-client resolution is ambiguous/unavailable.
Add an explicit structured counterparty navigation/resolution object or equivalent fields.
It must expose, where valid:
- is_client
- client_id
- GFCID where appropriate
- resolution status
Do NOT resolve by name alone.
Do NOT turn ambiguous entity-to-client candidates into client links.
This is needed so Stage 6 can make:
3M India → clickable internal Client Record
versus:
external/unresolved Legal Entity → entity detail only
explicit.
6. LIST VS PAIRWISE SCHEMA CONSISTENCY
Audit:
/clients/{id}/relationships
against:
/clients/{source}/relationships/{target}
And audit:
/clients/{id}/correlations
against:
/clients/{source}/correlations/{target}
A relationship result item and correlation result item must have the same canonical domain/result schema regardless of whether it came from the list or pairwise route.
A list route may wrap items with pagination metadata, but individual result objects must not become semantically different or lose fields.
Add explicit schema-equivalence regression tests.
The Stage 6 UI must not need separate interpretation logic for the same relationship simply because it came from a list versus pairwise call.
7. CANONICAL VS QUERY-RELATIVE DIRECTION
Ensure field names make this distinction impossible to confuse.
Preserve both:
- factual/canonical relationship direction;
- query-relative direction.
The existing reverse 3M India → 3M test must continue to reference the same canonical owns relationship and must never fabricate inverse ownership.
If current field names are already explicit, leave them unchanged.
If ambiguous, make a backward-compatible contract clarification rather than changing relationship truth.
8. RELATIONSHIP HISTORY POINTER
This is useful but not a blocker.
Where a current relationship version has previous versions, expose a lightweight history reference if the stored model can support it cheaply:
- current version ID/version
- prior-version existence/count or IDs
Do not build a full history API or UI.
Use the real 3M/Solventum ownership case to validate this if applicable:
- earlier 19.9%
- later 14.8%
Never collapse these into one percentage.
9. CORRELATION CATEGORY NORMALIZATION
Keep the six approved definition semantics unchanged.
Normalize only the category metadata if needed to the approved four-category vocabulary:
- GROUP_STRUCTURE
- COMMERCIAL_DEPENDENCY
- FINANCING
- PRODUCT_DEPENDENCY
Expected mapping:
- SHARED_CONTROLLER → GROUP_STRUCTURE
- SHARED_SUPPLIER → COMMERCIAL_DEPENDENCY
- SHARED_CUSTOMER → COMMERCIAL_DEPENDENCY
- SUPPLY_CHAIN → COMMERCIAL_DEPENDENCY
- SHARED_LENDER → FINANCING
- SHARED_PRODUCT_DEPENDENCY → PRODUCT_DEPENDENCY
Category must remain governance/UI metadata only.
It must not alter matching semantics or correlation fingerprints unless the approved fingerprint contract explicitly includes category metadata.
Preserve migration/replay safety.
10. POSITIVE DERIVED FIXTURE CONTRACT
Real Stage 5 data currently has no positive two-hop derived correlation.
This is NOT permission to create synthetic production data.
Use isolated tests/fixtures to create at least:
A. positive SHARED_INTERMEDIATE example
Client A → supplier X
Client B → supplier X
resulting in:
SHARED_SUPPLIER
B. positive DIRECTED_CHAIN example
Client A → entity X → Client B
using one of the approved directed definitions.
Validate the entire serialized public Stage 5/5.1 response shape, including:
- endpoint identities
- intermediate entity
- both hops
- evidence lineage
- relationship/version identifiers
- qualifiers where applicable
- coverage
- execution status
- visibility/hub metadata
- deterministic explanation
- persisted_result = false
These tests are specifically intended to become the contract against which Stage 6 renders a positive derived correlation before one exists in the sparse real graph.
11. REAL 3M REGRESSION
Repeat local read-only validation against the real existing relationship database.
Confirm at minimum:
3M → 3M India
- direct result found
- owns
- 75% qualifier
- both endpoints use persisted qualifying identity links
- canonical direction preserved
- related Client Record metadata present for 3M India
3M India → 3M
- same factual relationship
- query-relative direction reversed
- no fabricated inverse ownership
3M → Solventum
- existing accepted owns
- existing accepted supplies
- explicit pairwise selected-client behavior remains correct
- current identity contract remains unchanged
Derived definitions
All six can still legitimately return zero against the current real graph.
Confirm each zero result carries:
- definition-specific execution status
- structured relevant coverage
- zero_is_not_universal_negative = true
12. PRESERVE ALL SAFETY INVARIANTS
Confirm:
- Client Universe rows = 3,670,650
- unique GFCIDs = 3,670,650
- source parquet unchanged
- relationship source database integrity clean
- no external provider calls
- no new research
- no new accepted relationship discovery
- no fuzzy merges
- no synthetic direct edges
- no persisted derived-result rows
- no frontend files modified
Do not weaken the identity/evidence gates to make tests pass.
13. TESTS
Add focused Stage 5.1 regression tests for:
1. per-definition execution state;
2. per-definition structured coverage;
3. zero-result coverage contract;
4. positive SHARED_INTERMEDIATE serialized result;
5. positive DIRECTED_CHAIN serialized result;
6. complete two-hop lineage;
7. intermediate-is-client metadata;
8. ambiguous intermediate/client resolution;
9. relationship counterparty client metadata;
10. relationship list/pairwise schema equivalence;
11. correlation list/pairwise schema equivalence;
12. canonical/query-relative direction distinction;
13. hub suppression metadata without deleting structural results;
14. no persisted derived result;
15. real 3M regressions.
Run the full backend suite.
14. REPORT
Create:
backend/data/CCR_V1_STAGE_5_1_UI_CONTRACT_HARDENING_REPORT.md
It must state:
- audit findings before changes;
- exactly which Stage 5 fields were already present;
- exactly which fields/contracts required changes;
- public response models after the patch;
- list/pairwise schema consistency result;
- positive derived fixture examples;
- real 3M regression results;
- per-definition coverage/status result;
- zero-result semantics;
- test totals;
- DB integrity results;
- provider calls = 0;
- Client Universe modifications = 0;
- frontend modifications = 0.
Finish with one of:
STAGE 5.1 PASS — READY FOR STAGE 6 UI
or
STAGE 5.1 HOLD — <specific unresolved blocker>
Stop after Stage 5.1.
Do NOT begin Stage 6.
