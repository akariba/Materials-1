==================================================
FINAL PHASE — PROJECT CLEANUP AND CONSOLIDATION
==================================================

Once the CCR Relationship Intelligence implementation is working end-to-end,
perform a deliberate project cleanup.

The final repository must contain ONE clean, understandable CCR correlation /
relationship-intelligence implementation.

Do NOT leave the project depending on old copied implementations, abandoned
POCs, duplicate modules, obsolete demo code, RPR code, or multiple versions
of the same logic.

IMPORTANT:
Do not blindly delete historical code.
Inspect it first, establish whether anything still depends on it, migrate any
genuinely reusable logic into the current architecture, run tests, and only
then remove obsolete material.

==================================================
1. INVENTORY THE REPOSITORY
==================================================

Inspect the complete CCR project tree.

Identify:

- current active application code
- historical CCRIG implementations
- archived relationship modules
- old SQLite implementations
- duplicate CAM parsers
- duplicate graph/path implementations
- duplicate entity resolvers
- duplicate R2D2 adapters
- duplicate model / Opus adapters
- old demo modules
- hardcoded five-company data
- obsolete frontend builds
- generated artifacts accidentally tracked as source
- temporary files
- debug files
- stale JSON/CSV/DB outputs
- unused test fixtures
- RPR-related files
- experimental notebooks/scripts
- dead configuration files
- duplicate schemas
- duplicate data directories

Do not assume a folder is obsolete purely because it is old.

==================================================
2. CLASSIFY EVERY LEGACY COMPONENT
==================================================

For each historical/duplicate module classify it as:

ACTIVE
= currently used by the real application

MIGRATE_LOGIC
= contains useful analytical logic that should be moved into the current
  implementation

TEST_ONLY
= required only by valid tests

ARCHIVE_REFERENCE
= useful historical reference but not required at runtime

GENERATED
= build/output artifact that should not be treated as source

OBSOLETE
= no longer required

UNRELATED
= not part of the CCR correlation project

For each item report:

PATH
PURPOSE
CURRENTLY_REFERENCED_BY
CLASSIFICATION
ACTION

Do not delete anything until this classification exists.

==================================================
3. NO RUNTIME REFERENCES TO OLD IMPLEMENTATIONS
==================================================

The final application must not import or dynamically reference historical
implementations merely because they contain useful logic.

If valuable logic exists in an old module:

OLD MODULE
    ↓
understand/test logic
    ↓
move/adapt logic into current canonical module
    ↓
update imports/tests
    ↓
verify behavior
    ↓
remove obsolete implementation

Do NOT leave patterns such as:

current code
→ ../archive/old_ccrig/...
→ old sqlite repository
→ copied legacy implementation

The active runtime must use only the current CCR project structure.

==================================================
4. ONE IMPLEMENTATION PER RESPONSIBILITY
==================================================

There should be one obvious current implementation for each major
responsibility.

Examples:

CAM extraction
→ one canonical implementation

entity resolution
→ one canonical implementation

relationship candidate generation
→ one canonical implementation

relationship scoring
→ one canonical implementation

typed path generation
→ one canonical implementation

relationship validation
→ one canonical implementation

R2D2 integration
→ one canonical adapter

Opus/model integration
→ one canonical adapter

direct-source evidence
→ one canonical implementation

DuckDB query layer
→ one canonical implementation

frontend API integration
→ one canonical implementation

Do not retain `v1`, `v2`, `new`, `final`, `final2`, `old`, `backup`, etc.
as competing runtime implementations.

==================================================
5. CLEAN STORAGE STRUCTURE
==================================================

Preserve the agreed architecture:

source/raw documents
        ↓
canonical Parquet artifacts
        ↓
DuckDB analytical/query layer
        ↓
current backend/API
        ↓
frontend

There must be no production:

- SQLite relationship database
- duplicate entity database
- duplicate exposure database
- parallel relationship store
- old database migrations
- copied CAM databases

SQLite may exist only as an isolated test fixture if genuinely required by
a valid test.

Final confirmation:

SQLITE_PRODUCTION_DEPENDENCY = NO

==================================================
6. REMOVE DEMO / FAKE DATA
==================================================

Search the repository for:

demo
mock
fake
sample
fixture
hardcoded
NVIDIA demo
five-company
smoke
test relationship
placeholder exposure
placeholder TFA
placeholder rating

Classify each occurrence.

Tests may legitimately use fixtures.

Production/runtime code must not rely on fabricated data.

Remove obsolete demo runtime paths once the real implementation works.

Do not delete valid test fixtures merely because they contain synthetic data.

==================================================
7. REMOVE RPR CONTAMINATION
==================================================

The CCR correlation project must have no RPR runtime dependency.

Search for:

RPR
Rapid Portfolio Review
step21
step22
step23
step24
step25
RPR-specific runner calls
RPR prompts
RPR frontend routes
RPR configuration

If an RPR file is unrelated to CCR:

classify it as UNRELATED and remove it from this project only after confirming
nothing in CCR legitimately depends on it.

Final confirmation:

RPR_RUNTIME_DEPENDENCY = NO

==================================================
8. CLEAN FRONTEND STRUCTURE
==================================================

Do not treat generated build files as primary source code.

Confirm the actual frontend source location.

Changes should originate from source files and then be rebuilt normally.

Inspect items such as:

