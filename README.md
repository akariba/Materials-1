CLIENT CORRELATION — STAGE 2A.2
RELATIONSHIP INGESTION, IDENTITY RESOLUTION AND ACCEPTANCE GATE

Work only in the CURRENT clean-reset repository.

DO NOT modify the authoritative source:
backend/Customer_latest.parquet

DO NOT change the Stage 1 Client Universe semantics.

DO NOT restore any old CCR database, CCR workflow, old frontend, dashboards, reports or relationship data.

DO NOT redesign the frontend in this task.

DO NOT execute large-scale external research.

DO NOT change the validated Stylus relationship-research policy unless technically necessary to consume its existing output contract.

OBJECTIVE

Build the production-grade application layer that converts external relationship-research results into governed Client Correlation observations, candidates, evidence and paths anchored to the authoritative 3,670,650-client universe.

The relationship system must be storage-independent and scalable.

==================================================
1. CLIENT UNIVERSE IS THE INTERNAL IDENTITY ANCHOR
==================================================

All research initiated for an internal client must begin from the Stage 1 ClientRepository.

Resolve the selected subject before research.

The application research context must include, where available:

client_id
gfcid
source_master_id
legal_name
known aliases
CAGID
legal_entity_id
country
other source identifiers required for deterministic identity resolution

Never send only a free-text company name when the selected subject is already an internal Client Universe entity.

The Client Universe establishes INTERNAL IDENTITY ONLY.

It does NOT itself establish an external relationship.

==================================================
2. CREATE NEW RELATIONSHIP REPOSITORY
==================================================

Create a completely new relationship repository and schema.

Do not reuse or migrate the archived CCR relationship database.

Follow the same architectural principle as Stage 1:

application repository contract
    ↓
storage adapter
    ↓
SQLite implementation now
    ↓
future PostgreSQL-compatible implementation later

Suggested logical entities:

research_runs
external_entities
relationship_observations
relationship_candidates
relationship_evidence
relationship_paths
relationship_path_hops

You may refine the physical schema if a better lead-level design exists.

Required semantics:

RELATIONSHIP_OBSERVATION
= sufficiently identified endpoints + admissible evidence + supported taxonomy + supported direction/connectivity/status semantics.

RELATIONSHIP_CANDIDATE
= relationship signal exists but one or more acceptance requirements remain unresolved.

NO_EVIDENCE
= requested relationship was not established from admissible evidence.

MENTION_ONLY
must never become a relationship.

==================================================
3. INTERNAL AND EXTERNAL ENDPOINT RESOLUTION
==================================================

Every endpoint must be resolved independently.

For each discovered related entity:

A. Search exact approved identifiers against Client Universe first.

B. Then deterministic normalized alias/name resolution where defensible.

C. If exactly one internal Client Universe entity is established:
   bind relationship endpoint to client_id.

D. If it is a real identifiable entity but not in Client Universe:
   create/reference external_entities.

E. If endpoint identity is unresolved:
   do NOT create a resolved entity.
   keep the result as a candidate with unresolved endpoint information.

Examples such as:

"Unnamed Limited- and Sole-Source Suppliers"
"Revolving Credit Facility Syndicate Lenders"
"Unnamed ERP / IT Infrastructure Vendor"
"Unnamed Pension Annuity Insurer"

must NOT be persisted as real entity nodes.

They remain unresolved candidate descriptors.

No fuzzy entity merges.

No automatic entity creation from vague text.

==================================================
4. STYLUS RESULT CONTRACT
==================================================

Build a parser/validator for the existing Stylus relationship research JSON contract.

Do not assume every returned finding is acceptable.

Process every finding through explicit gates:

1 schema valid
2 subject identity valid
3 related-entity identity status
4 relationship_type allowed
5 evidence present where required
6 evidence source admissible
7 source reference/provenance usable
8 direction supported by evidence
9 connectivity supported
10 temporal status supported
11 materiality treatment valid
12 direct/indirect semantics valid

Persist the raw research result separately from accepted normalized records for audit/replay.

Never silently repair unsupported claims.

==================================================
5. DIRECT VS INDIRECT RELATIONSHIPS
==================================================

This is critical.

Do not flatten evidence-backed multi-hop relationships.

