CCR RELATIONSHIP CORRELATION — PHASE 1
FULL DATA / REPOSITORY FORENSIC AUDIT

You are working inside the CURRENT CCR repository opened in VSCode.

This is CCR only.

DO NOT inspect, modify, import from, or change:
- Lending
- CCRIG
- RPR
- any other repository or project

Do not implement the relationship engine yet.
Do not redesign the frontend.
Do not run SEC research.
Do not run Web research.
Do not call external APIs.
Do not modify source datasets.
Do not overwrite any SQLite database.
Do not fabricate relationships or enrichment.

This phase is READ-ONLY discovery and validation.

==================================================
1. OBJECTIVE
==================================================

We are preparing to build a CCR Relationship Correlation / Relationship Intelligence capability.

The intended eventual architecture is:

CCR client/exposure population
    ↓
canonical client identity
    ↓
entity resolution
    ↓
SEC / authoritative reference enrichment
    ↓
high-quality Web enrichment where allowed
    ↓
relationship candidate discovery
    ↓
relationship evidence
    ↓
relationship classification
    ↓
quality / confidence / admissibility gates
    ↓
CCR relationship graph
    ↓
AI Create Relationship configurable analysis

BUT DO NOT BUILD THIS YET.

First establish exactly what data and code already exist.

There are three particularly important assets expected in the repository:

1. Customer_latest.parquet
   - approximately 3 million customer/client records
   - this is the MASTER client/customer dataset

2. thousandClients.csv
   - despite its filename, DO NOT assume it contains exactly 1,000 records
   - this is the CCR working extract created from exposure/client information
   - determine its actual row count and actual client population

3. backend/data/ccr_clients.sqlite3
   - existing application artifact / SQLite database
   - determine exactly how it was built and what it contains

There may also be:

backend/scripts/build_ccr_client_artifact.py

and existing frontend/backend structures.

==================================================
2. HARD RULE: MASTER VS CCR POPULATION
==================================================

Treat:

Customer_latest.parquet

as the MASTER client reference universe unless repository evidence proves otherwise.

Treat:

thousandClients.csv

as a CCR-derived population/exposure extract.

Do not treat the CSV as authoritative for attributes that should come from the master unless that is explicitly how the current build works.

Do not assume:
- one CSV row = one client
- every client exists once
- every row represents one legal entity
- all exposure rows are client-level
- every client maps cleanly to Customer_latest.parquet

Determine these facts empirically.

==================================================
3. FIRST — INVENTORY THE REPOSITORY
==================================================

Inspect the current repository tree.

Report relevant files under:

backend/
backend/app/
backend/app/core/
backend/app/routers/
backend/data/
backend/scripts/
frontend/

Also search the entire CURRENT repository for:

CCR
client
customer
exposure
relationship
correlation
graph
network
SEC
EDGAR
CIK
LEI
GLEIF
Stylus
preset
AI Create Relationship
relationship configuration
external research
web research
R2D2
confidence
evidence
source tier
admissibility

Do NOT assume these components exist.

Report exactly what exists.

For every relevant discovered file provide:

PATH
PURPOSE
USED BY
STATUS:
- active
- apparently legacy
- unclear
- generated artifact

==================================================
4. AUDIT Customer_latest.parquet
==================================================

Use an efficient Parquet-aware method.

Prefer:
- pyarrow
- parquet metadata
- DuckDB if already available
- pandas only where reasonable

Do not convert the 3M-row file to CSV.

Report:

FILE PATH
FILE SIZE
ROW COUNT
COLUMN COUNT
ROW GROUP COUNT
PARQUET SCHEMA

For every column report:

COLUMN
TYPE
NON-NULL COUNT
NULL COUNT
NULL %
APPROX/EXACT DISTINCT COUNT where practical
SAMPLE VALUES (safe short examples only)

Identify candidate fields for:

- master client/customer ID
- CAGID or equivalent internal ID
- legal entity name
- short/client/display name
- alternate names
- parent name
- ultimate parent
- country
- country of incorporation
- domicile
- address
- city
- state
- postal code
- industry
- sector
- NAICS
- SIC
- LEI
- CIK
- ticker
- exchange
- public/private indicator
- legal entity type
- client type
- website/domain
- status / active flag
- hierarchy fields
- regulatory identifiers

Do not invent mappings.
If field meaning is unclear mark UNKNOWN.

==================================================
5. MASTER DATA QUALITY
==================================================

Perform data-quality tests on Customer_latest.parquet.

At minimum:

A. ID QUALITY

Determine likely primary client identifier(s).

For each likely identifier report:

rows
non-null
unique
duplicate count
duplicate %
blank/whitespace count

B. LEGAL NAME QUALITY

For primary legal/client name field(s):

non-null count
blank count
unique raw names
unique normalized names

Create a TEMPORARY in-memory normalization only for analysis:

uppercase/lowercase normalization
trim whitespace
collapse repeated spaces
remove obvious punctuation differences

