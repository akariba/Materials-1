You are continuing work on the existing CCR Relationship Intelligence repository.

The immediate objective is to build a searchable CAM evidence corpus from the existing heterogeneous raw-data folder and integrate it cleanly with the existing DuckDB / Parquet architecture.

This phase is NOT relationship extraction.
This phase is NOT SEC enrichment.
This phase is NOT web enrichment.
This phase is NOT MapReduce relationship extraction.

The objective is:

Convert the existing CAM repository into a deterministic, inspectable, searchable evidence layer that can later support entity-centric queries such as:

"Find every CAM passage potentially relevant to NVIDIA."

Do not redesign the existing application.
Do not overwrite existing canonical data structures.
Do not modify production relationship logic.

Proceed autonomously through the following steps.

==================================================
PHASE 0 — INSPECT THE EXISTING DATA ARCHITECTURE
==================================================

Before creating anything new, inspect the current repository and determine exactly what already exists.

Locate:

- existing DuckDB files
- .duckdb files
- .db files
- DuckDB connection code
- DuckDB initialization logic
- Parquet views/tables
- SQL schema definitions
- canonical entity structures
- CAGID/GFCID structures
- existing relationship tables
- existing CAM tables
- existing evidence structures

Identify:

- active DuckDB file/path
- whether DuckDB is persistent or created dynamically
- schemas
- tables
- views
- external Parquet files queried through DuckDB

Open the existing DuckDB in READ-ONLY mode first wherever technically possible.

Do not modify the database during discovery.

Produce an inventory for every table/view containing:

schema
object_name
object_type
row_count
columns
column_types
likely primary/business keys
source file if external
likely purpose

Pay particular attention to anything representing:

canonical entities
CAGID
GFCID
client/customer master
entity aliases
normalized entity names
relationships
relationship evidence
CAM/document metadata

Determine whether a canonical entity table already exists.

If one exists, treat it as the existing source of truth unless the repository clearly indicates otherwise.

DO NOT create a second competing canonical entity master.

==================================================
PHASE 1 — INSPECT THE RAW DATA FOLDER
==================================================

Recursively inspect the existing raw-data / CAM repository exactly as it currently exists.

Do not rename, move, delete, reorganize, or modify source files.

Identify and classify:

PDF
DOCX
DOC
XLS
XLSX
CSV
JSON
Parquet
TXT
other formats

The repository may contain a mixture of:

CAM PDFs/DOCX
CAGID reference files
Excel files
JSON files
customer/entity data
Parquet files
supporting metadata
previously generated artifacts

Do not assume every file is a CAM.

==================================================
PHASE 2 — CLASSIFY FILE ROLES
==================================================

Classify every source file into one of:

CAM_DOCUMENT
ENTITY_REFERENCE
CAGID_REFERENCE
CUSTOMER_MASTER
SUPPORTING_METADATA
EXISTING_DERIVED_ARTIFACT
UNKNOWN
UNSUPPORTED

If uncertain, use UNKNOWN.

Do not infer business meaning from filenames alone when content inspection is required.

Create a raw-file inventory.

==================================================
PHASE 3 — BUILD A NON-DESTRUCTIVE DOCUMENT MANIFEST
==================================================

Create one structured record per source document/file.

Use fields approximately equivalent to:

document_id
filename
full_path
relative_path
source_folder
file_type
file_size
file_hash
classification
CAGID
GFCID
client_name
canonical_entity_id
document_date
parser_used
parse_status
parse_warning
created_at

Rules:

- document_id must be stable and reproducible
- calculate a file hash for duplicate detection
- do not infer CAGID from uncertain fuzzy matching
- leave unknown fields null
- do not alter source files

Persist the manifest as:

cam_documents.parquet

or use an equivalent repository-consistent name.

==================================================
PHASE 4 — PARSE THE CAM DOCUMENTS
==================================================

Parse only files classified as CAM/document content.

Preserve source provenance.

For PDFs preserve where possible:

document_id
page_number
section/header
paragraph/text block
source order
table indicator
source position

Do not remove page provenance.

For DOCX preserve:

document_id
heading hierarchy
section
paragraph
table content
source order

For structured formats preserve their existing structure where practical.

IMPORTANT:

Do not summarize source content.
Do not paraphrase source content.
Do not use an LLM to rewrite source text.
Preserve original evidence text.

==================================================
PHASE 5 — CREATE PASSAGE-LEVEL SEARCH RECORDS
==================================================

Convert parsed CAM content into searchable passages.

Prefer semantic/business boundaries such as:

heading
section
paragraph group
table
page

Avoid arbitrary very small chunks unless technically required.

Every passage must retain full provenance.

Target schema:

passage_id
document_id
page_number
section
heading
block_type
sequence_number
text
source_location
character_count
token_estimate if available

Persist as:

cam_passages.parquet

==================================================
PHASE 6 — REUSE THE EXISTING CANONICAL ENTITY DATA
==================================================

Inspect the existing DuckDB / Parquet data and determine how canonical entities are currently represented.

Possible identifiers include:

