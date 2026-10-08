# CCR Relationship Intelligence — Execute 10-Company Hybrid CAM Pilot and Assess Results

## Objective

Execute the hybrid CAM extraction approach for the existing ten-company production cohort.

Combine our established CAM evidence index with the MapReduce-style LLM extraction architecture, followed by semantic checking, Opus refinement where appropriate, deterministic verification and graph analytics.

**This is an execution and validation task, not another general audit or architecture proposal.**

We want measurable results for each company individually, a consolidated comparison, and your independent technical opinion about whether the hybrid approach is better than our previous implementation.

## 1. Scope — exactly 10 production clients

Use the existing canonical production cohort:

1. NVIDIA Corporation
2. Oracle Corporation
3. Intel Corporation
4. Microsoft Corporation
5. Amazon.com Inc.
6. Alphabet Inc.
7. CoreWeave Inc.
8. Taiwan Semiconductor Manufacturing Company
9. OpenAI OpCo LLC
10. Hut 8 Corporation

Resolve each against the current canonical entity universe.

Preserve exact legal-entity identities. Do not merge parent companies, subsidiaries or affiliated entities simply because they share a corporate family.

Process only these ten as seed companies. Related external entities may be discovered, resolved and retained as counterparties.

Use actual production CAM documents, indexed evidence and existing production relationship records. No demo or fabricated data.

## 2. Establish baseline before execution

For every company capture the current state:

- Existing verified direct relationships.
- Existing review-required candidates.
- Existing indirect paths.
- Existing hidden relationship candidates.
- Unique related companies.
- Source document coverage.
- Entity-resolution status.
- Existing evidence quality.

Record this baseline before running additional extraction.

Do not modify historical verified records or overwrite the canonical production relationship artifact.

## 3. Execute the hybrid extraction

Use:

CAM INDEX → RETRIEVE → MAP → SEMANTIC CHECK → REDUCE → OPUS REFINEMENT → DETERMINISTIC VALIDATION → VERIFIED GRAPH.

### Stage A — Indexed retrieval

For each company:

- Retrieve all relevant indexed CAM documents and passages.
- Identify applicable company aliases and identifiers.
- Expand into surrounding sections when necessary.
- Preserve source document, passage, page and section references.
- Include relevant third-party CAM evidence that mentions the seed company.
- Reuse existing parsed documents and avoid unnecessary reindexing.

### Stage B — MapReduce relationship extraction

Use the MapReduce-style techniques studied in the CoreAI project, but implement them within our existing CCR architecture.

Process relevant CAM sections in bounded parallel batches.

Extract all genuinely supported relationships, including:

- Parent/subsidiary and ownership.
- Strategic partnership.
- Equity investment.
- Lending, financing and guarantees.
- Customer and supplier.
- Cloud infrastructure and compute dependencies.
- Joint ventures and contractual arrangements.
- Material technology and operational dependencies.
- Other approved canonical relationship types.

Require exact evidence for every candidate.

Do not treat simple company co-mentions as relationships.

### Stage C — Semantic checker and Opus refinement

Apply the existing maker/checker architecture.

Use the approved R2D2 gateway and Opus where available.

Verify:

- Correct subject and related entity.
- Canonical identity.
- Relationship semantics.
- Direction.
- Exact source evidence.
- Relationship taxonomy.
- Economic relevance.

Categorize each result as ACCEPT, CORRECT, REJECT or NEEDS_REVIEW.

If Opus or another model stage fails, record the failure explicitly rather than claiming successful validation.

### Stage D — Deterministic validation

Enforce mandatory checks before VERIFIED status:

- Exact source provenance.
- Canonical IDs.
- Valid excerpt.
- Direction.
- Valid taxonomy.
- No unsupported assertions.
- No false entity merges.
- Independent checker outcome.
- Preserved source lineage.

Unknown relationship types must not silently become `advisor`.

Review-required records cannot be promoted automatically.

### Stage E — Reduce and graph analytics

Deduplicate equivalent claims without losing evidence or legitimate parallel relationship types.

Calculate indirect paths only from eligible verified underlying edges.

Keep path provenance, intermediate entities, hop counts and edge IDs.

Do not manufacture indirect or hidden relationships to populate the frontend.

## 4. Generate separate statistics for EACH company

Create one complete report per company.

Use the following consistent structure:

### COMPANY: [Legal entity name]

**A. Evidence coverage**

- Canonical CAGID:
- Number of CAM documents searched:
- Number of documents containing relevant evidence:
- Number of passages retrieved:
- Number of MapReduce chunks processed:
- Source coverage limitations:

