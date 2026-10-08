ORACLE CONTROLLED CAM EXTRACTION EXPERIMENT — IMPLEMENT AND EXECUTE

Objective

The current CCR production workflow has been completed, validated and committed. Preserve that working implementation.

Now implement and execute a controlled Oracle Corporation CAM relationship extraction experiment, comparing three approaches:

* A — Existing CCR indexed extraction pipeline
* B — Colleague-style MapReduce LLM pipeline
* C — Hybrid indexed retrieval + MapReduce + independent Opus review

This is an evidence-quality and extraction-completeness experiment, not a frontend redesign or a general repository audit.

Do not execute this prompt while another Luna task has uncommitted changes. First confirm the previous task has finished and the working baseline is preserved.

Repositories and reference material

Primary CCR project:

C:\Users\ak54743\Downloads\Param\CCR Correlation

Colleague’s implementation, READ ONLY:

C:\Users\ak54743\Downloads\phr-tool-main (1)\phr-tool-main

Relevant colleague implementation:

* phr-backend/src/phr_backend/services/orchestrator.py
* phr-backend/src/phr_backend/services/agents/cam_distiller.py
* phr-backend/src/phr_backend/services/agents/subportfolio.py
* phr-backend/src/phr_backend/services/agents/portfolio.py
* phr-backend/src/phr_backend/services/analysis_config_loader.py
* phr-backend/templates/indirect_exposure.yaml
* Implemented maker/checker prompts and output schemas

Colleague audit package:

C:\Users\ak54743\Downloads\CoreAI_Audit_2026-10-08

Historical report for comparison only:

C:\Users\ak54743\Downloads\Param\CCR Correlation\output\reports\CoreAI_relationship_report_20260928.html

IMPORTANT: The historical report’s source-producing job and document-level provenance were not established by the earlier audit. Its 12 Oracle relationship records are unverified reference candidates, NOT a validated truth set. Do not copy them into production or treat their count as an acceptance target.

Phase 1 — Establish Oracle source coverage

Use Oracle Corporation’s exact canonical entity identity, CAGID 1005020529, subject to confirmation against the current canonical master.

Discover all CAM documents in the existing indexed corpus that actually contain evidence about Oracle, including CAMs whose primary subject is another client.

Use the existing:

* cam_documents
* cam_passages
* cam_entity_mentions
* Canonical entity master
* DuckDB/Parquet query infrastructure

Report:

1. Total indexed CAM documents.
2. Oracle-related documents.
3. Oracle-related passages.
4. Direct legal-name matches.
5. Identifier matches.
6. Alias matches.
7. Ambiguous matches.
8. Relevant PDF parsing failures/timeouts.
9. Documents excluded and why.

Do not assume that Oracle Corporation and ORACLE GLOBAL SERVICES ROMANIA SRL are the same legal entity.

Preserve exact legal identity, canonical IDs and parent/subsidiary mappings separately.

Also preserve external relationship counterparties outside the ten-company cohort when correctly resolved.

If the source corpus does not support a meaningful comparison, report the limitation before performing expensive LLM calls.

Phase 2 — Implement three independent approaches

Pipeline A — Existing CCR baseline

Run the currently implemented indexed CAM extraction and verification pipeline.

Do not alter its extraction logic to improve its results during this experiment.

Persist:

* Retrieved source passages.
* Raw maker outputs.
* Candidate relationships.
* Semantic validation decisions.
* Deterministic validation decisions.
* Accepted relationships.
* Review-required relationships.
* Rejected findings with reasons.

Pipeline B — Colleague-style MapReduce

Reproduce the useful processing structure from the colleague’s implementation inside a new, isolated CCR experimental module.

Architecture:

CAM documents/chunks
→ Parallel MAP relationship distillation
→ Intermediate semantic checker
→ REDUCE cross-document consolidation
→ Final semantic checker
→ Deterministic validation
→ Structured relationship records

Adopt the proven design concepts, not the colleague’s unverified historical relationship dataset.

The MAP prompt must require:

* Named subject and related legal entity.
* Directional relationship.
* Explicit relationship category.
* Exact CAM excerpt.
* Source document and passage/page reference.
* Identifiers when explicitly available.
* A relationship assertion supported by the excerpt.

The checker must reject unsupported or speculative edges.

Do not count co-mentions, general industry exposure, financial discussion or proximity as physical relationships.

The REDUCE process must preserve distinct relationships and all supporting citations rather than merging everything by entity pair.

Pipeline C — Hybrid

Use CCR’s indexed retrieval to identify Oracle-relevant evidence first.

Then:

Indexed retrieval
→ Context-aware MAP extraction
→ Semantic checker
→ REDUCE / consolidation
→ Independent Claude Opus refinement
→ Existing deterministic checker
→ Canonical identity reconciliation
→ Final evidence-backed graph records

Opus must independently review evidence and verify:

