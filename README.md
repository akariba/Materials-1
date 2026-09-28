Stage 7 senior review is approved. Implement only the authorized Stage 7 corrections and completion path below. Do not start Stage 8.
1. Approved execution architecture
Freeze this architecture:
- Stylus executes only SEC_FILING + R2D2_WEB.
- Existing audited CCR backend provider remains the sole GLEIF execution channel.
- Provider execution topology is operational only; it does not alter source class.
- All provider outputs merge only through the existing CCR V1 identity/evidence/claim/relationship ingestion contracts.
Do not:
- add GLEIF to Stylus
- rename a Stylus preset to imply GLEIF capability
- create a fake GLEIF adapter
- rerun GLEIF merely because Stylus does not execute it
- change the frozen 8-entity selection
- create a new pilot fingerprint
- change relationship ontology
- change correlation definitions
- loosen identity/evidence gates
- start Stage 8
The existing Stage 7 frozen selection fingerprint remains authoritative.
2. Preserve the frozen manifest/fingerprint
Do not version or regenerate the governed Stage 7 selection manifest merely because execution routing changed.
Add an auditable execution-routing note associated with the existing Stage 7 run/fingerprint stating:
- GLEIF → existing CCR backend audited provider
- SEC_FILING → Stylus
- R2D2_WEB → Stylus
This note is operational metadata only and must not change:
- population
- selection fingerprint
- ontology
- evidence policy
- identity policy
- correlation definitions
- depth limits
Validate before continuing that the original frozen fingerprint is unchanged.
3. Correct the coverage model
Implement explicit source-class coverage for each applicable:
entity × relationship_family × required_source_class
Required source classes must come from the existing frozen Stage 7 request/scope matrix. Do not assume that every entity/family necessarily requires all three providers if the frozen scope says otherwise.
Each required source class must independently have one of:
- COMPLETE
- NOT_ATTEMPTED
- UNAVAILABLE
Keep result/finding counts separate from execution status.
The entity×family top-level coverage outcome remains exactly:
- NOT_ELIGIBLE
- NOT_RESEARCHED
- RESEARCHED_FOUND
- RESEARCHED_NONE_FOUND
- PARTIAL
- UNAVAILABLE
Do not add IDENTITY_UNRESOLVED as a seventh top-level outcome.
Use IDENTITY_UNRESOLVED only as a reason code.
Mechanical roll-up rules
Implement deterministic roll-up rather than allowing callers/runners to assert a top-level result manually.
At minimum:
- Family/entity outside governed scope → NOT_ELIGIBLE
- No required source class attempted → NOT_RESEARCHED
- Every required source class COMPLETE and qualifying accepted result exists → RESEARCHED_FOUND
- Every required source class COMPLETE and no qualifying accepted result exists → RESEARCHED_NONE_FOUND
- Mix containing COMPLETE plus any required NOT_ATTEMPTED or UNAVAILABLE → PARTIAL
- Some work attempted but required scope remains incomplete → PARTIAL
- UNAVAILABLE only where all legitimate required research/resolution paths have genuinely been attempted/exhausted and are unavailable; never use it for merely unattempted work.
Preserve reason codes independently, e.g.:
- IDENTITY_UNRESOLVED
- provider/authentication unavailable
- source-specific configuration failure
- other existing governed reasons
A positive finding from one provider must not make incomplete required provider scope appear complete.
Likewise, a zero finding from GLEIF cannot produce RESEARCHED_NONE_FOUND while required SEC/Web scope remains incomplete.
4. Correct existing Stage 7 coverage records
Re-evaluate the current Stage 7 records under the corrected computation.
In particular:
- remove any top-level IDENTITY_UNRESOLVED
- convert it to an appropriate top-level governed outcome plus reason code
- reassess any RESEARCHED_NONE_FOUND/CURRENT result that was produced while a required source class remained incomplete
- preserve independent freshness fields; do not invent a global freshness policy
EPA must be NOT_ELIGIBLE for this ACTIVE relationship pilot, because regulatory-body relationships are outside the active V1 ontology for this run.
EPA is not an outstanding Stylus target.
5. Retain existing GLEIF research
Do not rerun successfully completed GLEIF work simply to satisfy execution topology.
Validate that the already completed Stage 7 GLEIF work has durable, auditable provenance sufficient for the existing CCR V1 identity/evidence contract.
Confirm for retained GLEIF material:
- registry response/record identity
- retrieval timestamp
- provider/source provenance
- original identifiers/query context
- retained payload or governed reproducible reference as required by the existing contract
A session log alone is insufficient.
If the existing audited cache already contains the necessary underlying GLEIF artifact, promote/reference it through the existing contract without provider re-query.
If a required durable artifact genuinely cannot be reconstructed from the audited retained material, stop and report that exact gap rather than silently rerunning or fabricating evidence.
Existing identity rules remain absolute:
- only VERIFIED + EXACT may qualify for V1 graph participation
- AMBIGUOUS cannot auto-promote
- NOT_FOUND cannot auto-promote
- provider identifier ambiguity cannot attach an entity to an arbitrary Client Record
6. Stylus authentication
Do not implement or use:
- browser JWT extraction
- copying browser tokens
- local token files
- token capture scripts
- persisted session credentials
- hidden curl/HTTP workarounds
Stylus must be used only through its supported interactive authentication/login flow.
Token expiry is an operational condition, not an architecture change.
If authentication currently requires the human operator to login through the Stylus UI, prepare the handoff and stop at that boundary.
7. Stylus execution scope
After the corrections above pass tests, determine exactly which frozen Stage 7:
entity × family × source-class
cells remain outstanding for:
- SEC_FILING
- R2D2_WEB
Use the existing frozen request matrix. Do not manufacture a new scope.
Produce a concise operator handoff showing only the outstanding Stylus jobs.
For every job provide exactly:
- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- ResearchInstruction
- AsOfDate
- required output filename
Use the existing Web + SEC Stylus preset. Do not label it Web + SEC + GLEIF.
Do not send EPA.
If the previous seven-job handoff contains jobs or source channels that no longer match the frozen source matrix, regenerate the handoff from the authoritative frozen scope rather than blindly retaining that list.
8. Stylus output is NOT evidence
Enforce this during ingestion.
Stylus output may contain:
- candidate findings
- source references
- excerpts
- retrieval metadata
But Stylus itself must never appear as the evidence source.
Before any claim can be accepted, retain/verify the actual underlying source artifact:
- SEC filing for SEC_FILING
- approved Web document/page for R2D2_WEB
- GLEIF registry artifact for GLEIF
Then preserve the existing lineage:
Document → Passage → Atomic Claim → Relationship → Relationship Version → Support → Qualifier
Exact passage/reference is mandatory.
No synthetic passage.
No model-generated excerpt treated as source text.
No claim whose only provenance is a Stylus JSON/session.
9. Resume semantics
Stage 7 remains the same controlled run, not a new pilot.
Completed provider scope should remain completed.
Resume only outstanding source-class work.
Make execution idempotent:
- no duplicate documents
- no duplicate passages
- no duplicate claims
- no duplicate relationships
- no duplicate relationship versions
- no duplicate qualifiers/support records
Existing accepted factual graph must remain unchanged unless new evidence passes all normal gates.
10. Correlation evaluation
Only after newly accepted factual relationships have been ingested, rerun the existing six query-time correlation definitions:
- SHARED_CONTROLLER
- SHARED_SUPPLIER
- SHARED_CUSTOMER
- SUPPLY_CHAIN
- SHARED_LENDER
- SHARED_PRODUCT_DEPENDENCY
Do not persist derived correlations.
Do not modify their definitions.
Do not exceed two hops.
Zero non-zero correlations remains a valid Stage 7 result.
Do not create facts or weaken gates to produce a correlation.
11. Tests required before any live Stylus handoff
Add focused tests covering at least:
1. all required sources COMPLETE + no result → RESEARCHED_NONE_FOUND
2. all required sources COMPLETE + accepted result → RESEARCHED_FOUND
3. GLEIF COMPLETE + SEC NOT_ATTEMPTED → PARTIAL
4. GLEIF COMPLETE + Web UNAVAILABLE → PARTIAL
5. zero providers attempted → NOT_RESEARCHED
6. fully ineligible entity/family → NOT_ELIGIBLE
7. IDENTITY_UNRESOLVED appears only as a reason, never top-level
8. ambiguous GLEIF result cannot create VERIFIED+EXACT link
9. Stylus session/output cannot serve as accepted evidence artifact
10. EPA rolls up to NOT_ELIGIBLE
11. frozen selection fingerprint remains unchanged
12. completed GLEIF source cells are not unnecessarily re-executed
13. pairwise/direct factual projection still excludes candidate/context/rejected material
14. six correlation definitions remain unchanged and query-time only
Run the relevant focused tests and full existing backend suite.
Do not change the frontend.
12. STOP POINT
After implementation/tests:
Do not attempt to automate the Stylus browser session.
Stop and report:
1. files changed
2. exact coverage-model correction
3. evidence that the frozen Stage 7 fingerprint is unchanged
4. GLEIF retained-artifact validation result
5. exact outstanding SEC/Web jobs
6. whether supported Stylus interactive login is ready
7. tests passed
8. any blockers
Then give me the first outstanding Stylus job only, with its six runtime inputs and expected filename, so I can execute it manually.
Do not start Stage 8.
