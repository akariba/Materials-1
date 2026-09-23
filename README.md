CCR DATA FOUNDATION — CANONICAL SUBJECT / ENTITY MIGRATION

Work only in the CURRENT CCR repository.

Read:

analysis/output/CCR_IDENTITY_EXCEPTION_DEEP_DIVE.md
analysis/output/CCR_EXPOSURE_ACTIVITY_ANALYSIS.md
analysis/output/ccr_identity_exception_resolution.csv
analysis/output/ccr_historical_conflict_groups.csv
analysis/output/ccr_exposure_row_patterns.csv

Inspect:

backend/data/ccr_relationship_intelligence.sqlite3

Do not modify:

Customer_latest.parquet
thousandClients.csv
backend/data/ccr_clients.sqlite3

No frontend work.
No SEC.
No GLEIF.
No Web.
No AI.
No relationship creation.

OBJECTIVE

Migrate the validated identity/exposure conclusions into the CCR relationship
database using an ADDITIVE migration.

==================================================
1. CCR SUBJECT REGISTRY
==================================================

Create:

ccr_subjects

Exactly one row per source CCR GFCID.

Expected:
16,769 rows.

Fields:

ccr_subject_key
source_gfcid
source_cagid
source_legal_name

entity_key nullable

identity_class
resolution_status
resolution_method

current_ccr_scope
current_exposure_present

credit_managed_flag
credit_managed_semantics

research_allowed
review_required

created_at

Rules:

current_ccr_scope = true
for all subjects present in thousandClients.csv.

current_exposure_present = true
means only that at least one row exists in this source extract.

Do NOT create ACTIVE_CLIENT or INACTIVE_CLIENT.

Set:

credit_managed_semantics =
'MANAGED_SCOPE_ATTRIBUTE_UNCONFIRMED'

==================================================
2. ENTITY REGISTRY
==================================================

Create or extend:

entity_registry

Entity classes:

MASTER_BACKED
DETERMINISTIC_MASTER_MATCH
CCR_ONLY_ENTITY
EXTERNAL_ENTITY

Do not populate EXTERNAL_ENTITY yet.

Populate:

16,755 MASTER_BACKED exact matches

4 DETERMINISTIC_MASTER_MATCH records

8 CCR_ONLY_ENTITY records

Expected canonical entities:

16,767

Fields should include:

entity_key
entity_class

master_gfcid
master_cagid

legal_name
normalized_name

country
industry
sector
lei

identity_quality
research_eligibility

created_at

Do not fabricate missing master fields.

==================================================
3. CCR-ONLY ENTITY KEYS
==================================================

For the 8 CCR-only subjects create stable non-master keys such as:

CCRONLY:<source_gfcid>

Do not create fake master GFCIDs.

Classify research readiness carefully.

Masked/private-bank subjects:
INSUFFICIENT_IDENTITY

Other sufficiently identified CCR-only subjects:
DISCOVERY_REQUIRED

==================================================
4. REVIEW-REQUIRED SUBJECTS
==================================================

Keep both unresolved ambiguous subjects in ccr_subjects.

Do not select a canonical master entity.

Set:

entity_key = NULL where appropriate
review_required = true
research_allowed = false
resolution_status = REVIEW_REQUIRED

Create:

identity_candidate_matches

Store all competing master candidates and reasons.

==================================================
5. EXPOSURE SOURCE ROWS
==================================================

Preserve all 25,000 rows.

Do not deduplicate.

Each row must link to:

ccr_subject_key

and, where trusted:

entity_key

Treat row grain as:

SOURCE_EXPOSURE_LINE

not as guaranteed one-row-per-facility.

Preserve existing source fields including:

FACILITY_ID
FACILITY_TYPE
FACILITY_DESCRIPTION

DIRECT_EXPOSURE
CONTINGENT_EXPOSURE
TOTAL_EXPOSURE
OSUC_AMOUNT
OUTSTANDING_AMOUNT
MTM_AMOUNT

RISK_RATING

country / region / industry classifications

==================================================
6. EXPOSURE SEMANTICS
==================================================

Persist explicit metadata:

currency = UNKNOWN
amount_unit = UNKNOWN
amount_as_of_period = UNKNOWN
additive_semantics = UNKNOWN
facility_lifecycle_status = UNKNOWN

Do not aggregate monetary values.

Safe structural aggregates are allowed:

exposure_row_count
distinct_facility_id_count
distinct_facility_type_count

Label these as structural counts.

==================================================
7. DUPLICATE HANDLING
==================================================

Do not delete the 8 exact duplicate groups / 16 rows.

Persist a diagnostic flag such as:

exact_source_duplicate_candidate

This means:

potential duplicate requiring source-owner clarification.

It does NOT mean:

delete.

==================================================
8. IDENTIFIER RULES
==================================================

Enforce/document:

GFCID:
strong master entity reference

CAGID:
grouping identifier, not unique entity key

legal_entity_id:
not unique entity key

No UNIQUE constraint on:

CAGID
legal_entity_id

Do not collapse true multi-entity records.

==================================================
9. MASTER CONFLICT REGISTRY
==================================================

Persist the validated current-snapshot conflict groups.

Categories:

COSMETIC_NAME_VARIANT
SHARED_IDENTIFIER
TRUE_MULTI_ENTITY
HIERARCHY_PROPAGATION
INSUFFICIENT_INFORMATION
PLACEHOLDER_NAME

Call them:

CURRENT_SNAPSHOT_CONFLICTS

not historical identifier reuse.

==================================================
10. VALIDATION
==================================================

Prove:

CCR source subjects = 16,769

Canonical entities = 16,767

Master-backed exact = 16,755

Deterministic master matches = 4

CCR-only entities = 8

Review-required subjects = 2

Exposure rows = 25,000

All exposure rows linked to ccr_subject_key = 25,000

Review-required research-enabled = 0

ACTIVE_CLIENT rows created = 0

INACTIVE_CLIENT rows created = 0

Monetary aggregation created = 0

Source duplicate rows deleted = 0

Relationships created = 0

External calls = 0

Foreign-key integrity = PASS

Source files unchanged = PASS

==================================================
11. REPORT
==================================================

Create:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md

Include:

population bridge
schema added
entity classes
CCR-only treatment
review-required treatment
exposure row treatment
duplicate handling
activity/scope semantics
credit_managed_flag treatment
amount restrictions
tests

FINAL RESPONSE:

CCR CANONICAL DATA MODEL: PASS / FAIL

CCR SUBJECTS:
actual

CANONICAL ENTITIES:
actual

MASTER EXACT:
actual

DETERMINISTIC:
actual

CCR ONLY:
actual

REVIEW REQUIRED:
actual

EXPOSURE ROWS:
actual

EXPOSURE ROWS LINKED TO SUBJECT:
actual

ACTIVE/INACTIVE STATES:
0 / FAIL

MONETARY AGGREGATION:
0 / FAIL

DUPLICATE SOURCE ROWS DELETED:
0 / FAIL

REVIEW SUBJECTS RESEARCH ENABLED:
0 / FAIL

RELATIONSHIPS CREATED:
0 / FAIL

EXTERNAL CALLS:
0 / FAIL

FOREIGN KEYS:
PASS / FAIL

REPORT:
backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md

STOP.
