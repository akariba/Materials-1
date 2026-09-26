CCR — CLIENT CORRELATION
V1 FOUNDATION MIGRATION — STAGE 1
ADDITIVE DOMAIN FOUNDATION + SCHEMA FOUNDATION

You are now implementing the first real CCR V1 architecture change after the completed CCR V1 Architecture Reconciliation Audit.

IMPORTANT:
The reconciliation audit has ALREADY been completed.

Do NOT rerun the audit.

Before making changes, read the completed reconciliation report in the repository and use its ACTUAL findings as the implementation baseline.

Expected report location is approximately:

backend/data/CCR_V1_ARCHITECTURE_RECONCILIATION_AUDIT.md

If the exact filename/path differs, locate the completed CCR V1 reconciliation report and use that.

The report is authoritative for:

- current schema version and tables;
- current Stage 2 relationship structures;
- exact 3M pilot state;
- evidence/document-retention findings;
- identity structures;
- current APIs;
- current tests;
- traversal/frontier structures;
- reusable components;
- components requiring adaptation;
- historical/audit-only structures.

Do not replace repository facts with assumptions from this prompt.

======================================================================
1. PRODUCT BOUNDARY
======================================================================

This project is:

CCR — CLIENT CORRELATION

Use CCR terminology in ALL newly created code, configuration, documentation, reports, classes and comments.

For this stage do NOT introduce or use unrelated product terminology.

The active CCR capability model is:

CLIENT UNIVERSE
CLIENT ENRICHMENT
ENTITY RESOLUTION
RELATIONSHIP RESEARCH
EVIDENCE
RELATIONSHIP GRAPH
CLIENT CONNECTIONS

The authoritative Client Universe remains:

backend/Customer_latest.parquet

approximately:

3,670,650 client records
3,670,650 unique GFCIDs

The existing Client Universe database/repository remains authoritative for internal client records.

DO NOT redesign or rebuild the Client Universe in this stage.

DO NOT introduce another client population.

DO NOT modify source-master rows.

======================================================================
2. PURPOSE OF THIS STAGE
======================================================================

The current Stage 2 implementation successfully proved important controls:

- deterministic/bounded processing;
- no fuzzy automatic merging;
- candidate retention;
- generic-descriptor exclusion;
- provider auditing;
- source-master immutability;
- replay/idempotence controls;
- no synthetic direct relationships;
- evidence-gated acceptance;
- bounded traversal.

However, its domain structures were built incrementally around the earlier pilot workflow.

CCR V1 now needs a stable foundation that separates:

CLIENT RECORD

from

LEGAL ENTITY

from

IDENTITY LINK

from

EVIDENCE

from

ATOMIC CLAIM

from

ACCEPTED RELATIONSHIP

from

RELATIONSHIP VERSION

from

QUALIFIERS

from

RESEARCH COVERAGE

This stage establishes those foundations ADDITIVELY.

It must NOT yet:

- run new relationship research;
- migrate all historical observations;
- replay the 3M pilot;
- delete historical Stage 2 data;
- remove traversal infrastructure;
- create client-connection algorithms;
- build the frontend;
- expand frontier nodes;
- call providers.

======================================================================
3. IMPLEMENTATION PHILOSOPHY
======================================================================

This is an ADDITIVE migration.

The existing Stage 2 schema and records are historical/audit evidence.

Do not destructively rewrite them.

Do not reinterpret old rows in place.

Do not delete existing tables.

Do not silently remap existing accepted relationships.

The intended transition pattern is:

CURRENT STAGE 2 DATA
        │
        │ preserved
        ▼
HISTORICAL / AUDIT COMPATIBILITY

while separately introducing:

CCR V1 DOMAIN FOUNDATION
        │
        ▼
future controlled migration/replay

The old and new models may coexist temporarily.

That is expected.

======================================================================
4. START WITH THE RECONCILIATION REPORT
======================================================================

Before coding:

1. Read the completed CCR V1 Architecture Reconciliation Audit.
2. Inspect all current schema-v8 relationship tables.
3. Inspect the repository/domain interfaces.
4. Inspect current evidence structures.
5. Inspect current entity/external-identity structures.
6. Inspect existing migration framework.
7. Inspect the test suite.

Then produce a short internal implementation map before editing.

Do not create another audit report.

Use the previous audit's classifications:

KEEP
KEEP + EXTEND
MIGRATE
DEPRECATE LATER
HISTORICAL AUDIT ONLY
NEEDS DESIGN DECISION

Respect those findings.

If this prompt conflicts with a hard repository fact identified by the reconciliation audit, preserve repository correctness and report the conflict.

======================================================================
5. CCR V1 CORE DOMAIN MODEL
======================================================================

Implement domain contracts for the following concepts.

Do not necessarily force each contract into a separate file if the repository conventions favour another structure.

But the concepts must remain semantically distinct.

----------------------------------------------------------------------
5.1 CLIENT RECORD
----------------------------------------------------------------------

A Client Record is the authoritative internal record represented by the existing Client Universe.

The existing Client Universe repository remains the source of truth.

Do NOT copy all 3.67M clients into a new CCR table.

CCR V1 should reference Client Universe records through the existing stable internal client key and source identifiers.

No new client authority.

----------------------------------------------------------------------
5.2 LEGAL ENTITY
----------------------------------------------------------------------

CCR V1 legal entities represent real-world legal entities that can participate in externally evidenced relationships.

V1 entity grain:

LEGAL_ENTITY only.

Do not implement generic ORGANISATION nodes in this stage.

Do not automatically convert unresolved names into legal entities.

An entity must support provenance-aware identifiers.

Strong identifiers may include, where actually available:

- LEI
- CIK where appropriate
- registry identifier
- other governed exact identifier

Names alone do NOT automatically establish entity identity.

Reuse/adapt the existing external-entity infrastructure where the reconciliation audit shows it is safe.

Do NOT create a duplicate entity system if existing structures can be extended cleanly.

----------------------------------------------------------------------
5.3 CLIENT ↔ ENTITY IDENTITY LINK
----------------------------------------------------------------------

Introduce an explicit CCR V1 identity-link concept between:

Client Record
and
Legal Entity

The domain must support at least:

link_type:

EXACT
ASSOCIATED

link_state:

VERIFIED
PROBABLE
UNVERIFIED
REJECTED

Also preserve:

basis
source/provenance
created_at
updated_at or versioning equivalent
policy/rule version where appropriate

IMPORTANT:

Do NOT invent VERIFIED links during this stage.

Do NOT bulk-map the 3.67M universe.

Do NOT infer SAME ENTITY from name similarity.

Do NOT infer SAME ENTITY from CAGID.

Do NOT assume legal_entity_id is automatically a valid LEI.

Existing exact identity evidence may only be migrated later through an explicit controlled migration/replay stage.

For now implement the capability and tests.

Identity rule:

strong relationship evidence
+
weak identity link
≠
accepted client-to-client connection

======================================================================
6. CCR V1 DOCUMENT / EVIDENCE FOUNDATION
======================================================================

The conceptual chain is:

DOCUMENT
    ↓
EVIDENCE PASSAGE
    ↓
ATOMIC CLAIM
    ↓
ACCEPTANCE
    ↓
RELATIONSHIP VERSION

Implement the storage/domain foundation required to support this chain.

----------------------------------------------------------------------
6.1 DOCUMENT
----------------------------------------------------------------------

A Document represents a retrieved source artifact or source representation.

Support metadata including, where available:

document_id
source_class
publisher/source
canonical reference or URL
publication_date
retrieved_at
content_hash
retention_mode
full_content_retained
replay_capability
metadata/provenance

Do NOT assume every document's full text may always be retained.

Support retention capability conceptually such as:

FULL_SNAPSHOT
RESTRICTED_SNAPSHOT
TRANSIENT_VERIFICATION

Use naming consistent with repository conventions.

The data model should allow:

FULL_SNAPSHOT:
replay/excerpt verification possible from retained content

RESTRICTED_SNAPSHOT:
only permitted representation retained

TRANSIENT_VERIFICATION:
verification occurred during ingestion but full content is not retained

Do not build licensing logic.

Build the metadata capability.

----------------------------------------------------------------------
6.2 EVIDENCE PASSAGE
----------------------------------------------------------------------

Evidence Passage represents an exact portion of a Document.

Support, where available:

passage_id
document_id
exact excerpt/text
start/end offsets OR another deterministic locator
passage_hash if useful
created_at/extracted_at

A passage must be traceable to its document.

Do not accept model-generated summaries as evidence passages.

