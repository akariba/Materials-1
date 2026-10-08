IMPORTANT — FIX LIVE APPLICATION AND RECONCILE CAM SOURCES.

Do not continue frontend redesign or historical CCRIG recovery.

We have two issues to resolve.

PHASE 1 — LIVE FRONTEND CONNECTION

The browser is currently opening:

frontend/dist/index.html

directly as a local file.

This is not a reliable way to access the FastAPI-backed application.

1. Identify the supported production FastAPI entry point.
2. Start the current CCR backend using the established project environment.
3. Verify GET / and GET /api/stats return HTTP 200.
4. Verify the canonical entity API returns actual records.
5. Verify the relationship API returns actual records.
6. Open the frontend using the backend HTTP address.
7. Confirm the graph and relationship table receive real API data.
8. Investigate any network/API error before changing the frontend.

Do not use the five-company demo API.

Do not fabricate entities or relationships.

Do not edit generated dist/index.html to compensate for a missing backend connection.

PHASE 2 — RESCU CAM DOCUMENT INVENTORY

Inspect recursively:

src/data/raw/RESCU/RESCU/

Compare every eligible PDF/DOCX/CAM document against:

cam_documents.parquet
cam_passages.parquet
cam_entity_mentions.parquet

Use normalized paths and document hashes.

Report:

- total raw source documents
- documents already indexed
- genuine unindexed documents
- exact duplicates
- parsing failures
- documents containing potentially relevant CCR/exposure information

Do not assume the current 66 indexed CAMs represent the entire source directory.

Do not delete raw documents.

If additional genuine CAM documents are missing from the index,
incrementally index them using the existing proven CAM parser,
preserving source provenance and avoiding duplicate passages.

Do not rerun the complete corpus unnecessarily.

PHASE 3 — DATA INTEGRITY

Confirm:

- canonical entity Parquet remains authoritative
- current production relationship artifact is preserved
- DuckDB remains the analytical query layer
- no production SQLite database is created
- no RPR dependency is introduced
- no demo records are promoted into production
- no existing verified relationship is lost

PHASE 4 — VALIDATION

Test:

1. Backend starts.
2. Frontend loads via HTTP.
3. Entity search works.
4. NVIDIA can be found by canonical CAGID.
5. Relationship table displays API records.
6. Network graph displays backend relationships.
7. Evidence/provenance is preserved.
8. CAM document coverage is reconciled.

Return:

FRONTEND_HTTP_CONNECTION: WORKING/BLOCKED
CANONICAL_ENTITY_API: WORKING/BLOCKED
RELATIONSHIP_API: WORKING/BLOCKED
RESCU_DOCUMENTS: <count>
ALREADY_INDEXED: <count>
NEWLY_INDEXED: <count>
DUPLICATES: <count>
TOTAL_CAM_DOCUMENTS: <count>
PRODUCTION_RELATIONSHIPS_PRESERVED: YES/NO
TESTS: <results>

Exact command to start the application:
<command>

Exact URL to open:
<url>

STOP after validation.