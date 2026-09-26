IMPLEMENT WITH LUNA — CLIENT RELATIONSHIP INTELLIGENCE V1
ARCHITECTURE RECONCILIATION AUDIT — CURRENT SCHEMA V8 / STAGE 2A.7
We are deliberately stopping further Stage 2A frontier-expansion development.
Do not implement Stage 2A.8.
Do not continue recursive relationship research.
Do not modify the frontend.
Do not redesign the Client Universe.
Do not perform destructive migrations.
Do not call SEC, Web, GLEIF, Stylus or any external provider in this task.
Do not change accepted relationship results.
Do not delete or rewrite historical Stage 2 run records.
This task is a repository and data architecture reconciliation audit.
You are operating on the current implementation whose latest known state is:
Stage 1      Client Universe foundation
Stage 2A.2   Relationship ingestion foundation
Stage 2A.3   Real 3M ingestion
Stage 2A.4   External entity resolution
Stage 2A.5   Provider readiness/recovery
Stage 2A.6   Hidden relationship traversal
Stage 2A.7   Frontier relationship expansion

Current relationship schema: v8
Current Client Universe: 3,670,650 rows
Latest backend suite: 48 tests passed

Latest Stage 2A.7 result:
Status: COMPLETED

Frontier endpoints researched: 2

Provider attempts:
SEC   2
Web   2
GLEIF 4

Cache hits: 2
Network attempts: 2
Provider failures: 4

Candidate findings: 0
Newly accepted observations: 0

Accepted graph edges:
3 before
3 after

2-hop paths: 0
3-hop paths: 0

Synthetic relationships: 0
Fuzzy merges: 0
Source-master modifications: 0

Client Universe remains:
3,670,650 rows

Stage 2A.6 was replayed afterwards and created no duplicate traversal or provider-audit work.
Current Stage 2A.7 reporting is expected around:
backend/data/FRONTIER_RELATIONSHIP_EXPANSION_STAGE_2A7_REPORT.md

and implementation includes approximately:
relationship_frontier_expansion.py
run_frontier_relationship_expansion_stage_2a7.py

Inspect the actual repository; do not rely on these paths if the implementation differs.
1. WHY DEVELOPMENT IS PAUSED HERE
The earlier architecture was built around:
research subject
→ accept depth-1 relationships
→ research accepted neighbours
→ traverse graph
→ hope to discover hidden paths

Stage 2A.7 has now tested that approach on the 3M pilot.
It researched actual depth-1 frontier entities and produced:
0 newly accepted observations
0 new graph edges
0 multi-hop paths

This result does not mean the product concept failed.
It means we now need to reconcile the implementation with a more deliberate V1 relationship-enrichment architecture before creating further stages.
Do not attempt to improve the Stage 2A.7 result during this task.
2. AUTHORITATIVE CLIENT UNIVERSE — DO NOT CHANGE
The active product universe remains:
backend/Customer_latest.parquet

Known properties:
3,670,650 source rows
3,670,650 unique GFCIDs
21 source columns

Current runtime Client Universe:
backend/data/client_universe.sqlite3

The historical thousandClients.csv / ~16K CCR population is not the active product universe and has no special enrichment authority.
Do not reintroduce it.
Do not use exposure membership as an enrichment rule.
Do not create a second active client universe.
All 3.67M Client Universe records remain eligible for the product subject to identity/research-policy constraints.
3. V1 PRODUCT DEFINITION TO RECONCILE AGAINST
Use the following as the target conceptual direction for the audit:
For every client record in the Client Universe, the platform should be able to identify the real-world entity the record represents where evidence permits, discover that entity's relationships with other entities from auditable evidence, recognize when related entities are themselves represented in the Client Universe, and allow analysts to explore direct and indirect connections between clients while keeping identity certainty, evidence provenance and enrichment coverage visible.

This is:
CLIENT RELATIONSHIP INTELLIGENCE
+
CLIENT RELATIONSHIP ENRICHMENT
+
STRUCTURAL CLIENT CONNECTION DISCOVERY

It is not currently a statistical-correlation product.
It is not a 16K CCR application.
It is not an exposure engine.
It is not an LLM-generated graph.
4. V1 CONCEPTUAL IDENTITY MODEL
The target conceptual separation is:
CLIENT RECORD
    ↓
GATED IDENTITY LINK
    ↓
LEGAL ENTITY
    ↓
ENTITY RELATIONSHIPS