----------------------------------------------------------------------
6.3 ATOMIC CLAIM
----------------------------------------------------------------------

A Claim represents ONE atomic assertion extracted from evidence.

It is NOT an accepted relationship.

Conceptually support:

claim_id
passage_id
subject reference
object reference OR unresolved mention OR unspecified object
relationship type/family candidate
direction/roles
polarity
stated dates
qualifier assertions
extraction provenance
extractor/prompt version
created_at

Important examples:

"B supplies A"
=
one claim

"B and C supply A"
=
two atomic claims from the same passage

"We rely on sole-source suppliers"
=
claim with unspecified object
NOT a relationship edge

A named but unresolved counterparty must remain resolvable later.

An unnamed counterparty must NOT become a placeholder entity.

======================================================================
7. CCR V1 RELATIONSHIP FOUNDATION
======================================================================

Introduce or adapt the relationship model so that:

RELATIONSHIP

and

RELATIONSHIP VERSION

are distinct concepts.

A Relationship represents the stable identity of a factual entity-to-entity relationship.

A Relationship Version represents the accepted state over time.

Do not migrate old observations yet.

----------------------------------------------------------------------
7.1 ACCEPTANCE STATE
----------------------------------------------------------------------

Support:

CANDIDATE
ACCEPTED
DISPUTED
REJECTED

Do not combine this with freshness.

Do not combine this with temporal validity.

Do not introduce numeric confidence.

----------------------------------------------------------------------
7.2 TEMPORAL FIELDS
----------------------------------------------------------------------

Support relationship-version temporal information where appropriate:

effective_from
effective_to
date precision if repository patterns permit
observed_from / earliest evidence
observed_to / latest evidence
last_verified_at

Do not fabricate dates.

Nullable/unknown dates are valid.

----------------------------------------------------------------------
7.3 EVIDENCE BASIS
----------------------------------------------------------------------

Support deterministic evidence basis:

PRIMARY
CORROBORATED
SINGLE_SECONDARY
INSUFFICIENT

Do not implement arbitrary HIGH/MEDIUM/LOW confidence for acceptance.

Do not create numeric relationship-confidence scores.

----------------------------------------------------------------------
7.4 SOURCE CLASS
----------------------------------------------------------------------

Prepare the model for governed underlying source classes such as:

REGISTRY
REGULATORY_FILING
ISSUER_FILING
ISSUER_IR
OFFICIAL_TRANSACTION_DOCUMENT
GOVERNMENT
EXCHANGE_FILING
APPROVED_NEWS
COMMERCIAL_DATASET
OTHER_APPROVED_SECONDARY

Retrieval mechanism and source class must remain separate concepts.

Example:

retrieval mechanism:
WEB

underlying source:
REGULATORY_FILING

must NOT count as independent Web corroboration of the filing.

No external calls are made in this stage.

======================================================================
8. CCR V1 QUALIFIER FOUNDATION
======================================================================

Qualifiers are assertions ABOUT an accepted/candidate relationship.

They are not separate relationship types merely because they change how an analyst describes the relationship.

A qualifier must support its own acceptance/evidence state.

Conceptually support:

ACCEPTED
CANDIDATE
DISPUTED
UNKNOWN

Potential qualifiers include:

ownership_percentage
voting_percentage
ownership_basis
control_basis

facility_amount
currency
commitment_share
secured
maturity

product_category
service_category
revenue_share
spend_share
sole_source
single_source

described_as_critical
described_as_strategic

agreement_name/reference

Do not need to implement every qualifier as a hardcoded column.

Use a governed extensible representation consistent with repository style.

Critical rule:

A valid base relationship must not fail merely because a qualifier is weak.

Example:

supplies = ACCEPTED

sole_source = CANDIDATE

described_as_critical = UNKNOWN

is valid.

======================================================================
9. CCR V1 ACTIVE RELATIONSHIP TYPES
======================================================================

Create the V1 ontology/domain definitions required for the six ACTIVE initial relationship types:

owns

controls

lends_to

provides_credit_support

supplies

depends_on_products_of

Do not yet create live research pipelines for them.

Do not migrate current data automatically.

The ontology should define, at minimum:

canonical type
family
direction semantics
inverse display label
allowed endpoint grain
active/passive/deferred research status
basic qualifier vocabulary
whether direct client-to-client display is eligible
whether graph-hop use is allowed

