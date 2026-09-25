CLIENT CORRELATION — STAGE 2A.6
BOUNDED MULTI-HOP / HIDDEN RELATIONSHIP DISCOVERY

Work only in the CURRENT clean-reset repository.

Do not redesign the frontend.
Do not modify Customer_latest.parquet.
Do not alter the 3.67M Client Universe identity model.
Do not perform a portfolio-wide external research run.
Do not fabricate relationships, identities, evidence, paths, or scores.

CURRENT VERIFIED FOUNDATION

- Client Universe: 3,670,650 clients.
- GFCID is the unique client-grain source identity.
- Stage 2A.5 completed successfully.
- SEC, approved Web, and GLEIF are READY.
- Accepted relationship observations currently exist.
- Solventum and Cabot provide positive-control relationships.
- Replay/idempotence is working.
- No fuzzy merges.
- No synthetic shortcuts.
- No source-master modification.
- Current hidden paths: 0.

OBJECTIVE

Prove that the system can discover genuine evidence-backed MULTI-HOP relationships starting from one selected Client Universe client.

This stage is NOT about discovering as many relationships as possible.

It is about establishing a defensible graph-expansion architecture that can later scale safely.

PRIMARY PILOT SUBJECT

Use the existing bounded 3M subject already used by Stages 2A.3–2A.5.

Do not create a new unrelated pilot.

CORE PRINCIPLE

SEARCH BROADLY.
ACCEPT NARROWLY.
EXPAND ONLY FROM ACCEPTED EDGES.

A candidate edge must NEVER be used as a graph hop.

A multi-hop path does NOT create a synthetic direct relationship between the path endpoints.

Example:

3M -> Solventum -> Entity X

does NOT mean:

3M -> Entity X

unless independent admissible evidence separately establishes that direct relationship.

--------------------------------------------------
1. GRAPH EXPANSION MODEL
--------------------------------------------------

Implement bounded graph traversal from the selected subject.

Initial maximum depth:

DEPTH 0:
selected Client Universe subject

DEPTH 1:
existing accepted relationships of subject

DEPTH 2:
accepted relationships discovered around accepted Depth-1 entities

DEPTH 3:
accepted relationships discovered around accepted Depth-2 entities

Maximum depth = 3.

Make depth configurable but default to 3.

Do not go beyond depth 3 in this stage.

--------------------------------------------------
2. BRANCHING CONTROL
--------------------------------------------------

Prevent graph explosion.

For every expandable entity:

- consider only evidence-backed relationship observations;
- rank/select only the strongest relevant accepted relationships;
- maximum expansion fan-out = 5 accepted edges per entity;
- candidates do not consume the accepted expansion allowance;
- unresolved generic descriptors must never be expansion nodes;
- NO_EVIDENCE records must never be expansion nodes.

Make fan-out configurable.

Default:

max_depth = 3
max_accepted_edges_per_node = 5

--------------------------------------------------
3. ENTITY RESOLUTION ORDER
--------------------------------------------------

For every discovered named entity:

FIRST:
attempt exact resolution into the 3.67M Client Universe.

Use exact supported identity fields only:
- client_id
- GFCID
- deterministic source_master_id
- exact normalized legal/canonical name
- approved aliases
- exact known legal entity identifiers

NO fuzzy matching.

If no defensible Client Universe match exists:

SECOND:
attempt governed external identity resolution using available approved providers.

Only create/reuse an external entity when identity acceptance gates pass.

If identity remains unresolved:

retain the relationship as candidate/unresolved.

Do not create an entity merely from descriptive text.

--------------------------------------------------
4. EXTERNAL RESEARCH
--------------------------------------------------

Research may use only approved provider infrastructure already implemented:

- SEC_FILINGS
- R2D2_WEB / approved Web
- GLEIF

Reuse:
- cache
- provenance
- evidence quality
- source policies
- identity gates
- AsOfDate
- replay protection
- provider audit logging

Do not bypass the existing provider layer.

Do not make direct uncontrolled internet calls.

--------------------------------------------------
5. PATH DEFINITION
--------------------------------------------------

Create a hidden/multi-hop path only when EVERY hop is an accepted relationship observation.

Example valid path:

Client A
 --accepted relationship-->
 External Entity B
 --accepted relationship-->
 Client C

or

Client A
 -> Client B
 -> External C
 -> Client D

Each path must preserve:

- ordered node IDs
- ordered relationship observation IDs
- relationship type per hop
- direction per hop
- connectivity per hop
- evidence references per hop
- evidence quality per hop
- relationship status per hop
- source channel per hop
- AsOfDate
- created/retrieved timestamps
- path depth
- path endpoint classifications
- whether endpoint is Client Universe or external

--------------------------------------------------
6. HIDDEN CLIENT-TO-CLIENT CORRELATION
--------------------------------------------------

A particularly important result is:

CLIENT UNIVERSE CLIENT
    ->
one or more accepted intermediaries
    ->
ANOTHER CLIENT UNIVERSE CLIENT

Classify this as:

HIDDEN_CLIENT_PATH

Do NOT classify it as a direct relationship.

Also support:

CLIENT_TO_EXTERNAL_PATH
EXTERNAL_TO_CLIENT_PATH
EXTERNAL_TO_EXTERNAL_PATH

but Client-to-Client hidden paths are the primary business outcome.

--------------------------------------------------
7. PATH STRENGTH
--------------------------------------------------

Do not invent a numerical AI score.

