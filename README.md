EXECUTE THE CCR IMPLEMENTATION — WRITE ACTUAL CODE

You have already produced CCR_Implementation_Blueprint.md.

I did not request another architecture document. I requested a fully implemented, functional CCR Relationship Intelligence application.

The planning phase is complete. You must now act as a Principal Software Engineer and implement the solution directly in my VS Code workspace.

1. Stop generating planning documents

Do not produce another blueprint, architecture proposal, pseudocode specification, or implementation checklist as your primary deliverable.

Your deliverables must be actual source-code changes, executable functionality, working APIs, validated data pipelines, and passing tests.

Use the existing blueprint as the implementation specification, but first reconcile it against the actual repository.

2. Work directly in the existing CCR Correlation project

Inspect the repository and determine which capabilities already exist.

Reuse working components, including:

* FastAPI backend
* React frontend
* DuckDB and Parquet architecture
* CAM document ingestion
* Canonical entity resolution
* Existing verified relationship processing
* Opus/R2D2 integration
* Credit Risk Intelligence panels
* Network graph components
* Existing PHR-compatible data structures

Do not create a competing project or second implementation.

Do not replace working components unless a specific defect requires a verified change.

Preserve all validated business logic, source evidence, and financial data.

3. Implement the blueprint in actual code

Follow the blueprint’s logical implementation sequence, beginning with the smallest end-to-end working path.

First implementation milestone

Build and connect:

1. Canonical entity ingestion and resolution.
2. CAM document extraction.
3. Persistent Parquet outputs and DuckDB views.
4. Verified relationship extraction and storage.
5. Live FastAPI entity and relationship endpoints.
6. React frontend integration showing actual backend data.

The first milestone must produce an operational application, not an empty repository skeleton.

Second implementation milestone

Implement:

* Evidence-grounded MapReduce extraction
* Semantic and deterministic validation
* Entity identity verification
* R2D2/Opus relationship refinement
* Direct and indirect relationship discovery
* Verified versus review-required classifications
* Relationship provenance and audit trail

Third implementation milestone

Implement accurate enrichment of the available client universe:

* Legal entity identifiers
* Parent and subsidiary structures
* External ratings
* Financial information
* Ownership and financing relationships
* Credit risk metrics where sufficient data exists
* Approved market and external evidence retrieval
* Per-client enrichment status and source provenance

Run a validated ten-client pilot before scaling to the full eligible universe.

Do not manufacture information when data is unavailable.

Fourth implementation milestone

Complete the existing frontend integration:

* Entity search and selection
* Credit Risk Intelligence
* Relationship graph
* Direct, indirect, and hidden-candidate filters
* Physical relationship records
* Portfolio analytics
* Stress analytics
* Risk heatmap

Preserve the current UI design and ensure all panels use real backend data.

4. Implement incrementally and verify

For each implementation batch:

1. Identify the exact existing files to modify.
2. Write or modify the code directly.
3. Update dependencies and imports where needed.
4. Run relevant unit tests.
5. Run integration checks when possible.
6. Fix errors caused by your changes.
7. Report files actually changed and tests actually executed.
8. Continue to the next batch.

Do not mark an implementation stage complete without executable code and verification.

5. Preserve the critical risk-data rules

The system must maintain:

* One deterministic canonical entity record per ordinary CAGID, with documented split behavior where required.
* No unverified automatic merging of entities.
* Separate evidence, identity, semantic, deterministic, and analyst-review states.
* No promotion of an LLM-generated claim into verified graph topology without the required validation.
* Preservation of multiple physical relationships between the same entities.
* No invented ratings, financials, correlations, or Citi exposures.
* No parent-level financials presented as subsidiary financials.
* Full evidence and provenance for published relationships.

6. Demonstrate actual execution

Start the application locally using the existing documented startup procedure.

Verify:

* FastAPI starts successfully.
* The frontend loads.
* The client registry returns real entities.
* Entity selection retrieves the correct profile.
* The relationship API returns persisted records.
* Graph edges correspond to actual validated relationships.
* Available credit information populates the correct entity.
* Missing information is explicitly identified.
* The application does not remain indefinitely in loading states.

If a test cannot run because of unavailable credentials or external infrastructure, record that limitation instead of claiming success.

7. Mandatory completion report

At the end of each batch, report:

* Files created
* Files modified
* Working functionality implemented
* Tests executed and results
* Remaining defects
* Next implementation batch

Do not substitute descriptions of files for the files themselves.

FINAL DIRECTIVE

Stop planning. Start coding now.

Use the existing blueprint as technical guidance, reconcile it with the current repository, and implement directly in the workspace.

Do not ask me to manually create individual source files.

Do not produce another Markdown artifact as your main output.

The result must be working application code, not another specification.

Begin with repository inspection and the first executable implementation milestone immediately.