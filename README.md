CCR DATA FOUNDATION — EXPOSURE & CLIENT ACTIVITY ANALYSIS

Work only in the CURRENT CCR repository.

This is CCR only.

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

Read the existing discovery/deep-dive reports first.

OBJECTIVE

Determine exactly what the 25,000 rows in:

thousandClients.csv

represent, why 16,769 unique GFCIDs produce 25,000 rows, and whether the
available data supports a governed client/activity classification.

Do NOT invent ACTIVE / INACTIVE definitions.

==================================================
1. ROW-GRAIN ANALYSIS
==================================================

Identify the likely business grain of one row.

Test whether rows appear to represent:

FACILITY
PRODUCT
NETTING_SET
EXPOSURE
ACCOUNT
LEGAL_ENTITY
DATE_SNAPSHOT
OTHER

Use column combinations and duplicate patterns.

Report:

25,000 total rows
16,769 unique GFCIDs
distribution of rows per GFCID

Show:

clients with 1 row
2 rows
3 rows
4 rows
5+ rows
maximum rows for one GFCID

For the top 20 multi-row clients show which fields differ between rows.

==================================================
2. COLUMN SEMANTICS
==================================================

For all 18 columns classify:

IDENTITY
GROUPING
EXPOSURE
FACILITY
PRODUCT
DATE
STATUS
CLASSIFICATION
REFERENCE
UNKNOWN

For each numeric field report:

min
max
median
null count
negative count
zero count
distinct count

Do not assume currency or units.

==================================================
3. DATE / STATUS FIELDS
==================================================

Identify every field that might indicate:

as-of date
effective date
maturity date
close date
open date
facility status
account status
client status
credit status

For each report:

field
values
distribution
business interpretation if defensible
confidence

Do not reinterpret unclear fields.

==================================================
4. MASTER ACTIVITY SIGNALS
==================================================

Inspect the 21-column Customer_latest.parquet schema for any fields that could
represent:

active/inactive
credit managed
client lifecycle
current/historical
closed/open
status
snapshot date

Especially inspect:

credit_managed_flag

Determine its observed values.

Compare it between:

A. the 16,769 CCR source clients
B. a representative/master-wide population

Report whether CCR clients are concentrated in one value.

Do NOT rename credit_managed_flag to active/inactive unless repository
documentation proves that meaning.

==================================================
5. CCR PRESENCE VS MASTER
==================================================

For the 16,769 CCR subjects classify:

MASTER_BACKED
CCR_ONLY
REVIEW_REQUIRED

Then determine whether exposure-file presence itself should mean:

CURRENT_CCR_POPULATION

This is a scope label only.

It must not automatically mean:

ACTIVE_CLIENT

unless proven.

==================================================
6. POSSIBLE ACTIVITY MODEL
==================================================

Based only on evidence, propose the safest lifecycle/scope states.

Potential concepts:

CURRENT_CCR_SCOPE
MASTER_ONLY
CCR_ONLY
REVIEW_REQUIRED
CURRENT_EXPOSURE_PRESENT
NO_CURRENT_CCR_EXPOSURE
UNKNOWN_ACTIVITY

Only recommend states supported by available data.

If ACTIVE / INACTIVE cannot be proven, say so explicitly.

==================================================
7. MULTI-ROW PATTERNS
==================================================

Determine the main causes of multiple rows per GFCID.

Create categories such as:

MULTIPLE_FACILITIES
MULTIPLE_PRODUCTS
MULTIPLE_ACCOUNTS
MULTIPLE_DATES
MULTIPLE_EXPOSURE_TYPES
IDENTICAL_DUPLICATE
UNKNOWN

Report client count and row count for each.

==================================================
8. DUPLICATES
==================================================

Check:

exact duplicate rows
duplicate GFCID + same relevant business attributes
duplicate rows differing only in non-business metadata

Do not delete anything.

Report whether any rows appear redundant.

==================================================
9. RECOMMENDATION
==================================================

Answer:

A. What does one `thousandClients.csv` row most likely represent?

B. Why are there 25,000 rows for 16,769 clients?

C. Can we defensibly identify active clients?

D. Can we defensibly identify current CCR exposure population?

E. Which fields can be used in the canonical database?

F. Which fields remain UNKNOWN and must not be used for scoring?

==================================================
10. OUTPUT
==================================================

Create:

analysis/output/CCR_EXPOSURE_ACTIVITY_ANALYSIS.md

and:

analysis/output/ccr_exposure_row_patterns.csv

FINAL RESPONSE:

CCR EXPOSURE / ACTIVITY ANALYSIS: PASS / FAIL

SOURCE ROWS:
25,000 / actual

UNIQUE GFCIDS:
16,769 / actual

ROW GRAIN:
<best-supported interpretation>

ROWS PER CLIENT
1 row:
2 rows:
3 rows:
4 rows:
5+ rows:
Maximum:

MAIN MULTI-ROW CAUSES:
1.
2.
3.

EXACT DUPLICATE ROWS:

STATUS FIELDS FOUND:
<list>

CREDIT_MANAGED_FLAG
Values:
CCR distribution:
Master distribution:
Can mean ACTIVE/INACTIVE: YES / NO

CAN DEFINE ACTIVE CLIENT:
YES / NO

CAN DEFINE CURRENT CCR SCOPE:
YES / NO

RECOMMENDED STATES:
<list>

UNKNOWN SEMANTICS:
<list>

SOURCE FILES MODIFIED:
0 / FAIL

PRODUCTION DB MODIFIED:
0 / FAIL

REPORT:
analysis/output/CCR_EXPOSURE_ACTIVITY_ANALYSIS.md

CSV:
analysis/output/ccr_exposure_row_patterns.csv

STOP.