Example:

3M -> Aearo Technologies
Aearo Technologies -> Cabot Corporation

must remain two direct observations.

The system may additionally derive a relationship PATH:

3M -> Aearo Technologies -> Cabot Corporation

but it must NOT create a synthetic direct 3M -> Cabot relationship unless separate evidence directly supports it.

Create:

relationship_paths
relationship_path_hops

Each hop must reference an accepted relationship observation.

Overall path strength cannot exceed the weakest hop.

A broken/unresolved hop invalidates the complete hidden path.

==================================================
6. EVIDENCE MODEL
==================================================

Evidence must be first-class data.

Every accepted observation must have at least one admissible evidence object.

Persist fields such as:

source_channel
source_tier
source_title
source_reference
publication_date
exact_excerpt
evidence_role
retrieved_at
content/source hash where available
research_run_id

Do not fabricate URLs, dates, excerpts or source identifiers.

Keep SEC evidence and Web evidence as separate evidence objects even when they support one semantic relationship.

==================================================
7. OBSERVATION VS CANDIDATE
==================================================

A result with unresolved endpoint identity must remain a candidate.

Examples from the current 3M test:

named and identified subsidiary with explicit SEC evidence
→ potentially RELATIONSHIP_OBSERVATION

named Solventum relationship with defensible endpoint identity and evidence
→ potentially RELATIONSHIP_OBSERVATION

unnamed credit facility lenders
→ RELATIONSHIP_CANDIDATE

unnamed sole-source suppliers
→ RELATIONSHIP_CANDIDATE

unnamed ERP vendor
→ RELATIONSHIP_CANDIDATE

unnamed pension insurer
→ RELATIONSHIP_CANDIDATE

joint venture requested but no named counterparty established
→ NO_EVIDENCE

Do not promote candidates automatically.

==================================================
8. SCALE AND STORAGE
==================================================

Design for:

3,670,650 internal clients
potentially millions of external entities
tens or hundreds of millions of future relationship observations/evidence records

Do NOT preload a giant graph in memory.

Use integer internal keys, indexed foreign keys and bounded queries.

Required indexing concepts:

subject/client endpoint
related/client endpoint
external entity endpoint
relationship type
relationship status
research run
source/evidence reference
observation state
candidate state

Graph traversal must later be bounded by depth and result count.

Repository methods must support migration from SQLite to PostgreSQL without changing route/business semantics.

==================================================
9. READ API
==================================================

Add bounded read APIs only.

Examples:

GET /api/relationships/{client_id}

GET /api/relationships/{client_id}/candidates

GET /api/relationships/{client_id}/paths

GET /api/relationships/{client_id}/evidence

GET /api/relationships/{client_id}/summary

All must be cursor/keyset bounded where lists can grow.

Do not build the graphical network page yet.

==================================================
10. TEST USING 3M ONLY
==================================================

Use the existing 3M Stylus result as a bounded fixture/sample.

Do NOT run research for the full 3.67M population.

Validate specifically that:

- 3M resolves to the Client Universe internal client.
- subject client_id is no longer null after application-side enrichment.
- named defensible endpoints can resolve to Client Universe or external entity.
- unresolved generic endpoints remain candidates.
- no fake entity is created for "Unnamed Suppliers", etc.
- direct relationships remain direct.
- evidence-backed multi-hop paths remain paths.
- no synthetic shortcut edge is created.
- NO_EVIDENCE is retained correctly.
- exact source evidence remains traceable.

==================================================
11. REPORT
==================================================

Create:

backend/data/RELATIONSHIP_INGESTION_STAGE_2A2_REPORT.md

Report:

schema created
repository architecture
indexes
3M internal identity resolution result
number of raw findings consumed
observations accepted
candidates retained
no-evidence findings
internal related entities resolved
external entities resolved
unresolved entities
evidence objects persisted
direct observations
indirect paths
synthetic shortcut relationships created: MUST BE 0
fuzzy merges performed: MUST BE 0
source master modified: MUST BE NO

Run tests and provide concise PASS/FAIL results.

STOP after Stage 2A.2.

Do not build the network UI yet.
Do not process the entire 3.67M universe through Stylus.
Do not restore the old CCR product.
