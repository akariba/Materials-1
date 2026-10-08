IMPLEMENTATION DIRECTIVE — BUILD THE COMPLETE STYLUS CCR PROJECT FOR 500 CLIENTS

1. YOUR ASSIGNMENT

You are the principal Python software engineer, database architect, credit-risk analytics specialist, LLM/MapReduce engineer, and frontend developer responsible for delivering CoreAI — CCR Relationship Intelligence.

I have already prepared my project folder and the core 500-client dataset.

I need you to generate a complete, executable, self-contained project, including every source-code file, configuration, prompt, checker, database module, API, test, startup script, and HTML visualization required to operate it.

This is NOT a request for another blueprint, architecture analysis, or implementation proposal.

Generate actual working source code as downloadable files and folders.

The final workflow must be:

500 combined clients → canonical identity resolution → CAM document ingestion → indexed retrieval → evidence-grounded MapReduce → independent semantic checker → deterministic checker → relationship reconciliation → R2D2/Opus refinement → SEC/approved web enrichment → financial/exposure validation → verified graph → indirect relationship analytics → interactive CoreAI HTML report with relationship map, portfolio analytics and geographic risk heatmap.

⸻

2. EXACT PROJECT DIRECTORY

The definitive project location is:

C:\Users\ak54743\Downloads\Stylus CCR

The existing input directory is:

C:\Users\ak54743\Downloads\Stylus CCR\raw

DO NOT create another project called ccr-relationship-intelligence in a different folder.

DO NOT create a second nested project inside Stylus CCR.

All generated files must belong to the Stylus CCR root.

This folder currently contains a raw directory holding the prepared input datasets.

The raw directory is user-owned. Treat its contents as immutable.

Do not rename, move, overwrite, truncate or delete anything inside raw.

Primary 500-client dataset

raw/500 CCR CLIENTS - COMBINED.parquet

This is the primary dataset for the 500-client portfolio.

I prepared it by combining client population, company identifiers and CCR data/exposures.

Do not recombine these original inputs unnecessarily if the combined Parquet already contains the required information.

Additional available datasets

The screenshot shows:

* raw/500 CCR CLIENTS.parquet
* raw/500 CCR CLIENTS - CCR DATA.parquet
* raw/500 CCR CLIENTS - IDENTIFIERS.parquet
* raw/500 CCR CLIENTS - MISSING IDENTIFIERS.parquet
* raw/ccr_data.parquet
* raw/Customer_latest.parquet
* raw/client_info.csv
* CAGID lookup JSON files.
* CAGID spreadsheets.
* Other reference/source folders including CLM, CRMPS, RESCU, CLFU and a dated OneDrive folder, where present.

Inspect the real filenames and schemas rather than assuming the list is exhaustive.

These additional files are primarily for validation, missing-identifier resolution and reference enrichment.

Do not assume that every folder contains CAMs. Classify its contents first.

Critical first step

Implement a reproducible read-only input audit that reports:

1. Actual number of portfolio clients.
2. Actual number of Parquet rows.
3. Distinct CAGIDs and GFCIDs.
4. Identifier completeness.
5. Duplicate clients.
6. Exposure fields.
7. Currency and units.
8. Sector classifications.
9. Country-of-risk availability.
10. CAM documents discovered by folder and format.

The expected population is 500 clients, but the validated dataset determines the actual number.

Do not fabricate successful reconciliation counts.

⸻

3. TARGET PROJECT FOLDER STRUCTURE

Generate the following complete structure directly beneath Stylus CCR.

Preserve existing Batch 1 source artifacts that were already generated in this conversation. Reconcile existing filenames and interfaces instead of duplicating incompatible modules.

