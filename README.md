CCR RELATIONSHIP CORRELATION — PHASE 2
CANONICAL CCR CLIENT + EXPOSURE FOUNDATION

You are working inside the CURRENT CCR repository opened in VSCode.

This is CCR ONLY.

Do not inspect, import from, modify, or depend on:
- Lending
- CCRIG
- RPR
- any other repository

Phase 1 has completed and produced:

backend/data/CCR_RELATIONSHIP_PHASE1_DATA_AUDIT.md

READ THAT REPORT FIRST.

Treat its findings as the starting evidence, but independently recompute
critical row counts during implementation rather than hardcoding report values.

==================================================
1. OBJECTIVE
==================================================

Build the clean canonical data foundation required for the future:

CCR Relationship Correlation / Relationship Intelligence system.

The intended future pipeline is:

Customer_latest.parquet
        ↓
master client reference
        ↓
CCR exposure population
        ↓
canonical CCR client identity
        ↓
legal/entity hierarchy
        ↓
external identity enrichment
        ↓
SEC / GLEIF / high-quality Web evidence
        ↓
relationship discovery
        ↓
AI Create Relationship configuration
        ↓
CCR relationship graph

THIS PHASE implements only:

MASTER REFERENCE
        +
CCR EXPOSURE EXTRACT
        ↓
CANONICAL CCR CLIENT UNIVERSE
        ↓
NORMALIZED EXPOSURE RECORDS
        ↓
IDENTITY RESOLUTION / EXCEPTIONS
        ↓
HIERARCHY READINESS
        ↓
RELATIONSHIP-RESEARCH READINESS

Do NOT implement relationship discovery yet.

==================================================
2. IMPORTANT KNOWN PHASE-1 FINDINGS
==================================================

Phase 1 reported approximately:

Customer_latest.parquet:
- 3.67M rows
- ~3.658M unique GFCIDs

thousandClients.csv:
- 25,000 facility/exposure rows
- 16,769 unique GFCIDs

Reconciliation:
- very high exact GFCID match
- 14 unresolved GFCIDs
- 31 unresolved CAGIDs

Existing ccr_clients.sqlite3:
- master/reference artifact
- ~3.658M customer records
- no proper CCR exposure/facility layer

These values MUST be recomputed from source.

Do not hardcode them.

==================================================
3. HARD SAFETY RULES
==================================================

DO NOT modify:

Customer_latest.parquet

DO NOT modify:

thousandClients.csv

DO NOT overwrite:

backend/data/ccr_clients.sqlite3

Treat ccr_clients.sqlite3 as a frozen/reference artifact for now.

Create a SEPARATE CCR relationship-intelligence database.

Preferred path:

backend/data/ccr_relationship_intelligence.sqlite3

If repository conventions strongly indicate another appropriate path/name,
document the reason before using it.

Do not delete or mutate Phase-1 outputs.

Do not make external network calls.

Specifically:

NO SEC
NO EDGAR
NO GLEIF API
NO Web search
NO R2D2
NO external AI research

==================================================
4. SOURCE AUTHORITY MODEL
==================================================

Enforce this authority model.

A. MASTER IDENTITY AUTHORITY

Customer_latest.parquet

is authoritative for master client/reference attributes when available.

B. CCR POPULATION / EXPOSURE AUTHORITY

thousandClients.csv

defines the CCR population in current scope and carries the exposure/facility
records relevant to this CCR prototype.

C. RELATIONSHIP AUTHORITY

NONE YET.

Neither file may manufacture a corporate/economic relationship merely because:

- two clients are in the same country
- two clients are in the same sector
- two clients have exposure
- two clients share a product
- two clients share an owner field
- two clients have similar names
- two clients appear near one another
- two entities belong to the same group classification

Those may later help candidate generation.

They are NOT external relationship evidence.

==================================================
5. BUILD A CANONICAL CCR DATABASE
==================================================

Create:

backend/data/ccr_relationship_intelligence.sqlite3

Use foreign keys where appropriate.

Enable:

PRAGMA foreign_keys = ON

Create an appropriate schema containing at minimum the following logical
structures.

Exact table names may be adapted slightly to repository naming conventions,
but preserve the semantics.

--------------------------------------------------
5A. canonical_clients
--------------------------------------------------

Exactly ONE canonical row per CCR client identity where resolvable.

Required fields should include where available:

ccr_client_key
gfcid
cagid
legal_name
display_name
normalized_name

country
country_code
country_of_risk
country_of_incorporation

industry
sector
industry_code
naics
sic

lei
cik
ticker
exchange

client_type
account_type
legal_entity_type

website
domain

parent_gfcid
parent_name
ultimate_parent_gfcid
ultimate_parent_name