canonical_entity_id
CAGID
GFCID
legal_name
normalized_name
aliases
CIK
LEI
ISIN
CUSIP
ticker
other identifiers

Use the existing entity structure.

Do not create a competing entity universe.

Document exactly which table/file is being used as the canonical entity source.

==================================================
PHASE 7 — BUILD ENTITY-MENTION INDEXING
==================================================

Create an entity-mention index from CAM passages.

This is for RETRIEVAL only.

Do NOT infer business relationships yet.

For each mention capture approximately:

mention_id
passage_id
document_id
mentioned_name
normalized_mentioned_name
canonical_entity_id
CAGID
GFCID
match_method
match_score
resolution_status
ambiguity_reason

Allowed resolution statuses:

MATCHED
AMBIGUOUS
UNRESOLVED

Prefer deterministic resolution using this general precedence:

1. exact known identifier
2. exact canonical legal name
3. known alias
4. normalized exact name
5. controlled high-confidence matching

Do not force ambiguous matches.

Persist as:

cam_entity_mentions.parquet

==================================================
PHASE 8 — BUILD THE ENTITY-CENTRIC SEARCH LAYER
==================================================

Create a reusable retrieval function conceptually equivalent to:

search_entity(seed_entity)

It should accept inputs such as:

NVIDIA
NVIDIA Corporation
canonical_entity_id
CAGID
GFCID

The function should:

1. Resolve the seed entity against the existing canonical entity master.
2. Retrieve validated names, aliases and identifiers.
3. Search all indexed CAM passages.
4. Return candidate passages with full provenance.

Return approximately:

seed_entity
canonical_entity_id
CAGID
GFCID
document_id
filename
source_folder
page_number
section
matched_term
passage_id
passage_text
retrieval_method
retrieval_reason

IMPORTANT:

This stage only discovers potentially relevant evidence.

It must NOT claim that a relationship exists.

==================================================
PHASE 9 — USE TRANSPARENT SEARCH FIRST
==================================================

For the first implementation prioritize:

exact company-name search
normalized-name search
known aliases
identifier search
CAGID search
GFCID search

Use DuckDB SQL and Parquet scanning where appropriate.

Do not introduce vector databases or embeddings unless:

- they already exist and are part of the current architecture, OR
- deterministic retrieval is demonstrated to have significant recall problems

The first retrieval layer should be transparent, debuggable and reproducible.

==================================================
PHASE 10 — INTEGRATE WITH EXISTING DUCKDB
==================================================

Do NOT overwrite existing tables.

Do NOT replace the existing canonical entity structure.

Preferred approach:

Keep CAM-derived datasets in Parquet:

cam_documents.parquet
cam_passages.parquet
cam_entity_mentions.parquet

Expose them through the existing DuckDB as tables or views.

Conceptually:

cam_documents
cam_passages
cam_entity_mentions

The integration should allow joins such as:

canonical_entity
→ canonical_entity_id / CAGID / GFCID
→ cam_entity_mentions
→ cam_passages
→ cam_documents

Reuse existing business keys.

Do not duplicate canonical identifiers unnecessarily.

If the repository already uses a different but equivalent persistence architecture, follow the existing architecture rather than forcing this exact implementation.

==================================================
PHASE 11 — BUILD A READ-ONLY DATABASE INSPECTOR
==================================================

Create a simple read-only inspection utility so the user can inspect what the agent built without needing advanced SQL knowledge.

Example:

python inspect_db.py

It should display:

DuckDB path
schemas
tables
views
row counts

Support functions equivalent to:

python inspect_db.py tables
python inspect_db.py describe <table>
python inspect_db.py sample <table>
python inspect_db.py search NVIDIA

The utility must be READ-ONLY by default.

The purpose is to make the DuckDB architecture visible and understandable.

==================================================
PHASE 12 — NVIDIA RETRIEVAL SMOKE TEST
==================================================

Use NVIDIA only as a seed-client example.

IMPORTANT:

Do NOT assume any dedicated NVIDIA CAM exists.

NVIDIA is simply the seed entity being investigated.

Resolve NVIDIA against the existing canonical entity universe.

Use available validated identity information such as:

NVIDIA
NVIDIA Corporation
CAGID
GFCID
known canonical aliases
other existing validated identifiers

Then search the entire indexed CAM corpus.

Report:

seed resolution status
canonical entity matched
CAGID if available
GFCID if available
number of CAM documents indexed
number successfully parsed
number failed
number linked to entities
number ambiguous
number unresolved
number of candidate CAM documents containing relevant NVIDIA mentions
number of candidate passages

For sample results provide:

filename
document_id
CAGID if available
page
section
matched term
retrieval method
retrieval reason
exact source passage

Do not call these relationships.

For example:

A CAM mentioning NVIDIA in general market commentary is only a candidate passage.

No relationship should be asserted at this stage.

==================================================
PHASE 13 — CREATE A HUMAN REVIEW REPORT
==================================================

Generate a human-readable inspection report.

Prefer:

cam_index_summary.xlsx

if appropriate spreadsheet dependencies already exist.

