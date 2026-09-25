CLIENT CORRELATION — STAGE 2A.4
EXTERNAL ENTITY IDENTITY RESOLUTION — BOUNDED 3M PILOT

Stage 2A.3 is complete.

Current real 3M ingestion result:

15 raw findings
1 accepted relationship observation
14 candidates
17 evidence objects
0 external entities
0 synthetic shortcut edges
0 fuzzy merges

The ingestion plumbing is working.

The next problem is identity resolution of NAMED related entities that are not
currently resolved to the 3.67M Client Universe.

DO NOT redesign the ingestion model.
DO NOT modify Customer_latest.parquet.
DO NOT build the frontend/network.
DO NOT create relationships merely because an entity identity is resolved.
DO NOT use fuzzy entity merging.
DO NOT create entities from unnamed/generic descriptors.

OBJECTIVE

For the existing persisted 3M Stage 2A.3 candidates only:

1. determine whether each named related entity is already an internal
   Client Universe client;
2. otherwise resolve it as a verified external entity where defensible;
3. persist external identity separately from Client Universe;
4. re-run the existing relationship acceptance gate;
5. promote only candidates whose endpoint identity AND relationship evidence
   independently satisfy the existing policy.

This is ENTITY RESOLUTION, not new relationship discovery.

==================================================
1. CLASSIFY THE EXISTING 14 CANDIDATES
==================================================

Read the actual persisted Stage 2A.3 candidate set.

Classify each related endpoint as one of:

NAMED_INTERNAL_CANDIDATE
NAMED_EXTERNAL_CANDIDATE
GENERIC_UNNAMED_DESCRIPTOR
NO_RELATED_ENTITY
IDENTITY_ALREADY_RESOLVED

Produce the complete list before performing provider work.

Examples of generic descriptors include:

Revolving Credit Facility Syndicate Lenders
Unnamed Limited- and Sole-Source Suppliers
Unnamed ERP / IT Infrastructure Vendor
Unnamed Pension Annuity Insurer

These are NOT legal entities.

They must remain unresolved candidate descriptors.

==================================================
2. INTERNAL CLIENT UNIVERSE RESOLUTION FIRST
==================================================

For every NAMED related entity:

Search the 3,670,650-client Client Universe first.

Allowed internal matching:

exact client_id
exact GFCID
exact CAGID only when uniqueness permits
exact legal_entity_id only when uniqueness permits
exact canonical/legal name
exact normalized alias

NO fuzzy merge.

NO similarity threshold.

NO model-based identity decision.

If exactly one client resolves:
classify endpoint as INTERNAL_CLIENT
and bind its client_id.

If more than one plausible internal record exists:
AMBIGUOUS_INTERNAL
and do not choose automatically.

If none resolves:
continue to external identity resolution.

==================================================
3. EXTERNAL IDENTITY RESOLUTION
==================================================

For named entities not found internally, use the preserved approved provider
stack only:

GLEIF
SEC
approved Web research

The goal is identity only.

Do NOT perform broad relationship discovery in this stage.

Preferred identity evidence:

GLEIF:
LEI
legal name
registered address
jurisdiction
parent identifiers where returned

SEC:
CIK
registrant legal name
ticker/exchange where authoritative
filing registrant identity

Approved Web:
official company domain
official corporate profile
official investor-relations page
government/regulatory identity reference

Do not use generic search-result snippets as final identity authority.

==================================================
4. EXTERNAL ENTITY MODEL
==================================================

Create an external entity only where identity is sufficiently established.

Each external entity must have a stable internal external_entity_id.

Persist where available:

external_entity_id
legal_name
normalized_name
entity_type
country/jurisdiction
LEI
CIK
ticker
official_domain
provider identity references
created_at
updated_at
identity_status
identity_provenance

External entities MUST remain separate from the Client Universe.

Never create a fake GFCID/client_id for an external entity.