Stylus CCR/
│
├── raw/                         # EXISTING - NEVER MODIFY
│
├── input/
│   └── cams/                    # New CAM documents can be copied here
│
├── config/
│   ├── app_config.yaml
│   ├── input_sources.yaml
│   ├── cohort_config.yaml
│   ├── model_routing.yaml
│   ├── relationship_taxonomy.yaml
│   ├── verification_policy.yaml
│   ├── financial_rules.yaml
│   └── source_policy.yaml
│
├── src/
│   ├── __init__.py
│   ├── main.py
│   ├── config_loader.py
│   │
│   ├── ingestion/
│   │   ├── scanner.py
│   │   ├── manifest.py
│   │   ├── pdf_parser.py
│   │   ├── docx_parser.py
│   │   ├── text_parser.py
│   │   ├── spreadsheet_parser.py
│   │   └── passage_segmenter.py
│   │
│   ├── cohort/
│   │   ├── parquet_loader.py
│   │   ├── schema_validator.py
│   │   ├── client_reconciler.py
│   │   └── cohort_statistics.py
│   │
│   ├── canonicalization/
│   │   ├── reference_loader.py
│   │   ├── identity_resolver.py
│   │   ├── alias_matcher.py
│   │   └── canonical_validator.py
│   │
│   ├── indexing/
│   │   ├── passage_store.py
│   │   ├── bm25_index.py
│   │   ├── entity_mention_index.py
│   │   └── retriever.py
│   │
│   ├── extraction/
│   │   ├── schemas.py
│   │   ├── map_extractor.py
│   │   ├── semantic_checker.py
│   │   ├── deterministic_checker.py
│   │   ├── reduce_aggregator.py
│   │   ├── verification_policy.py
│   │   └── pipeline.py
│   │
│   ├── llm/
│   │   ├── r2d2_client.py
│   │   ├── model_router.py
│   │   ├── opus_refiner.py
│   │   ├── prompt_registry.py
│   │   └── usage_tracker.py
│   │
│   ├── prompts/
│   │   ├── map_relationships.md
│   │   ├── semantic_checker.md
│   │   ├── reduce_relationships.md
│   │   ├── opus_refinement.md
│   │   ├── sec_fact_extraction.md
│   │   └── portfolio_summary.md
│   │
│   ├── enrichment/
│   │   ├── sec_client.py
│   │   ├── approved_web_client.py
│   │   ├── external_entity_matcher.py
│   │   ├── evidence_reconciler.py
│   │   ├── financial_enrichment.py
│   │   └── ratings_enrichment.py
│   │
│   ├── financials/
│   │   ├── source_fact_validator.py
│   │   ├── currency_validator.py
│   │   ├── exposure_aggregator.py
│   │   └── financial_ratios.py
│   │
│   ├── graph/
│   │   ├── graph_builder.py
│   │   ├── graph_paths.py
│   │   ├── graph_similarity.py
│   │   ├── hidden_candidates.py
│   │   └── community_detection.py
│   │
│   ├── analytics/
│   │   ├── portfolio_analytics.py
│   │   ├── concentration_analytics.py
│   │   ├── geographic_analytics.py
│   │   ├── sector_analytics.py
│   │   └── heatmap_engine.py
│   │
│   ├── storage/
│   │   ├── parquet_repository.py
│   │   ├── duckdb_views.py
│   │   ├── schema_registry.py
│   │   └── audit_log.py
│   │
│   ├── reporting/
│   │   ├── report_builder.py
│   │   ├── report_data.py
│   │   ├── html_renderer.py
│   │   ├── excel_export.py
│   │   └── csv_export.py
│   │
│   ├── api/
│   │   ├── server.py
│   │   ├── schemas.py
│   │   ├── entities.py
│   │   ├── relationships.py
│   │   ├── graph.py
│   │   ├── portfolio.py
│   │   ├── enrichment.py
│   │   └── jobs.py
│   │
│   └── jobs/
│       ├── job_registry.py
│       └── pipeline_runner.py
│
├── frontend/
│   ├── index.html
│   ├── css/
│   │   └── coreai.css
│   ├── js/
│   │   ├── application.js
│   │   ├── graph.js
│   │   ├── selection.js
│   │   ├── relationship_table.js
│   │   ├── geographic_heatmap.js
│   │   ├── portfolio.js
│   │   └── dossier.js
│   └── assets/
│       └── world_countries.geojson
│
├── data/
│   ├── processed/
│   ├── indexes/
│   └── manifests/
│
├── output/
│   ├── extraction/
│   ├── verification/
│   ├── enrichment/
│   ├── graph/
│   ├── analytics/
│   ├── reports/
│   └── logs/
│
├── scripts/
│   ├── audit_inputs.py
│   ├── rebuild_index.py
│   ├── run_extraction.py
│   ├── run_enrichment.py
│   ├── validate_results.py
│   ├── generate_report.py
│   ├── setup.ps1
│   ├── start.ps1
│   ├── run_all.ps1
│   └── setup.sh
│
├── skills/
│   ├── ingest_cams.md
│   ├── mapreduce_extraction.md
│   ├── resolve_entities.md
│   ├── check_relationships.md
│   ├── enrich_relationships.md
│   ├── generate_coreai_report.md
│   └── troubleshoot.md
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── .env.example
├── .gitignore
├── pyproject.toml
├── requirements.txt
├── README.md
├── ARCHITECTURE.md
├── DATA_DICTIONARY.md
└── IMPLEMENTATION_MANIFEST.md

