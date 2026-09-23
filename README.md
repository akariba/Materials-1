CCR RELATIONSHIP FOUNDATION — RELATIONSHIP UNIVERSE MODEL

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md

Inspect the current schema of:

backend/data/ccr_relationship_intelligence.sqlite3

Also inspect existing Phase-3 tables before creating anything.

Do NOT duplicate tables that already provide the required capability.

No SEC calls.
No GLEIF calls.
No Web calls.
No Helix/AI calls.
No frontend work.
No relationship discovery yet.

OBJECTIVE

Prepare the canonical entity model so future externally discovered entities
can participate in CCR relationships even when they are not CCR exposure
subjects.

The target model is:

CCR SUBJECT
    ↓
CANONICAL ENTITY
    ↔
RELATIONSHIP
    ↔
CANONICAL / EXTERNAL ENTITY

A relationship endpoint must NOT require membership in ccr_subjects.

==================================================
1. ENTITY UNIVERSE
==================================================

Use the existing:

entity_registry

as the universal entity table.

Confirm it supports:

MASTER_BACKED
DETERMINISTIC_MASTER_MATCH
CCR_ONLY_ENTITY
EXTERNAL_ENTITY

Do not populate fake external entities.

Document:

ccr_subject != entity

A CCR subject belongs to the CCR source population.

An entity is a node in the broader relationship universe.

==================================================
2. EXTERNAL ENTITY CONTRACT
==================================================

Define how a future SEC/GLEIF/Web discovered company becomes:

EXTERNAL_ENTITY

Required fields/concepts:

entity_key
entity_class = EXTERNAL_ENTITY

legal_name
normalized_name
country

lei
cik
ticker
website/domain where verified

identity_quality
identity_status

created_from_source
created_from_research_run

review_required

Do NOT create external entities from local similarity/correlation alone.

External entities require defensible identity evidence.

==================================================
3. ENTITY IDENTIFIERS
==================================================

Inspect existing identifier_aliases / external_identity tables.

Reuse them if possible.

Ensure the model can represent multiple identifiers per entity:

GFCID
CAGID
LEI
CIK
TICKER
DOMAIN
LEGAL_NAME_ALIAS
OTHER

Fields/concepts:

entity_key
identifier_type
identifier_value
normalized_value

source
quality
verified
is_primary

Do not create uniqueness rules that incorrectly collapse entities.

LEI and CIK may be strongly identifying where valid.

CAGID remains non-unique.

==================================================
4. ENTITY NAME ALIASES
==================================================

Ensure the model supports:

official legal name
former name
trade name
source alias
normalized name

A name alias does NOT automatically create entity equivalence.

Persist:

entity_key
name
normalized_name
alias_type
source
verified

==================================================
5. RELATIONSHIP TAXONOMY
==================================================

Create or validate a configurable relationship type catalogue.

Initial types:

PARENT
SUBSIDIARY
ULTIMATE_PARENT

SUPPLIER
CRITICAL_SUPPLIER
CUSTOMER
KEY_CUSTOMER

INVESTOR
SPONSOR

LENDER
FINANCING_RELATIONSHIP

STRATEGIC_PARTNER
JOINT_VENTURE

TECHNOLOGY_PROVIDER
TECHNOLOGY_DEPENDENCY

INFRASTRUCTURE_PROVIDER
INFRASTRUCTURE_DEPENDENCY

SERVICE_PROVIDER

MANUFACTURING_PARTNER
DISTRIBUTOR
SOURCE_OF_INPUTS

OTHER_EVIDENCE_BACKED_RELATIONSHIP

Taxonomy availability does NOT assert that a relationship exists.

==================================================
6. RELATIONSHIP ENDPOINT MODEL
==================================================

Create or adapt a relationship observation structure so every relationship
can reference:

subject_entity_key
related_entity_key

Both foreign keys point to entity_registry.

Neither endpoint must belong to ccr_subjects.

Relationship direction must be explicit.

