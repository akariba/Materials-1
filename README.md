DO NOT IMPLEMENT FROM THE OCTOBER 1 AUDIT DIRECTLY.

That file is historical and partially superseded.

Use today's cleanup addendum and current runtime as authoritative.

Perform a bounded CURRENT-vs-HISTORICAL reconciliation only.

==================================================
1. CURRENT STATE FIRST
==================================================

Inspect the CURRENT production runtime and report:

- current production relationship artifact path
- current row count
- current schema
- current relationship types
- DIRECT / INDIRECT / HIDDEN counts
- evidence statuses
- source types
- provenance fields
- scoring/weight fields
- canonical entity ID fields
- whether multiple edge types per pair are preserved

Do not use October 1 counts as current facts.

==================================================
2. RECOVER ONLY ANALYTICAL LOGIC
==================================================

From the historical implementation identify the exact reusable code for:

- canonical relationship taxonomy
- base relationship weights
- source-quality weights
- recency multiplier
- financial-materiality multiplier
- relationship score formula
- hierarchy / parent / ultimate-parent logic
- direct / indirect / hidden classification
- typed path logic
- candidate scoring / ranking

For each item classify:

KEEP_CURRENT
REUSE_HISTORICAL_LOGIC
ADAPT
DO_NOT_RESTORE

==================================================
3. DO NOT RESTORE THESE HISTORICAL BEHAVIORS
==================================================

Explicitly reject:

- monolithic old src/main.py architecture
- old four-company sample mode
- duplicate-CAGID row processing
- old demo runtime paths
- placeholder extractors/checkers
- verify=False TLS behavior
- RPR-named runtime dependencies
- silent unknown-type fallback weight of 0.3
- old generated-report architecture
- old 59-row output as source of truth

==================================================
4. TAXONOMY NORMALIZATION
==================================================

The old audit shows noncanonical values such as:

named_supplier/customer
board_interlock / key_person_overlap
M&A activity (divestiture)
M&A activity (acquisition)
acquisition
debt/financing

Do not assign these a generic 0.3 score.

Create/reuse explicit mapping:

raw_relationship_type
→ canonical_relationship_type
→ taxonomy_status

taxonomy_status:

CANONICAL
NORMALIZED_ALIAS
REVIEW_REQUIRED
UNSUPPORTED

Only CANONICAL or validated NORMALIZED_ALIAS values may enter verified graph scoring.

==================================================
5. CURRENT CAM IS PRIMARY INTERNAL EVIDENCE
==================================================

The historical audit says CAM was not active in the old extraction path.

That is obsolete.

Current architecture must use:

CAM evidence index
+
canonical entity resolution
+
existing relationship artifact
+
external evidence
+
R2D2
+
Opus refinement

CAM must not be omitted.

==================================================
6. SECURITY / CONFIG CLEANUP
==================================================

Do not restore:

verify=False

or old RPR environment-variable dependencies.

Report any remaining references to:

RPR_VERTEX_BASE_URL
RPR_STEP25_MAX_CONCURRENT
RPR-specific paths/configuration

and classify whether they are still active.

Do not change them yet unless clearly safe and CCR-specific replacement already exists.

==================================================
7. ENTITY DUPLICATION
==================================================

The historical audit identified duplicate CAGIDs in the old reference list.

Check the CURRENT canonical entity universe.

Do not assume this old defect still exists.

Report:

physical rows
unique CAGIDs
duplicate CAGID count
whether current canonical loader deduplicates correctly

Do not change canonicalization unless current evidence proves a defect.

==================================================
8. FINAL DELTA REPORT
==================================================

Return:

CURRENT RELATIONSHIP ARTIFACT:
<path / rows>

CURRENT TAXONOMY:
<count>

HISTORICAL LOGIC TO REUSE:
<list>

HISTORICAL LOGIC TO REJECT:
<list>

CURRENT CAM ACTIVE:
YES/NO

CURRENT DUPLICATE-CAGID ISSUE:
YES/NO

CURRENT RPR RUNTIME DEPENDENCY:
YES/NO

CURRENT verify=False:
YES/NO

SCORING:
CURRENT / ADAPT HISTORICAL / MISSING

INDIRECT PATH LOGIC:
CURRENT / ADAPT HISTORICAL / MISSING

HIERARCHY:
CURRENT / ADAPT HISTORICAL / MISSING

STOP after this report.

Do not edit frontend.
Do not run broad enrichment.
Do not create another relationship store.