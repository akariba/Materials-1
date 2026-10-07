You are continuing work on the existing CCR Relationship Intelligence repository.

The CAM indexing phase has already been implemented.

Current state:

- CAM evidence indexing layer exists.
- cam_documents.parquet exists.
- cam_passages.parquet exists.
- cam_entity_mentions.parquet exists.
- DuckDB/Parquet integration exists.
- inspect_db.py exists.
- search_cam.py exists.
- NVIDIA canonical entity resolution works.
- deterministic text retrieval works.
- relationship extraction has NOT been run yet.

The current blocker is:

BLOCKED_BY_PARSING

because PDF CAM documents were intentionally skipped/guarded to prevent parser stalls.

Current observed results include approximately:

- 66 CAM documents
- 29 parsed successfully
- 37 failed/skipped PDFs
- 1053 passages generated

A second issue exists:

- NVIDIA canonical identity resolves successfully.
- plain passage-text search finds NVIDIA candidate passages.
- structured entity-mention retrieval currently returns fewer or zero matching passages.

This is an IMPLEMENTATION/FIX task.

Do NOT perform another architecture audit.

Do NOT proceed to relationship extraction.

The objective is to make the CAM index complete and reliable before relationship extraction starts.

==================================================
1. FIX PDF PARSING SAFELY
==================================================

Inspect the existing PDF parsing implementation.

Identify the exact reason PDF parsing was guarded/disabled.

Determine whether the issue is:

- parser library stall
- specific malformed PDFs
- encrypted PDFs
- scanned/image-only PDFs
- extremely large PDFs
- table-heavy PDFs
- timeout handling
- multiprocessing/thread interaction
- file corruption
- other

Do not guess.

Implement bounded PDF parsing.

Requirements:

- every PDF must be attempted individually
- one bad PDF must never hang the full indexing run
- use a strict per-file timeout
- record parser start/end time
- record parser failure reason
- preserve page provenance
- preserve original text where available
- do not summarize or rewrite content
- do not silently skip failures

Use the existing parser where possible.

Only introduce a fallback parser if required.

Do NOT use OCR unless a PDF is genuinely image-only and the repository already has an approved OCR path.

If OCR is not available/approved, mark image-only PDFs clearly as requiring OCR rather than inventing text.

==================================================
2. ADD PARSER FALLBACK LOGIC
==================================================

For each PDF attempt:

PRIMARY PARSER
→ if success, keep result

If timeout/failure:
→ try bounded fallback parser if available and appropriate

If fallback also fails:
→ record explicit failure

Suggested statuses:

PARSED_PRIMARY
PARSED_FALLBACK
IMAGE_ONLY_NEEDS_OCR
ENCRYPTED
CORRUPT
TIMEOUT
EMPTY_TEXT
FAILED_OTHER

Every failure must retain:

document_id
filename
error_type
error_message
parser_used
elapsed_time

==================================================
3. REBUILD ONLY THE PDF PORTION
==================================================

Do not unnecessarily reprocess working DOCX/TXT/JSON documents.

Process the previously failed/skipped PDF CAMs.

Merge the successful PDF outputs back into:

cam_documents.parquet
cam_passages.parquet

non-destructively.

Preserve stable document IDs.

Do not duplicate documents or passages.

==================================================
4. VERIFY PAGE/SECTION PROVENANCE
==================================================

For successfully parsed PDFs verify:

- document_id
- filename
- page_number
- sequence_number
- section/header if detectable
- exact passage text
- source_location

No PDF passage should lose its source document reference.

Page number must be present whenever technically available.

==================================================
5. FIX ENTITY-MENTION INDEX CONSISTENCY
==================================================

NVIDIA currently resolves correctly in the canonical entity master, but structured entity-mention retrieval does not fully match transparent passage-text retrieval.

Investigate why.

Trace:

canonical NVIDIA identity
→ legal name / aliases
→ passage matching
→ entity mention creation
→ canonical entity resolution
→ cam_entity_mentions
→ search_cam.py