Examples:

A --SUPPLIER_OF--> B

A --PARENT_OF--> B

A --TECHNOLOGY_PROVIDER_TO--> B

Do not infer inverse meaning silently.

==================================================
7. RELATIONSHIP OBSERVATION STATES
==================================================

Use explicit states:

EXTERNAL_OBSERVATION
PROPOSAL_PENDING_REVIEW
CONFIRMED
CONFLICT
HISTORICAL
REJECTED

Do not store local research candidates here.

Research candidates remain in the existing correlation candidate layer.

Candidate != relationship observation.

==================================================
8. EVIDENCE REQUIREMENT
==================================================

A relationship observation must be attachable to one or more evidence records.

Inspect existing:

source_documents
evidence_snippets
research_runs

Reuse these.

Ensure future relationship observations can link to:

evidence_id
source_document_id
research_run_id

A relationship cannot become CONFIRMED merely from:

same sector
same country
same name pattern
candidate score
AI statement without source evidence

==================================================
9. GLEIF STRUCTURAL OBSERVATIONS
==================================================

Inspect existing:

gleif_relationship_observations

Do NOT merge them automatically into confirmed generic PARENT relationships.

Define the future mapping contract:

GLEIF direct accounting consolidating parent
→ candidate PARENT structural observation

GLEIF ultimate accounting consolidating parent
→ candidate ULTIMATE_PARENT structural observation

Preserve exact GLEIF semantics and evidence source.

No network calls in this task.

==================================================
10. CCR MEMBERSHIP VIEW
==================================================

Create a simple query/view that answers:

Is this entity a CCR subject?

For example:

entity_ccr_membership

Fields:

entity_key
is_ccr_subject
ccr_subject_key
current_ccr_scope
review_required

External entities should return:

is_ccr_subject = false

This will make frontend graph filtering straightforward later.

==================================================
11. VALIDATION FIXTURES
==================================================

Use database-only test fixtures / transactions.

Do NOT invent production relationships.

Prove the schema can represent:

A. CCR entity → CCR entity relationship

B. CCR entity → external entity relationship

C. external entity → CCR entity relationship

D. external entity → external entity relationship

Rollback or isolate fixtures from production business tables after tests.

Production relationship count must remain unchanged.

==================================================
12. TESTS
==================================================

Prove:

CCR subjects = 16,769 unchanged

Canonical entities = 16,767 unchanged

Production EXTERNAL_ENTITY count = 0

Production relationships created = 0

A relationship endpoint can reference an external entity

A relationship endpoint does not require ccr_subject membership

Research candidate cannot be treated as relationship

CAGID remains non-unique

Review-required CCR subjects remain research-disabled

Foreign keys pass

Source files unchanged

No external network calls

==================================================
13. REPORT
==================================================

Create:

backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md

Include:

entity vs CCR-subject distinction
external entity contract
identifier model
relationship taxonomy
relationship endpoint model
evidence requirements
GLEIF mapping contract
CCR membership view
tests

FINAL RESPONSE:

CCR RELATIONSHIP UNIVERSE MODEL: PASS / FAIL

CCR SUBJECTS:
actual

CANONICAL ENTITIES:
actual

EXTERNAL ENTITIES CREATED:
0 / FAIL

PRODUCTION RELATIONSHIPS CREATED:
0 / FAIL

CCR→CCR ENDPOINT TEST:
PASS / FAIL

CCR→EXTERNAL ENDPOINT TEST:
PASS / FAIL

EXTERNAL→CCR ENDPOINT TEST:
PASS / FAIL

EXTERNAL→EXTERNAL ENDPOINT TEST:
PASS / FAIL

CANDIDATE / RELATIONSHIP SEPARATION:
PASS / FAIL

EVIDENCE LINK CONTRACT:
PASS / FAIL

FOREIGN KEYS:
PASS / FAIL

EXTERNAL CALLS:
0 / FAIL

REPORT:
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md

STOP.
