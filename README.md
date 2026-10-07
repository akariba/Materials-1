You are continuing work on the existing CCR Relationship Intelligence repository.

The CAM indexing and PDF-repair phases are already complete enough to proceed with one remaining blocker:

BLOCKED_BY_ENTITY_MENTION_INDEX

Do NOT repeat the architecture audit.
Do NOT redesign the application.
Do NOT perform relationship extraction yet.
Do NOT perform SEC or web enrichment yet.

This is a targeted IMPLEMENTATION/FIX task.

Current observed state:

- 66 CAM documents
- 37 PDFs
- 27 PDFs parsed successfully
- 10 PDFs timed out
- 29 DOCX/TXT parsed successfully
- 3,015 passages
- 1,752 entity mentions
- NVIDIA transparent text retrieval finds 33 passages across 12 documents
- Canonical NVIDIA seed resolution works
- Exact passage provenance is intact
- The current blocker is entity-mention resolution

Two specific issues have been observed:

1. Field/schema labels such as "CAGID" can be incorrectly treated as entity mentions.
2. Legal-name normalization is too aggressive. For example:
   NVIDIA Corporation
   NVIDIA Limited
   NVIDIA Corp
   can collapse to the same normalized key such as "nvidia", causing valid exact-name matches to become ambiguous.

The objective of this task is:

Fix entity mention candidate generation and resolution so that valid company mentions resolve conservatively and deterministically without false positives.

==================================================
1. TRACE CURRENT ENTITY-MENTION LOGIC
==================================================

Inspect the current code responsible for:

passage text
→ mention candidate extraction
→ name normalization
→ canonical candidate lookup
→ ambiguity handling
→ cam_entity_mentions output

Identify the exact files/functions involved.

Do not change code until the current logic is traced.

==================================================
2. FIX FALSE ENTITY CANDIDATES
==================================================

Create a conservative exclusion mechanism for obvious schema/field labels.

At minimum, labels such as these must never become entity candidates merely because they appear in text:

CAGID
GFCID
CIK
LEI
ISIN
CUSIP
BBG_Ticker
Ticker
Identifier
Entity ID
Reference ID
Document ID
Record Type
Source
Section
Page
Rating
Currency
Country

Do not hard-code only these exact examples if the repository has a better field-label registry.

Prefer reusing schema metadata or a controlled exclusion set.

The exclusion must apply only to field labels / metadata tokens, not to genuine company names that happen to contain similar text.

==================================================
3. CHANGE RESOLUTION PRECEDENCE
==================================================

Implement conservative resolution precedence.

Use this order:

1. Exact identifier match
2. Exact canonical legal-name match
3. Exact validated alias match
4. Case-insensitive exact legal-name match
5. Case-insensitive exact alias match
6. Controlled normalized-name match
7. Controlled fuzzy/high-confidence fallback if already part of the architecture

Important:

EXACT CANONICAL LEGAL NAME MUST WIN BEFORE SUFFIX-STRIPPED NORMALIZATION.

Example:

"NVIDIA Corporation"

must resolve directly to the canonical record whose legal_name is exactly NVIDIA Corporation if that record is unique.

Do not first normalize it to "nvidia" and then declare ambiguity among multiple NVIDIA-family entities.

==================================================
4. KEEP NORMALIZATION CONSERVATIVE
==================================================

Inspect current normalization logic.

Do not globally remove legal suffixes too early.

If normalization strips:

Corporation
Corp
Limited
Ltd
Inc
LLC
PLC
SA
AG
etc.

then use suffix-stripped normalization only as a fallback candidate-generation step.

Do not use the suffix-stripped form as the primary identity key.

Preserve both:

raw_name
normalized_full_name
normalized_suffix_stripped_name

or the repository-equivalent structure.

==================================================
5. HANDLE SHORT / PARTIAL NAMES CORRECTLY
==================================================

A mention such as:

"NVIDIA"

may legitimately match multiple canonical entities.

Do not force it to NVIDIA Corporation unless there is additional valid evidence such as:

- validated alias mapping
- exact identifier in the same passage/context
- deterministic client/CAGID context already attached to the source
- other existing authoritative mapping

If multiple valid canonical entities remain:

resolution_status = AMBIGUOUS

If none remain:

resolution_status = UNRESOLVED

Do not use the fact that NVIDIA is the current seed query to force resolution.

==================================================
6. FIX CAM_ENTITY_MENTIONS OUTPUT
==================================================

Rebuild the affected mention-index rows.

Each row should retain:

