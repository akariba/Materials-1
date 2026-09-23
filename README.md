CCR DATA FOUNDATION — IDENTITY EXCEPTION RESOLUTION

Work only in the CURRENT CCR repository.

This is CCR, not Lending.

Read the existing discovery outputs:

analysis/output/customer_data_discovery_report.md
analysis/output/unmatched_exposure_clients.csv
analysis/output/ambiguous_matches.csv
analysis/output/attribute_reconciliation.csv
analysis/output/match_summary.csv

Also inspect the actual source schemas as needed:

Customer_latest.parquet
thousandClients.csv

DO NOT modify either source file.
DO NOT modify production SQLite.
DO NOT work on frontend.
DO NOT run SEC, GLEIF, Web or AI.
DO NOT create relationships.

OBJECTIVE

Explain and, where defensible, resolve the:

- 8 unmatched exposure clients
- 6 ambiguous matches

against the 3.6M customer master.

For each exception inspect all available identity fields including where present:

GFCID
CAGID
legal name
normalized legal name
country
entity/client type
LEI
owner/reference fields
active/inactive/history indicators
other stable internal identifiers

For each row classify the root cause as one of:

MASTER_HISTORY
IDENTIFIER_CONFLICT
DUPLICATE_MASTER_ENTITY
NAME_VARIANT
INACTIVE/HISTORICAL_RECORD
ONE_TO_MANY
MISSING_MASTER_RECORD
BAD_SOURCE_IDENTIFIER
OTHER

Then assign one of:

RESOLVED_EXACT
RESOLVED_DETERMINISTIC
REVIEW_REQUIRED
UNRESOLVED

IMPORTANT

Do not resolve an entity using fuzzy name similarity alone.

A deterministic resolution must have a defensible identifier or combination
of identity attributes.

Do not silently collapse distinct legal entities.

For the 44 historical legal-entity conflict groups, inspect why they were
classified that way and confirm whether they represent:

- repeated snapshots of the same legal entity
- genuine multiple legal entities
- historical identifier reuse
- inactive/current record combinations
- another pattern

Do not change all 44 records. This task is analysis first.

Create:

analysis/output/ccr_identity_exception_resolution.csv

Columns:

source_row_or_client
source_gfcid
source_cagid
source_name
candidate_master_gfcid
candidate_master_cagid
candidate_master_name
root_cause
resolution_status
resolution_method
evidence_fields
notes

Also create:

analysis/output/CCR_IDENTITY_EXCEPTION_REPORT.md

The report should contain:

1. 8 unmatched — root causes
2. 6 ambiguous — root causes
3. deterministic resolutions found
4. still unresolved
5. interpretation of the 44 historical conflict groups
6. any source-data defect
7. recommended canonical handling

FINAL RESPONSE:

CCR IDENTITY EXCEPTION ANALYSIS: PASS / FAIL

UNMATCHED
Original: 8
Deterministically resolved:
Review required:
Still unresolved:

AMBIGUOUS
Original: 6
Deterministically resolved:
Review required:
Still unresolved:

HISTORICAL CONFLICT GROUPS
Count:
Same-entity history:
True multi-entity:
Identifier reuse:
Other:

SOURCE FILES MODIFIED:
0 / FAIL

PRODUCTION DB MODIFIED:
0 / FAIL

REPORT:
<path>

CSV:
<path>

STOP.
