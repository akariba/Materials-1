DO NOT MODIFY ANY DATA OR CODE YET.

Re-audit the Lending source hierarchy using the actual business purpose
of the two Excel workbooks.

LENDING ONLY.
No CCR.
No R2D2.
Read-only.

The previous audit may have conflated:
- benchmark population,
- CAM expected population,
- CAM availability metadata,
- physically ingested CAM documents,
- and relationship evidence.

Establish the source hierarchy first.

1. AI Economy Study_Masterfile.xlsx

Treat this as the portfolio/population and exposure benchmark.

Inspect every sheet and classify its purpose, including:
- Master file
- Pivot
- Pivot - Core AI
- Pivot - Core AI Detailed View
- Core AI - Raw data
- CAM Data
- any other sheet present

Identify exactly:
- total unique CAGIDs
- CoreAI population
- Technology population
- We have CAM? status
- Latest CAM Date
- exposure fields
- facility fields
- rating fields
- industry fields
- geography/country fields
- portfolio ownership fields

Do NOT assume every benchmark entity is required to have a CAM file.

2. Core AI CAMs.xlsx

Treat this as the CAM control / tracking workbook.

Determine:
- number of populated CAGIDs
- unique CAGIDs
- CAM = Y
- CAM = N
- CAM = N/A
- blank CAM statuses
- comments/status exceptions
- relationship names
- exposure amounts
- cancelled / migrated / transferred cases

Reconcile its CAGIDs against the Masterfile CoreAI population.

Explain every difference.

3. CAM AVAILABILITY MATRIX

Build a read-only reconciliation by CAGID:

CAGID
canonical_name
population
in_masterfile
in_core_ai_cams_tracker
tracker_cam_status
masterfile_we_have_cam
masterfile_latest_cam_date
cam_data_tab_present
physical_cam_document_present
physical_document_names
document_subject_resolved
document_parse_status
relationships_extracted
validated_relationships
review_required_relationships

Do this for the complete relevant population.

4. CAM COVERAGE

Report separately:

A. Benchmark clients
B. Clients expected to have CAM according to control data
C. Clients marked as having CAM
D. Clients with physical CAM files supplied to this project
E. CAM files successfully parsed
F. CAM files whose subject was correctly resolved
G. CAM files producing relationship candidates
H. CAM files producing validated relationships

Do NOT label B-H as equivalent.

5. TECHNOLOGY POPULATION

Reassess the previous statement that 343 Technology clients are
“missing CAM documents.”

Determine instead:
- whether Technology clients are expected to have CAMs;
- whether CAM metadata exists in the CAM Data sheet;
- whether physical CAM files were simply not supplied to this project;
- whether missing physical files are a data-quality failure,
  a scope limitation, or expected behavior.

Do not call them missing until the authoritative reference says they
should be present.

6. REFERENCE DATA ROLE

For every structured file/sheet determine whether it is:

- POPULATION_REFERENCE
- CAM_CONTROL_REFERENCE
- CAM_AVAILABILITY_METADATA
- EXPOSURE_REFERENCE
- FACILITY_REFERENCE
- ENTITY_REFERENCE
- RELATIONSHIP_EVIDENCE
- OTHER

Structured exposure/reference data must not be promoted to relationship
evidence unless it explicitly establishes the relationship.

7. ACTUAL CAM DOCUMENTS

Inventory every PDF/DOCX CAM/AR/QR/CCM source.

For every file report:
- filename
- document type
- intended CAGID
- intended entity
- resolved CAGID
- resolved entity
- parsing success
- pages/paragraphs/tables extracted
- relationship candidates
- validated
- review-required
- rejected
- blocker if zero validated relationships

8. FINAL RECONCILIATION

Explain precisely:

- what the 418 benchmark represents;
- what the CoreAI population represents;
- what the Core AI CAMs workbook represents;
- what the CAM Data tab represents;
- what the physical CAM corpus represents;
- which population should be used as the denominator for CAM coverage;
- which data is allowed to create relationship truth.

Do not repair anything.
Do not rebuild anything.
Do not modify the frozen baseline.

Return the reconciliation and STOP.