This structure is the functional target, not permission to generate empty placeholder files. Each implemented file must contain its real assigned logic.

If a module has already been correctly implemented in Batch 1 under a different location, reuse it and document the corresponding actual path.

⸻

4. 500-CLIENT COHORT PROCESSING

The source population must come from:

raw/500 CCR CLIENTS - COMBINED.parquet

The combined dataset already joins much of the required information. Avoid rebuilding that source if unnecessary.

Create a normalized cohort containing source-backed fields such as:

* Client display name.
* Canonical legal name.
* CAGID.
* GFCID.
* LEI.
* CIK.
* ISIN.
* CUSIP.
* Bloomberg ticker.
* Sector.
* Country of risk.
* Country of domicile.
* Currency.
* TFA Limit.
* TFA OSUC.
* Other available exposure measures.
* Available internal risk ratings.
* Source row reference.
* Data as-of date.

These are target concepts, not an assertion that every column exists in the current Parquet.

Missing values must be marked unavailable.

Do not automatically manufacture identifiers, exposures or ratings.

Create deterministic identifier reconciliation using the supporting Parquet files, customer master, client_info.csv, and existing validated canonicalization rules.

Never merge companies merely because their names resemble each other.

The resulting population must remain traceable to its original source records.

⸻

5. CAM INGESTION

The project must support a corpus of CAM documents associated with the 500 clients and other relevant parties.

The user may copy new CAMs into:

input/cams/

The initial existing source folders under raw/ must be inventoried and classified before being configured as additional read-only CAM roots.

Supported files:

* PDF.
* DOCX.
* TXT.
* CSV.
* XLSX, where it contains relevant source data.

Each document must have:

* Stable document ID.
* File path.
* SHA-256 hash.
* Source classification.
* Parse status.
* Extraction status.
* Page or section metadata.
* Parsed text.
* Passage records.
* Parser warnings.

Process each CAM once per source version.

Do not send every CAM to an LLM every time the application starts.

PDF parsing must be bounded with explicit timeout and failure handling.

For documents that cannot be extracted safely, report the failure rather than pretending ingestion succeeded.

⸻

6. INDEXED CAM SEARCH — THE FOUNDATION

Before running MapReduce, build a reusable CAM search index.

Use the architecture already proven in the existing CCR project:

CAM documents → normalized passages → entity mentions → lexical index → entity-centric retrieval

Implement BM25 or a comparable deterministic lexical search approach.

Index:

* Full and normalized entity names.
* CAGID/GFCID when present.
* LEI/CIK and other validated identifiers.
* Relevant counterparties.
* CAM section names.
* Deal/project names.
* Source passage identifiers.

For each of the 500 clients, retrieve directly relevant passages and bounded supporting context.

Do not run a separate full-corpus MapReduce scan 500 times.

