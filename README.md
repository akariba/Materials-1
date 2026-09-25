CLIENT CORRELATION — STAGE 1
BUILD THE 3.67M MASTER CLIENT DATABASE

Work only in the CURRENT clean-reset repository.

AUTHORITATIVE SOURCE:

backend/Customer_latest.parquet

Known source row count:

3,670,650

Known source columns:

21

IMPORTANT

This task is ONLY about building the master client/entity database.

Do NOT:
- restore the old CCR application
- use the old 16k population
- use thousandClients.csv
- create relationships
- create correlation candidates
- call SEC
- call GLEIF
- call Web
- build a graph
- build AI
- build dashboards

The 3.67M master source is the foundation.

==================================================
1. PROFILE THE AUTHORITATIVE SOURCE FIRST
==================================================

Inspect:

backend/Customer_latest.parquet

Read schema and metadata without loading the entire dataset into memory.

Report the exact 21 columns with:

column name
data type
null count
non-null count
distinct count where practical
sample values

Determine the actual business grain.

Specifically investigate:

GFCID
CAGID
legal_entity_id
legal_name
country
industry
sector
entity/client type
credit_managed_flag
any parent/group identifiers
any source/update fields

Do not infer semantics from field names alone where the data can test them.

==================================================
2. DETERMINE WHAT 3,670,650 MEANS
==================================================

Answer explicitly:

Are 3,670,650 rows equal to 3,670,650 unique clients?

Calculate:

total rows
distinct GFCID
duplicate GFCID rows
distinct CAGID
duplicate CAGID groups
distinct legal_entity_id
duplicate legal_entity_id groups

Determine maximum rows per:

GFCID
CAGID
legal_entity_id

Use bounded examples to explain duplicate patterns.

Do not merge anything yet.

==================================================
3. IDENTITY KEY DECISION
==================================================

Based on actual data, determine the strongest available master-client key.

Prior work suggested GFCID may be the strongest entity-level key,
but revalidate that against the complete 3.67M source.

Do not assume:

CAGID = client
legal_entity_id = unique entity
legal name = unique entity

Document the decision.

==================================================
4. CREATE THE NEW DATABASE
==================================================

Create:

backend/data/client_universe.sqlite3

This becomes the PRIMARY database for the new Client Correlation application.

Do not reuse:

ccr_clients.sqlite3

Do not reuse:

ccr_relationship_intelligence.sqlite3

Those are legacy artifacts.

==================================================
5. DATABASE MODEL
==================================================

Keep the initial model simple.

Create:

A. client_master

One row per defensible master-client/entity grain.

Use the strongest validated key.

Preserve all useful original source attributes.

Recommended structure where supported by the source:

client_key
gfcid
cagid
legal_entity_id

legal_name
normalized_legal_name

country
country_code

industry
sector

entity_type

credit_managed_flag

source_row_count

source_snapshot

created_at

Do not fabricate values.

NULL remains NULL.

B. client_identifiers

Use only where multiple identifiers genuinely need separate storage.

Structure:

client_key
identifier_type
identifier_value
normalized_value

Possible types only when actually present:

GFCID
CAGID
LEGAL_ENTITY_ID
LEI
OTHER

C. source_lineage

Preserve enough information to trace a client back to the original Parquet.

Do not duplicate the entire raw file unnecessarily.

==================================================
6. DUPLICATE HANDLING
==================================================

Do not silently collapse conflicting records.

If multiple source rows share the chosen client key:

compare all business fields.

Classify:

EXACT_DUPLICATE
CONSISTENT_MULTIROW
ATTRIBUTE_CONFLICT

For conflicts, preserve traceability.

Never arbitrarily choose one conflicting value without documenting the rule.

==================================================
7. SEARCH OPTIMIZATION
==================================================

The primary use case is interactive client search across millions of clients.

Create indexes for actual available fields such as:

gfcid
cagid
legal_entity_id
normalized_legal_name
country
industry
sector

Use SQLite FTS5 if available and appropriate for legal-name search.

Create a search structure supporting:

exact GFCID
exact CAGID
exact legal entity ID
exact legal name
prefix legal name
name token search

Do not allow unbounded full-table responses.

==================================================
8. NORMALIZATION
==================================================

For search only, create deterministic normalized text.

For legal names:

trim whitespace
normalize repeated spaces
case-normalize
safe Unicode normalization

Do NOT:

