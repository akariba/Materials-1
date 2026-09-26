CLIENT CORRELATION — STAGE 2A.7 — EVIDENCE-BACKED FRONTIER EXPANSION PILOT
Continue from the completed Stage 2A.6 implementation.
Do NOT redesign traversal.
Do NOT modify the 3.67M Client Universe source.
Do NOT fabricate relationships or create synthetic shortcuts.
Stage 2A.6 correctly demonstrated that the current accepted graph has no second-level edges. Provider attempts were 0 because traversal operated only over already-persisted accepted observations.
Stage 2A.7 must now perform the missing operation:
research the accepted depth-1 endpoints and expand the graph with independently evidence-backed relationships.
1. Pilot root
Use the same real 3M root used in Stage 2A.6.
Obtain its currently accepted direct neighbors from the relationship repository.
Only accepted/evidence-backed depth-1 endpoints may become frontier research subjects.
Candidates, generic descriptors, NO_EVIDENCE findings, unresolved identities, or synthetic entities must NOT become traversal-expansion seeds.
2. Frontier research
For each eligible depth-1 entity:
run bounded external relationship discovery using the existing approved provider infrastructure:
- SEC_FILINGS
- R2D2_WEB / approved Web
- GLEIF where applicable
Research the entity itself, not merely its relationship back to 3M.
Discover its strongest defensible relationships permitted by the existing controlled taxonomy.
Use the existing Stylus-derived evidence, identity, direction, materiality and acceptance policies unchanged.
Search broadly but accept narrowly.
3. Strict pilot bounds
This is NOT a universe-wide crawl.
For this pilot:
- root depth = 0
- existing direct neighbors = depth 1
- actively research depth-1 entities only
- maximum newly accepted relationships per frontier entity = 3
- do not recursively research depth-2 entities yet
- use the existing AsOfDate
- preserve provider caching, audit and replay semantics
This keeps the research bounded while giving Stage 2A.6 actual second-level graph material.
4. Identity resolution
Every discovered related entity must pass deterministic identity handling.
Resolution order:
1. exact Client Universe identity where defensible;
2. existing external entity identity;
3. new external entity only when external identity is sufficiently established;
4. otherwise remain unresolved candidate.
Never fuzzy-merge.
Never create a Client Universe client from external text.
Never treat a similar company name as identity proof.
Critically, check whether a discovered endpoint already exists among the 3,670,650 Client Universe clients.
This is essential because the product ultimately needs to discover Client-Universe-to-Client-Universe correlations.
5. Relationship acceptance
Only persist a new accepted relationship observation when:
- both endpoint identities satisfy policy;
- relationship semantics are explicit;
- direction is supported where required;
- evidence is admissible;
- relationship type is in controlled taxonomy;
- evidence meets the existing acceptance threshold.
Otherwise preserve it as candidate / unresolved / no-evidence according to existing contracts.
Do not lower thresholds to manufacture graph depth.
6. After frontier research
Once new accepted observations are persisted:
rerun the existing Stage 2A.6 traversal from 3M.
Now evaluate:
3M -> depth-1 entity -> depth-2 entity
and, where naturally available:
3M -> A -> B -> C
Do not create synthetic 3M -> B or 3M -> C relationships.
A path is a path, not a direct relationship.
7. Correlation detection
Explicitly identify when a valid evidence-backed path connects:
Client Universe client → one or more intermediaries → another Client Universe client
Persist the path and its ordered hops.
Preserve:
- relationship type per hop
- direction per hop
- evidence references per hop
- endpoint identity provenance
- weakest-hop strength
- path depth
- internal/external entity classification
A hidden path must never be stronger than its weakest hop.
8. Provider activity must be real
Unlike Stage 2A.6, this stage is expected to execute provider research.
Report separately:
- frontier entities considered
- frontier entities researched
- SEC attempts
- Web attempts
- GLEIF attempts
- cache hits
- provider failures
- documents retrieved
- candidate findings
- accepted new observations
- unresolved endpoints
- new external entities
- discovered endpoints resolving to Client Universe
Provider attempts = 0 is NOT sufficient for Stage 2A.7 unless there are genuinely zero eligible frontier entities, in which case stop and report why.
9. Path results
After expansion report:
- accepted graph edges before Stage 2A.7
- accepted graph edges after Stage 2A.7
- new second-level edges
- 2-hop paths
- 3-hop paths
- Client-Universe-to-Client-Universe paths
- paths involving external intermediaries
- synthetic direct relationships created: MUST BE 0
Do NOT force a hidden path to exist.
A legitimate result of zero paths is acceptable if genuine provider research has been performed and no admissible second-level relationship survives the gates.
10. Replay/integrity
Exact replay must not duplicate:
- provider attempts where cache/replay semantics prohibit it
- external identities
- observations
- evidence objects
- graph edges
- paths
Source master modifications must remain 0.
Fuzzy merges must remain 0.
Synthetic shortcuts must remain 0.
11. Validation
Run the full backend test suite.
Add focused tests for:
- accepted frontier entity triggers research
- candidate frontier does not
- second-level relationship acceptance
- exact Client Universe endpoint resolution
- external endpoint resolution
- duplicate prevention
- weak evidence remains candidate
- path creation after new edge
- path weakest-hop semantics
- no synthetic direct relationship
- replay/idempotence
Produce:
backend/data/FRONTIER_RELATIONSHIP_EXPANSION_STAGE_2A7_REPORT.md
At the end provide a concise PASS/FAIL summary and actual pilot counts.
Do not work on frontend/UI in this stage.
