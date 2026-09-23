Perform a new READ-ONLY data discovery analysis focused only on:

backend/Customer_latest.parquet
backend/thousandClients.csv

Do not redesign the UI.
Do not modify either source file.
Do not change the production database yet.
Do not create relationship logic yet.

PURPOSE

I need to understand these two datasets well enough to design the correct Lending customer/entity database.

Business understanding:

1. Customer_latest.parquet is believed to be the enterprise/master customer file.
   It contains approximately 3.6 million customer records.
   I have also heard that it may contain both active and inactive customers, but this has NOT been verified.

2. thousandClients.csv came from an exposure population.
   It was originally introduced so the application would have a manageable set of lending clients with exposure data to start analysis and visualization.

Do not assume either statement is fully correct.
Validate everything from the files.

==================================================
TASK 1 — PROFILE BOTH FILES
==================================================

For each file report:

- row count
- column count
- complete column list
- data types
- null count and null percentage per column
- distinct count for important columns
- obvious identifier columns
- name / legal-name columns
- status columns
- active/inactive indicators
- country / region columns
- sector / industry columns
- hierarchy / parent / group columns
- customer type / legal entity type columns
- dates
- exposure-related fields
- any CAGID-like fields
- any internal customer IDs
- any external IDs

Do not dump millions of records.

Use efficient Parquet analysis using PyArrow, DuckDB, Polars or equivalent.
Do not load the full 3.6M dataset into Python memory unnecessarily.

==================================================
TASK 2 — IDENTIFY THE CUSTOMER MASTER KEY
==================================================

Determine which columns in Customer_latest.parquet appear to function as:

- primary customer identifier
- CAGID
- legal entity identifier
- customer number
- parent/group identifier

For every candidate identifier calculate:

- non-null %
- distinct %
- duplicate count
- duplicate examples
- whether one identifier maps to several names
- whether one name maps to several identifiers

Do NOT assume a field is unique because its name looks like an ID.

==================================================
TASK 3 — UNDERSTAND ACTIVE / INACTIVE POPULATION
==================================================

Search the master file for any fields that may indicate:

- ACTIVE
- INACTIVE
- CLOSED
- TERMINATED
- ARCHIVED
- CURRENT
- customer lifecycle status
- effective/end dates
- relationship status
- account/customer status

Report the actual values and counts.

If no explicit active/inactive field exists, say so.

Do not infer active status from missing exposure.

==================================================
TASK 4 — ANALYZE THE EXPOSURE CLIENT FILE
==================================================

Profile thousandClients.csv independently.

Determine exactly what a row represents.

Examples to investigate:

- one row per client?
- one row per CAGID?
- one row per exposure?
- one row per facility?
- one row per customer-sector combination?
- multiple rows per client?

Identify:

- client identifier
- client name
- reported exposure
- CAM count
- country
- sector
- risk fields
- classifications
- any source-system identifier

Calculate unique-client counts using every plausible key.

==================================================
TASK 5 — MATCH THE TWO FILES
==================================================

Determine how thousandClients.csv relates to Customer_latest.parquet.

Test candidate joins in this order where fields exist:

1. exact CAGID / customer ID
2. other exact internal identifiers
3. normalized identifier
4. exact legal/customer name
5. normalized name

Name normalization may be used ONLY for analysis.

Examples:
- uppercase
- trim whitespace
- remove harmless punctuation
- normalize repeated spaces

Do NOT merge records based only on fuzzy names.

For every matching method report:

MATCHED
UNMATCHED
AMBIGUOUS
ONE-TO-ONE
ONE-TO-MANY
MANY-TO-ONE

Provide percentages.

Example expected report structure:

Exposure clients                  1,000
Exact ID matches                    xxx
Unique master matches               xxx
Ambiguous master matches            xxx
Name-only potential matches         xxx
No master match                     xxx

Use actual results only.

==================================================
TASK 6 — INVESTIGATE ONE-TO-MANY CASES
==================================================

For exposure clients matching multiple master rows, determine why.

Look for patterns such as:

- same CAGID with multiple records
- different legal entities
- branches
- historical versions
- active/inactive duplicates
- country variants
- aliases
- parent/child structures
- duplicate ingestion
- source-system duplicates

Give representative examples without changing the data.

==================================================
TASK 7 — COMPARE ATTRIBUTES
==================================================