Identify the exact mismatch.

Possible causes to inspect:

- case normalization
- punctuation
- NVIDIA vs NVIDIA Corporation
- alias handling
- mention extraction rules
- canonical name normalization
- mention resolver thresholds
- missing mention creation
- passage filtering
- CAGID/GFCID join mismatch

Do not loosen matching globally without evidence.

==================================================
6. REQUIRE RETRIEVAL CONSISTENCY
==================================================

After repair, run NVIDIA again.

Compare:

A. transparent passage-text search
B. structured cam_entity_mentions retrieval

Every obvious deterministic NVIDIA mention found by text search should either:

- appear in structured mention retrieval, OR
- have an explicit documented reason why it is excluded.

Generate a reconciliation table:

document_id
passage_id
text_search_match
mention_index_match
canonical_entity_id
resolution_status
difference_reason

==================================================
7. REBUILD ENTITY-MENTION INDEX
==================================================

Rebuild only the necessary entity-mention records after fixing the bug.

Do not recreate the canonical entity master.

Do not modify CAGID/GFCID source-of-truth data.

Preserve:

MATCHED
AMBIGUOUS
UNRESOLVED

Do not force ambiguous matches.

==================================================
8. RUN COMPLETE INDEX VALIDATION
==================================================

After the PDF repair and mention-index repair, report:

CAM documents discovered
PDF documents
DOCX documents
other supported CAM documents

parsed successfully
failed
parsed with fallback
image-only needing OCR
timeouts
corrupt/encrypted

passages generated

entity mentions generated

MATCHED mentions
AMBIGUOUS mentions
UNRESOLVED mentions

missing page provenance
missing document provenance
duplicate passage IDs
duplicate document IDs

==================================================
9. NVIDIA SMOKE TEST
==================================================

Run:

python search_cam.py NVIDIA

Report:

canonical seed resolution
canonical_entity_id
CAGID
GFCID
legal_name

candidate documents from transparent text search
candidate passages from transparent text search

candidate documents from entity-mention retrieval
candidate passages from entity-mention retrieval

reconciliation differences

Show sample passages with:

filename
document_id
page
section
passage_id
exact text
retrieval method

Do NOT claim relationships yet.

==================================================
10. DO NOT DO THESE THINGS
==================================================

Do NOT:

- perform relationship extraction
- run LLM MapReduce
- add semantic relationship inference
- run SEC enrichment
- run web enrichment
- calculate graph distance
- calculate Jaccard
- add hidden relationships
- redesign frontend
- migrate database
- rewrite canonical entity logic
- change existing business relationship taxonomy

This phase is only:

PDF PARSING REPAIR
+
ENTITY-MENTION INDEX REPAIR
+
INDEX VALIDATION

==================================================
11. FINAL STATUS
==================================================

Return exactly one of:

CAM_INDEX_READY

CAM_INDEX_READY_WITH_WARNINGS

BLOCKED_BY_PDF_PARSER

BLOCKED_BY_IMAGE_ONLY_PDFS

BLOCKED_BY_ENTITY_MENTION_INDEX

BLOCKED_BY_SOURCE_DATA

BLOCKED_BY_UNKNOWN_ERROR

CAM_INDEX_READY should only be returned if:

1. all parseable CAM documents are indexed,
2. PDF failures are explicitly classified,
3. one bad PDF cannot stall the pipeline,
4. NVIDIA transparent search and entity-mention search are materially consistent,
5. provenance remains intact.

==================================================
STOP CONDITION
==================================================

STOP once:

- PDF parsing is bounded and reliable,
- failed PDFs are classified,
- the index is rebuilt,
- entity-mention retrieval is repaired,
- NVIDIA retrieval consistency is verified,
- final index-quality metrics are produced.

Do NOT continue to relationship extraction.

The next phase will perform evidence-backed relationship extraction on retrieved passages.