Use policy/configuration data where practical instead of spreading type logic throughout application code.

----------------------------------------------------------------------
9.1 PASSIVE / OPPORTUNISTIC TYPES
----------------------------------------------------------------------

The architecture may also recognise:

manages
licenses_to
partners_with
litigates_against

but DO NOT spend major engineering effort on research behavior for them.

They are not active research families in this stage.

----------------------------------------------------------------------
9.2 DEFERRED
----------------------------------------------------------------------

Do not implement active support for:

provides_professional_services_to
broad passive equity-holding harvest
regulatory relationship harvesting
organisation-grain entities
natural-person external research

======================================================================
10. CONTROL BASIS MUST PRESERVE SOURCE SEMANTICS
======================================================================

For future control relationships, preserve source-specific basis.

Examples:

GLEIF Level 2 may support:

controls
control_basis = ACCOUNTING_CONSOLIDATION

SEC Exhibit 21 may support:

controls
control_basis = SUBSIDIARY_DISCLOSURE

Do NOT silently normalize these into a universal legal-control assertion without preserving their stated basis.

This stage only needs the model capability.

Do not harvest new control relationships.

======================================================================
11. RESEARCH OUTCOME / ENRICHMENT COVERAGE FOUNDATION
======================================================================

CCR V1 needs to distinguish:

NOT_ELIGIBLE
NOT_RESEARCHED
RESEARCHED_FOUND
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE

Freshness separately:

CURRENT
STALE

Implement or adapt a CCR V1 enrichment/research-coverage contract that can track coverage by:

entity
relationship family
scope/source set
as_of
policy version

Important:

RESEARCHED_NONE_FOUND
means:

"the configured research scope completed successfully and found no qualifying relationship"

It must NEVER mean:

"this relationship does not exist."

Provider failure must not become NONE_FOUND.

NOT_RESEARCHED must permit reason codes, such as:

identity_unresolved
not_prioritized
family_not_in_scope
policy_ineligible

Do not execute research.

======================================================================
12. EVENTS — FOUNDATION ONLY
======================================================================

CCR V1 distinguishes events from persistent relationships.

Examples of events:

acquisition
spin-off
facility signing
facility termination
litigation settlement

Do not build a complete event subsystem unless needed to avoid locking the model incorrectly.

At minimum:

- ensure the new relationship/version model does not require events to be represented as permanent relationship types;
- create only the minimum domain/storage abstraction required if the architecture naturally needs it now.

If introducing events would significantly expand scope, defer actual event persistence and document that decision.

======================================================================
13. CLIENT CONNECTIONS — DO NOT IMPLEMENT YET
======================================================================

Do NOT implement connection mining in this stage.

Do NOT add new traversal algorithms.

Do NOT create shared-supplier or shared-controller calculations yet.

The future direction includes:

DIRECT client-to-client relationships as a view/category

and derived structures such as:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN

Potential hidden-by-default structures later:

SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY
SHARED_SPONSOR

But this stage ends before connection implementation.

The new foundation must merely make those queries possible later.

======================================================================
14. EXISTING STAGE 2 DATA
======================================================================

Preserve all existing Stage 2 data.

This includes any existing:

observations
candidates
evidence
external entities
identity records
provider attempts
resolution runs
recovery runs
traversal runs
frontier expansion runs
paths
hop evidence
provider caches

Do not migrate these automatically.

Do not reinterpret current 3M relationships under V1 during this stage.

Do not delete them.

The completed reconciliation audit already determined their future disposition.

Respect that classification.

======================================================================
15. CURRENT 3M PILOT
======================================================================

The 3M pilot becomes the future CCR V1 regression/replay case.

DO NOT replay it in this stage.

DO NOT call providers.

DO NOT change accepted 3M observations.

DO NOT create new 3M relationships.

Only ensure the new architecture is capable of supporting the future flow:

stored/retrieved evidence
    ↓
evidence passage
    ↓
atomic claims
    ↓
V1 acceptance
    ↓
relationship/version
    ↓
compare against historical result

Future comparison states:

CONFIRMED
RECLASSIFIED
DOWNGRADED
REJECTED
NEW

Do not implement the comparison workflow now unless a minimal reusable enum/contract is clearly needed.

======================================================================
16. EXISTING TRAVERSAL / FRONTIER INFRASTRUCTURE
======================================================================

