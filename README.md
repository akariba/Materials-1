CCR V1 — STAGE 7.1 COVERAGE CORRECTION + CONTROLLED SEC RESUME
You are the implementation agent.
Stage 7 has already executed once and stopped correctly with:
- run status PARTIAL_PROVIDER_SCOPE
- frozen 8-entity pilot manifest
- no new accepted relationships
- no manufactured correlations
- SEC research not executed because SEC operational configuration was absent
- GLEIF executed
- Web not executed
Senior review has now authorized a narrow Stage 7 continuation only.
DO NOT START STAGE 8.
1. Immutable Stage 7 pilot boundary
Resume the exact same frozen selection manifest and fingerprint.
Do NOT:
- add entities;
- remove entities;
- substitute entities;
- change the selection rationale;
- change the ontology;
- change identity gates;
- change relationship acceptance gates;
- change evidence-basis rules;
- change the six correlation definitions;
- change two-hop maximum depth;
- enable recursive traversal;
- perform fuzzy identity matching;
- manufacture or synthesize relationship edges;
- weaken VERIFIED + EXACT;
- weaken ACCEPTED relationship-version requirements;
- redesign the UI;
- implement AI Analyst;
- implement AI Create Correlation;
- begin Stage 8.
Frozen population remains:
- ROOT_3M
- KNOWN_3M_INDIA
- KNOWN_SOLVENTUM
- KNOWN_CABOT
- UNRESOLVED_AEARO
- UNRESOLVED_3M_BELGIUM
- UNRESOLVED_BNY_TRUSTEE
- UNRESOLVED_EPA
PART A — Coverage semantic correction
Before any SEC network request, audit the current Stage 7 coverage implementation.
Coverage must be evaluated at least at:
entity × relationship_family × required_source_scope × as_of_date × policy_version
Do not use the run-level PARTIAL_PROVIDER_SCOPE as a substitute for these records.
Implement the following explicit three-way rule.
A1. PROVIDER_SPECIFIC_NO_FINDING
One source class was successfully queried and returned no qualifying finding.
This alone must NOT imply:
RESEARCHED_NONE_FOUND
for the relationship family.
A2. RESEARCHED_NONE_FOUND
This is permitted only when:
- every source class required for that entity + family under the governed source policy was actually attempted;
- each required source returned a valid response, including explicit empty results;
- no qualifying accepted claim was found;
- no required source is unavailable, blocked, skipped, or unexecuted.
A3. PARTIAL
Must be emitted if at least one required source class:
- could not be queried;
- lacked required operational configuration;
- failed because of provider outage;
- was otherwise unavailable.
A successful negative result from one source must never compensate for another required source that never ran.
PART B — Audit the current 3M India coverage state
Current Stage 7 reporting has:
KNOWN_3M_INDIA = RESEARCHED_NONE_FOUND / CURRENT
while other entities were PARTIAL because SEC did not execute.
Do not simply relabel it.
Determine from the actual governed source-scope configuration:
1. Which source classes are required for each ACTIVE relationship family for 3M India?
2. Is SEC actually required, optional, or not applicable?
3. Is Web required, optional, or not applicable?
4. Was the complete governed required-source set actually executed?
If GLEIF alone legitimately satisfies a specific family’s required source scope, preserve the complete result.
If SEC was required but unexecuted, correct the family coverage outcome to PARTIAL.
Report the decision family by family, not as an undocumented global label.
Add regression tests for this exact distinction.
PART C — SEC configuration must be operational-only
Configure the required SEC EDGAR request identity/contact mechanism using environment/configuration appropriate to the existing provider implementation.
Do not hardcode personal credentials or secrets into source files.
Before changing the operational SEC configuration, capture:
- frozen selection-manifest hash;
- pilot input fingerprint;
- ontology/config fingerprint;
- correlation-definition catalogue fingerprint;
- acceptance-policy fingerprint if available;
- relationship database schema/version;
- existing accepted relationship count;
- existing correlation-definition count.
After the configuration change, capture them again.
Assert mechanically that all semantic fingerprints are byte-identical.
The SEC operational configuration must not change:
- pilot population;
- selection manifest;
- source-policy semantics;
- ontology;
- identity gates;
- relationship gates;
- correlation catalogue;
- correlation depth.
If any semantic fingerprint changes unexpectedly:
STOP. DO NOT RUN RESEARCH.
PART D — EPA ontology-fit disposition
Do not silently delete EPA from the frozen selection.
Determine whether any currently ACTIVE V1 relationship type could legitimately have EPA as an endpoint.
Current ACTIVE types are exactly:
- owns
- controls
- lends_to
- provides_credit_support
- supplies
- depends_on_products_of
Do not add a regulatory relationship type.
If EPA cannot participate in an ACTIVE V1 relationship under the frozen ontology:
- preserve EPA in the frozen pilot manifest;
- classify the applicable research family/scope as NOT_ELIGIBLE or the already-governed equivalent;
- give an explicit governed reason such as OUTSIDE_ACTIVE_ONTOLOGY_SCOPE;
- do not treat GLEIF NOT_FOUND as the decisive reason;
- do not attempt to manufacture an entity identity merely to keep EPA in the graph.
Report the exact disposition.
PART E — Resume the SAME Stage 7 pilot
Only after Parts A–D pass, resume the same Stage 7 pilot.
Use the existing persisted manifest and run identity/resume mechanism.
Do not create a replacement pilot run merely to bypass the previous partial result.
The intended evidence pipeline remains:
source document
→
stored document snapshot/reference
→
exact passage
→
atomic claim
→
endpoint identity resolution
→
relationship acceptance
→
relationship version
→
qualifier
→
query-time correlation evaluation
No model-generated text may itself become evidence.
PART F — Provider sequence
F1. SEC
Run SEC as the next primary relationship-research source.
Use the existing provider/evidence infrastructure.
Research must remain document-centric.
Do not perform client-pair answer-shopping.
Extract only explicit claims supported by actual retained source passages.
F2. GLEIF
Continue using GLEIF primarily for legal-entity identity resolution and registered-entity evidence.
Do not interpret:
- NOT_FOUND
- ambiguous name search
- multiple candidates
as negative relationship evidence.
Do not auto-promote ambiguous candidates.
F3. Web
Keep Web disabled initially.
After SEC completes, identify explicit named unresolved evidence or identity gaps.
Only then may approved Web/official sources be used, and only for those named gaps.
Do not enable broad Web crawling simply because the provider is available.
PART G — Specific unresolved endpoint handling
Aearo
GLEIF NOT_FOUND is not final.
Attempt resolution through authoritative SEC/official-document exact legal-name evidence.
3M Belgium
Preserve AMBIGUOUS until exact legal-entity evidence distinguishes the entity.
BNY trustee
Preserve ambiguity unless a filing identifies the precise registered trustee entity.
Also distinguish trustee/facility context from an actual V1 relationship endpoint.
Do not create a financing relationship solely from an administrative/trustee role.
EPA
Follow Part D ontology-fit rules.
PART H — Relationship acceptance remains frozen
A factual graph edge may enter CCR V1 only when all existing gates pass.
At minimum:
- endpoint identity is eligible under frozen policy;
- required identity state/type passes;
- source evidence is admissible;
- atomic claim is explicit;
- relationship type is one of the frozen ontology types;
- direction is explicit and valid;
- relationship version reaches ACCEPTED;
- relationship support/evidence lineage exists.
No candidate/context-only/rejected observation becomes factual simply because it helps produce a correlation.
PART I — Correlation behavior
Do not change the correlation engine.
Preserve exactly the current six definitions:
- SHARED_CONTROLLER
- SHARED_SUPPLIER
- SHARED_CUSTOMER
- SUPPLY_CHAIN
- SHARED_LENDER
- SHARED_PRODUCT_DEPENDENCY
Correlations remain:
- query-time;
- derived from accepted factual relationships;
- maximum two relationship hops;
- non-persisted as derived-result rows;
- evidence/identity gated.
Evaluate all six again after enrichment.
Zero results are acceptable.
A positive correlation must arise naturally from accepted graph facts.
PART J — Stage 7 completion criterion
Stage 7 is NOT complete merely because SEC successfully runs.
Declare Stage 7 complete only when every applicable:
selected entity × ACTIVE relationship family
has reached a governed terminal research outcome such as:
- RESEARCHED_FOUND
- valid RESEARCHED_NONE_FOUND
- NOT_ELIGIBLE
- or another explicitly governed terminal state justified by the frozen policy.
No applicable entity/family pair may remain PARTIAL because a required provider was not executed.
Also require:
- every identity attempt has an explicit final state;
- all accepted claims have evidence lineage;
- replay/idempotence passes;
- no fuzzy merges;
- no synthetic factual relationships;
- no ambiguous candidate auto-promotion;
- no manufactured correlations;
- all six definitions evaluated after the final graph state.
A non-zero correlation is NOT required for Stage 7 success.
PART K — Required validation/report
Create:
backend/data/CCR_V1_STAGE_7_1_SEC_RESUME_REPORT.md
and an updated machine-readable run manifest if the current architecture uses one.
Report:
1. pre/post semantic fingerprints;
2. proof pilot selection remained frozen;
3. SEC operational configuration status without exposing sensitive values;
4. per-entity × family required-source scope;
5. corrected coverage outcomes;
6. 3M India coverage determination and rationale;
7. EPA ontology-fit disposition;
8. provider attempts by source;
9. retrieved source documents;
10. retained passages;
11. atomic claims;
12. endpoint identity decisions;
13. accepted relationship versions;
14. qualifiers;
15. candidate/context/rejected observations;
16. coverage state by entity/family;
17. before/after factual relationship counts;
18. before/after six correlation-definition results;
19. exact relationship hops for every non-zero correlation, if any;
20. replay/idempotence;
21. SQLite integrity;
22. Client Universe unchanged;
23. source master unchanged;
24. external calls performed;
25. remaining limitations;
26. explicit Stage 7 completion decision.
Run all relevant backend regression tests.
Do not modify the frontend.
STOP CONDITION
Stop after Stage 7.1/resumed Stage 7 validation.
Do not start Stage 8.
End with exactly one of:
STAGE 7 COMPLETE — READY FOR SENIOR REVIEW
or
STAGE 7 STILL PARTIAL — SENIOR REVIEW REQUIRED
Explain precisely why.