Never insert an external entity into Customer_latest.parquet.

==================================================
5. ENTITY DEDUPLICATION
==================================================

External entity creation must be idempotent.

Deduplicate only using strong identifiers such as:

LEI
CIK
other authoritative registration ID

or exact deterministic identity evidence.

Do NOT collapse companies because their names are similar.

Report:

external entities attempted
external entities created
existing external entities reused
ambiguous external identities
unresolved external identities
fuzzy merges

Fuzzy merges MUST equal 0.

==================================================
6. RE-EVALUATE EXISTING RELATIONSHIP CANDIDATES
==================================================

Once endpoint identity has been established, rerun the existing Stage 2A.2
acceptance policy.

Identity resolution alone does NOT create a relationship.

For each candidate independently validate:

subject identity
related endpoint identity
relationship taxonomy
direction
relationship semantics
admissible evidence
evidence specificity
AsOfDate
status support
materiality support if present

Then assign:

RELATIONSHIP_OBSERVATION
RELATIONSHIP_CANDIDATE
NO_EVIDENCE
REJECTED_INVALID

Do not weaken the existing evidence gate.

==================================================
7. SPECIFIC 3M ENDPOINTS
==================================================

Inspect all named entities actually contained in the imported result.

Where present, specifically test:

3M India Limited
Aearo / Aearo Technologies / Aearo Holding Corp.
3M Belgium
Solventum Corporation
BNY Mellon
Cabot Corporation
EPA
and every other NAMED endpoint in the persisted result.

Do not assume any of these are external.

Search the Client Universe first.

For each report:

input name
internal match result
resolved internal client_id if applicable
external identity result if applicable
LEI
CIK
official domain
final endpoint class
relationship candidate outcome

==================================================
8. UNNAMED ENDPOINT RULE
==================================================

DO NOT create entity nodes for:

unnamed suppliers
unnamed lenders
unnamed insurers
unnamed technology vendors
generic groups
industry descriptions
facility descriptions

Keep these as unresolved relationship candidates.

No entity should exist with names like:

"Unnamed Supplier"
"Revolving Credit Facility Syndicate Lenders"

==================================================
9. PATH RECOMPUTATION
==================================================

After any newly accepted direct observations are persisted:

recompute bounded evidence-backed paths.

Only accepted observations may form graph hops.

Candidate relationships must not form confirmed hidden paths.

Do not generate direct A->C shortcuts from A->B->C.

Report:

accepted direct relationships
candidate relationships
external entity endpoints
internal endpoints
multi-hop paths
synthetic shortcut edges

Synthetic shortcut edges MUST remain 0.

==================================================
10. IDEMPOTENCE
==================================================

Run the exact Stage 2A.4 resolution process twice.

Second execution must not duplicate:

external entities
identifier aliases
relationship observations
evidence links
candidate records
paths

==================================================
11. REPORT
==================================================

Create:

backend/data/EXTERNAL_ENTITY_RESOLUTION_STAGE_2A4_REPORT.md

Include a table for every Stage 2A.3 candidate:

related endpoint
relationship type
initial state
Client Universe match
external identity resolution
strong identifiers
identity authority
final endpoint type
final relationship state
reason

Final totals:

existing candidates processed
internal Client Universe endpoints resolved
external entities created
external entities reused
generic descriptors retained
ambiguous identities
unresolved named identities
promoted observations
remaining candidates
no-evidence findings
accepted direct edges
derived paths
synthetic shortcuts
fuzzy merges
duplicate records on replay
Customer_latest.parquet modified

PASS REQUIREMENTS

Customer_latest.parquet modified = NO
fuzzy merges = 0
generic descriptor entities created = 0
synthetic shortcut edges = 0
duplicate records after replay = 0
all external entities have defensible identity provenance

STOP after the bounded 3M external identity-resolution pilot.

Do not start broad 3.67M research.
Do not build the network UI yet.