* Entity A and B identities.
* Relationship direction.
* Relationship taxonomy.
* Whether the excerpt actually asserts the relationship.
* Whether the source is primary or indirect.
* Whether aliases or subsidiaries were improperly merged.
* Whether a relationship is duplicated or contradicted elsewhere.

Opus may correct or reject proposals. It must not invent source excerpts, IDs or relationships.

Use approved existing enterprise model routes and the CCR virtual environment. Do not introduce public consumer API access or a dependency on the colleague’s runtime.

Phase 3 — Common verification contract

All three pipelines must be evaluated against the same verification policy.

A relationship can be VERIFIED only if:

1. Its source document is identifiable.
2. The exact excerpt can be found in the underlying source.
3. The relevant source location is retained.
4. Both endpoints are resolved to appropriate canonical entities, or a clearly governed external-entity policy permits the target.
5. Direction and relationship category are supported.
6. Semantic validation passes.
7. Deterministic validation passes.

Anything unresolved must remain REVIEW_REQUIRED or REJECTED.

Preserve these distinctions:

* Physical direct relationship
* Verified multi-hop indirect relationship
* Candidate hidden dependency
* Unverified relationship proposal
* Purely topological proximity

A multi-hop path is not a new direct physical relationship.

Never create a verified relationship from a candidate hidden dependency without source evidence for the underlying edges.

Never promote a relationship only because a confidence label says HIGH or VERY_HIGH.

Do not write any of the three experimental outputs into existing verified production tables.

Phase 4 — Controlled comparative execution

Execute all three pipelines for Oracle.

Use the same underlying CAM corpus and record source coverage differences explicitly.

Keep model configurations, evaluation criteria and resource budgets comparable. If different models or context budgets are needed, disclose them in the comparison.

Record separately:

* Retrieval time.
* MAP time.
* Checker time.
* REDUCE time.
* Total elapsed time.
* Model calls and token usage, where available.
* Approximate relative execution cost.

Do not permit one experiment’s results to seed another.

SEC and web enrichment should remain out of the primary CAM-only comparison. They may be used afterward in a clearly separated corroboration exercise, not to compensate silently for missing CAM evidence.

Phase 5 — Oracle comparison report

Generate one comparison table:

Metric	A: Indexed	B: MapReduce	C: Hybrid
Relevant documents			
Processed passages			
Raw candidates			
Verified distinct relationships			
Review required			
Rejected			
Unique supporting citations			
Identity ambiguities			
Duplicate proposals			
Unsupported relationship proposals			
Runtime			
Model usage/cost			

Also produce a relationship-level comparison with:

* Oracle legal entity.
* Related entity.
* Relationship type/direction.
* Pipeline(s) finding the relationship.
* Exact citation reference.
* Verification outcome.
* Reason for disagreement between pipelines.

Calculate overlap and unique contribution:

* Verified relationships common to all three.
* Verified only by A.
* Verified only by B.
* Verified only by C.
* Verified by two methods but absent from the third.

Manually inspect a bounded, representative set of accepted, rejected and disputed relationship records against the actual CAM source. Do not use LLM agreement as an independent accuracy measure.

Classify additional findings as genuine discoveries, duplicates, ambiguous identities or false positives.

Compare the historical colleague Oracle records only as an unverified candidate coverage checklist. Explain which can be reproduced from actual available CAM evidence and which cannot.

Do not artificially maximize the relationship count.

Phase 6 — Decision and recommendation

Provide Luna’s independent technical assessment:

1. Which architecture produces the best verified relationship coverage?
2. Which produces fewer false positives?
3. Which most reliably preserves provenance?
4. Which handles cross-document evidence best?
5. Which creates the most unresolved entity ambiguity?
6. What is the latency and model cost trade-off?
7. Is the hybrid objectively better enough to justify adopting it?
8. Should MapReduce become a fallback only for difficult CAMs?
9. Which implementation should be used for the remaining nine companies?

Provide a proposed final production architecture, but do not activate it across the other nine companies yet.

Deliverables

Persist experimental artifacts under a clearly identified new CCR experiment directory, including:

* Oracle source coverage manifest.
* Three raw extraction outputs.
* Three checker decision sets.
* Three verified relationship datasets.
* Rejected/review datasets.
* Comparison CSV/JSON.
* Evidence audit report.
* Model execution statistics.
* Final architecture recommendation.

Add focused tests and run relevant existing regression tests.

Do not modify the colleague’s repository, canonical master, production verified relationships, or established frontend design.

Do not mark the experiment successful without actually running it and producing measurable results.

Final status must be one of:

* ORACLE_COMPARISON_COMPLETE
* BLOCKED_BY_SOURCE_COVERAGE
* BLOCKED_BY_MODEL_RUNTIME
* BLOCKED_BY_VERIFICATION
* PARTIAL_COMPARISON

Finish with a clear recommendation based on the observed evidence, not assumptions.

Execute the experiment now, after confirming that no other Luna task is still modifying the baseline.