Use document and passage caching.

A passage relevant to several clients should be extracted only once for the same source/prompt/model version, then its resulting physical relationships should be linked to all relevant clients.

This is essential for processing 500 clients efficiently.

⸻

7. HYBRID MAPREDUCE EXTRACTION ENGINE

Implement the complete evidence-based extraction architecture.

Stage 1 — MAP

For each selected CAM passage, the maker model extracts:

* Entity A.
* Entity B.
* Source aliases and identifiers.
* Relationship type.
* Direction.
* Relationship roles.
* Deal or contract.
* Deal/commitment amount, when stated.
* Original amount currency.
* Date.
* Exact evidence excerpt.
* Document ID.
* Page and section.
* Passage ID.
* Confidence with explanation.

The MAP output must be strict JSON validated through Pydantic.

Map outputs may contain candidates; candidates are not automatically verified.

Stage 1.5 — Independent semantic checker

Use a logically separate model pass.

Check the maker’s output against the exact original source passage.

Classify:

* ACCEPT.
* CORRECT.
* REJECT.
* NEEDS_REVIEW.

Verify whether the claimed relationship truly follows from the source.

Reject co-mentions or merely inferred commercial relationships.

Check relationship direction, financial amounts and entity ambiguity.

Stage 1.75 — Deterministic checker

Perform actual Python validation:

* Exact excerpt verification.
* Source document existence.
* Passage existence.
* Page/section provenance.
* Taxonomy membership.
* Valid endpoints.
* Resolved or ambiguous entity identity.
* No unsupported amounts.
* No contradictory direction.
* No false self-relationships.
* Duplicate policy.
* Evidence and schema compliance.

Stage 2 — REDUCE

Aggregate validated candidates across passages and CAM documents.

Preserve separate physical relationship records.

Never deduplicate solely by unordered entity pair.

For example, the same two companies may simultaneously have an investment relationship, contractual relationship and strategic partnership.

These are separate economic facts.

Stage 2.5 — Portfolio checker

Run independent aggregation checks.

Validate:

* Unique physical relationship IDs.
* Source provenance.
* Relationship counts.
* Canonical entity counts.
* Parallel relationship records.
* Verified versus review-required partitions.
* Evidence completeness.
* Financial amount semantics.
* Cohort coverage.

Stage 3 — Portfolio-wide REDUCE/MERGE

Generate:

* Company-to-company relationships.
* Shared counterparties.
* Cross-client dependencies.
* Project-financing structures.
* Common investors.
* Common lenders.
* Customer/tenant concentrations.
* Sponsor concentrations.
* Sector dependencies.

Preserve all source evidence and verification states.

Stage 4 — Opus refinement

Use R2D2 and approved Claude Opus for complex ambiguous cases.

Opus can:

* Correct relationship classifications.
* Resolve complex deal structures using available evidence.
* Propose canonical identity corrections.
* Suggest missing supporting passages.
* Investigate parent/subsidiary distinctions.
* Refine risk explanations.
* Identify unverified indirect dependency hypotheses.

Opus must NOT invent evidence or directly override deterministic verification.

Its outputs must re-enter identity and source validation.

Stage 5 — Final verification

Only qualifying relationships enter the verified graph.

Maintain independent stores for:

VERIFIED

REVIEW_REQUIRED

REJECTED

CANDIDATE

UNVERIFIABLE_SOURCE

ERROR

Physical source records must be preserved regardless of graph eligibility.

⸻

8. RELATIONSHIP TAXONOMY

Reuse the business semantics from the PHR CoreAI relationship reports and available PHR implementation.

Reference project:

C:\Users\ak54743\Downloads\ccrig-master (3)\ccrig-credit-workbench\phr-tool-main

Relevant historical report:

C:\Users\ak54743\Downloads\Param\CCR Correlation\output\reports\CoreAI_relationship_report_20260928.html

Use those as read-only functional references wherever accessible.

At minimum, the application should support validated categories for:

* Lender.
* Borrower.
* Guarantor.
* Parent.
* Subsidiary.
* Investor.
* Investee.
* Sponsor.
* Tenant.
* Landlord.
* Customer.
* Supplier.
* Contracted customer.
* Offtaker.
* Joint venture.
* Strategic partnership.
* Infrastructure dependency.
* Advisor.
* Other explicitly sourced relationships.

Ensure canonical relationship types preserve direction.

Do not convert every unmapped relationship into advisor.

An unknown type must be review-required until it can be mapped safely.

⸻

9. R2D2 AND APPROVED ENRICHMENT

Integrate approved enterprise AI and research providers.

The project must be self-contained and must not depend on an unrelated RPR installation or virtual environment.

LLM roles

Recommended model-routing pattern:

* Approved fast model: extraction.
* Approved Sonnet model: semantic checking.
* Approved Opus model: complex refinement.
* Deterministic Python: identity, evidence checks, numeric calculations and graph eligibility.

Read actual model identifiers from configuration.

Implement:

* Timeouts.
* Retries.
* Rate limits.
* Token budgeting.
* Model usage reporting.
* Incremental checkpoints.
* Cancellation.
* Idempotency.
* No automatic rerun on browser refresh.

External enrichment sequence

CAM first, SEC second, approved web third.

For each eligible client or candidate:

1. Identify the company using resolved identifiers.
2. Query available approved SEC evidence when relevant.
3. Retrieve grounded public financial/relationship information through the approved enterprise search provider.
4. Compare external evidence with CAM claims.
5. Preserve all three source layers independently.
6. Record contradictions.
7. Revalidate candidate identity.
8. Update enrichment and verification status where policy permits.

If no grounded external citations are available, return an explicit error such as:

BLOCKED_BY_GROUNDING

Do not turn an ungrounded search answer into verified evidence.

Do not send internal CAM content to unapproved public services.

⸻

10. FINANCIAL AND EXPOSURE ENRICHMENT

This is a credit-risk application.

Preserve and display the actual financial data already available in the 500-client combined Parquet dataset.

In addition, extract validated financial facts from CAM and approved SEC sources.

Target metrics, where supported:

* TFA Limit.
* TFA OSUC.
* Outstanding exposure.
* Citi direct exposure.
* Quantifiable Citi indirect exposure.
* Deal/commitment value.
* Revenue.
* EBITDA.
* Total debt.
* Cash.
* Net debt.
* Net leverage.
* Interest coverage.
* Liquidity.
* Debt maturities.
* External credit ratings.
* CAM ORR/RRR/FORR.

Every populated metric must carry:

* Source.
* Original currency.
* Display currency.
* Units.
* Reporting period.
* Calculation method.
* Data as-of date.
* Evidence reference.
* Validation status.

Never repeat the previous currency bug where USD values were presented as MAD.

Use strict field-level validation.

Do not treat entity-level exposure, relationship-level deal value and indirect look-through exposure as interchangeable.

Never turn missing exposure into $0.

Indirect exposure must remain non-quantifiable unless an approved calculation can be reproduced from actual source data.

⸻

11. DUCKDB + PARQUET DATABASE

DuckDB is the query engine.

Parquet is the persistent analytical storage.

Do not introduce a second unrelated database.

Create source-backed datasets for:

* Cohort clients.
* Canonical identities.
* Source documents.
* CAM passages.
* Entity mentions.
* MAP candidates.
* Semantic decisions.
* Deterministic decisions.
* Physical relationships.
* Verified relationships.
* Review-required relationships.
* Evidence citations.
* External enrichment.
* Financial facts.
* Exposure measures.
* Graph edges.
* Indirect paths.
* Portfolio analytics.
* Geographic risks.
* Pipeline runs.
* Job execution and audit logs.

Provide typed schemas, primary/stable identifiers and joins.

All generated outputs must include source/run versions or enough lineage to reconstruct their origin.

A later extraction run must not silently overwrite historical evidence without an auditable replacement record.

⸻