remove meaningful company suffixes from stored legal name
merge entities because names look similar
perform fuzzy entity resolution
invent aliases

Keep:

legal_name = source truth

normalized_legal_name = search helper

==================================================
9. COUNTRY / CLASSIFICATION
==================================================

Profile actual values.

Do not silently remap country or industry values unless the transformation is
deterministic and separately stored.

Preserve source value.

Optional normalized value may exist alongside it.

==================================================
10. DATA QUALITY TABLE
==================================================

Create a compact:

client_data_quality

or equivalent summary mechanism.

Track useful factual issues such as:

missing legal name
missing GFCID
duplicate GFCID
identifier conflicts
country missing
classification missing

Do not create subjective risk/confidence scores.

==================================================
11. BUILD SAFELY
==================================================

The build must be restartable.

Use:

transactions
batch inserts
parameterized SQL

Avoid loading all 3.67M rows into RAM.

Prefer PyArrow/Parquet batch iteration or equivalent bounded processing.

Provide progress logging.

If interrupted, the source Parquet must remain untouched.

==================================================
12. VALIDATE THE COMPLETE DATABASE
==================================================

After build, report:

source rows
master client rows
distinct GFCID
distinct CAGID
distinct legal_entity_id

exact duplicate source rows
multirow clients
conflicting clients

clients with legal name
clients with country
clients with industry
clients with sector

database size

index count

FTS status

Run:

PRAGMA integrity_check
PRAGMA foreign_key_check

==================================================
13. SEARCH PERFORMANCE TEST
==================================================

Run bounded benchmarks.

Measure:

exact GFCID lookup
exact CAGID lookup
exact legal name
prefix legal-name search
token/name search
country-filtered search

Use several representative queries.

Report latency.

Do not cherry-pick only cached queries; distinguish cold/warm where practical.

==================================================
14. MINIMAL API
==================================================

After database validation, add ONLY:

GET /api/clients/summary

GET /api/clients/search?q=&limit=

GET /api/clients/{client_key}

GET /api/clients/{client_key}/identifiers

Maximum default search result size should be bounded.

No relationship endpoints yet.

==================================================
15. MINIMAL FRONTEND CONNECTION
==================================================

Keep the frontend simple.

Replace the temporary page with only:

CLIENT CORRELATION

[ Search 3.67M clients... ]

and a simple search-results list.

When a result is clicked, show:

legal name
GFCID
CAGID
country
industry/sector
other real identifiers

No graph yet.

No dashboard.

No cards everywhere.

No relationship UI yet.

The sole purpose is to prove the 3.67M universe is searchable and usable.

==================================================
16. LEGACY IS OFF-LIMITS
==================================================

Do not import data from:

thousandClients.csv
old CCR SQLite databases
legacy relationship tables
old candidate tables

The new database must derive from:

Customer_latest.parquet

only.

==================================================
17. REPORT
==================================================

Create:

backend/data/CLIENT_UNIVERSE_BUILD_REPORT.md

Include:

source schema
business grain
identity key analysis
database schema
actual row counts
duplicate analysis
data quality
indexes
search performance
API validation
known limitations

==================================================
FINAL RESPONSE
==================================================

CLIENT UNIVERSE BUILD: PASS / FAIL

AUTHORITATIVE SOURCE ROWS:
3,670,650

ACTUAL MASTER CLIENTS:
<actual unique client count>

PRIMARY CLIENT KEY:
<actual>

DISTINCT GFCID:
<actual>

DUPLICATE GFCID:
<actual>

DISTINCT CAGID:
<actual>

DISTINCT LEGAL_ENTITY_ID:
<actual>

DATABASE:
backend/data/client_universe.sqlite3

DATABASE SIZE:
<actual>

FTS SEARCH:
PASS / FAIL / NOT USED

EXACT-ID SEARCH:
<latency>

NAME SEARCH:
<latency>

SQLITE INTEGRITY:
PASS / FAIL

FOREIGN KEYS:
PASS / FAIL

SOURCE PARQUET MODIFIED:
NO / FAIL

LEGACY CCR DATA IMPORTED:
0 / FAIL

RELATIONSHIPS CREATED:
0 / FAIL

CLIENT SEARCH UI:
PASS / FAIL

REPORT:
backend/data/CLIENT_UNIVERSE_BUILD_REPORT.md

STOP.

DO NOT START CORRELATION OR RELATIONSHIP DISCOVERY.