Important:
A GFCID is currently proven to be unique at source-record grain.
We have not proven that:
1 GFCID = exactly 1 real-world legal entity

or that:
multiple GFCIDs with some repeated identifier
= same legal entity

Therefore do not infer that during this audit.
We need to distinguish:
CLIENT RECORD
LEGAL ENTITY
INTERNAL GROUPING
INTERNAL SOURCE LINK
EXTERNAL RELATIONSHIP

Do not collapse them.
5. V1 IDENTITY LINK STATES
Conceptually, a future record-to-entity identity link may carry:
type:
EXACT
ASSOCIATED

state:
VERIFIED
PROBABLE
UNVERIFIED
REJECTED

This task must determine whether the existing schema already has any equivalent concept.
Do not implement it yet.
Important future principle:
strong relationship evidence
+
weak endpoint identity
≠
accepted client-to-client connection

6. V1 ENTITY GRAIN
For V1, assume:
LEGAL_ENTITY

is the only active external entity grain.
Do not create generic organisation/group nodes merely because a source says something like:
Samsung

when the precise legal entity is not established.
Such references should eventually remain named unresolved mentions until identity evidence resolves them.
This is only a target semantic for the audit.
Do not migrate anything yet.
7. V1 EVIDENCE CHAIN
The target conceptual evidence model is:
DOCUMENT
    ↓
EVIDENCE PASSAGE
    ↓
ATOMIC CLAIM
    ↓
DETERMINISTIC ACCEPTANCE POLICY
    ↓
RELATIONSHIP
    ↓
RELATIONSHIP VERSION

This is critical.
We need to know what the current implementation has today.
Specifically inspect whether Stage 2 currently stores:
source URL/reference only
excerpt only
Stylus output only
provider response
retrieved raw document
normalized document text
document content hash
passage offsets
claim objects
evidence objects
relationship observations
relationship versions

Do not assume.
Report the actual state.
8. DOCUMENT RETENTION — AUDIT ONLY
The future architecture should support different evidence-retention capabilities because not every source necessarily permits full persistent content storage.
Conceptually:
FULL_SNAPSHOT
RESTRICTED_SNAPSHOT
TRANSIENT_VERIFICATION

Possible future metadata includes:
retention_mode
full_content_retained
excerpt_retained
replay_capability
source/reference
content_hash
retrieval_timestamp

Do not implement these yet.
Instead determine:
1. Does anything equivalent already exist?
2. Are full source documents stored for the current 3M pilot?
3. Are normalized source bodies stored?
4. Are only excerpts/URLs stored?
5. Can current accepted observations be independently replayed from immutable stored evidence?
This is one of the most important audit findings.
9. V1 CLAIM MODEL
Target concept:
An atomic claim represents exactly what one evidence passage asserts.
Examples:
B supplies A

A owns 19.9% of B

Lender X lends to Borrower Y

A depends on products of B

An unnamed statement such as:
"We rely on limited and sole-source suppliers."

would eventually remain:
subject = A
family = supply
object = unspecified

and must not create a placeholder entity edge.
Audit whether the current Stage 2 finding/evidence model already separates:
what source said

from:
what system accepted

If not, identify precisely where those concepts are currently conflated.
10. V1 RELATIONSHIP ACCEPTANCE STATE
Future conceptual acceptance states:
CANDIDATE
ACCEPTED
DISPUTED
REJECTED

Freshness is separate.
Temporal validity is separate.
Evidence basis is separate.
Audit what the current implementation stores today.
Look for overlapping concepts such as:
finding_type
relationship_supported
mention_only
confidence
connectivity
relationship_status
analyst_review_required
materiality

List every relevant field/table/enum.
Classify each as:
KEEP
POSSIBLY KEEP
OVERLAPPING
SUPERSEDED BY V1 CONCEPT
LEGACY / NEEDS DECISION

Do not remove anything.
11. V1 EVIDENCE BASIS
Target conceptual evidence basis:
PRIMARY
CORROBORATED
SINGLE_SECONDARY
INSUFFICIENT

No numerical AI confidence is required for acceptance.
Audit:
- current confidence fields;
- source-tier logic;
- evidence thresholds;
- provider-channel logic;
- source-channel logic;
- corroboration logic;
- source-independence logic.
Determine whether current code distinguishes:
retrieval tool

from:
underlying source

For example:
Web Search retrieves SEC filing

should ultimately remain SEC/filing evidence, not independent Web evidence.
Report current behavior.
12. ACTIVE V1 RELATIONSHIP TYPES
The current proposed ACTIVE V1 research types are:
owns
controls
lends_to
provides_credit_support
supplies
depends_on_products_of