12. VERIFIED RELATIONSHIP NETWORK MAP

Create an interactive relationship network map for the 500-client population and their resolved external counterparties.

The map must NOT render all relationships as one unreadable cluster.

Use:

* Clear circular or compact nodes.
* Readable labels.
* Controlled spacing.
* Radial and hierarchical layouts.
* Grouping by source client, sector or community.
* Smooth zoom and pan.
* Click-to-expand.
* Collapse branches.
* Reset view.
* Fit-to-view.
* Search.
* Node highlighting.
* Edge highlighting.
* Lazy loading for larger neighborhoods.
* A practical limit on simultaneously rendered nodes.

Relationship display rules

Solid edges = verified relationships.

Dashed edges = review-only candidate relationships, if explicitly enabled as an overlay.

Do not include review-only edges in confirmed indirect-path calculations.

Synchronized interaction

Selecting a client in the client table must update:

* Graph.
* Credit Risk Intelligence panel.
* Physical relationship database.
* Financial data.
* Verified relationship summary.
* Available indirect paths.

Clicking a graph node must produce the same selection behavior.

Clicking a relationship row must highlight the relevant graph edge and reveal its exact source evidence.

The data must come from one shared selection state.

⸻

13. GEOGRAPHIC RISK HEATMAP

Create a separate Geographic Risk Heatmap section.

Use bundled country geometry so the report remains functional without external CDNs.

Required outputs:

* Country of risk.
* Client count by country.
* Available TFA OSUC by country.
* Available TFA Limit by country.
* Concentration share.
* Verified counterparty relationships.
* Country coverage/missing-data statistics.

Support coloring by a user-selected, source-backed metric.

If actual country risk, default signals or stress measurements are unavailable, display:

NOT AVAILABLE

or:

NOT CALCULABLE

Do not substitute imaginary risk scores.

Also create a sector concentration heatmap with sectors and clients or sector-to-sector verified dependency counts.

Each heatmap tile or country must be inspectable and must disclose its underlying source clients and aggregation formula.

Distinguish an exposure heatmap from a modeled stress heatmap.

⸻

14. COMPLETE COREAI HTML REPORT

The final application must generate this report automatically:

output/reports/CoreAI_500_Client_Relationship_Intelligence.html

The HTML must open as a standalone interactive report without depending on a running cloud service or external JavaScript CDN.

Embed or bundle all essential data, CSS, JavaScript and geographic assets appropriately. The exported report should work offline, including when opened directly as a local HTML file.

The frontend may also be served through FastAPI for live interaction and manually triggered updates.

Main page sections

A. Executive dashboard

Show:

* Portfolio clients.
* Canonical entity coverage.
* Total unique external counterparties.
* Physical relationship records.
* Verified relationships.
* Review-required candidates.
* Verified indirect paths.
* Number of CAMs processed.
* Source coverage.
* Available exposure totals.

Every KPI must have a clear definition.

B. Select entities

Use the PHR-style table with:

* Name.
* CAGID.
* TFA Limit.
* TFA OSUC.
* Indirect Exposure UTD/SI.
* RRR.
* Relationship count.

Restore exact available column semantics.

Include search and filters.

C. Relationship network map

An interactive, readable map with direct, indirect and review overlays.

D. Credit Risk Intelligence

A large right-side panel with:

* Rating.
* Financials.
* Identity.
* Relationships.
* Distance.
* Grounded investigation.

Make this panel wide enough to display financial information comfortably.

E. Physical relationship database

Preserve every physical record.

Columns must include:

* Company A.
* Company B.
* Relationship type.
* Relationship perspective.
* Deal/commitment.
* Citi indirect exposure.
* Source.
* Evidence excerpt.
* Confidence.
* Evidence status.
* Verification status.

Support CSV and XLSX export.

F. Portfolio analytics

Provide source-backed concentration and relationship analysis.

G. Geographic risk heatmap

Display country-level portfolio coverage, exposure or verified stress data.

H. Sector concentration heatmap

Show cross-sector concentration or dependency patterns.

