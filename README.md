CCR DATA FOUNDATION — IDENTITY EXCEPTION DEEP DIVE

Use the analysis ALREADY completed.

Do not rerun the entire 3.6M master discovery unless a specific value needs
verification.

Read:

analysis/output/CCR_IDENTITY_EXCEPTION_REPORT.md
analysis/output/ccr_identity_exception_resolution.csv
analysis/output/unmatched_exposure_clients.csv
analysis/output/ambiguous_matches.csv
analysis/output/attribute_reconciliation.csv
analysis/output/match_summary.csv

This is CCR ONLY.

Do not modify:
- Customer_latest.parquet
- thousandClients.csv
- production SQLite
- frontend
- relationship logic

No SEC.
No GLEIF.
No Web.
No AI enrichment.

OBJECTIVE

Expand the current identity-exception analysis enough that we can decide how
the canonical CCR database should treat every exception.

The previous summary was too high level.

==================================================
1. THE 8 UNMATCHED CLIENTS
==================================================

Create a table with ONE ROW PER unmatched CCR client.

Show every useful available identity field:

source row count
GFCID
CAGID
legal name
normalized name
country
client/entity type
industry/sector
LEI if present
beneficial-owner/reference fields if present
exposure record count

For each client show:

MASTER GFCID MATCH:
YES / NO

MASTER CAGID MATCH:
YES / NO

MASTER EXACT LEGAL NAME MATCH:
YES / NO

MASTER NORMALIZED NAME MATCH:
YES / NO

MASTER LEI MATCH:
YES / NO / NOT AVAILABLE

Then explain:

WHY IT IS UNMATCHED

Classify likely interpretation:

NEW_OR_ABSENT_MASTER_ENTITY
STALE_SOURCE_IDENTIFIER
SPV_OR_SPECIAL_ENTITY
SOURCE_DATA_DEFECT
NAME/IDENTIFIER QUALITY ISSUE
UNKNOWN

Do not resolve based on guesswork.

Most importantly answer:

Should this CCR entity still receive its own canonical CCR entity record even
though it is absent from the 3.6M master?

YES / NO / REVIEW

Give reason.

==================================================
2. THE 6 AMBIGUOUS CLIENTS
==================================================

Create a section for each of the six cases.

For each show:

SOURCE CLIENT
- GFCID
- CAGID
- legal name
- country
- other identifiers

ALL MASTER CANDIDATES

For every competing master candidate show:

master GFCID
master CAGID
legal name
country
entity type
LEI
active/status fields
other differentiating fields

Then explain exactly WHY the CAGID is one-to-many.

For the 4 deterministically resolved cases show:

SELECTED MASTER RECORD
RESOLUTION RULE
FIELDS THAT PROVED THE MATCH
WHY OTHER CANDIDATES WERE REJECTED

For the 2 review-required cases show:

CANDIDATE A
CANDIDATE B
...
WHAT IS IDENTICAL
WHAT IS DIFFERENT
WHAT INFORMATION IS MISSING
WHAT WOULD RESOLVE THE CASE

Do not use fuzzy name matching as decisive evidence.

==================================================
3. THE 44 HISTORICAL CONFLICT GROUPS
==================================================

The previous output:

TRUE MULTI-ENTITY = 5
OTHER = 39

is too coarse.

Reclassify ALL 44 groups into more informative categories.

Try categories such as:

TRUE_MULTI_ENTITY
COSMETIC_NAME_VARIANT
SHARED_CAGID
SHARED_GFCID
HIERARCHY_PROPAGATION
OWNER_REFERENCE_PROPAGATION
PLACEHOLDER_NAME
DUPLICATE_MASTER_ROW
LEGAL_NAME_VARIANT
COUNTRY_VARIANT
ENTITY_TYPE_VARIANT
IDENTIFIER_CONFLICT
INSUFFICIENT_INFORMATION
OTHER

Use additional categories if the data requires them.

Goal:

OTHER should be used only when genuinely unavoidable.

For every category report:

group count
record count
representative examples
database implication

Then provide a separate detailed table for the 5 TRUE_MULTI_ENTITY groups.

For each group show all entities and identifiers.

==================================================
4. MASTER SNAPSHOT LIMITATION
==================================================

The current master appears to contain snapshot:

20260806

Explain clearly what CAN and CANNOT be inferred from having only this snapshot.

In particular distinguish:

CURRENT DUPLICATE / CONFLICT

from:

HISTORICAL IDENTIFIER REUSE

Do not call something historical reuse unless actual historical records prove
it.

==================================================
5. ATTRIBUTE RECONCILIATION
==================================================

Summarize the important differences between:

thousandClients.csv

and

Customer_latest.parquet

for matched clients.

For each overlapping identity/reference field report:

field
same count
different count
CCR null / master populated
CCR populated / master null
conflict count
recommended authority

Examples:

legal name
country
industry
sector
entity type
LEI
owner/reference fields

Do not include exposure-only fields as master identity conflicts.

==================================================
6. CANONICAL MODEL DECISION
==================================================

Based on the evidence, recommend how the CCR canonical model should handle:

A. master-matched CCR client

B. CCR client absent from master

C. deterministic one-to-many resolution

D. unresolved ambiguous identity

E. true multi-entity shared identifier

F. cosmetic name variants

G. hierarchy / owner-reference propagation

Do not implement yet.

Use concepts such as:

CANONICAL
CCR_ONLY_ENTITY
REVIEW_REQUIRED
IDENTIFIER_ALIAS
MASTER_REFERENCE
EXTERNAL_ENTITY

where appropriate.

==================================================
7. POPULATION RECONCILIATION
==================================================

Give a precise proposed population bridge.

Start from:

16,769 unique CCR source GFCIDs

Show:

exact master matched
deterministically resolved ambiguous
CCR-only unmatched
review-required ambiguous
other excluded/duplicate cases if any

Then calculate the recommended number of canonical CCR subject entities.

Do not force this number to equal the old 16,755.

Derive it from the analysis.

==================================================
8. CREATE UPDATED REPORT
==================================================

Create:

analysis/output/CCR_IDENTITY_EXCEPTION_DEEP_DIVE.md

Also create:

analysis/output/ccr_historical_conflict_groups.csv

Columns should include:

group_id
classification
gfcid
cagid
legal_name
country
lei
entity_type
record_count
reason
canonical_recommendation

Do not overwrite the previous report.

==================================================
9. FINAL RESPONSE
==================================================

Return:

CCR IDENTITY DEEP DIVE: PASS / FAIL

UNMATCHED CLIENTS
Total: 8
CCR-only entities recommended:
Source defects:
Review required:
Other:

AMBIGUOUS
Total: 6
Deterministically resolved: 4
Review required: 2

For each review-required case:
<one-line description>

44 CONFLICT GROUPS
True multi-entity:
Cosmetic name variant:
Shared identifier:
Hierarchy/owner propagation:
Duplicate row:
Placeholder:
Identifier conflict:
Insufficient information:
Other:

PROPOSED CCR CANONICAL POPULATION
Source unique CCR clients:
Master matched:
Deterministic resolutions:
CCR-only canonical entities:
Review-required:
Recommended canonical subject count:

MOST IMPORTANT DATA MODEL IMPLICATIONS
1.
2.
3.
4.
5.

REPORT:
analysis/output/CCR_IDENTITY_EXCEPTION_DEEP_DIVE.md

DETAIL CSV:
analysis/output/ccr_historical_conflict_groups.csv

SOURCE MODIFICATIONS:
0 / FAIL

PRODUCTION DB MODIFICATIONS:
0 / FAIL

STOP.