Passive/opportunistic ontology support:
manages
licenses_to
partners_with
litigates_against

Deferred for initial implementation/research:
provides_professional_services_to
broad passive equity holdings
regulatory relationships
organisation-grain relationships
natural-person external enrichment

Do not modify the current taxonomy.
Audit the existing controlled relationship types and create a mapping table:
CURRENT TYPE
→
V1 TYPE / QUALIFIER / EVENT / DEFERRED / UNKNOWN

Examples to investigate:
critical_supplier
supplier
customer_dependency
contracted_customer
technology_dependency
infrastructure_dependency
service_provider
parent_company
subsidiary
equity_investor
sponsor
guarantor
lender
backleverage_financing
strategic_partner
joint_venture
legal_counterparty
regulator
advisor
competitor
fund_at_target
revenue_concentration

Do not assume the expected mapping.
Inspect actual code/configuration and report it.
13. QUALIFIERS VS RELATIONSHIP TYPES
Target V1 principle:
supplies

may have qualifiers such as:
category
product/service category
sole_source
single_source
revenue_share
spend_share
described_as_critical

Therefore:
critical_supplier

may not need to be a distinct relationship type.
Likewise ownership percentage should be a qualifier on:
owns

not a new type.
Audit where the current implementation encodes these concepts.
Do not change them.
14. EVENT VS RELATIONSHIP
Target V1 principle:
spin-off
acquisition
facility signing
facility termination
litigation settlement

may be events.
Persistent states such as:
owns
controls
lends_to
supplies

are relationships.
Audit whether the current schema has an event model or whether event-like concepts are encoded as relationship observations.
Report examples from the current 3M pilot if applicable.
No migration yet.
15. CURRENT 3M PILOT — FULL RECONCILIATION
This is mandatory.
Identify the current 3M root precisely.
Earlier stages reported approximately:
client_id 437487
GFCID 0000426083

Verify against actual current data.
Then provide the exact current state of all 3M-related records:
accepted observations
candidate findings
no-evidence findings
external identities
external entities
evidence records
provider attempts
resolution records
recovery records
traversal records
frontier records
paths

Give exact counts.
16. RECONCILE THE ACCEPTED-COUNT DISCREPANCY
This is mandatory.
Earlier reports produced apparently different counts:
Stage 2A.5:
approximately 4 accepted observations

Stage 2A.6:
approximately 5 accepted edges inspected

Stage 2A.7:
3 accepted graph edges before and after

Determine exactly why.
Possible explanations might include:
observation vs graph-edge semantics
duplicate representations
directional edges
current-state filters
subject-scoped filters
different pilot runs
relationship-version filters
schema migrations

Do not speculate.
Trace the actual rows and code paths.
Provide a table showing:
ID
SUBJECT
OBJECT
RELATIONSHIP TYPE
ACCEPTANCE STATE
SOURCE STAGE
CURRENTLY COUNTED AS GRAPH EDGE?
WHY / WHY NOT

This discrepancy must be understood before any migration.
17. 3M CURRENT ACCEPTED RELATIONSHIPS
List the actual currently accepted 3M relationships.
For every one report:
subject
object
current type
direction
internal/external identity
evidence count
evidence source classes/channels
source references
current acceptance fields
current confidence/materiality fields if present
stage that accepted/promoted it

Do not change anything.
18. CAN THE 3M PILOT BE REPLAYED?
Determine one of:
FULL_REPLAY_POSSIBLE
PARTIAL_REPLAY_ONLY
REFETCH_REQUIRED
RESEARCH_REQUIRED_FROM_SCRATCH

Give the exact reason.
Specifically verify whether stored evidence allows:
document
→ passage
→ claim extraction
→ acceptance

without making a new network call.
If only excerpts/URLs exist, say so explicitly.
Do not refetch anything in this task.
19. FRONTIER EXPANSION AUDIT
Inspect Stage 2A.7.
Report:
which 2 frontier endpoints were researched
why each qualified as frontier
which providers were called
which provider calls failed
why they failed
which calls hit cache
what evidence/documents were returned
why candidate findings = 0
why accepted findings = 0

Determine whether zero new relationships resulted from:
no documents
provider failures
identity failures
relationship evidence failures
acceptance threshold
research query quality
scope limits

or some combination.
Do not rerun it.
20. PROVIDER FAILURE AUDIT
Stage 2A.7 reported:
provider failures: 4