mention_id
passage_id
document_id
mentioned_name
normalized_mentioned_name
canonical_entity_id
CAGID
GFCID
match_method
match_score if applicable
resolution_status
ambiguity_reason

The match_method should clearly distinguish:

exact_identifier
exact_legal_name
exact_alias
case_insensitive_legal_name
case_insensitive_alias
normalized_name
fuzzy
other

==================================================
7. NVIDIA RECONCILIATION TEST
==================================================

Run NVIDIA retrieval again after the fix.

Use both:

A. transparent passage-text search
B. structured cam_entity_mentions retrieval

For every NVIDIA-related passage found by transparent text search, classify the structured result as:

MATCHED
AMBIGUOUS
UNRESOLVED
EXCLUDED_AS_FALSE_ENTITY_CANDIDATE
MISSING_FROM_MENTION_INDEX

Produce a reconciliation table with:

document_id
filename
page
section
passage_id
exact passage text
query_term
mentioned_name
canonical_entity_id
CAGID
GFCID
match_method
resolution_status
ambiguity_reason
text_search_found
mention_index_found

==================================================
8. SPECIFIC NVIDIA EXPECTATION
==================================================

If the passage contains exactly:

"NVIDIA Corporation"

and there is one canonical legal-name record exactly equal to NVIDIA Corporation,
then the result should be MATCHED to that record.

If the passage contains only:

"NVIDIA"

and multiple canonical entities remain after authoritative alias/identifier checks,
then AMBIGUOUS is acceptable.

Do not force all NVIDIA-family mentions to the same entity.

==================================================
9. FALSE-CANDIDATE TEST
==================================================

Explicitly test passages containing labels such as:

CAGID:
GFCID:
LEI:
CIK:
ISIN:

Confirm these are not emitted as legal entity mentions unless there is some separate legitimate entity-name context.

Report how many false schema-label mentions were removed.

==================================================
10. REGRESSION CHECK
==================================================

Ensure the fix does not break:

- exact identifier matching
- exact legal-name matching for other companies
- alias matching
- existing canonical entity IDs
- CAGID/GFCID joins
- document/passsage provenance
- DuckDB/Parquet compatibility

Run the relevant existing tests.

Add narrowly scoped tests for:

- exact legal name beats normalized ambiguity
- short name remains ambiguous when appropriate
- field labels are excluded
- alias still resolves correctly
- identifier match still has highest priority

==================================================
11. DO NOT CHANGE THESE
==================================================

Do NOT:

- modify canonical source-of-truth data
- merge or split canonical entities
- change CAGID/GFCID master data
- change relationship extraction prompts
- perform relationship extraction
- add MapReduce
- add SEC
- add web
- change graph metrics
- change frontend
- migrate database
- force ambiguous names to the current seed entity

This task is only:

MENTION CANDIDATE FIX
+
RESOLUTION PRECEDENCE FIX
+
NVIDIA RECONCILIATION
+
REGRESSION TESTING

==================================================
12. FINAL REPORT
==================================================

Report:

1. Root cause
   - why CAGID became an entity mention
   - why NVIDIA Corporation became ambiguous

2. Code changed
   - exact files/functions

3. Mention index results
   - total mentions before
   - total mentions after
   - false field-label mentions removed
   - MATCHED
   - AMBIGUOUS
   - UNRESOLVED

4. NVIDIA reconciliation
   - transparent text-search passages
   - structured mention-index passages
   - correctly matched NVIDIA Corporation mentions
   - ambiguous short NVIDIA mentions
   - unresolved NVIDIA mentions
   - missing mentions
   - false CAGID/GFCID/etc. mentions removed

5. Regression tests
   - tests run
   - tests passed
   - tests failed

6. Final status

Return exactly one of:

CAM_INDEX_READY

CAM_INDEX_READY_WITH_WARNINGS

BLOCKED_BY_ENTITY_MENTION_INDEX

BLOCKED_BY_REGRESSION

BLOCKED_BY_UNKNOWN_ERROR

CAM_INDEX_READY should only be returned if:

- exact legal-name resolution works correctly,
- schema labels are no longer treated as entities,
- NVIDIA text retrieval and mention-index retrieval reconcile materially,
- ambiguous short names remain ambiguous rather than being forced,
- existing identifier/entity resolution behavior remains intact.

==================================================
STOP CONDITION
==================================================

STOP after the entity-mention index is repaired and NVIDIA reconciliation passes.

Do NOT proceed to relationship extraction.

The next phase will use the corrected retrieved passages for evidence-backed relationship extraction.