CLIENT CORRELATION — STAGE 2A.3
REAL STYLUS RESULT INGESTION PILOT — 3M ONLY

Stage 2A.2 is complete.

Now perform ONE bounded end-to-end ingestion pilot using the actual exported
Stylus relationship-research JSON for 3M Company.

DO NOT call Stylus.
DO NOT call SEC/Web/GLEIF.
DO NOT perform new external research.
DO NOT process any other Client Universe client.
DO NOT modify Customer_latest.parquet.
DO NOT build the network UI.
DO NOT loosen any Stage 2A.2 validation gates.

Locate the manually exported Stylus JSON supplied by the user under:

backend/data/stylus_import/

Use the actual file exactly as supplied.
Do not rewrite, normalize, enhance, or regenerate its research content.

OBJECTIVE

Prove the production path:

actual Stylus JSON
    ->
schema validation
    ->
3M Client Universe subject resolution
    ->
related endpoint resolution
    ->
evidence validation
    ->
observation/candidate/no-evidence classification
    ->
relationship repository persistence
    ->
bounded read API verification

==================================================
1. SUBJECT RESOLUTION
==================================================

Resolve "3M Company" against the Stage 1 Client Universe BEFORE accepting
any relationship finding.

Report the exact resolved:

client_id
gfcid
source_master_id
legal_name
matching identifier/method

The persisted subject endpoint for every valid 3M relationship MUST use the
resolved Client Universe client_id.

A subject client_id of null after ingestion is FAIL.

Do not use fuzzy matching.

==================================================
2. INGEST THE ACTUAL STYLUS RESULT
==================================================

Persist the raw imported Stylus response for audit.

Run every finding through the existing Stage 2A.2 acceptance gates.

Do not trust Stylus classifications automatically.

For every finding determine:

ACCEPTED OBSERVATION
CANDIDATE
NO_EVIDENCE
REJECTED_INVALID

with an explicit machine-readable reason.

==================================================
3. RELATED ENTITY RESOLUTION
==================================================

For every NAMED related entity:

First attempt deterministic Client Universe resolution using approved exact
identifiers and normalized exact aliases/names.

If exactly one Client Universe client resolves:
bind its client_id.

If the entity is clearly identifiable but does not exist in Client Universe:
use external_entities.

If identity cannot be established:
retain as candidate/unresolved.

Generic descriptors MUST NOT become entity records.

Explicitly test examples from the 3M output such as:

Revolving Credit Facility Syndicate Lenders
Unnamed Limited- and Sole-Source Suppliers
Unnamed ERP / IT Infrastructure Vendor
Unnamed Pension Annuity Insurer

These must NOT be created as real entities.

==================================================
4. NAMED FINDINGS
==================================================

Inspect named entities returned by the real Stylus file, including where
present examples such as:

3M India Limited
Solventum Corporation
Aearo entities / Aearo Technologies
3M Belgium
BNY Mellon
Cabot Corporation
EPA or other regulator/counterparty entities

Do not assume they are all valid observations.

Validate identity, relationship semantics, direction and evidence separately.

Report whether each resolved as:

INTERNAL_CLIENT
EXTERNAL_ENTITY
UNRESOLVED
REJECTED

==================================================
5. RELATIONSHIP SEMANTICS
==================================================

Verify that:

- subsidiary remains subsidiary
- equity investor remains equity investor
- strategic partner remains strategic partner
- lender requires an identified lender endpoint
- supplier requires an identified supplier endpoint for observation status
- legal counterparty remains the correct directional semantic
- regulator relationships are accepted only if permitted by the controlled taxonomy
- service-provider findings require an identified counterparty

Do not manufacture a relationship because Stylus labelled it one.

==================================================
6. EVIDENCE
==================================================

For each accepted observation report:

relationship type
subject
related entity
direction
source channel
source tier
source reference
publication date
number of admissible evidence objects

Preserve separate SEC and Web evidence objects.

Do not invent a URL or convert a generic source description into a precise
source reference.

==================================================
7. HIDDEN / INDIRECT PATH TEST
==================================================

After direct observations are accepted, derive paths only from accepted
observations.

Example concept:

3M
 -> Aearo
 -> another counterparty

may produce a relationship path if both hops independently pass.

It must NOT produce a synthetic direct relationship.

Report:

accepted direct edges
derived multi-hop paths
synthetic shortcut edges

Synthetic shortcut edges MUST equal 0.

==================================================
8. PERSISTENCE AND REPLAY
==================================================

The ingestion must be idempotent.

Import the exact same 3M Stylus result twice.

The second import must NOT duplicate:

research run content
relationship observations
candidates
evidence
external entities
paths

Use deterministic provenance/content hashes or equivalent repository-level
deduplication.

Report first-import and second-import counts.

==================================================
9. API VERIFICATION
==================================================

Using the resolved 3M client_id, exercise:

GET /api/relationships/{client_id}
GET /api/relationships/{client_id}/candidates
GET /api/relationships/{client_id}/paths
GET /api/relationships/{client_id}/evidence
GET /api/relationships/{client_id}/summary

Confirm bounded responses and correct Client Universe identity.

==================================================
10. REPORT
==================================================

Create:

backend/data/RELATIONSHIP_REAL_3M_INGESTION_STAGE_2A3_REPORT.md

Include:

Stylus source artifact name
raw findings count
3M resolved client_id
3M resolved GFCID
accepted observations
candidates
no-evidence findings
rejected findings
internal related clients resolved
external entities created
unresolved endpoint descriptors
evidence objects
direct edges
multi-hop paths
synthetic shortcut edges
fuzzy merges
duplicate records after second import
source master modified

Then provide a table for every Stylus finding:

related entity
relationship type
Stylus classification
application classification
endpoint resolution
evidence result
final persisted state
reason

PASS criteria:

3M internal client_id non-null
synthetic shortcuts = 0
fuzzy merges = 0
generic unnamed entity nodes = 0
duplicate records after replay = 0
Customer_latest.parquet modified = NO

STOP after this bounded 3M pilot.
