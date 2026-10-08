CCR Relationship Intelligence — Full Production Implementation

EXECUTION DIRECTIVE

Continue implementation in the existing CCR Correlation / CCR Relationship Intelligence project.

Implement the application now. Do not restart discovery, historical audits, architectural reviews or repository cleanup.

The objective is to transform the existing partially integrated CCR application into a functional, evidence-driven Counterparty Relationship Intelligence and Risk Analytics Platform.

Work on the existing codebase. Reuse validated modules, preserve working functionality, and avoid introducing duplicate implementations.

Complete the implementation in controlled phases, run actual tests, fix issues and deliver a working application.

⸻

1. PRESERVE THE EXISTING ARCHITECTURE

The current project already contains substantial working functionality.

Reuse:

* FastAPI production backend
* Canonical entity universe
* CAM parsing and evidence index
* Parquet analytical artifacts
* DuckDB analytical/query layer
* Production relationship repository
* Existing NVIDIA backend integration
* Relationship taxonomy and scoring
* Entity reconciliation
* Typed graph-path calculations
* Direct-source evidence validation
* Approved R2D2 integration
* Claude model integration
* Existing frontend structure
* Existing tests

Do not create a separate application.

Do not introduce production SQLite.

Do not restore obsolete CCRIG or RPR runtime dependencies.

Do not reconstruct the historical monolithic pipeline.

Do not use the five-company client demonstration as the production database.

Before modifications, create a safe Git checkpoint preserving current work.

2. ACTIVATE THE REAL PRODUCTION APPLICATION

The actual CCR production application must become the default execution path.

Implement:

1. Production FastAPI startup.
2. Production frontend served over HTTP.
3. Canonical entity search.
4. Production relationship retrieval.
5. Entity-specific intelligence retrieval.
6. Real graph topology loading.
7. Relationship evidence retrieval.
8. Backend-driven analytics.

Use existing endpoints where possible.

Existing NVIDIA functionality exposed through /api/nvidia/backend should be connected to the appropriate production views without creating a competing entity model.

The production application must support any available canonical company, not just NVIDIA.

Use server-side search, pagination and bounded graph expansion rather than sending the entire entity universe to the browser.

Keep the five-company client demonstration isolated as a historical rollback/testing reference.

Do not silently serve demonstration data if the production API is unavailable.

3. USE ONE CANONICAL DATA FLOW

Maintain:

CAM and approved external sources
→ deterministic extraction
→ canonical entity resolution
→ relationship candidates
→ evidence retrieval
→ AI refinement
→ deterministic validation
→ persistent Parquet artifacts
→ DuckDB analytical views
→ FastAPI
→ frontend.

Use the current production artifacts rather than creating another source of truth.

The current relationship model already includes direct and indirect records, evidence/provenance fields, and source metadata.

Preserve parallel relationships between identical counterparties.

For instance, strategic partnership and equity investment must remain separate records even when they connect the same entities.

Do not replace the broader production relationship universe with a bounded NVIDIA-only snapshot.

4. CAM FACTS AND CITI EXPOSURE

Use the existing repaired CAM index and any newly indexed, eligible source documents.

Extract actual disclosed information where available:

Entity information

* CAGID
* GFCID
* LEI
* CIK
* ISIN/CUSIP
* Legal name
* Parent and subsidiary
* Ultimate parent
* Country of risk
* Industry and sector

Internal credit information

* RLR
* FORR
* Citi EXP
* TFA
* Facility limits and amounts
* Lending exposure
* Maturity
* Guarantors
* Collateral
* Other available credit metrics

Financial information

* Revenue
* EBITDA
* Total debt
* Cash
* Leverage
* Liquidity
* Financial covenant information

Relationship information

* Ownership
* Investment
* Supplier/customer
* Financing
* Strategic partnership
* Joint venture
* Guarantee
* Lease/offtake
* Commercial dependency
* Shared infrastructure
* SPV arrangements
* Material contracts

Every extracted field must preserve its original source, subject entity, page/section, exact supporting excerpt, value, unit and date where available.

Do not attribute exposure belonging to another CAM subject to NVIDIA merely because NVIDIA is mentioned in the document.

Citi EXP and TFA must never be estimated by an LLM.

If a value is unavailable, identify whether the reason is genuinely missing source data, incomplete extraction, ambiguous entity attribution or failed mapping.

5. RELATIONSHIP CLASSIFICATION