I. Methodology and definitions

Explain graph paths, Jaccard, source evidence, financial units, TFA, indirect exposure and verification rules.

⸻

15. PERFORMANCE AND COST CONTROL

This project covers 500 clients. Avoid an architecture that becomes prohibitively slow or expensive.

Required optimizations:

1. Parse each document once per version.
2. Cache passage indexing.
3. Retrieve relevant passages before making LLM calls.
4. Cache extraction by document, passage, prompt and model version.
5. Deduplicate repeated MAP work.
6. Use bounded batching and configurable concurrency.
7. Check source hashes on every run.
8. Reprocess only changed sources or changed extraction policies.
9. Use cheaper approved models for straightforward extraction.
10. Reserve Opus for ambiguous or high-value cases.
11. Perform graph analytics deterministically.
12. Generate reports from existing validated Parquet outputs.
13. Use paginated API queries.
14. Render bounded graph neighborhoods instead of thousands of nodes simultaneously.

Include an execution-cost report recording document count, model calls, token usage where available, retry count, elapsed time and model-specific cost only when actual pricing is configured.

⸻

16. AUTOMATION AND STARTUP

I want a straightforward Windows experience.

Create:

setup.ps1

start.ps1

run_all.ps1

Also provide corresponding Python CLI commands.

After configuration, the expected startup flow should be:

cd "C:\Users\ak54743\Downloads\Stylus CCR"
.\scripts\setup.ps1
.\scripts\run_all.ps1
.\scripts\start.ps1

setup.ps1:

* Creates the project virtual environment.
* Installs required Python packages.
* Validates key dependencies.
* Validates configuration.
* Checks existing inputs.

run_all.ps1:

* Performs input validation.
* Builds the cohort.
* Scans configured CAM sources.
* Parses new documents.
* Rebuilds affected indexes.
* Runs the MapReduce pipeline where approved credentials are configured.
* Applies checkers.
* Builds the verified graph.
* Performs explicitly enabled enrichment.
* Calculates supported analytics.
* Generates the HTML report.
* Produces a detailed run summary.

The script must make expensive LLM/external operations explicit before execution, including a configurable dry-run mode. It must not silently incur large costs merely because it was started.

start.ps1:

* Launches the local FastAPI application.
* Serves the interactive UI.
* Prints the local address.
* Reports missing prerequisites clearly.

The application must not depend on the PHR project, RPR virtual environment or a particular VS Code conversation.

⸻

17. VALIDATION REQUIREMENTS

Create real executable tests.

Dataset tests

* Primary Parquet can be read.
* Cohort count is reconciled.
* CAGID/GFCID semantics are preserved.
* Duplicate clients are identified.
* Currency fields are not silently transformed.
* Missing source values remain missing.

Extraction tests

* MAP candidates follow schema.
* Source excerpts are retrievable.
* Semantic checker rejects unsupported relationships.
* Deterministic checker catches incorrect citations.
* Parallel physical records are retained.
* No unsupported entity merges occur.
* Review-only records cannot enter verified topology.

Financial tests

* Original currency is retained.
* Amount units are validated.
* Missing metrics are not zero-filled.
* Different exposure measures are not incorrectly added.
* Financial ratios use consistent periods.

Graph tests

* Verified edges use valid relationship IDs.
* Indirect paths contain only verified edges.
* Hop distance and Jaccard are reproducible.
* No graph candidate is presented as a verified contract.

Frontend tests

* 500-client search.
* Client selection.
* Graph expansion.
* Relationship row selection.
* Dossier synchronization.
* Geographic heatmap availability.
* Exported HTML functionality.
* CSV/XLSX export.
* Missing-data display.
* Error and timeout handling.

Generate a final validation report with actual test results only where execution was genuinely performed.

⸻

18. IMPLEMENTATION STRATEGY

Generate the project in complete functional batches.

Batch A — Foundation

Deliver the complete runnable scaffold, configuration, 500-client Parquet loader, input auditor, entity validation, DuckDB/Parquet storage and initial tests.

