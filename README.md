Prompt for Luna — CCR Relationship Intelligence: 10-Company Production Pilot
1. EXECUTION DIRECTIVE
Continue working in the existing CCR Relationship Intelligence application.
Stop attempting to build and display the entire 3.64-million-entity universe.
We are narrowing the implementation to a controlled 10-company production pilot.
The objective is to deliver a high-quality, fully operational relationship intelligence application using actual production data.
Do not create a demonstration dataset.
Do not create synthetic relationships.
Do not replace existing production data.
Do not restart historical audits or rebuild the architecture.
Implement the complete relationship intelligence pipeline for the selected 10 companies, including:
- CAM extraction and enrichment.
- Canonical entity identification.
- Direct relationship discovery.
- Indirect relationship construction.
- Hidden dependency investigation.
- R2D2 evidence retrieval.
- Claude Opus refinement.
- Relationship validation and scoring.
- Interactive graph visualization.
- Relationship Records.
- Credit Risk Intelligence.
- Stress Analytics.
- Portfolio Analytics.
- Risk Heatmap.
Make these 10 companies work exceptionally well before attempting larger-scale deployment.
2. RESTRICT THE ACTIVE PRODUCTION UNIVERSE
Create a configurable production cohort containing these 10 companies:
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
Resolve every company against the existing canonical entity universe.
Use actual identifiers:
- CAGID
- GFCID
- LEI, where available
- CIK, where applicable
- Canonical legal name
- Ultimate parent
- Parent/subsidiary hierarchy
Do not assign invented identifiers.
Carefully distinguish corporate groups from their operating subsidiaries.
For example, an exposure belonging to a particular Microsoft subsidiary must not automatically become an exposure to every Microsoft legal entity.
For OpenAI, resolve the actual legal entities represented in production data rather than assuming that the commercial brand identifies a unique legal counterparty.
Before accepting each entity into the cohort, validate its identity against available production records.
If a selected company cannot be resolved reliably, report the issue and choose a suitable replacement from the same AI infrastructure ecosystem using available production evidence.
Preserve NVIDIA, Oracle and OpenAI as priority investigation targets.
Important architectural rule
Keep the existing complete canonical database and production relationship artifacts unchanged.
Introduce a controlled cohort filter or cohort-specific analytical view.
The production source remains:
Parquet → DuckDB → FastAPI → Frontend
Do not create another database or a competing relationship engine.
The application should initially display only the 10 primary companies.
However, connected companies discovered through validated relationships must be accessible as secondary graph nodes.
Ten primary companies does not mean ten total graph nodes or ten total relationships.
3. COMPLETE RELATIONSHIP EXTRACTION
For each selected company, retrieve and examine all relevant information available from the current approved production sources.
Do not rely exclusively on the existing relationship table.
Reuse the indexed CAM documents and existing extraction components.
Extract:
Corporate relationships
- Parent/subsidiary.
- Beneficial ownership.
- Equity investment.
- Joint ventures.
- Strategic partnerships.
- Corporate guarantees.
Commercial relationships
- Supplier/customer.
- Cloud service agreements.
- GPU procurement.
- Infrastructure provisioning.
- Manufacturing agreements.
- Material contracts.
- Revenue dependencies.
- Long-term service agreements.
Financial relationships
- Lending facilities.
- Financing arrangements.
- Borrower/guarantor structures.
- Credit support.
- Collateral.
- Contractual financing dependencies.
- Citi lending exposure, where sourced.
- TFA, where sourced.
Infrastructure relationships
- Data centres.
- Power supply arrangements.
- Semiconductor fabrication.
- GPU infrastructure.
- Shared suppliers.
- Shared cloud providers.
- Shared SPVs.
Do not assume a relationship exists simply because two companies operate in the same industry.
Every extracted record must retain its actual source and evidence.
4. USE R2D2 FOR DEEP RELATIONSHIP RESEARCH
Activate the existing R2D2 integration for the 10 companies.
Do not ask R2D2 for generic company descriptions.
Instead, execute targeted relationship investigations.
For NVIDIA, investigate its actual evidenced relationships involving semiconductor manufacturing, GPU distribution, AI infrastructure financing, cloud providers, strategic investments and data-centre counterparties.
For Oracle and OpenAI, investigate their evidenced commercial agreements, cloud infrastructure arrangements, financing relationships and other material contractual dependencies.
Apply similarly targeted research to the remaining seven companies.
Use approved primary sources wherever possible, including SEC filings, official company disclosures, investor relations documents and contractual announcements.
Retrieve exact supporting passages with document identifiers, URLs, publication dates and relevant entities.
Do not fabricate URLs, excerpts or relationship dates.
Provider failures must be reported accurately.
Use bounded requests, retry limits and resumable checkpoints.
5. APPLY CLAUDE OPUS REFINEMENT
Once deterministic extraction and R2D2 retrieval are complete, send the consolidated evidence to the existing approved Claude Opus integration.
Opus must refine relationship intelligence rather than replace the original evidence.
Its responsibilities include:
- Entity reconciliation.
- Relationship classification.
- Directionality.
- Duplicate identification.
- Contradiction analysis.
- Missing relationship discovery.
- Corporate hierarchy reconciliation.
- Hidden dependency hypotheses.
- Evidence consistency assessment.
- Structured relationship descriptions.
Require schema-valid structured output.
Each AI-proposed relationship must be linked to actual supporting evidence before promotion.
Do not treat an Opus-generated conclusion as independently verified evidence.
Preserve distinctions between:
CAM_FACT
EXTERNAL_SOURCE_FACT
AI_CANDIDATE
VERIFIED_RELATIONSHIP
DERIVED_RELATIONSHIP
REVIEW_REQUIRED
AI confidence and evidence verification must remain separate.
6. MAKE DIRECT, INDIRECT AND HIDDEN RELATIONSHIPS WORK
DIRECT
Identify actual relationships between canonical entities.
Each record must include:
- Source company.
- Target company.
- Relationship type.
- Direction.
- Canonical identifiers.
- Supporting evidence.
- Evidence status.
- Confidence.
- Relationship strength.
- Source date.
Preserve multiple relationship types between the same entities.
INDIRECT
Use the existing graph engine to derive relationships through verified direct edges.
Example:
Company A → Company B → Company C
The path must contain at least two independently verified relationships.
Retain every intermediate company and supporting edge identifier.
Support controlled multi-hop discovery, initially up to three hops where computationally reasonable.
Do not build verified paths using unresolved candidates.
HIDDEN
Investigate previously unrecognized dependencies, including:
- Common financing providers.
- Shared suppliers.
- Shared infrastructure.
- Shared customers.
- Common ownership.
- Indirect guarantees.
- SPV structures.
- Material contractual dependencies.
For example, two selected companies might share a critical infrastructure supplier.
If both supplier relationships are verified, the shared dependency may be reported as a graph-derived finding.
If an additional economic relationship is hypothesized but not established, classify it as a hidden candidate requiring review.
Do not invent hidden relationships merely to populate the graph.
7. FIX RELATIONSHIP QUALITY
The previous production implementation exposed inconsistent relationship verification.
Correct this before generating portfolio conclusions.
Requirements:
1. Remove unsafe relationship taxonomy fallbacks.
2. Distinguish generic validation success from evidence verification.
3. Preserve source references.
4. Enforce canonical entity resolution.
5. Preserve different relationship types between identical endpoints.
6. Exclude unsupported relationships from verified graph paths.
7. Keep review-required candidates available for investigation.
8. Reconcile relationship counts by classification and verification status.
Do not convert missing values into zeros.
Do not mark records verified when their supporting evidence cannot be retrieved.
8. BUILD THE ACTUAL 10-COMPANY APPLICATION
Maintain the current four application pages.
Correlation
Display the 10 primary companies clearly.
Allow users to select an individual company or view the entire cohort.
Build the graph using actual production relationships.
Support:
- Zoom and pan.
- Clickable companies.
- Clickable edges.
- Directional relationships.
- Distinct relationship types.
- Multi-hop expansion.
- Evidence inspection.
- Relationship strength.
- Verified versus review-required classification.
Apply readable graph layouts with controlled node spacing.
Do not render millions of entities.
Use bounded graph expansion and server-side loading.
Secondary connected companies should appear only when relevant to the selected relationship investigation.
Relationship Records
Make the relationship table fully functional.
Include:
- Fullscreen mode.
- Resizable height.
- Vertical and horizontal scrolling.
- Sorting.
- Filtering.
- Search.
- Pagination.
- Evidence drill-down.
- Indirect path inspection.
- Relationship type.
- Relationship classification.
- Source and target.
- Confidence.
- Verification status.
- Relationship strength.
The table must include all eligible relationship records discovered for the cohort, not an arbitrary ten-row subset.
Credit Risk Intelligence
Populate the existing company dossier using production evidence.
Include available:
- Internal ratings.
- External ratings.
- Revenue.
- EBITDA.
- Debt.
- Cash.
- Leverage.
- Liquidity.
- Country of risk.
- Ownership.
- Citi EXP.
- TFA.
- Lending facilities.
- Maturity information.
Do not fabricate missing figures.
Internal Citi exposure must remain tied to the correct legal counterparty, facility, reporting date and currency.
A rating or stress indicator must not appear without a traceable source or documented calculation.
Stress Analytics
Preserve the working world map.
Limit primary analysis to the selected cohort and verified connected dependencies.
Show available:
- Countries of risk.
- Geographic dependencies.
- Verified exposure concentrations.
- Infrastructure locations where sourced.
- Cross-border relationships.
- Evidence-backed stress transmission paths.
Do not produce decorative financial risk signals.
Portfolio Analytics and Risk Heatmap
Use the selected cohort for:
- Relationship concentration.
- Common counterparties.
- Shared infrastructure.
- Supplier concentration.
- Lending exposure concentration.
- Geographic exposure.
- Counterparty interconnectedness.
Use real inputs only.
Avoid double-counting exposures or interpreting relationship strength as financial exposure.
9. PERFORMANCE AND SCALABILITY
This is a production-data pilot, not a replacement demonstration application.
The 10-company limit should apply to the active analytical cohort.
Do not destroy, truncate or overwrite the full production universe.
Create configurable controls for:
- Primary cohort size.
- Connected-node expansion.
- Maximum graph hops.
- Server-side pagination.
- Evidence retrieval budgets.
- R2D2 research batches.
- Opus refinement batches.
The default application should load the 10 primary companies quickly without searching or rendering millions of entities in the browser.
Persist validated cohort results using the existing Parquet/DuckDB architecture.
Maintain clear lineage to the full production sources.
Avoid automatically triggering enrichment after browser refresh or backend restart.
Enrichment must run through an explicit controlled execution path.
The future scaling path should allow expansion from 10 to 25, 50, 100 and eventually the broader production universe without redesigning the system.
10. IMPLEMENTATION SEQUENCE
Execute the work in this order.
Phase A — Production cohort
Resolve the 10 canonical companies and implement the default cohort filter.
Phase B — Evidence extraction
Retrieve their available CAM facts, relationships, ownership records, financials and exposure data.
Phase C — Relationship enrichment
Run targeted R2D2 retrieval and Opus refinement.
Phase D — Relationship intelligence
Validate direct edges, calculate indirect paths, investigate hidden dependencies and persist the resulting cohort artifacts.
Phase E — Frontend completion
Connect the real graph, Relationship Records, entity dossier, Stress Analytics, Portfolio Analytics and Risk Heatmap.
Phase F — End-to-end validation
Test the running production application with all 10 companies.
Fix actual runtime failures.
Preserve completed work when external providers are unavailable.
Do not stop after each phase to produce another audit report.
11. ACCEPTANCE CRITERIA
The pilot is complete only when:
- Exactly 10 primary production entities are selectable.
- All 10 resolve to actual canonical records.
- The full production database remains intact.
- The application no longer defaults to the five-company demonstration.
- Relevant CAM facts are extracted and displayed.
- Actual production relationships are retrieved.
- R2D2 enrichment executes where authorized.
- Opus refinement executes where authorized.
- Direct relationships have retrievable supporting evidence.
- Indirect relationships contain verified supporting paths.
- Hidden candidates are clearly distinguished from verified findings.
- The network graph loads correctly.
- Users can expand connected companies beyond the 10 primary entities.
- Relationship Records is fully functional and resizable.
- Available Citi EXP/TFA values are correctly attributed.
- Credit Risk Intelligence displays sourced information.
- The world map remains operational.
- Portfolio Analytics and Risk Heatmap consume real data.
- The application survives browser refresh and backend restart.
- Existing production data and unrelated functionality remain intact.
- Automated and runtime acceptance tests pass.
Do not manufacture records or loosen verification standards to satisfy an expected relationship count.
12. REQUIRED FINAL REPORT
After implementation and testing, report:
CCR RELATIONSHIP INTELLIGENCE
10-COMPANY PRODUCTION PILOT