Do not delete Stage 2A.6 or 2A.7 infrastructure.

Do not continue developing it.

Leave historical execution/audit records intact.

Where necessary:

- mark old structures as legacy/historical in documentation;
- keep them operational enough for existing read-only audit APIs/tests;
- do not wire new CCR V1 relationships into old traversal automatically.

The future connection engine will be designed after V1 relationships and identity links exist.

======================================================================
17. SCHEMA MIGRATION
======================================================================

Create ONE additive migration from the current relationship schema version.

The reconciliation audit should tell you the current exact version.

If it is schema v8 as expected:

create schema v9.

If the current repository reports another version:

use the actual next version.

The migration must be:

ADDITIVE
IDEMPOTENT
REPLAY-SAFE
NON-DESTRUCTIVE

No DROP TABLE.

No destructive ALTER.

No deletion of Stage 2 data.

No rewriting of historical rows.

Use foreign keys and indexes deliberately.

Do not prematurely create massive indexes that are not required by the Stage 1 workload.

======================================================================
18. STORAGE / REPOSITORY BOUNDARY
======================================================================

Continue using repository abstractions.

Do not make application/domain code dependent directly on SQLite-specific behavior where avoidable.

SQLite remains acceptable for this local stage.

Do NOT migrate to PostgreSQL in this task.

Add/extend repository contracts for the new CCR V1 concepts.

Potential concepts include:

entity
client_entity_identity_link
document
evidence_passage
claim
relationship
relationship_version
relationship_support
qualifier
enrichment_coverage

Use naming that matches the actual existing repository style.

Do not create gratuitous repository interfaces if one well-structured CCR repository boundary is cleaner.

======================================================================
19. TERMINOLOGY CLEANLINESS
======================================================================

ALL new artifacts created by this stage must use CCR naming.

Examples:

CCR
Client Correlation
Client Universe
Client Enrichment
Entity Resolution
Relationship Research
Evidence
Relationship Graph
Client Connections

Do not copy unrelated historical naming into new class/table/config/report names.

Do not rename historical files in this stage unless required to prevent active runtime ambiguity.

Legacy names may remain untouched for audit/history.

New code must not make new dependencies on unrelated legacy policy files.

======================================================================
20. CODE ORGANIZATION
======================================================================

Follow existing backend architecture and conventions.

Prefer adapting reusable components identified by the reconciliation audit.

Do NOT build a parallel application.

Do NOT duplicate:

client repository
provider infrastructure
database connection framework
migration framework
common provenance/audit utilities

when existing implementation is reusable.

But do not force incompatible Stage 2 concepts into CCR V1 merely to reduce file count.

======================================================================
21. REQUIRED TESTS
======================================================================

Add focused tests for the new CCR V1 foundation.

At minimum test:

1. schema migration is additive;

2. existing Stage 2 tables/data survive migration;

3. source Client Universe remains unchanged;

4. client-record/entity identity link supports:
   EXACT
   ASSOCIATED
   VERIFIED
   PROBABLE
   UNVERIFIED
   REJECTED;

5. no identity link is automatically VERIFIED from a name alone;

6. unresolved named mention does not create a legal entity automatically;

7. unnamed claim does not create an entity;

8. document → evidence passage lineage is preserved;

9. one passage may produce multiple atomic claims;

10. one atomic relationship claim has one relationship assertion;

11. relationship acceptance state is separate from freshness;

12. relationship version supports unknown/open temporal fields;

13. qualifier state is independent from base relationship state;

14. weak qualifier does not downgrade an accepted base relationship;

15. evidence basis enum supports:
    PRIMARY
    CORROBORATED
    SINGLE_SECONDARY
    INSUFFICIENT;

16. retrieval mechanism is separate from underlying source class;

17. RESEARCHED_NONE_FOUND cannot be created when outcome is PARTIAL/UNAVAILABLE;

18. research coverage tracks entity + family + policy/scope;

19. no synthetic direct relationship is created from path concepts;

20. historical Stage 2 3M records are unchanged;

21. existing no-fuzzy-merge invariants still pass;

22. existing source-master immutability tests still pass;

23. existing test suite remains green unless a test is explicitly and defensibly superseded.

Do not weaken old tests merely to make the migration pass.

If an old test encodes a genuinely superseded behavior, identify it explicitly before changing it.

Prefer compatibility in this stage.

