IMPORTANT STORAGE ARCHITECTURE GUARDRAIL — APPLY THIS BEFORE CONTINUING.

The previous CCRIG implementation may contain an old SQLite persistence layer.

DO NOT restore SQLite as a production/runtime database.

The current CCR Relationship Intelligence data architecture is the source of truth and must remain intact.

Current architecture to preserve:

- canonical entities in existing Parquet artifacts
- CAM documents/passages/entity mentions in existing Parquet artifacts
- DuckDB as the analytical/query layer over those artifacts
- existing relationship outputs in Parquet / JSONL or the current repository-equivalent format
- current API/backend integration

==================================================
1. RECOVER LOGIC, NOT THE OLD DATABASE
==================================================

When examining the historical CCRIG implementation, separate:

A. reusable BUSINESS / ANALYTICAL LOGIC

from:

B. old PERSISTENCE / STORAGE IMPLEMENTATION

Reuse where valuable:

- candidate-first relationship discovery
- relationship scoring
- pairwise calibration
- typed second-order paths
- path strength
- CounterpartyRelevance
- EventRelevance
- Fact / Derived / Exposure classification
- relationship normalization
- tests
- R2D2/Opus orchestration logic where applicable

Do NOT automatically reuse:

- SQLite database
- SQLite schemas
- SQLite repositories/DAOs
- old database migrations
- old persistence-specific query code
- old entity master
- old duplicate data stores

==================================================
2. SQLITE RULE
==================================================

Search the historical CCRIG implementation for:

sqlite
sqlite3
.db files
SQLAlchemy SQLite URLs
repository/DAO classes tied to SQLite

Report exactly what SQLite was used for.

Classify each use as:

LOGIC_COUPLED_TO_SQLITE
PERSISTENCE_ONLY
TEST_FIXTURE
CACHE
LEGACY_UNUSED

Do NOT create or modify any SQLite production database.

SQLite may remain only as a temporary test fixture if existing isolated tests require it.

It must NOT become:

- canonical entity storage
- CAM storage
- relationship source of truth
- exposure source of truth
- frontend runtime database

==================================================
3. CURRENT DUCKDB/PARQUET REMAINS AUTHORITATIVE
==================================================

Map recovered CCRIG concepts onto the CURRENT schemas.

For example:

old CCRIG relationship object
        ↓
current relationship Parquet/schema

old candidate table
        ↓
current candidate artifact/schema

old scoring output
        ↓
current relationship records

old path calculations
        ↓
current canonical entity IDs + verified edge data

Do not duplicate data simply to satisfy the old implementation.

==================================================
4. DO NOT CREATE A SECOND SOURCE OF TRUTH
==================================================

There must be ONE authoritative representation for each domain:

Canonical entities
→ existing canonical Parquet/entity structures

CAM evidence
→ existing CAM index/passages

Relationships
→ current relationship artifacts/schema

Exposure
→ CAM-derived current exposure structures

Graph analytics
→ derived from current verified relationship records

Do not create a parallel SQLite copy that can diverge from these datasets.

==================================================
5. BEFORE IMPLEMENTING, REPORT
==================================================

Before making storage-related changes, show me:

CURRENT STORAGE
- canonical entity location
- CAM document/passages location
- relationship storage
- exposure storage
- DuckDB views/tables
- frontend/API read path

OLD CCRIG STORAGE
- SQLite files
- SQLite schemas
- what data they contained
- which algorithms depended on them

REUSE PLAN
For every old CCRIG module classify:

REUSE_AS_IS
ADAPT_TO_CURRENT_SCHEMA
LOGIC_ONLY
DO_NOT_REUSE

==================================================
6. TARGET ARCHITECTURE
==================================================

The target must remain conceptually:

Raw / canonical Parquet
        ↓
DuckDB analytical/query layer
        ↓
CAM + canonical entities + verified relationships
        ↓
recovered CCRIG scoring/path algorithms
        ↓
derived relationship/graph artifacts
        ↓
API
        ↓
frontend

NOT:

DuckDB + SQLite as competing production databases.

==================================================
7. STOP CONDITION
==================================================

If the recovered CCRIG algorithms cannot currently operate without recreating SQLite:

STOP.

Explain exactly which modules are coupled to SQLite and propose the smallest adapter needed to run the same logic against the current Parquet/DuckDB structures.

Do NOT create SQLite merely because the historical code expects it.

Proceed only after confirming:

SQLITE_PRODUCTION_DEPENDENCY = NO
CURRENT_DUCKDB_PARQUET_ARCHITECTURE_PRESERVED = YES