**B. Relationship extraction**

- Existing verified direct relationships:
- New raw candidates:
- Candidates accepted by semantic checker:
- Candidates corrected:
- Candidates rejected:
- Candidates needing review:
- Candidates passing deterministic verification:
- Newly verified direct relationships:
- Total unique verified direct relationships:
- Unique verified counterparties:
- Duplicate claims merged:
- Unsupported or unresolved entity references:

**C. Relationship breakdown**

Provide counts by canonical relationship type, such as investor, customer, supplier, strategic partner, lender, guarantor, parent, subsidiary and contractual dependency.

Show the source entity, target entity, direction, type and evidence reference for each newly verified relationship.

**D. Indirect and hidden dependencies**

- Verified indirect paths:
- New indirect paths compared with baseline:
- Maximum verified hop distance:
- Significant shared counterparties:
- Hidden relationship hypotheses:
- Evidence-verified hidden relationships:
- Review-required hidden candidates:

Explain every material indirect path through its underlying verified edges.

**E. Financial and credit-risk significance**

Where the actual evidence permits, identify:

- Citi exposure or facility references.
- TFA and committed amounts.
- Material contractual amounts.
- Ownership percentages.
- Significant financial dependencies.
- Potential credit concentrations.
- Possible contagion pathways.

Do not invent missing amounts or derive Citi exposure from external contracts.

**F. Performance**

- Runtime:
- Number of LLM calls:
- Input/output tokens:
- Estimated cost:
- Cache hits:
- Errors or retries:
- Verification success rate:

**G. Individual assessment**

Provide your technical interpretation:

1. Did the hybrid approach discover meaningful new relationships?
2. What did indexed-only extraction miss?
3. What did MapReduce recover?
4. Were the discoveries economically significant or mostly low-value associations?
5. What evidence gaps remain?
6. Is this company sufficiently covered for the pilot?
7. What precise improvement should be made next?

Give a per-company rating: STRONG / MODERATE / WEAK / INSUFFICIENT EVIDENCE, based on measured extraction quality and evidence coverage, not the company's creditworthiness.

## 5. Produce a consolidated comparison table

Generate the following table using actual execution statistics.

| Company | Baseline verified direct | New verified direct | Total verified direct | Verified indirect paths | Review required | Rejected | Runtime | Quality assessment |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| NVIDIA | | | | | | | | |
| Oracle | | | | | | | | |
| Intel | | | | | | | | |
| Microsoft | | | | | | | | |
| Amazon | | | | | | | | |
| Alphabet | | | | | | | | |
| CoreWeave | | | | | | | | |
| TSMC | | | | | | | | |
| OpenAI | | | | | | | | |
| Hut 8 | | | | | | | | |
| TOTAL | | | | | | | | |

Ensure count definitions are consistent.

Separate unique business relationships from evidence rows, duplicated mentions, physical records and graph-derived paths.

Do not double-count relationships discovered from both endpoints of the ten-company cohort.

## 6. Evaluate the hybrid approach against the previous pipeline

Compare:

**Previous indexed extraction**

Versus

**New index + MapReduce + checker/refinement pipeline**

Measure:

- Additional verified relationship discoveries.
- Coverage improvements.
- Unsupported candidate rate.
- Entity-resolution quality.
- New meaningful indirect dependencies.
- Changes in source traceability.
- Runtime and cost.
- Reliability and reproducibility.

A higher raw candidate count alone is not an improvement.

Explain whether additional verified discoveries justify the increased processing complexity and cost.

If the hybrid finds few new verified relationships, investigate whether the limitation is retrieval, relationship extraction, canonical entity resolution, evidence verification or simply absence of evidence.

Do not loosen validation to manufacture a better result.

## 7. Luna — give your independent technical opinion

After completing execution, provide your own evidence-based assessment as the implementation engineer.

Answer these questions directly:

**1. Which approach is better?**

- Existing CAM index extraction alone?
- Document-level MapReduce alone?
- Hybrid index + MapReduce?

Explain why, based on the ten-company execution.

**2. Is our relationship database becoming genuinely useful for counterparty credit risk?**

Assess whether the results support meaningful financial, contractual, ownership and infrastructure dependency analysis.

**3. Are we missing important relationships?**

Identify the most likely remaining gaps and whether they arise from missing CAM evidence, extraction quality, identity resolution, missing SEC/web corroboration or validation rules.

**4. Is our indirect-risk methodology defensible?**