source_master_row_reference where practical

identity_status
identity_quality
identity_resolution_method

sec_research_eligible
gleif_research_eligible
web_research_eligible

created_at
build_version

IMPORTANT:

Only populate fields that actually exist or are defensibly derived from
existing local fields.

Do not fabricate missing identifiers.

If multiple possible columns correspond to the same concept, document the
mapping.

--------------------------------------------------
5B. exposure_records
--------------------------------------------------

Preserve the original CCR exposure/facility granularity.

Do NOT collapse the 25,000 source rows into one row per client.

Create one normalized record per relevant source row.

Include:

exposure_record_id
source_row_number or stable source-row hash
ccr_client_key
gfcid
cagid

all meaningful exposure/facility/product fields

raw amount/value fields
normalized numeric representation where safe

source_file
build_version

Retain original source values where needed for auditability.

If a field's unit is not documented:

DO NOT guess.

Persist:

unit_status = UNKNOWN

or equivalent metadata.

--------------------------------------------------
5C. client_exposure_summary
--------------------------------------------------

Create a derived one-row-per-client summary.

Include only mathematically valid aggregations.

Possible fields where data permits:

exposure_record_count
facility_count
product_count

reported exposure totals
positive exposure totals
negative exposure totals
zero exposure rows

But do not sum fields unless they are actually additive.

Before aggregating each numeric field classify it:

ADDITIVE
NON_ADDITIVE
UNKNOWN

Do not aggregate NON_ADDITIVE or UNKNOWN measures into misleading totals.

Persist this classification somewhere explicit.

--------------------------------------------------
5D. identity_resolution
--------------------------------------------------

Persist the exact CCR → master reconciliation.

At minimum:

source_gfcid
source_cagid
source_name

matched_master_gfcid
matched_master_cagid
matched_master_name

resolution_status
resolution_method
match_quality
conflict_reason

Statuses should include concepts such as:

EXACT_GFCID
EXACT_CAGID
GFCID_CAGID_CONFLICT
MASTER_DUPLICATE
CCR_DUPLICATE_IDENTIFIER
UNRESOLVED
REVIEW_REQUIRED

Do not force unresolved records into a resolved state.

--------------------------------------------------
5E. identity_exceptions
--------------------------------------------------

Persist every unresolved or conflicting identity condition.

Include:

exception_id
source_record/client
exception_type
gfcid
cagid
name
description
candidate_master_ids if relevant
status
review_required

The known Phase-1 unresolved populations must therefore be visible and
queryable rather than hidden.

--------------------------------------------------
5F. identifier_aliases
--------------------------------------------------

Create a bounded identity/alias table for existing local identifiers.

Examples:

GFCID
CAGID
LEI
CIK
ticker
legal-name alias

Fields:

ccr_client_key
identifier_type
identifier_value
normalized_value
source
is_primary
quality

Do not create inferred aliases from arbitrary fuzzy name matching.

--------------------------------------------------
5G. hierarchy_records
--------------------------------------------------

Extract any actual hierarchy information already present in the master.

Possible relationship concepts:

LEGAL_PARENT
ULTIMATE_PARENT
BENEFICIAL_OWNER
INTERNAL_PARENT
UNKNOWN_HIERARCHY_TYPE

CRITICAL:

Do not automatically equate:

owner
beneficial owner
parent
ultimate parent
relationship manager hierarchy
account hierarchy

Determine semantics from field names/data/repository context.

Persist:

child_client_key
parent_reference
hierarchy_type
source_field
source_value
quality
status

If a hierarchy concept cannot be established reliably, mark it UNKNOWN or
REVIEW_REQUIRED.

Do not manufacture ownership edges.

==================================================
6. EXPOSURE SEMANTICS ANALYSIS
==================================================

Phase 1 identified exposure semantics as a blocker.

Resolve as much as possible LOCALLY.

Inspect:

- source column names
- README
- comments
- build scripts
- any existing data dictionaries
- configuration
- tests
- API code

For every numeric CCR field create a classification:

FIELD
BUSINESS CONCEPT
TYPE
UNIT
UNIT STATUS
ADDITIVE?
CAN SUM ACROSS ROWS?
CAN SUM ACROSS CLIENTS?
NEGATIVE VALUES VALID?
ZERO VALUES VALID?
SOURCE OF INTERPRETATION
CONFIDENCE

Allowed UNIT STATUS:

CONFIRMED
LIKELY
UNKNOWN

Do not convert LIKELY into CONFIRMED.

Do not invent currency.

Generate:

backend/data/CCR_EXPOSURE_DATA_DICTIONARY.md

==================================================
7. IDENTITY QUALITY SCORE
==================================================

Create an EXPLAINABLE categorical identity-quality classification.