Production URL:
Git commit:

Primary companies resolved: /10
Canonical identifiers verified:

CAM documents examined:
CAM facts extracted:

R2D2 investigations executed:
R2D2 investigations successful:

Opus refinements executed:
Opus refinements successful:

Verified direct relationships:
Verified indirect paths:
Hidden verified findings:
Hidden review-required candidates:

Ownership/hierarchy relationships:
Financial/contractual relationships:
Shared infrastructure dependencies:

Citi EXP coverage:
TFA coverage:

Relationship Records: PASS/FAIL
Network graph: PASS/FAIL
Credit Risk Intelligence: PASS/FAIL
Stress Analytics: PASS/FAIL
Portfolio Analytics: PASS/FAIL
Risk Heatmap: PASS/FAIL

API tests:
Integration tests:
Browser tests:

Known data gaps:
Remaining blockers:
Files modified:

FINAL EXECUTION INSTRUCTION
Focus exclusively on delivering a robust 10-company production-data pilot.
Use the current architecture and actual production sources.
Prioritize relationship quality, completeness of available evidence, verified indirect paths, actionable hidden-dependency discovery and a fully working application.
Do not initiate another full-universe enrichment exercise.
Do not create another isolated demo.
Do not substitute generic AI-generated company information for real relationship evidence.
IMPLEMENT → ENRICH → VALIDATE → VISUALIZE → TEST → FIX.
Once the 10-company pilot meets its acceptance criteria, preserve it as the validated baseline for future scaling.
