Do not change code yet.

Confirm whether the CAM indexing repair is actually complete.

1. Report final parsing coverage:
   - total CAM documents
   - PDF CAMs
   - PDFs successfully parsed
   - PDFs parsed with fallback
   - PDFs still failed
   - image-only/OCR-required PDFs
   - DOCX/TXT successfully parsed

2. Run NVIDIA retrieval through BOTH:
   A. plain passage-text search
   B. cam_entity_mentions structured retrieval

3. Reconcile every NVIDIA result.

For each returned result show:

query
mentioned_name
canonical_entity_id
CAGID
GFCID
filename
page
section
exact passage
match_method
resolution_status

4. Investigate this specific suspicious behavior:
A search for NVIDIA appears to return a row where:
mentioned_name = "CAGID"

Determine whether:
- this is only a display/serialization issue,
- the wrong entity mention is attached to the passage,
- the parser interpreted a field name such as CAGID as an entity,
- or the search function is mixing passage-text results with entity-mention results.

Do not guess.

5. NVIDIA should resolve to NVIDIA Corporation's canonical entity consistently wherever the passage actually refers to NVIDIA.

6. Report:
   text-search NVIDIA passages
   structured-mention NVIDIA passages
   correctly resolved NVIDIA mentions
   ambiguous NVIDIA mentions
   incorrect NVIDIA mentions
   missing NVIDIA mentions

7. Do not perform relationship extraction yet.

Return exactly one:

CAM_INDEX_READY
CAM_INDEX_READY_WITH_WARNINGS
BLOCKED_BY_ENTITY_MENTION_INDEX
BLOCKED_BY_PARSING