Implement one consistent representation for:

DIRECT

An explicit, evidence-backed relationship between two canonical entities.

Examples:

* Parent/subsidiary
* Ownership
* Equity investment
* Supplier/customer
* Guarantor/borrower
* Lender/borrower
* Strategic partnership
* Joint venture
* Lessor/lessee
* Offtaker/provider
* Infrastructure dependency

Each direct relationship must preserve direction, relationship type, canonical endpoints and supporting evidence.

INDIRECT

A deterministically derived path through two or more verified direct edges.

For example:

NVIDIA → Entity A → Entity B

Store:

* Origin
* Destination
* Intermediate entities
* Hop count
* Typed edges
* Supporting edge identifiers
* Evidence for every underlying edge
* Path strength
* Derived status

Reuse the current typed-path engine and supported hop limits.

Do not generate a verified indirect path using an AI candidate, unsupported edge or review-required relationship.

HIDDEN

A previously unrecognized economic, structural or contractual dependency.

Possible examples:

* Shared supplier
* Shared customer
* Common SPV
* Shared guarantor
* Common financing
* Indirect ownership
* Infrastructure concentration
* Shared revenue dependency

R2D2 and Opus may discover these relationships.

They must initially remain review-required candidates unless an independently sufficient evidence contract is satisfied.

EXPOSURE

Citi EXP, TFA, facilities and internal credit exposure must remain separate from relationship types and confidence scores.

Use the existing FACT / DERIVED / EXPOSURE / AI_CANDIDATE separation.

6. FIX RELATIONSHIP TAXONOMY AND VALIDATION

The current historical/current reconciliation identified an unsafe taxonomy fallback where unrecognized relationships can become advisor.

Remove this unsafe behavior from the active ingestion/validation path.

Use explicit taxonomy outcomes:

* CANONICAL
* NORMALIZED_ALIAS
* REVIEW_REQUIRED
* UNSUPPORTED

Unrecognized labels cannot become verified graph edges through a default relationship type or weight.

Preserve the existing canonical taxonomy and supported explicit aliases.

Similarly, validation_status=PASSED by itself is not sufficient evidence verification.

Only include records satisfying the complete applicable semantic, deterministic, canonical identity and evidence checks in the verified graph.

Review-required records must be retained for investigation, not discarded or promoted.

7. RELATIONSHIP SCORING

Reuse the existing scoring model.

Retain the current established calculation where applicable:

Relationship weight = min(1, round(base relationship weight × source quality × recency multiplier × financial materiality multiplier, 3))

Do not invent new arbitrary weights.

Retain the current source-weight policy, explicit recency thresholds and financial-materiality definitions.

Do not apply valid weights to unsupported or unresolved relationship types.

For graph distance, reuse the existing weighted shortest-path implementation, including its documented edge-cost transformation.

Provide interpretable explanations of scores and supporting evidence.

Candidate discovery scores must remain separate from verified relationship strength.

8. R2D2 EVIDENCE ENRICHMENT

Use the current approved CCR-native R2D2 integration.

Generate targeted research tasks for each relevant relationship candidate.

Search for:

* Corporate ownership and hierarchy
* Investment
* Financing
* Supplier/customer contracts
* Strategic partnerships
* Cloud and data-centre dependencies
* SPVs
* Guarantees
* Leases
* Offtake
* Material commercial agreements
* Shared counterparties
* Relevant corporate events

Do not rely on one generic company-summary prompt.

R2D2 results are retrieved evidence/context, not verified edges.

Resolve the underlying primary publisher/document source wherever possible.

Reuse the approved direct-source pipeline:

SEC/EDGAR → official investor relations → annual reports → official company disclosures → other approved direct publishers.

Source evidence must retain a real document/URL, exact excerpt and available publication/effective date.

Do not weaken evidence requirements to make more relationships appear.

Do not restart the previous generic ADK grounding investigation.

9. CLAUDE OPUS REFINEMENT

Activate the current approved Opus integration after evidence retrieval.

Provide Opus with:

1. Canonical entities.
2. Deterministic CAM facts.
3. Existing direct relationships.
4. CAM relationship candidates.
5. R2D2 evidence.
6. Verified direct-source evidence.
7. Existing graph context.

Require structured, schema-valid JSON.

Opus responsibilities:

* Entity reconciliation
* Relationship classification
* Directionality
* Taxonomy normalization proposals
* Contradiction detection
* Deduplication
* Candidate discovery
* Relationship relevance assessment
* Hidden-dependency investigation
* Evidence synthesis