Reuse the existing Stylus Batch 1 where compatible.

Batch B — CAM indexing and MapReduce

Deliver the complete ingestion, indexing, retrieval, MAP, semantic checker, deterministic checker, REDUCE, identity reconciliation and final verification code.

Batch C — R2D2/Opus and enrichment

Deliver the complete model adapters, Opus refinement, SEC/approved web integration, evidence reconciliation and financial validation code.

Batch D — Graph and portfolio analytics

Deliver verified graphs, indirect paths, sector/country concentration, exposure aggregation and geographic analytics.

Batch E — Full CoreAI frontend

Deliver HTML, CSS, JavaScript, relationship map, heatmaps, entity tables, dossiers, filters and exports.

Batch F — End-to-end integration

Deliver Windows scripts, local FastAPI service, integration tests, documentation, skills and final project package.

Every batch must have usable code artifacts and a manifest explaining their dependencies.

Do not replace source files with large design narratives.

⸻

19. SOURCE-BASED PILOT VERIFICATION

Before attempting the entire 500-client run, the code must support a controlled pilot.

Use a few companies actually found in the combined source, such as Oracle, NVIDIA, Intel, Hut 8 or other confirmed source entries.

Do not assume any example has a dedicated CAM.

For each pilot company, report:

* Source client record.
* Canonical match status.
* CAM passages retrieved.
* MAP candidate count.
* Semantic checker outcomes.
* Deterministic validation results.
* Verified relationships.
* Review-required results.
* SEC/web enrichment results.
* Graph nodes and edges.
* Financial coverage.
* Missing-data explanations.

After verifying the workflow, make the same pipeline capable of processing the full source cohort through incremental batches.

Do not fabricate a successful pilot if the models or documents are unavailable.

⸻

20. REQUIRED FINAL DELIVERABLES

I expect:

Deliverable 1: Complete Stylus CCR project folder structure.

Deliverable 2: Actual Python source code for all implemented processing modules.

Deliverable 3: Full MapReduce extraction engine and verification pipeline.

Deliverable 4: Working enterprise R2D2/Opus integration with approved-model configuration.

Deliverable 5: SEC and approved web enrichment adapters.

Deliverable 6: Reproducible DuckDB/Parquet database schemas and views.

Deliverable 7: Complete graph and portfolio analytics logic.

Deliverable 8: Interactive CoreAI HTML report with readable relationship graph and geographic/sector heatmaps.

Deliverable 9: Windows startup and execution scripts.

Deliverable 10: Tests, implementation manifest, instructions and reusable agent skills.

Deliverable 11: A project package preserving the entire required directory hierarchy, preferably a ZIP if artifact packaging is supported.

Deliverable 12: A precise distinction between code generated, code actually executed, validated functionality and environment-dependent components that remain untested.

When the actual data are not available to your execution environment, write robust code that reads the documented files at runtime and generates the report from real outputs. Do not create fabricated 500-client results.

⸻

21. START NOW — IMPORTANT

The master project folder is:

C:\Users\ak54743\Downloads\Stylus CCR

The authoritative client input is:

raw/500 CCR CLIENTS - COMBINED.parquet

The existing raw directory must remain unchanged.

Your first priority is to reconcile the already-generated Batch 1 artifacts with this exact project location and then generate the full remaining codebase.

Do not start by creating another blueprint.

Do not recreate an unrelated project folder.

Do not provide pseudocode instead of real files.

Do not claim deployment or tests without actual execution.

If you cannot modify the user’s local directory directly, generate complete downloadable artifacts retaining the exact relative project paths, so I can place them in Stylus CCR or hand them to my VS Code coding agent.

Start generating the actual project files immediately, continue through all batches, and preserve compatible source-code interfaces throughout.

The final objective is simple: I provide the 500-client Parquet dataset and CAMs, configure approved enterprise services, run the pipeline, and receive a functioning evidence-grounded CoreAI relationship intelligence application and interactive HTML report.