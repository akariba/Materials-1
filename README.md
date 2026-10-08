CCR Relationship Intelligence — 10-Company DuckDB Production View and Fast Frontend

OBJECTIVE

Consolidate the implementation around only 10 selected companies.

Do not analyze, enrich, calculate graph paths for, or display the entire production entity universe.

Create a dedicated, optimized DuckDB analytical layer restricted to the 10-company cohort, and make the existing production frontend use that layer exclusively.

This is a focused production implementation, not a demonstration.

1. Fixed company cohort

Use the following 10 priority organizations:

1. NVIDIA
2. Oracle
3. OpenAI
4. Microsoft
5. Amazon
6. Alphabet
7. CoreWeave
8. Intel
9. Hut 8
10. TSMC

Resolve each organization to its appropriate canonical legal entity using the existing production entity master.

Store validated CAGIDs and available other identifiers in one cohort configuration.

Do not fabricate legal entities, identifiers or Citi client status. Flag unresolved companies for review instead of silently substituting another company.

2. Create dedicated DuckDB views

Reuse the current DuckDB-over-Parquet architecture.

Implement these logical views, adapting their names and schemas to existing code where appropriate:

* v_cohort_entities — the selected canonical entities.
* v_cohort_relationships — physical relationship records between cohort entities.
* v_cohort_verified_edges — fully evidence-verified direct graph edges.
* v_cohort_indirect_paths — graph-derived paths within the cohort.
* v_cohort_candidates — hidden and review-required candidate records.
* v_cohort_facts — CAM and validated external facts attributed to cohort entities.
* v_cohort_exposures — sourced Citi EXP, TFA and facility data.
* v_cohort_evidence — citations and provenance for cohort records.

Use existing data models and verification rules.

Strict cohort boundary: both graph endpoints and every intermediate path entity must belong to the 10-company cohort. External company mentions may remain in source evidence, but they must not create additional analytical nodes or trigger enrichment outside the cohort.

If this restriction prevents indirect paths from being formed, show zero valid paths rather than manufacturing connections.

Do not overwrite full-universe Parquet data or create a new persistent production database.

3. Optimize performance

DuckDB views alone are not sufficient if every request must rescan millions of rows.

Implement an efficient bounded preparation process:

1. Resolve the cohort CAGIDs once.
2. Filter the existing production Parquet inputs.
3. Reuse source pushdown and efficient DuckDB joins.
4. Persist compact, refreshable cohort Parquet snapshots where appropriate.
5. Create DuckDB views over the compact cohort data.
6. Precompute eligible relationship graphs and indirect paths.
7. Cache expensive deterministic aggregations.
8. Refresh the cohort only through an explicit controlled operation.

Keep one authoritative source of truth; cohort snapshots are rebuildable derived artifacts.

Do not execute R2D2, Opus or large CAM searches during ordinary frontend page loading.

4. Switch the frontend exclusively to the cohort

The production frontend at http://127.0.0.1:8000/ must default to the 10-company cohort.

All four pages must use the same active cohort.

Correlation

Display only the 10 primary companies.

* No long list of millions of entities.
* No automatic insertion of secondary companies.
* Real verified direct relationships.
* Real graph-derived indirect paths.
* Hidden candidates shown separately.
* Real graph selection and evidence drill-down.

Relationship Records

Load only records eligible for the cohort.

Keep all valid relationship types between each selected pair.

Provide filtering, searching, fullscreen expansion and fast table navigation.

Credit Risk Intelligence

When a user clicks a company, immediately populate its available:

* Ratings
* Financials
* Identity
* Ownership/hierarchy
* Relationships
* Exposure information
* Graph distances
* Evidence/provenance

Stress Analytics, Portfolio Analytics and Risk Heatmap

Calculate and display information only for the active cohort.

No default queries over millions of entities.

5. Fast data loading and interaction

Target the following performance after warmup on the current workstation:

Action	Performance target
Initial frontend load	Under 2 seconds
Fetch 10 entities	Under 200 ms
Fetch cohort relationships	Under 500 ms
Select company and populate dossier	Under 500 ms
Switch dossier tabs	Under 200 ms
Graph filter or selection	Under 300 ms
Open relationship evidence	Under 500 ms

These are engineering targets, not assumed results. Measure actual latency and report any missed targets.

Use bounded payloads, efficient API responses, server-side filtering and cached deterministic data where appropriate.

Do not reinitialize the full graph or reload unrelated panels when a user changes one company selection.

6. Preserve accuracy

All information must come from production CAM, canonical entity records, validated external sources or explicitly identified deterministic calculations.

Preserve:

* FACT
* DERIVED
* EXPOSURE
* AI_CANDIDATE
* REVIEW_REQUIRED
* VERIFIED

Do not display review-required relationships as verified.

Do not invent exposure amounts, credit ratings, relationship strengths or missing financials.

Use existing taxonomy, scoring and validation modules.

7. Complete controlled enrichment

For these 10 companies only:

* Use existing CAM evidence.
* Identify missing facts and relationships.
* Run targeted R2D2 retrieval when explicitly invoked.
* Run Claude Opus refinement when explicitly invoked.
* Validate any new findings.
* Update cohort snapshots.
* Refresh the frontend views.

Do not schedule research for the full canonical universe or automatically rerun investigations on browser refresh.

8. Acceptance tests

Verify:

* Exactly 10 configured primary companies.
* All resolvable entries use actual canonical identities.
* DuckDB views return only eligible cohort entities and edges.
* No full-universe query runs on ordinary frontend page loading.
* No extra graph nodes appear outside the cohort.
* No unsupported path contributes to verified indirect results.
* Relationship Records matches the cohort data.
* Clicking each company updates the dossier.
* All frontend pages use the same cohort.
* Data and evidence remain accurate.
* Full production Parquet artifacts remain unchanged.
* Existing tests pass.
* Application restart preserves the cohort configuration.
* Page refresh does not trigger enrichment.
* Measured response times are reported.

9. Final delivery

Report:

COHORT COMPANIES: 10

CANONICAL ENTITIES RESOLVED:

DUCKDB COHORT VIEWS:

COHORT RELATIONSHIP RECORDS:

VERIFIED DIRECT:

VERIFIED INDIRECT:

HIDDEN / REVIEW REQUIRED:

CAM FACTS:

CITI EXP / TFA COVERAGE:

INITIAL PAGE LOAD TIME:

COMPANY SELECTION LATENCY:

RELATIONSHIP API LATENCY:

DOSSIER POPULATION LATENCY:

GRAPH PERFORMANCE:

TEST RESULTS:

PRODUCTION URL:

COMMIT HASH:

REMAINING BLOCKERS:

Implement the bounded DuckDB views, switch the existing frontend to them, optimize interactions, and deliver a working 10-company production application. Do not restart architectural audits or scale beyond the cohort.