Opus must not fabricate:

* Citi exposure amounts
* Facility limits
* Credit ratings
* Source URLs
* Supporting excerpts
* Relationship dates
* Verified entity links

All AI results must pass deterministic validation before promotion.

Preserve AI-processing provenance independently from verification status.

10. PRIORITY — RELATIONSHIP RECORDS TABLE

Make this a fully operational production component.

Rename the section:

Relationship Records

Remove unnecessary client-demo terminology.

Connect it to the real production relationship APIs.

Display:

* Direct verified facts
* Indirect derived paths
* Hidden candidates
* Hierarchy and ownership links
* Review-required relationships

Implement real filters:

ALL | DIRECT | INDIRECT | HIDDEN | VERIFIED | REVIEW REQUIRED

Required functionality:

* Fullscreen expand/collapse
* Mouse-resizable height
* Column resizing where practical
* Horizontal and vertical scrolling
* Sorting
* Entity search
* Relationship-type filters
* Evidence-status filters
* Server-side pagination
* Expandable relationship details
* Clickable source/provenance
* Source dates
* Full indirect path inspection

The user must be able to enlarge the table to occupy substantially more of the screen without repeatedly scrolling a small panel.

Use clear columns for:

* Entity A
* Entity B
* Relationship type
* Direction
* Classification
* Confidence
* Relationship strength
* Citi EXP / TFA when sourced
* Source
* Source date
* Evidence status
* Intermediate path
* Evidence drill-down

Do not fabricate additional records or hide records because two edges share the same entity pair.

11. IMPROVE CORRELATION NETWORK VISUALIZATION

Keep the current page layout, but replace the basic bubble-like visual behavior with a professional interactive network.

Reuse the current graph library where possible.

Requirements:

* Better node layout and spacing
* Clear company labels
* Professional depth-enhanced nodes
* Directional edges
* Multiple edge types between the same pair
* Zoom
* Pan
* Rotate or 3D-like interaction where supported
* Fit-to-screen
* Highlight connected entities
* Node selection
* Edge selection
* Evidence and relationship tooltips
* Expand connected relationships

Use a consistent color model:

Blue: Verified direct

Orange: Verified indirect

Purple: Hidden candidate/dependency

Grey dashed: Review-required/unresolved evidence

Show a legend.

Make colors reflect actual validated relationship classifications rather than visual decoration.

Do not treat graph proximity as relationship evidence.

12. POPULATE CREDIT RISK INTELLIGENCE

The current right-hand dossier must load real company intelligence.

Rating

Populate sourced CAM internal ratings, external agency ratings and available rating history.

If no external agency rating exists, show an appropriately labeled alternative risk indicator rather than inventing an agency rating.

Financials

Retrieve actual sourced financial values from CAM, approved company annual reports, SEC filings and approved market providers.

Market data from approved Yahoo Finance or equivalent sources may be displayed with source and timestamp.

Never confuse stock-price performance with credit rating or internal exposure.

Identity

Populate canonical identifiers, parent, subsidiary, ultimate-parent and ownership relationships.

Relationships

Show all relevant direct, indirect and hidden/review-required records.

Distance

Use genuine graph calculations for hop distance and weighted paths.

Calculate Jaccard only when the underlying comparison universe is defined and data is sufficient.

Missing metrics must not be displayed as misleading zeros.

13. STRESS ANALYTICS — REAL-WORLD MAP

Preserve the existing full-world map geometry and working geographic rendering.

Make the map more informative using grounded production data.

Implement:

* Real country-of-risk coverage
* Country/sector breakdowns
* Verified exposure-based sizing where available
* Risk legends
* Country selection and drill-down
* Relationship-linked geographic connections
* Evidence-backed macro-event overlays
* Tooltip showing company, country, event, source and date

Potential event categories:

* Interest-rate shocks
* Liquidity squeezes
* Geopolitical conflicts
* Tariff/trade disruptions
* AI infrastructure concentration
* Technology-sector stress

Events must be sourced and dated.

Connect countries with arcs only when there is real underlying cross-country relationship, exposure, or specifically supported event transmission.

Where modeled shock impacts are implemented, distinguish scenarios from observed conditions and document the assumptions.

Do not create decorative arcs or fabricated stress numbers.

14. RISK HEATMAP AND PORTFOLIO ANALYTICS

