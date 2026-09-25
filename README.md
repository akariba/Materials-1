IMPORTANT ARCHITECTURE AMENDMENT — APPLY TO THE CURRENT CLIENT UNIVERSE BUILD

Do not restart the task.

Apply these requirements to the implementation already in progress.

The ~3.67M client universe must be engineered at LEAD / PRINCIPAL-LEVEL
quality, not as a one-off SQLite import.

The local implementation may use SQLite today, but the DATA MODEL,
QUERY CONTRACTS and APPLICATION LAYERS must be scalable and portable.

==================================================
1. ARCHITECTURAL PRINCIPLE
==================================================

Separate four concepts explicitly:

1. AUTHORITATIVE SOURCE
   Customer_latest.parquet
   immutable source snapshot

2. OPERATIONAL CLIENT UNIVERSE
   optimized searchable representation of the master clients

3. RELATIONSHIP INTELLIGENCE
   future graph/relationship observations, evidence and paths

4. APPLICATION/API
   must not depend directly on SQLite-specific SQL everywhere

Do NOT mix all four into one giant database/table.

==================================================
2. DATABASE ROLE
==================================================

client_universe.sqlite3 is the LOCAL operational implementation.

Do not design the product so that business logic assumes:

database = SQLite forever

Create a clean persistence/repository boundary so the implementation can later
move to PostgreSQL or another server-grade relational engine without changing
business logic or API contracts.

SQLite-specific details should remain inside the storage implementation.

==================================================
3. PRIMARY KEY DESIGN
==================================================

Use a compact internal surrogate key for joins.

Preferred concept:

client_id INTEGER PRIMARY KEY

Keep natural/source identifiers separately:

gfcid
cagid
legal_entity_id
source_master_id

Do not use long text identifiers as every internal foreign key.

Do not replace the source identifiers.

The pattern should be:

internal client_id
+
source identifiers

This will matter when millions of relationship edges are added later.

==================================================
4. DO NOT CREATE A GIANT UNCONTROLLED WIDE TABLE
==================================================

Keep client_master focused on commonly accessed canonical attributes.

Do not duplicate large text fields or identifier values unnecessarily.

Use separate structures where justified:

client_master
client_identifiers
client_aliases
source_lineage
ingestion_runs
data_quality_issues

Do not over-normalize either.

The goal is:

fast entity lookup
fast relationship joins
clear provenance
manageable schema evolution

==================================================
5. FUTURE RELATIONSHIP SCALE
==================================================

Design client_id so the future graph can reference the complete 3.67M
population efficiently.

Future relationship storage should conceptually support:

relationship_id
source_client_id
target_client_id
relationship_type
direction
state
first_observed_at
last_observed_at

Evidence and source documents must be separate from relationship edges.

DO NOT build those tables in this task unless a minimal empty schema is
required for architectural compatibility.

Do not populate relationships.

==================================================
6. INDEX STRATEGY
==================================================

Indexes must be deliberate.

Do not simply index every column.

Build indexes based on real query patterns.

At minimum evaluate:

UNIQUE / lookup:
gfcid where uniqueness is validated

LOOKUP:
cagid
legal_entity_id

SEARCH:
normalized_legal_name

FILTER:
country
industry
sector

IDENTIFIER TABLE:
(identifier_type, normalized_value)

Potential relationship joins later:
client_id

Use EXPLAIN QUERY PLAN to prove representative queries use indexes.

Avoid indexes that materially increase storage/write cost without supporting
a real query.

==================================================
7. SEARCH ARCHITECTURE
==================================================

Do NOT implement search as:

LIKE '%query%'

against 3.67M rows.

Use an appropriate indexed search layer.

SQLite:
FTS5 where available and appropriate.

Keep the search contract implementation-independent so it could later become:

PostgreSQL full-text search
pg_trgm
OpenSearch / Elasticsearch

without changing the frontend search API.

==================================================
8. PAGINATION
==================================================

Do not use large OFFSET pagination as the primary architecture.

For large result sets prefer stable keyset/cursor pagination.

Example concept:

after=<sort_key/client_id>

API responses should expose bounded result sets.

Never return arbitrary millions of records.

==================================================
9. INGESTION ARCHITECTURE
==================================================

The 3.67M import must be:

streamed/batched
transactional
restartable
idempotent
observable

Do not load all source rows into memory.

Persist an ingestion_run record containing:

run_id
source path
source SHA-256
source row count
started_at
completed_at
status
rows_processed
rows_inserted
rows_rejected
schema_version

If the same source hash is already successfully ingested, do not accidentally
duplicate the universe.

==================================================
10. SCHEMA VERSIONING
==================================================

Introduce an explicit schema version / migration mechanism.

Do not evolve the production schema through ad-hoc:

CREATE TABLE IF NOT EXISTS

inside GET/read requests.

All schema creation and migrations must happen through controlled startup,
migration or build procedures.

Read APIs must remain read-only.

==================================================
11. DATA TYPE DISCIPLINE
==================================================

Do not store everything as arbitrary TEXT merely because the source came from
Parquet.

Select appropriate types based on actual semantics.

However:

identifiers that may contain leading zeroes must remain TEXT.

Examples likely requiring TEXT:

GFCID
CAGID
LEI
CIK if treated as identifier
source IDs

Do not silently coerce identifiers to numeric values.

==================================================
12. NULL / UNKNOWN SEMANTICS
==================================================

Maintain strict distinction among:

NULL
empty string
not supplied
not applicable
unresolved

Do not populate fake defaults.