Trace them exactly.
For each report:
provider
endpoint/entity
request purpose
error category
HTTP/status if available
retry status
cached fallback if any
whether failure affected research completeness

Do not call the providers.
This helps distinguish:
real no evidence

from:
research incomplete because provider failed

21. CURRENT NEGATIVE-OUTCOME MODEL
Audit whether current code distinguishes:
NOT_RESEARCHED
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE
IDENTITY_UNRESOLVED
NO_EVIDENCE

If it does not, explain exactly what it currently stores.
This matters because a provider failure must never be interpreted as:
relationship does not exist

22. CURRENT IDENTITY MODEL
Inspect all identity-related tables/code.
Report how the implementation currently represents:
internal client
external entity
external identity
candidate identity
resolved identity
unresolved endpoint
generic descriptor

Determine whether:
external entity

and:
internal client

can currently represent the same real-world organization safely.
Explain current behavior when an externally discovered legal entity happens to match one of the 3.67M Client Universe records.
Does it:
reuse client?
create external entity?
create link?
create duplicate?
stay unresolved?

Do not modify behavior yet.
23. INTERNAL MASTER FIELDS — AUDIT, DO NOT INTERPRET
Audit current use of:
cagid
cagid_name
beneficial_owner_gfcid
legal_entity_id
lei_legal_name
gfcid_type
customer_type_desc
account_type_desc

For each report:
stored?
indexed?
used in identity resolution?
used in relationship creation?
used in traversal?
used in search?
used only as metadata?

Important:
Do not assign new semantics to these fields.
In particular:
CAGID ≠ identity proof
beneficial_owner_gfcid semantics remain unconfirmed
legal_entity_id ≠ automatically valid LEI

24. OLD CAM / LENDING ASSUMPTIONS
Search active code/configuration/knowledge files for concepts such as:
CAM
Lending authority
CAM corroboration
CAM relationship
CCR
exposure
thousandClients
portfolio exposure

Classify each occurrence:
ACTIVE AND STILL NECESSARY
LEGACY BUT HARMLESS
CONFLICTS WITH V1
ARCHIVED
UNKNOWN

Do not delete anything.
Pay particular attention to research-policy files currently containing sections like:
CAM corroboration

or wording that gives CAM/Lending records authority beyond the Client Universe identity boundary.
Report whether those rules would conflict with the new separation of:
client-record identity
entity identity
external evidence
relationship acceptance

25. CURRENT TRAVERSAL / PATH MODEL
Inventory Stage 2A.6 and 2A.7 structures:
traversal runs
frontier tables
path tables
path nodes
hop evidence snapshots
replay fingerprints
frontier research records

For each classify:
KEEP AS USEFUL INFRASTRUCTURE
KEEP FOR HISTORICAL AUDIT ONLY
POSSIBLY SIMPLIFY
SUPERSEDED BY V1 CONNECTION MODEL
UNKNOWN

Do not remove them.
Remember:
V1 currently treats ordinary graph paths as derived/query results.
Client connections may become governed derived structures.
We have not yet decided their persistent representation.
26. DATABASE SCHEMA INVENTORY
Produce a concise but complete inventory of all relationship-intelligence tables in schema v8.
For each table:
table
purpose
row count
primary key
important foreign keys
important indexes
which stage created it
whether current runtime code reads/writes it
V1 disposition

V1 disposition must be one of:
KEEP
KEEP + EXTEND
MIGRATE
DEPRECATE LATER
HISTORICAL AUDIT ONLY
NEEDS DESIGN DECISION

Do not modify schema.
27. CODE INVENTORY
Identify the principal implementation modules involved in:
client repository
relationship repository
relationship ingestion
identity resolution
provider recovery
frontier research
traversal
API
schema/migrations
research policy
provider adapters

For each classify:
REUSABLE
REUSABLE WITH ADAPTATION
LEGACY
SUPERSEDED CONCEPT
NEEDS INSPECTION

No refactoring yet.
28. API INVENTORY
List current client/relationship APIs.
For each:
method/path
purpose
bounded?
currently used?
current backing repository
compatible with V1?

Do not add APIs.
29. TEST INVENTORY
The latest suite reports:
48 passed

Run the existing local backend tests if safe and network-free.
Report:
total
passed
failed
skipped
duration

Then classify tests:
CLIENT UNIVERSE CONTRACT
RELATIONSHIP INGESTION
IDENTITY RESOLUTION
PROVIDER RECOVERY
TRAVERSAL
FRONTIER EXPANSION
LEGACY