Connect these pages to the existing backend data.

Risk Heatmap should show an explainable counterparty-by-risk-dimension matrix where usable inputs exist.

Portfolio Analytics should aggregate verified relationships and Citi exposures, with direct and indirect concentration analysis.

Do not calculate aggregate exposure by summing repeated facility/counterparty rows without checking duplication and attribution.

Preserve unavailable-data indicators where necessary.

Keep the current four tabs:

* Correlation
* Stress Analytics
* Portfolio Analytics
* Risk Heatmap

No large CSS redesign.

15. SECURITY AND DEPLOYMENT

Remove active insecure TLS fallbacks such as verify=False from affected production provider paths.

Use the approved Citi CA/certificate configuration.

If certificate configuration is unavailable, fail safely and report the specific provider as blocked. Do not silently disable verification.

Preserve the existing CCR-specific environment and dependency configuration.

Do not create a dependency on RPR paths, runners, environment variables or old implementations.

Use one supported production startup command.

Avoid editing generated frontend files independently of their maintained source. If the current frontend genuinely has only a maintained static HTML artifact, make the smallest controlled change and document that choice; do not start a wholesale frontend-framework migration.

16. IMPLEMENTATION ORDER

Execute sequentially:

Phase 1 — Production activation

Real FastAPI/frontend connection and canonical entity search.

Phase 2 — Relationship intelligence

Verified direct records, indirect paths, hidden candidate separation, hierarchy, taxonomy safety.

Phase 3 — NVIDIA enrichment

CAM, R2D2, Opus, evidence validation, sourcing and existing graph integration.

Phase 4 — Frontend integration

Professional graph, Relationship Records table and populated entity dossier.

Phase 5 — Portfolio and geographic analytics

Stress map, portfolio analytics and risk heatmap using genuinely available data.

Phase 6 — End-to-end validation

Integration tests, browser validation, safe cleanup, documentation and final commit.

Do not stop after each phase to request permission or generate a new audit unless an essential user decision is genuinely required.

If external providers are blocked, continue independent implementation tasks and report the blocker accurately.

Avoid unlimited retries, uncontrolled enrichment batches and changes outside this project.

17. ACCEPTANCE CRITERIA

The implementation is complete when:

* Production frontend starts through HTTP without demo mode.
* Real canonical company search works.
* NVIDIA loads correctly from the production backend.
* At least one other company can be loaded using the same generic production flow.
* Verified direct relationships render correctly.
* Verified indirect paths are graph-derived.
* Hidden candidates are represented separately.
* Hierarchy and ownership relationships retain evidence.
* Taxonomy fallback is safe.
* Relationship Records table is resizable and fullscreen-capable.
* Evidence drill-down works.
* Graph visualization is interactive and clearly classified.
* Credit Risk Intelligence uses sourced information.
* Citi EXP/TFA values are never fabricated or misattributed.
* R2D2 and Opus outputs are schema-validated when providers are available.
* World map works with production data.
* Risk Heatmap and Portfolio Analytics show meaningful sourced outputs wherever data permits.
* No production SQLite.
* No RPR runtime dependency.
* Existing valid production relationships are preserved.
* Regression tests pass.
* Browser refresh and server restart do not restore the client demo unexpectedly.

18. FINAL DELIVERY

Provide a short implementation report with actual measured results:

PRODUCTION APPLICATION URL:

STARTUP COMMAND:

CANONICAL ENTITIES ACCESSIBLE:

PRODUCTION RELATIONSHIP RECORDS:

VERIFIED DIRECT:

VERIFIED INDIRECT:

HIDDEN VERIFIED:

HIDDEN REVIEW REQUIRED:

HIERARCHY / OWNERSHIP:

NVIDIA BACKEND:

CITI EXP:

TFA:

R2D2:

OPUS:

CREDIT RISK INTELLIGENCE:

RELATIONSHIP RECORDS TABLE:

NETWORK GRAPH:

STRESS ANALYTICS:

PORTFOLIO ANALYTICS:

RISK HEATMAP:

TEST RESULTS:

REMAINING BLOCKERS:

FILES MODIFIED:

COMMIT HASH:

Do not declare a capability working merely because its code exists. Verify its runtime behavior through the actual production API and application.

IMPLEMENT, TEST, FIX AND DELIVER. NO MORE AUDIT LOOPS, DUPLICATE ARCHITECTURES OR DEMO-ONLY SOLUTIONS.