frontend/dist
build
bundle output
generated index.html
temporary screenshots
smoke outputs

Generated artifacts should either:

- be regenerated by the normal build process
- be ignored by git where appropriate
- remain only if the project explicitly requires them to be versioned

Do not maintain hand-edited generated files in parallel with source files.

==================================================
9. CLEAN DATA / ARTIFACT DIRECTORIES
==================================================

Separate clearly:

SOURCE DOCUMENTS

CANONICAL DATA

DERIVED DATA

CACHE / TEMPORARY OUTPUT

TEST FIXTURES

Do not mix all outputs in one directory.

Remove stale intermediate artifacts only when they can be safely regenerated
and are not required for provenance.

Preserve original source/evidence required for auditability.

==================================================
10. IMPORT AND DEPENDENCY AUDIT
==================================================

After cleanup, scan imports/references.

Confirm there are no references to:

- deleted modules
- archive folders
- obsolete SQLite repositories
- demo modules
- RPR modules
- old schema versions
- duplicate adapters

Also identify unused dependencies in requirements/package configuration.

Do not remove a dependency merely because static search misses dynamic use;
verify safely.

==================================================
11. TEST CLEANUP
==================================================

Tests should reflect the current architecture.

Keep tests that validate:

- relationship scoring
- pairwise calibration
- typed paths
- entity resolution
- CAM extraction
- exposure extraction
- provenance
- relationship evidence
- indirect relationships
- hidden candidates
- R2D2 integration where testable
- Opus schema validation
- DuckDB/Parquet access
- API contracts

Migrate useful tests from historical CCRIG modules into the current test
structure.

Do not keep an entire legacy implementation alive solely so its old tests can
run.

==================================================
12. TARGET PROJECT STRUCTURE
==================================================

Do not force this exact naming if the repository already has a good equivalent,
but the final structure should be conceptually clear:

CCR_RELATIONSHIP_INTELLIGENCE/
    backend/
        api/
        cam/
        entities/
        relationships/
        scoring/
        graph/
        evidence/
        enrichment/
        stress/
        portfolio/
        storage/

    frontend/
        src/
        public/

    data/
        raw/
        canonical/
        derived/

    tests/
        cam/
        entities/
        relationships/
        graph/
        evidence/
        integration/

    config/

    scripts/
        only maintained operational scripts

Avoid parallel structures such as:

old_ccrig/
new_ccrig/
ccrig2/
ccrig_final/
legacy/
backup/
demo_backend/
real_backend/

The goal is one obvious active code path.

==================================================
13. SAFE DELETION PROCEDURE
==================================================

Before deleting obsolete files:

1. ensure the current state is committed
2. list proposed deletions
3. explain why each is obsolete
4. search all repository references
5. migrate any useful code/tests first
6. run tests
7. remove the obsolete items
8. run tests again
9. run the application
10. perform the NVIDIA end-to-end smoke test

Do NOT use broad destructive deletion commands without reviewing the target
files.

==================================================
14. DOCUMENT THE FINAL ARCHITECTURE
==================================================

Create or update a concise architecture/readme document explaining:

- main application entry points
- CAM ingestion
- canonical data locations
- DuckDB role
- relationship generation
- evidence validation
- R2D2 role
- Opus refinement role
- graph derivation
- stress/event processing
- frontend/API flow
- test commands
- local run instructions

Do not document historical architecture as if it were still active.

==================================================
15. FINAL CLEANUP ACCEPTANCE
==================================================

Confirm:

[ ] one canonical CCR relationship-intelligence implementation
[ ] no duplicate runtime implementations
[ ] no dependency on old CCRIG folders
[ ] useful historical algorithms migrated into current modules
[ ] useful historical tests migrated
[ ] obsolete legacy code removed
[ ] no production SQLite dependency
[ ] DuckDB + Parquet preserved
[ ] no RPR runtime dependency
[ ] no hardcoded five-company production data
[ ] no fabricated production relationships
[ ] generated frontend assets not maintained as competing source
[ ] no dead imports
[ ] no broken paths
[ ] no duplicate entity stores
[ ] no duplicate relationship stores
[ ] source / canonical / derived data clearly separated
[ ] README/architecture reflects actual implementation
[ ] all tests pass
[ ] NVIDIA end-to-end flow passes
[ ] frontend starts successfully
[ ] backend starts successfully

==================================================
16. FINAL REPORT
==================================================

Report:

PROJECT STRUCTURE:
<final important directories>

LEGACY MODULES FOUND:
<count + summary>

MIGRATED:
<modules/logic moved into current architecture>

REMOVED:
<obsolete paths>

KEPT AS TEST-ONLY:
<paths>

DUPLICATES REMOVED:
<summary>

RPR FILES REMOVED / ISOLATED:
<summary>

SQLITE:
NO PRODUCTION DEPENDENCY

DUCKDB/PARQUET:
PRESERVED

DEMO RUNTIME DATA:
REMOVED

BROKEN / STALE REFERENCES:
0

TESTS:
<passed>/<total>

NVIDIA E2E:
PASS / FAIL

FRONTEND:
PASS / FAIL

BACKEND:
PASS / FAIL

FINAL COMMIT:
<hash>

Do not claim the project is clean simply because tests pass.
The final repository must also be structurally understandable, contain one
active implementation per responsibility, and have no hidden dependency on
historical code.