Do not use:

UNKNOWN
N/A
0

unless those values genuinely came from the authoritative source.

==================================================
13. SOURCE PRESERVATION
==================================================

Customer_latest.parquet remains immutable.

Never rewrite it as part of application operation.

Record:

SHA-256
row count
schema
ingestion timestamp

The operational database is derived and rebuildable from the authoritative
source.

==================================================
14. QUERY SERVICE BOUNDARY
==================================================

Create a clear application service/repository abstraction.

Conceptually:

ClientRepository
    get_client()
    find_by_identifier()
    search_clients()
    list_clients()
    get_identifiers()

Business/API code should use that contract.

It should NOT contain raw SQLite SQL scattered throughout route handlers.

==================================================
15. API DESIGN
==================================================

Design API contracts so millions of records remain manageable.

Example:

GET /api/clients/search?q=&limit=&cursor=

Response should include:

items
next_cursor
has_more

Do not expose database row offsets as the public contract.

Client detail should resolve via stable client key.

==================================================
16. CONCURRENCY / LOCAL SQLITE
==================================================

For the local deployment evaluate appropriate SQLite operational settings,
including WAL where appropriate.

Do not blindly set performance PRAGMAs.

Document:

journal mode
synchronous mode
foreign keys
busy timeout
read/write connection strategy

Optimize for:

many reads
rare controlled writes

which matches the client-universe workload.

==================================================
17. ANALYZE / QUERY PLANNER
==================================================

After loading/indexing the database:

run the appropriate ANALYZE process.

Validate query plans for representative searches.

Report whether scans are:

INDEX SEARCH
FTS SEARCH
FULL TABLE SCAN

Unexpected full scans on interactive endpoints are a FAIL.

==================================================
18. PERFORMANCE TARGETS
==================================================

On the current workstation, use measurable practical targets.

Target where realistically achievable:

exact identifier lookup:
< 100 ms warm

client detail:
< 100 ms warm

name search returning first page:
< 300 ms warm

filtered search:
< 500 ms warm

These are engineering targets, not reasons to fake results.

Report actual numbers even if slower.

==================================================
19. SCALE TEST
==================================================

Validate against the COMPLETE universe.

Do not demonstrate scalability using a 10k-row development subset.

Test:

3.67M-row database startup
concurrent/sequential searches
repeated search
deep result navigation through cursor pagination
identifier lookups
filter combinations

Watch memory consumption.

The API must not materialize giant result sets.

==================================================
20. DATABASE SIZE / DUPLICATION
==================================================

Report:

source Parquet size
SQLite database size
index size where practical
FTS size
total storage multiplication

Avoid needless copies of the complete source payload.

The operational database may be larger than the Parquet because of indexes,
but the growth must be explainable.

==================================================
21. FUTURE SERVER DEPLOYMENT
==================================================

Document the migration path, but DO NOT implement it now.

Target future architecture could be:

Authoritative Parquet
        ↓
ingestion
        ↓
PostgreSQL client universe
        ↓
relationship/evidence store
        ↓
API
        ↓
network application

The local SQLite implementation must preserve compatible concepts.

Do NOT introduce PostgreSQL today unless there is a concrete requirement.

==================================================
22. FUTURE GRAPH SCALE
==================================================

Do not assume that all possible pairs across 3.67M clients can be materialized.

3.67M × 3.67M pairwise comparison is not a valid architecture.

Correlation discovery later must use:

candidate generation
blocking
indexed attributes
relationship-specific presets
external search
bounded graph expansion

Never perform naïve all-to-all correlation.

This requirement is CRITICAL.

==================================================
23. LEAD-LEVEL QUALITY GATES
==================================================

The implementation should demonstrate:

clear responsibility boundaries
schema documentation
migration/versioning
deterministic ingestion
idempotency
source lineage
indexed queries
bounded APIs
cursor pagination
no hidden writes on reads
no unbounded memory operations
no all-to-all comparisons
clean rollback/rebuild path
storage portability
tests for important invariants

==================================================
24. ADD TO THE CURRENT REPORT
==================================================

Extend:

backend/data/CLIENT_UNIVERSE_BUILD_REPORT.md

with sections:

Architecture
Schema rationale
Identity strategy
Index strategy
Search architecture
Pagination strategy
Ingestion/rebuild strategy
SQLite operational configuration
Query-plan validation
Storage footprint
Performance benchmarks
Scale limitations
PostgreSQL migration path
Future graph/relationship architecture

==================================================
FINAL ARCHITECTURAL GATE
==================================================

In the final response also include:

ARCHITECTURE QUALITY:
PASS / FAIL

FULL 3.67M DATASET USED:
YES / NO

STREAMING INGESTION:
PASS / FAIL

IDEMPOTENT REBUILD:
PASS / FAIL

SCHEMA VERSIONED:
YES / NO

READ ENDPOINTS MUTATE DATABASE:
NO / FAIL

KEYSET/CURSOR PAGINATION:
PASS / FAIL

FTS/INDEXED NAME SEARCH:
PASS / FAIL

UNEXPECTED FULL TABLE SCANS:
0 / <count>

SOURCE LINEAGE:
PASS / FAIL

REPOSITORY/STORAGE ABSTRACTION:
PASS / FAIL

SQLITE-SPECIFIC LOGIC ISOLATED:
YES / NO

NAIVE ALL-TO-ALL CORRELATION:
NOT USED / FAIL

FUTURE SERVER MIGRATION PATH:
DOCUMENTED / FAIL