Otherwise CSV/Markdown is acceptable.

Suggested tabs/sections:

DuckDB Inventory
Raw File Inventory
CAM Documents
Parse Failures
Duplicate Files
CAGID Mapping
Ambiguous Entities
Unresolved Entities
NVIDIA Retrieval Results
Integration Map

The spreadsheet/report is only for human inspection.

The real machine-readable artifacts remain Parquet/DuckDB.

==================================================
PHASE 14 — CREATE AN ARCHITECTURE INTEGRATION MAP
==================================================

Document exactly:

EXISTING STRUCTURES REUSED

For example:

existing DuckDB
canonical entity table
CAGID master
GFCID master
existing aliases
existing reference data

NEW STRUCTURES ADDED

For example:

cam_documents
cam_passages
cam_entity_mentions

JOIN KEYS

For example:

canonical_entity_id
CAGID
GFCID
document_id
passage_id

EXISTING STRUCTURES NOT MODIFIED

Explicitly list them.

CONFLICTS FOUND

Examples:

multiple competing entity masters
duplicate CAGIDs
conflicting schemas
duplicate IDs
inconsistent aliases
two different relationship models

Do not silently resolve architectural conflicts.

Report them.

==================================================
PHASE 15 — QUALITY CHECKS
==================================================

Check the indexing layer for:

duplicate source files
duplicate document IDs
duplicate passage IDs
empty parsed documents
failed PDFs
failed DOCX
missing page provenance
missing document provenance
missing CAGIDs
ambiguous entity resolution
unresolved entities
unexpected encodings
very large passages
very small/unusable passages

Generate a parse/index quality report.

==================================================
PHASE 16 — DO NOT DO THESE THINGS YET
==================================================

Do NOT:

perform final relationship extraction
infer supplier relationships
infer customer relationships
infer ownership relationships
infer guarantees
infer lending relationships
perform SEC enrichment
perform web enrichment
run graph proximity
calculate Jaccard
calculate weighted path distance
run hidden-relationship discovery
redesign the frontend
migrate to PostgreSQL
introduce Neo4j
introduce Hadoop
introduce Spark
introduce MapReduce relationship extraction
rewrite the canonical entity system
change existing production relationship logic
overwrite existing DuckDB tables
delete existing Parquet artifacts
send all CAMs together to an LLM

This phase is strictly:

INSPECT
→ INVENTORY
→ PARSE
→ INDEX
→ LINK
→ SEARCH
→ VERIFY

==================================================
REQUIRED OUTPUT ARTIFACTS
==================================================

Create or confirm equivalents of:

cam_documents.parquet
cam_passages.parquet
cam_entity_mentions.parquet

duckdb_inventory.json
raw_file_inventory.json
integration_map.json
parse_quality_report.json

cam_index_summary.xlsx

Create read-only utilities equivalent to:

inspect_db.py
search_cam.py

Do not overwrite unrelated production artifacts.

==================================================
FINAL REPORT
==================================================

When finished, provide a concise report containing:

1. EXISTING DUCKDB

Report:

database location
schemas discovered
tables/views discovered
canonical entity source
CAGID/GFCID structures found
existing relationship structures found

2. RAW DATA INVENTORY

Report:

total files
CAM documents
entity/reference files
unsupported files
duplicates

3. PARSING RESULTS

Report:

documents parsed successfully
failures
warnings
PDF results
DOCX results
provenance quality

4. NEW INDEXING ARTIFACTS

List exact files/tables/views created.

5. DUCKDB INTEGRATION

Explain exactly:

what existing objects were reused
what new objects were added
how they connect
which join keys are used

6. NVIDIA RETRIEVAL TEST

Report:

seed resolution
canonical identity used
candidate documents
candidate passages
sample passages with provenance

Do NOT claim any relationship exists.

7. DATA-QUALITY GAPS

List factual issues such as:

missing CAGIDs
ambiguous aliases
unparsed PDFs
duplicate files
missing provenance
unresolved entities

8. READ-ONLY INSPECTION INSTRUCTIONS

Show exactly how the user can inspect:

tables
schemas
row counts
sample records
NVIDIA search results

using the created inspection utilities.

9. FINAL STATUS

Return exactly one of:

CAM_INDEX_READY

CAM_INDEX_READY_WITH_WARNINGS

BLOCKED_BY_SOURCE_DATA

BLOCKED_BY_PARSING

BLOCKED_BY_EXISTING_DB_CONFLICT

Include the reasons.

==================================================
STOP CONDITION
==================================================

STOP when:

1. the existing DuckDB has been inspected
2. the raw CAM repository has been inventoried
3. CAM content has been parsed into searchable passages
4. CAM-derived Parquet/index artifacts exist
5. those artifacts are integrated non-destructively with the existing DuckDB architecture
6. the read-only database inspector exists
7. NVIDIA retrieval has been tested
8. the final integration report has been produced

Do NOT proceed to relationship extraction.

The next phase will take the retrieved passages for a seed entity such as NVIDIA and determine which passages actually establish evidence-backed relationships between entities.