Evaluate verified direct-edge coverage, typed paths, hop limits, economic materiality and the distinction between true dependencies and graph proximity.

**5. Is Opus refinement adding measurable value?**

Identify corrected relationships, rejected hallucinations, verified incremental discoveries and additional cost.

**6. Should we scale beyond ten companies?**

Give a clear GO / CONDITIONAL GO / NO GO recommendation with supporting evidence.

**7. What are the five highest-impact next improvements?**

Rank them by expected impact on verified relationship discovery, analytical usefulness and implementation effort.

Do not provide a favorable recommendation just because the implementation completed successfully.

## 8. Implementation and execution safeguards

- Preserve existing production data and relationship source of truth.
- Keep the ten-company production view in DuckDB.
- Write new outputs to additive, versioned artifacts.
- Maintain separate verified, review-required and rejected records.
- No fake companies, financial values, exposures or relationships.
- No project-wide reconstruction.
- No dependency on the CoreAI/PHR runtime.
- No frontend redesign during this task.
- Bound API concurrency, retries and execution duration.
- Capture partial results safely if a model or source fails.
- Do not claim full completion when companies remain unprocessed.
- Run focused acceptance tests and full regression tests.

## 9. Deliverables

Produce:

1. `hybrid_cam_10_company_summary.md` — executive summary and your final opinion.
2. `hybrid_cam_10_company_statistics.csv` — comparable statistics, one row per company.
3. `hybrid_cam_relationships.parquet` — newly extracted relationship records with provenance and verification status.
4. `hybrid_cam_indirect_paths.parquet` — verified-edge-only derived paths.
5. `hybrid_cam_exceptions.md` — unresolved identities, missing evidence, rejected claims and runtime issues.
6. `hybrid_cam_execution_manifest.json` — exact source hashes, model versions, prompts, timestamps, token consumption and pipeline status.

Use stable paths and avoid duplicating existing relationship stores.

## 10. Final response format

End your execution report with:

- TEN_COMPANIES_PROCESSED: X/10
- BASELINE_VERIFIED_DIRECT:
- NEW_VERIFIED_DIRECT:
- TOTAL_UNIQUE_VERIFIED_DIRECT:
- VERIFIED_INDIRECT_PATHS:
- REVIEW_REQUIRED:
- REJECTED:
- OPUS_REFINEMENT_STATUS:
- TOTAL_RUNTIME:
- ESTIMATED_LLM_COST:
- TEST_RESULTS:
- HYBRID_VS_PREVIOUS: BETTER / COMPARABLE / WORSE / INCONCLUSIVE
- LUNA_RECOMMENDATION: GO / CONDITIONAL_GO / NO_GO

**Execute the ten-company experiment now, produce the individual statistics, and give your independent judgment. Do not stop after another architecture review.**


## Reference Project — CoreAI / PHR MapReduce Pipeline

The colleague's project is located at:

**Project root:**
`C:\Users\ak54743\Downloads\phr-tool-main (1)\phr-tool-main`

**Backend:**
`C:\Users\ak54743\Downloads\phr-tool-main (1)\phr-tool-main\phr-backend`

**Frontend:**
`C:\Users\ak54743\Downloads\phr-tool-main (1)\phr-tool-main\phr-frontend`

Inspect the existing backend implementation, particularly:

- `phr-backend/src/phr_backend/services/orchestrator.py`
- `phr-backend/src/phr_backend/services/agents/cam_distiller.py`
- `phr-backend/src/phr_backend/services/agents/subportfolio.py`
- `phr-backend/src/phr_backend/services/agents/portfolio.py`
- `phr-backend/src/phr_backend/services/agents/base.py`
- `phr-backend/src/phr_backend/templates/indirect_exposure.yaml`
- `phr-backend/src/phr_backend/templates/checkers/`

Identify and reuse the applicable **CAM MapReduce extraction, prompts, batching, maker/checker, aggregation and evidence-preservation techniques**.

Integrate the useful techniques into our existing CCR Relationship Intelligence implementation, using our current CAM index, DuckDB/Parquet, canonical entity universe, R2D2 and Opus.

**Important constraints:**

1. Treat the colleague's project as a read-only reference.
2. Do not modify its files or execute its full pipeline.
3. Do not import its runtime as a dependency.
4. Do not copy its report data into our production relationship database.
5. Adapt its proven extraction techniques and prompts to our stricter canonical-identity and evidence-verification requirements.
6. Execute and compare the hybrid approach for our existing ten production clients.
7. Produce individual statistics and your independent technical recommendation.