Do NOT create a mysterious ML score.

Recommended categories:

HIGH
MEDIUM
LOW
UNRESOLVED

Example principles:

HIGH:
- exact stable master identifier
- no conflicting identifier
- legal name present

MEDIUM:
- stable identifier resolved
- some useful identity fields missing

LOW:
- weak or incomplete master identity
- unresolved hierarchy/alias ambiguity

UNRESOLVED:
- no defensible canonical master mapping

Store reasons.

For example:

identity_quality_reason = [
  "EXACT_GFCID_MATCH",
  "LEGAL_NAME_PRESENT",
  "CAGID_CONFLICT"
]

Use actual applicable reasons only.

==================================================
8. RESEARCH-READINESS FLAGS
==================================================

We will use these in the SEC/GLEIF/Web phase later.

Do NOT run research yet.

Create deterministic readiness fields.

--------------------------------------------------
SEC readiness
--------------------------------------------------

sec_research_eligible = true only where existing local information provides
a defensible SEC identity path.

Strong examples may include:

- valid existing CIK
- another explicit local SEC identifier

Do not assume every US company is SEC registered.

If only company name/country exists:

SEC status should be:

UNKNOWN / DISCOVERY_REQUIRED

not eligible-by-fact.

--------------------------------------------------
GLEIF readiness
--------------------------------------------------

If valid LEI exists:

GLEIF_LOOKUP_READY

If no LEI but high-quality legal identity exists:

GLEIF_DISCOVERY_REQUIRED

Otherwise:

INSUFFICIENT_IDENTITY

--------------------------------------------------
Web readiness
--------------------------------------------------

May be READY when there is sufficiently specific legal identity to construct
a bounded future research query.

Avoid marking generic/ambiguous names as high-quality Web-ready.

Persist reasons.

==================================================
9. RELATIONSHIP CANDIDATE SIGNALS — DATA ONLY
==================================================

Do NOT create relationships.

But identify which LOCAL fields may later be used for candidate generation.

Classify each candidate signal as:

IDENTITY
BLOCKING
CANDIDATE_SIGNAL
RELATIONSHIP_EVIDENCE

For this phase:

RELATIONSHIP_EVIDENCE should almost certainly be NONE unless the local data
contains genuine independently sourced relationship evidence.

Examples of candidate signals may include:

same sector
same country
same industry
common ultimate parent where genuinely established
same issuer group
similar classification

But explicitly record:

candidate signal ≠ relationship evidence

Create an internal registry/table or JSON config if appropriate:

candidate_signal_registry

with:

signal_name
source_field
classification
description
safe_for_candidate_generation
safe_as_relationship_evidence

==================================================
10. DO NOT BUILD N×N PAIRS
==================================================

There are ~16k CCR clients.

Do NOT produce a full dense pair matrix.

Do NOT calculate:

16k × 16k

relationship scores.

Do NOT create millions of speculative client pairs.

Future architecture will use candidate generation before research/scoring.

For this phase only establish the normalized entity foundation.

==================================================
11. PERFORMANCE REQUIREMENT
==================================================

Do not repeatedly scan the entire 3.6M-row Parquet unnecessarily.

Use efficient approaches:

- PyArrow predicate/column projection
- DuckDB where appropriate
- chunked processing
- indexed temporary lookup structures

Load only required columns.

The final CCR relationship database should contain only the data required for
the CCR population and relationship workflow.

Do NOT copy all ~3.6M master customer records into the new relationship
database.

The existing ccr_clients.sqlite3 can remain the large reference artifact.

==================================================
12. BUILD SCRIPT
==================================================

Create a deterministic builder.

Preferred:

backend/scripts/build_ccr_relationship_foundation.py

The script should:

1. inspect source schemas
2. load CCR extract
3. determine CCR population
4. obtain corresponding master records
5. reconcile identities
6. preserve exceptions
7. normalize exposure records
8. generate safe exposure summaries
9. extract hierarchy fields
10. calculate research-readiness states
11. populate SQLite
12. validate counts
13. write build report

Running twice from unchanged input should produce logically identical business
data.

Timestamp metadata may differ.

==================================================
13. SOURCE HASHES / LINEAGE
==================================================

Record source lineage.

At minimum persist/hash:

Customer_latest.parquet
thousandClients.csv

Record:

path
file size
SHA-256 if practical
modified time
build time

The final database should be traceable back to its sources.

==================================================
14. TESTS
==================================================

Add tests.

At minimum prove:

1. Source Parquet unchanged.

2. Source CSV unchanged.

3. Existing ccr_clients.sqlite3 unchanged.

4. Number of canonical CCR identities equals the independently derived
resolvable CCR population plus explicit unresolved handling.

5. No duplicate canonical primary client key.