======================================================================
22. NO EXTERNAL PROVIDER ACTIVITY
======================================================================

This stage must make:

SEC calls: 0
GLEIF calls: 0
Web calls: 0
Stylus calls: 0

Do not run recovery scripts that call providers.

Do not rerun Stage 2A.7.

Do not refetch 3M evidence.

Tests must use fixtures/mocks/local data only.

======================================================================
23. NO FRONTEND
======================================================================

Frontend modifications:

0

Do not build the graph UI.

Do not change navigation.

Do not add V1 pages.

Do not add evidence drawers.

Backend/domain foundation only.

======================================================================
24. SOURCE MASTER INTEGRITY
======================================================================

At the end verify:

Customer_latest.parquet unchanged

Client Universe:
3,670,650 rows expected

GFCID uniqueness unchanged

No Client Universe source records inserted/updated/deleted by this stage.

CCR V1 data must remain additive around the Client Universe.

======================================================================
25. COMPATIBILITY WITH CURRENT APIs
======================================================================

Do not break existing bounded client APIs.

Do not intentionally break existing read-only Stage 2 audit/relationship APIs.

If compatibility requires a thin adapter, add the smallest safe adapter.

Do not expose the full new V1 API in this stage.

A future stage will introduce the proper CCR V1 API surface after V1 data has been migrated/replayed.

======================================================================
26. REQUIRED DOCUMENTATION
======================================================================

Create one implementation report:

backend/data/CCR_V1_FOUNDATION_STAGE_1_REPORT.md

It must contain:

1. Executive result

2. Reconciliation report used as baseline

3. Exact schema version before/after

4. New CCR V1 domain concepts implemented

5. New tables

6. New indexes/constraints

7. Repository/domain contracts added or adapted

8. Identity-link model

9. Document/evidence/passage model

10. Claim model

11. Relationship/version model

12. Qualifier model

13. Evidence-basis model

14. Enrichment-coverage model

15. Event handling decision

16. Existing Stage 2 compatibility

17. Existing 3M data integrity

18. Client Universe integrity

19. Terminology/boundary checks

20. Tests added

21. Full test results

22. Known deferrals

23. Recommended next CCR stage

Keep the recommendation concise.

Do NOT write the entire next implementation prompt.

======================================================================
27. VALIDATION
======================================================================

Run:

- backend test suite;
- compile/static checks already standard for this repository;
- SQLite foreign-key check;
- schema verification;
- migration replay/idempotence check;
- read-only existing Stage 2 API sanity checks where practical;
- Client Universe integrity checks.

No external network calls.

======================================================================
28. REQUIRED FINAL STATUS
======================================================================

Finish your response with exactly this style:

CCR V1 FOUNDATION — STAGE 1

Status: PASS / PARTIAL / FAIL

Reconciliation baseline:
<actual report used>

Schema before:
<actual>

Schema after:
<actual>

New CCR V1 tables:
<count and names>

Existing Stage 2 tables deleted:
0

Historical relationship rows modified:
0

Client Universe rows:
<actual>

Client Universe source modifications:
0

Identity-link foundation:
PASS / FAIL

Document/evidence foundation:
PASS / FAIL

Atomic-claim foundation:
PASS / FAIL

Relationship/version foundation:
PASS / FAIL

Qualifier foundation:
PASS / FAIL

Evidence-basis foundation:
PASS / FAIL

Enrichment-coverage foundation:
PASS / FAIL

External provider calls:
0

New relationship research performed:
0

New accepted relationships:
0

New candidates from research:
0

New paths:
0

Frontend files modified:
0

Backend tests:
<actual>

Foreign-key errors:
<actual>

Migration replay:
PASS / FAIL

Existing 3M historical data preserved:
YES / NO

Fuzzy auto-merges introduced:
0

Synthetic direct edges introduced:
0

Report:
backend/data/CCR_V1_FOUNDATION_STAGE_1_REPORT.md

Recommended next action:
<one concise sentence>

======================================================================
29. STOP CONDITION
======================================================================

After completing this Stage 1 foundation:

STOP.

Do not proceed automatically to:

- historical-data migration;
- 3M replay;
- new provider research;
- connection mining;
- Stage 2A.8;
- frontend work;
- PostgreSQL;
- graph database work.

We will review Stage 1 before authorizing the next CCR implementation stage.