DO NOT modify the source file.

Identify:
- exact duplicate names
- normalized duplicate names
- suspicious placeholder names
- N/A / UNKNOWN / TEST / DUMMY-like values
- obvious encoding problems

Give counts and representative examples.

C. IDENTIFIER QUALITY

If available test:

LEI:
- expected length/format
- duplicates
- invalid-looking values

CIK:
- numeric/normalized validity
- duplicates
- invalid-looking values

Ticker:
- coverage
- duplicate ticker cases
- exchange ambiguity if exchange exists

Do not externally validate identifiers yet.

D. ENTITY HIERARCHY

Determine whether Customer_latest already contains:

parent
immediate parent
ultimate parent
legal hierarchy
relationship manager hierarchy
business hierarchy

Clearly distinguish true legal/corporate hierarchy from internal client classifications.

E. COVERAGE PROFILE

Calculate coverage % for all fields potentially useful for CCR relationship discovery.

Especially:

legal name
country
industry
sector
LEI
CIK
ticker
website
parent
ultimate parent
public/private

==================================================
6. AUDIT thousandClients.csv
==================================================

Do not trust the filename.

Report:

FILE SIZE
ROW COUNT
COLUMN COUNT
COLUMN NAMES
INFERRED TYPES

For every field:

COLUMN
TYPE
NON-NULL
NULL
DISTINCT
SAMPLE VALUES

Then classify every column as one of:

CLIENT_IDENTITY
CLIENT_REFERENCE
EXPOSURE
LIMIT
PRODUCT
LEGAL_ENTITY
PORTFOLIO
DATE
CLASSIFICATION
UNKNOWN

Determine:

- actual unique CCR clients
- actual number of rows
- whether rows repeat because of exposures/products/netting sets/etc.
- whether there are duplicate identical rows
- likely client identifier
- total number of unique identifiers
- missing identifier rows
- duplicate identifier distribution

If exposure fields exist:

DO NOT assume units.

Report:
field name
min
max
median
sum
negative-count
zero-count
null-count

But label units UNKNOWN unless established by repository/source metadata.

==================================================
7. RECONCILE CCR CSV TO 3M MASTER
==================================================

Determine the strongest deterministic join key between:

thousandClients.csv

and:

Customer_latest.parquet

Possible keys may include:
CAGID
client/customer ID
LEI
another internal identifier

Do not fuzzy-match names yet unless there is no deterministic identifier.

Report candidate join keys and quality.

For the best available deterministic key calculate:

CCR unique clients
matched to master
unmatched
master duplicates for join key
CCR duplicate identifiers
one-to-one matches
one-to-many matches
many-to-one conditions

Produce percentages.

If multiple candidate IDs exist, compare them.

For unmatched CCR clients:
show up to 20 representative records with only useful diagnostic fields.

Do NOT repair them yet.

==================================================
8. AUDIT ccr_clients.sqlite3
==================================================

Open read-only.

Report:

SQLite version if relevant
file size

List every table/view/index.

For each table:

name
row count
columns
primary key
foreign keys
indexes

Show schema.

Determine whether database contains:

client master
CCR population
exposure information
relationship information
SEC information
web information
evidence
configuration
graph edges
AI configuration

Report actual contents, not assumptions.

==================================================
9. TRACE BUILD LINEAGE
==================================================

Inspect:

backend/scripts/build_ccr_client_artifact.py

and every file it imports or calls that is relevant.

Explain exactly:

INPUTS
    ↓
TRANSFORMATIONS
    ↓
MATCHING / FILTERING
    ↓
OUTPUTS

Determine:

- whether it reads Customer_latest.parquet
- whether it reads thousandClients.csv
- how it joins them
- which columns survive
- whether data is aggregated
- whether duplicate clients are collapsed
- whether exposure rows are collapsed
- how ccr_clients.sqlite3 is produced
- whether values are hardcoded
- whether any mock/synthetic values exist
- whether any records are silently dropped
- whether row counts are validated
- whether there are tests

Do not change the script.

==================================================
10. SEARCH FOR EXISTING SEC INFRASTRUCTURE
==================================================

We expect the future CCR relationship engine to rely heavily on SEC where applicable.

Search CURRENT CCR repository for any existing:

SEC
EDGAR
submissions API
companyfacts
CIK mapping
filing parser
10-K
10-Q
8-K
DEF 14A
13D
13G
13F
filing cache
SEC user-agent configuration
rate limiting
SEC source tier
SEC evidence structure

Report:

EXISTS / DOES NOT EXIST

for each relevant capability.

If something exists, report:
file
class/function
configuration
cache
runtime contract
outputs

DO NOT call SEC.

==================================================
11. SEARCH FOR EXISTING WEB RESEARCH INFRASTRUCTURE
==================================================

Search only the current CCR repository.

Identify whether there is any existing:

R2D2
web search
external research
source-quality classifier
publisher allowlist
publisher denylist
source tier
evidence admissibility
confidence calculation
URL normalization
research caching

Report exact implementation if found.

Do not execute it.

==================================================
12. SEARCH FOR STYLUS / UI PRESET
==================================================

Search for:

Stylus
stylus
preset
theme
design tokens
CSS variables
Tailwind configuration
component library
layout system

Determine whether the CURRENT CCR repository already contains or references the
existing Stylus preset.

Report exact path(s).

Do not modify the preset.

If no local Stylus preset exists, say:

STYLUS_PRESET_LOCAL = NOT FOUND

Do not invent one.

==================================================
13. EXISTING RELATIONSHIP / CORRELATION CAPABILITY
==================================================

Search for any implementation of:

relationship
related entity
correlation
network
graph
edge
node
supplier
customer
parent
subsidiary
investor
sponsor
lender
technology dependency
strategic partner
industry relation
macro/theme relation

Report whether each is:

IMPLEMENTED
PARTIAL
PLACEHOLDER
NOT FOUND

If graph/network UI exists, report current routes/components/API dependencies.

If correlation math exists, explain what "correlation" means there.

Do not assume Pearson correlation is the intended CCR relationship model.

==================================================
14. AI / MODEL CONFIGURATION
==================================================

Search for:

OpenAI
AI provider
model
Luna
LLM
prompt
AI config
AI create relationship
relationship config
preset

Report:

- provider abstraction if any
- environment variables
- model configuration
- prompt locations
- structured-output schemas
- deterministic fallback
- cache
- retry behavior

Do not expose secrets.
Only report environment VARIABLE NAMES, never secret values.

==================================================
15. DATA ACCURACY / STRUCTURAL VERDICT
==================================================

After completing the audit, provide an evidence-based assessment.

Answer:

A. Is Customer_latest.parquet structurally suitable as the 3M master reference source?

B. Is thousandClients.csv structurally suitable as the CCR population/exposure source?

C. Can CCR clients be deterministically reconciled to the master?

D. Is ccr_clients.sqlite3 a faithful derivative of those inputs?

E. What information is currently missing for relationship discovery?

F. Which master fields are usable immediately for candidate generation?

G. Which fields must NOT be treated as relationship evidence?

IMPORTANT PRINCIPLE:

Exposure, common geography, common industry, shared classification, or mere
co-occurrence do NOT by themselves establish a relationship.

They may be candidate-generation/blocking signals, but not relationship evidence.

==================================================
16. DO NOT IMPLEMENT YET
==================================================

Do not:

- modify data
- build new database tables
- add SEC
- add Web
- add relationship engine
- add UI
- add relationship presets
- change Stylus
- create synthetic relationships
- create fake test business data

This phase ends with analysis only.

==================================================
17. OUTPUT FILE
==================================================

Create:

backend/data/CCR_RELATIONSHIP_PHASE1_DATA_AUDIT.md

Do not overwrite any unrelated existing report.

The report must contain:

1. Repository inventory
2. Master Parquet audit
3. CCR CSV audit
4. CCR-to-master reconciliation
5. SQLite audit
6. Build lineage
7. Existing SEC infrastructure
8. Existing Web infrastructure
9. Existing Stylus/preset state
10. Existing relationship capability
11. Existing AI/model configuration
12. Data-quality findings
13. Critical blockers
14. Recommendations for Phase 2

==================================================
18. FINAL RESPONSE TO ME
==================================================

Do not paste the entire report into chat.

Return exactly:

CCR PHASE 1 DATA AUDIT: PASS / FAIL

MASTER PARQUET
Rows:
Columns:
Likely primary ID:
Unique primary IDs:
Duplicate primary IDs:
Legal-name coverage:
LEI coverage:
CIK coverage:
Ticker coverage:
Parent coverage:
Ultimate-parent coverage:

CCR CSV
Rows:
Unique CCR clients:
Likely client ID:
Exposure fields:
Duplicate client rows:
Missing client IDs:

MASTER RECONCILIATION
Matched:
Unmatched:
One-to-one:
Ambiguous:
Match rate:

CCR SQLITE
Tables:
Client rows:
Exposure rows:
Relationship rows:
Build lineage understood: YES / NO

SEC INFRASTRUCTURE
Existing: YES / PARTIAL / NO
Key files:

WEB INFRASTRUCTURE
Existing: YES / PARTIAL / NO
Key files:

STYLUS PRESET
Found locally: YES / NO
Path:

RELATIONSHIP ENGINE
Existing: YES / PARTIAL / NO

AI CREATE RELATIONSHIP CONFIG
Existing: YES / PARTIAL / NO

TOP 10 DATA QUALITY FINDINGS
1.
2.
3.
4.
5.
6.
7.
8.
9.
10.

PHASE 2 BLOCKERS
1.
2.
3.

REPORT:
<exact path>

No implementation yet.
STOP.