Identify which tests represent invariants worth preserving:
no fuzzy merge
no synthetic edge
master unchanged
replay/idempotence
candidate cannot become accepted without gates
generic descriptor cannot become entity

Do not rewrite tests.
30. SOURCE MASTER INTEGRITY
Verify read-only:
Customer_latest.parquet
row count
GFCID uniqueness
source hash if available

and current Client Universe database parity.
There must be:
0 source-master modifications

This task must not touch the master.
31. RECONCILIATION MATRIX
Produce a major section in the report called:
CURRENT → V1 RECONCILIATION MATRIX
For every major concept show:
CURRENT CONCEPT
CURRENT IMPLEMENTATION
V1 CONCEPT
ACTION LATER
RISK

At minimum include:
client
external entity
identity resolution
finding
candidate
no evidence
evidence
confidence
materiality
relationship observation
relationship type
relationship direction
connectivity
provider attempt
research run
path
traversal
frontier
hidden relationship
CAM corroboration

32. DO NOT DESIGN THE MIGRATION YET
You may identify dependencies and likely migration difficulty.
But do not create:
schema v9
migration scripts
new repositories
new tables
new APIs
new relationship types
new acceptance code

That comes after the audit.
This task should tell us what exists and what conflicts.
33. ONE ALLOWED REPOSITORY CHANGE
You may create exactly one substantive new artifact:
backend/data/CLIENT_RELATIONSHIP_V1_ARCHITECTURE_RECONCILIATION_AUDIT.md

If a tiny temporary diagnostic script is absolutely necessary, prefer executing it without committing it.
Do not modify production code.
Do not modify schema.
Do not modify tests.
Do not modify configs.
Do not modify frontend.
34. REPORT REQUIRED SECTIONS
The audit report must contain:
1. Executive result
2. Current repository baseline
3. Schema v8 inventory
4. Code inventory
5. API inventory
6. Test inventory
7. 3M pilot exact current state
8. Accepted-count discrepancy reconciliation
9. Evidence/document retention audit
10. 3M replay capability
11. Stage 2A.7 frontier audit
12. Provider failure audit
13. Current identity architecture
14. Internal master-field usage
15. CAM/CCR/Lending legacy assumptions
16. Traversal/path infrastructure assessment
17. Current → V1 reconciliation matrix
18. Reusable components
19. Components requiring adaptation
20. Components likely to be deprecated later
21. Blocking unknowns
22. Recommended implementation sequence — HIGH LEVEL ONLY
23. Validation results

Section 22 must remain high-level.
Do not create implementation prompts in the report.
35. FINAL STATUS FORMAT
At the end output:
CLIENT RELATIONSHIP V1 RECONCILIATION AUDIT

Status: PASS / PARTIAL / FAIL

Client Universe rows:
Source master modified:
Schema version:
Backend tests:

Current accepted 3M observations:
Current accepted 3M graph edges:
Reason for observation/edge count difference:

3M full source documents retained:
3M replay capability:

Stage 2A.7 frontier endpoints:
Stage 2A.7 new accepted relationships:
Stage 2A.7 paths:
Stage 2A.7 provider failures:

Current tables inventoried:
Current modules inventoried:
Current APIs inventoried:

Components reusable as-is:
Components reusable with adaptation:
Components requiring eventual migration:
Components historical/audit only:

Fuzzy merges detected:
Synthetic direct edges detected:
Unexpected Client Universe modifications:

Recommended next action:

Be factual.
If something cannot be established from the repository, report:
UNKNOWN

Do not infer.
36. ABSOLUTE CONSTRAINTS
For this task:
external provider calls = 0
new accepted observations = 0
new candidates = 0
new external entities = 0
new paths = 0
new schema migrations = 0
frontend modifications = 0
source-master modifications = 0

Do not call Stylus.
Do not run relationship discovery.
Do not run frontier expansion.
Do not rerun provider recovery if it makes external calls.
This is an audit.
37. IMPORTANT PHILOSOPHY
Do not judge the current Stage 2 implementation as “bad”.
It was useful experimental infrastructure and established several controls we likely want to preserve:
no fuzzy merging
strict identity resolution
provider audit
candidate retention
generic-descriptor exclusion
no synthetic direct edges
bounded traversal
idempotent replay
source-master immutability

The purpose now is to determine how that work should evolve into the more stable Client Relationship Intelligence V1 architecture.
Preserve useful controls.
Do not preserve complexity merely because it exists.