Path strength must be based on existing governed relationship/evidence properties.

The strength of a multi-hop path must never exceed its weakest hop.

If any hop later becomes invalid/unaccepted, the path must no longer qualify as accepted.

Store path state explicitly.

Suggested states:

ACCEPTED_PATH
CANDIDATE_PATH
INVALIDATED_PATH

For this stage, only ACCEPTED_PATH may be treated as a validated hidden correlation.

--------------------------------------------------
8. CYCLE / DUPLICATE CONTROL
--------------------------------------------------

Implement:

- visited entity control per traversal;
- no immediate A -> B -> A loops;
- deterministic path fingerprints;
- duplicate path suppression;
- deterministic replay;
- canonical path ordering only where semantics permit;
- preserve direction.

Do not merge semantically different paths merely because endpoints match.

--------------------------------------------------
9. STORAGE ARCHITECTURE
--------------------------------------------------

Keep the storage design scalable and adapter-driven.

Do not couple application logic directly to SQLite.

Add repository contracts/interfaces for:

- graph neighbors
- accepted observations
- path persistence
- traversal runs
- expansion frontier
- path retrieval

SQLite remains the current local adapter.

The design must remain migratable later to PostgreSQL / graph-capable storage without rewriting business logic.

Do NOT migrate databases in this stage.

--------------------------------------------------
10. TRAVERSAL RUN MODEL
--------------------------------------------------

Persist a bounded traversal run with:

- traversal_run_id
- root client_id
- root GFCID
- max_depth
- fanout limit
- AsOfDate
- started_at
- completed_at
- status
- provider attempts
- nodes evaluated
- accepted edges inspected
- candidates encountered
- new identities resolved
- new accepted observations
- paths found
- hidden Client Universe endpoint paths found
- replay fingerprint

Exact replay must not create duplicate provider attempts, entities, observations, evidence, or paths.

--------------------------------------------------
11. BOUNDED 3M PILOT
--------------------------------------------------

Run ONE bounded pilot.

Root:
existing 3M Client Universe entity.

Start from the currently accepted graph.

Expand accepted related entities.

Try to reach at least depth 2.

Depth 3 may be used only where the evidence permits it.

Do NOT loosen acceptance criteria merely to create a path.

A correct result of zero hidden paths is acceptable if the evidence does not support them.

The purpose is to prove architecture and traversal correctness.

--------------------------------------------------
12. REQUIRED API
--------------------------------------------------

Add bounded read APIs only as necessary, such as:

GET /api/relationships/{client_id}/network

GET /api/relationships/{client_id}/paths

GET /api/relationships/{client_id}/neighbors

GET /api/relationship-traversals/{traversal_run_id}

Support depth parameter only within the governed maximum.

Example:

?depth=1
?depth=2
?depth=3

Never return millions of nodes.

Use bounded pagination / cursors where appropriate.

--------------------------------------------------
13. REQUIRED TESTS
--------------------------------------------------

Test at minimum:

- accepted edge can be traversed;
- candidate edge cannot be traversed;
- NO_EVIDENCE cannot be traversed;
- unresolved generic descriptor cannot become a node;
- exact Client Universe resolution is preferred over external entity creation;
- external entity created only after identity gates pass;
- 2-hop accepted path persistence;
- 3-hop accepted path persistence;
- weakest-hop rule;
- path does not create a synthetic direct relationship;
- cycle prevention;
- duplicate path prevention;
- replay/idempotence;
- direction preservation;
- same endpoints with different semantic paths remain distinct;
- no fuzzy identity merge;
- source master remains unchanged;
- provider errors do not generate accepted relationships;
- depth limit enforced;
- fan-out limit enforced.

Run the complete backend regression suite afterward.

--------------------------------------------------
14. REPORT
--------------------------------------------------

Create:

backend/data/HIDDEN_RELATIONSHIP_DISCOVERY_STAGE_2A6_REPORT.md

Report:

CLIENT UNIVERSE ROWS:
ROOT SUBJECT:
ROOT CLIENT_ID:
ROOT GFCID:

MAX DEPTH:
FANOUT:

TRAVERSAL STATUS:

NODES EVALUATED:
CLIENT UNIVERSE NODES:
EXTERNAL NODES:

ACCEPTED EDGES INSPECTED:
NEW ACCEPTED EDGES:
CANDIDATES RETAINED:
UNRESOLVED ENTITIES:

SEC ATTEMPTS:
WEB ATTEMPTS:
GLEIF ATTEMPTS:

2-HOP PATHS:
3-HOP PATHS:
HIDDEN CLIENT-TO-CLIENT PATHS:

SYNTHETIC DIRECT RELATIONSHIPS CREATED: 0 / FAIL
FUZZY MERGES: 0 / FAIL
MASTER CLIENT ROWS MODIFIED: 0 / FAIL
GENERIC DESCRIPTORS USED AS NODES: 0 / FAIL
CANDIDATE EDGES USED IN ACCEPTED PATHS: 0 / FAIL

REPLAY:
PASS / FAIL

FULL BACKEND TESTS:
PASS / FAIL

SCALABLE REPOSITORY BOUNDARY:
PASS / FAIL

Then show the most informative discovered path, if any, as:

ROOT
  -> relationship type / direction / evidence source
ENTITY
  -> relationship type / direction / evidence source
ENTITY

If no valid hidden path is discovered, report that honestly.

Do not fabricate one to obtain a successful-looking result.

STOP after Stage 2A.6.
Do not build the network UI yet.