For matched clients compare overlapping attributes between the two files.

Examples where available:

Name
Country
Sector
Industry
Region
Customer type
Parent/group
Status

For each overlapping field calculate:

- exact agreement %
- null in exposure / populated in master
- populated in exposure / null in master
- conflicting value %
- representative conflicts

This will tell us which dataset should be authoritative for each attribute.

==================================================
TASK 8 — UNDERSTAND POPULATION COVERAGE
==================================================

Determine:

A. How many Customer master entities exist overall.

B. How many appear in thousandClients.csv.

C. How many master entities have exposure represented by thousandClients.csv.

D. Whether thousandClients.csv appears to be:
   - a true 1,000-client sample,
   - top-exposure clients,
   - a filtered population,
   - or something else.

Do not assume the filename describes the real row/client count.

==================================================
TASK 9 — DISCOVER MASTER-DATA STRUCTURE
==================================================

Look for fields in Customer_latest.parquet that could support future relationship intelligence.

Specifically identify potential data for:

OWNERSHIP
- parent customer
- ultimate parent
- group
- legal hierarchy

GEOGRAPHY
- country
- incorporation country
- operating country
- region

ENTITY CLASSIFICATION
- entity type
- customer type
- legal form

INDUSTRY
- sector
- industry
- subsector

IDENTITY
- legal name
- alternate name
- identifiers

STATUS
- active/inactive/current/historical

Do not create relationships yet.

Just identify what the master can support.

==================================================
TASK 10 — DATA QUALITY
==================================================

For Customer_latest.parquet report:

- duplicate IDs
- duplicate normalized names
- missing IDs
- missing names
- suspicious placeholder names
- missing countries
- missing sectors
- conflicting classifications
- unexpectedly repeated records
- potentially historical versions

For thousandClients.csv do the equivalent analysis.

==================================================
TASK 11 — DATABASE DESIGN RECOMMENDATION
==================================================

Based ONLY on the analysis, propose the future logical model.

Do not implement it yet.

I expect something conceptually similar to:

CUSTOMER_MASTER
    customer_id
    cagid
    legal_name
    entity_type
    status
    country
    sector
    parent_id
    ultimate_parent_id
    source

EXPOSURE
    exposure_id
    customer_id
    reported_osuc
    as_of_date
    source

CUSTOMER_ALIAS / IDENTIFIER
    customer_id
    identifier_type
    identifier_value
    source

but derive the recommendation from the actual files.

Explicitly state which dataset should be authoritative for:

- customer identity
- customer name
- country
- sector
- lifecycle status
- hierarchy
- exposure

==================================================
IMPORTANT
==================================================

Do NOT assume that every 3.6M customer should appear in the Lending application.

Separate these concepts:

MASTER CUSTOMER UNIVERSE

vs

LENDING / EXPOSURE POPULATION

vs

RELATIONSHIP-CONNECTED ENTITIES

A master customer can exist without current Lending exposure.

Likewise a related entity may eventually need to be represented even if it has no Lending exposure.

This distinction is critical to the database design.

==================================================
OUTPUT
==================================================

Return a structured report:

1. EXECUTIVE FINDINGS
2. CUSTOMER_MASTER PROFILE
3. EXPOSURE FILE PROFILE
4. CANDIDATE IDENTIFIERS
5. ACTIVE / INACTIVE ANALYSIS
6. MATCHING RESULTS
7. ONE-TO-MANY / AMBIGUOUS MATCHES
8. ATTRIBUTE AGREEMENT
9. MASTER POPULATION VS EXPOSURE POPULATION
10. DATA QUALITY ISSUES
11. USEFUL MASTER-DATA RELATIONSHIP FIELDS
12. AUTHORITATIVE SOURCE RECOMMENDATION
13. PROPOSED DATABASE MODEL
14. QUESTIONS / UNKNOWN DATA
15. RECOMMENDED NEXT STEP

Also create compact analysis artifacts under a new analysis/output folder:

- schema_customer_master.csv
- schema_exposure_clients.csv
- match_summary.csv
- unmatched_exposure_clients.csv
- ambiguous_matches.csv
- attribute_reconciliation.csv
- customer_data_discovery_report.md

Do not export millions of master rows.

Do not modify source files.

Stop after the analysis and recommendation.
Do not build the new database yet.