6. Every normalized exposure row either:
   - references a canonical client
   OR
   - is represented in a clearly identified unresolved exception state.

7. Original CCR source row count reconciles to:
   normalized rows + explicitly rejected/exception rows.

8. No records silently disappear.

9. Identity conflicts are not silently promoted.

10. GFCID/CAGID disagreement is persisted.

11. Exposure units are not fabricated.

12. UNKNOWN exposure semantics remain UNKNOWN.

13. Non-additive fields are not summed.

14. No SEC calls.

15. No Web calls.

16. No GLEIF calls.

17. No synthetic business relationships created.

18. Build is deterministic.

19. Foreign-key integrity passes.

20. No full N×N relationship pair generation occurs.

==================================================
15. VALIDATION QUERIES
==================================================

After building, run and report queries for:

canonical CCR clients
resolved identities
unresolved identities
identity conflicts

exposure rows
exposure rows linked
exposure rows unresolved

clients with:
CIK
LEI
ticker
website
parent
ultimate parent

SEC:
READY
DISCOVERY_REQUIRED
INSUFFICIENT

GLEIF:
LOOKUP_READY
DISCOVERY_REQUIRED
INSUFFICIENT

Web:
READY
AMBIGUOUS
INSUFFICIENT

identity quality:
HIGH
MEDIUM
LOW
UNRESOLVED

Do not hardcode expected values.

==================================================
16. BUILD REPORT
==================================================

Create:

backend/data/CCR_RELATIONSHIP_PHASE2_FOUNDATION_REPORT.md

Include:

SOURCE RECONCILIATION
CANONICAL CLIENTS
EXPOSURE NORMALIZATION
EXPOSURE SEMANTICS
IDENTITY EXCEPTIONS
HIERARCHY COVERAGE
IDENTIFIER COVERAGE
RESEARCH READINESS
DATA QUALITY
TEST RESULTS
PERFORMANCE
OPEN ISSUES

Include exact table row counts.

==================================================
17. IMPORTANT FUTURE CONTRACT
==================================================

Design the foundation so that Phase 3 can later add external evidence without
changing canonical client identity.

Future evidence should be attachable by:

ccr_client_key

and related external/canonical entity key.

Future relationship evidence will need fields such as:

subject_entity
related_entity
relationship_type
direction
source_channel
publisher
source_title
filing_type
published_date
source_reference
evidence_excerpt
source_tier
admissibility
confidence
research_run_id

DO NOT populate these yet.

Only ensure the identity model will support them.

==================================================
18. DO NOT IMPLEMENT YET
==================================================

Do not implement:

SEC connector
GLEIF connector
Web research
R2D2
relationship extraction
relationship scoring
relationship confidence
relationship graph
AI Create Relationship
relationship configuration UI
Stylus changes
frontend redesign

Those are later phases.

==================================================
19. FINAL RESPONSE FORMAT
==================================================

Return exactly:

CCR PHASE 2 FOUNDATION: PASS / FAIL

DATABASE:
<path>

SOURCE
Master rows:
CCR source rows:
Unique CCR GFCIDs:
Unique CCR CAGIDs:

CANONICAL IDENTITY
Canonical clients:
Exact GFCID:
Exact CAGID fallback:
Conflicts:
Unresolved:
High quality:
Medium quality:
Low quality:

EXPOSURE
Normalized exposure rows:
Linked exposure rows:
Unresolved exposure rows:
Numeric exposure fields:
Confirmed-unit fields:
Unknown-unit fields:
Additive fields:
Non-additive/unknown fields:

HIERARCHY
Clients with parent:
Clients with ultimate parent:
Hierarchy conflicts:
Hierarchy unknown:

IDENTIFIERS
CIK:
LEI:
Ticker:
Website/domain:

RESEARCH READINESS
SEC ready:
SEC discovery required:
SEC insufficient:
GLEIF lookup ready:
GLEIF discovery required:
GLEIF insufficient:
Web ready:
Web ambiguous:
Web insufficient:

INTEGRITY
Foreign keys: PASS / FAIL
Source row reconciliation: PASS / FAIL
Source files unchanged: PASS / FAIL
Existing ccr_clients.sqlite3 unchanged: PASS / FAIL
External calls made: 0 / FAIL
Synthetic relationships created: 0 / FAIL
Dense N×N pairs generated: 0 / FAIL

TESTS:
X passed / Y failed

REPORT:
backend/data/CCR_RELATIONSHIP_PHASE2_FOUNDATION_REPORT.md

EXPOSURE DICTIONARY:
backend/data/CCR_EXPOSURE_DATA_DICTIONARY.md

PHASE 3 READY:
YES / NO

If NO:
list only genuine blockers.

STOP.
