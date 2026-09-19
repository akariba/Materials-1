STOP ALL NEW FEATURE DEVELOPMENT.

Do NOT work on:
- network-map enhancement
- R2D2
- SEC
- web enrichment
- OSUC visualization
- dashboards
- configuration enhancements

The database build completed technically, but the resulting counts raise serious data-quality concerns.

We now need a STRICT DATA VALIDATION / GROUNDING PASS.

==================================================
WHY THIS IS REQUIRED
==================================================

Current output reports approximately:

- 54 files discovered
- 48 source documents parsed
- 31,371 reconciled entities
- 29,255 portfolio clients
- 26,453 canonical relationships
- 28,850 indirect/cross-document records
- 22,627 historical/terminated
- 6,504 low-confidence records
- only 380 multi-source corroborated relationships

These numbers may indicate that portfolio/master workbooks or row-level records have been interpreted too broadly as clients/entities/relationships.

For example, the UI currently shows an entity such as:

"UBS Sterling Corporate Bond Indexed Fund"

as a PORTFOLIO CLIENT even though it has zero extracted relationships.

That may be legitimate data, but it must be proven.

DO NOT assume the current database is correct merely because parsing succeeded.

The objective now is:

PROVE WHICH RECORDS ARE REAL, TRACE THEM TO SOURCE EVIDENCE, REMOVE OR reclassify incorrectly inferred records, and establish trustworthy population boundaries.

==================================================
1. IDENTIFY THE ROLE OF EVERY SOURCE FILE
==================================================

Inspect every input file and classify it into exactly one primary role:

A. RELATIONSHIP EVIDENCE SOURCE
Examples:
- CAM
- CCM
- credit approval memo
- annual review
- quarterly review
- financing memo
- other narrative credit document

B. PORTFOLIO / ENTITY MASTER
Examples:
- priority population
- customer master
- Citi data layer
- masterfile

C. LOOKUP / REFERENCE DATA

D. OTHER / NOT USED

This distinction is critical.

A portfolio/master workbook can establish that an entity exists.

It MUST NOT automatically create a relationship simply because two entities or attributes occur in rows.

==================================================
2. REBUILD THE DEFINITION OF "PORTFOLIO CLIENT"
==================================================

Do NOT mark every entity found in master/reference files as a Lending portfolio client.

Determine which exact source/field establishes:

is_portfolio_client = true

Document the rule.

If there is no reliable field, do not guess.

Create separate concepts:

- portfolio_client
- external_related_entity
- master/reference entity
- unresolved entity

Then recalculate counts.

I expect a clear explanation for why the current result says 29,255 portfolio clients.

==================================================
3. RELATIONSHIPS MUST REQUIRE DOCUMENT EVIDENCE
==================================================

Every canonical relationship MUST be linked to at least one genuine relationship evidence record.

A relationship cannot be created solely from:

- being in the same spreadsheet
- being in the same industry
- appearing in adjacent rows
- having similar attributes
- co-mention without relationship language
- portfolio membership
- common country
- common rating
- common category

Require evidence that actually states or strongly supports a relationship.

For every canonical relationship verify:

relationship_id
entity_a
entity_b
relationship_type
source_document
source_location
evidence_excerpt

If evidence_excerpt does not demonstrate the relationship, it must not remain canonical.

==================================================
4. AUDIT A RANDOM SAMPLE
==================================================

Take a reproducible random sample of at least:

- 25 HIGH / VERY HIGH confidence relationships
- 25 MEDIUM confidence relationships
- 25 LOW confidence relationships
- 25 INDIRECT / cross-document relationships
- 25 HISTORICAL relationships

For each record display:

Entity A
Entity B
Relationship Type
State
Connectivity
Confidence
Source File
Exact Evidence
Reason for classification

Then automatically assess whether the source excerpt actually supports:

A. the two entities
B. the relationship type
C. direction
D. state
E. direct/indirect classification

Produce error counts.

Do not hide failures.

==================================================
5. VALIDATE "INDIRECT / HIDDEN"
==================================================

The current database reports approximately 28,850 indirect/cross-document records.

That is suspiciously large.

An INDIRECT / HIDDEN relationship should mean something specific.

Valid example:

CoreWeave's own CAM does not mention Supermicro,
but another internal CAM explicitly documents
Supermicro -> CoreWeave.

That may be classified:

CROSS_DOCUMENT_DISCOVERY = true

It should NOT become indirect merely because:

- it came from another file
- the source subject differs
- the entities occur in different tables
- there was no direct match in the subject CAM

Separate:

CONNECTIVITY:
DIRECT / INDIRECT

from:

DISCOVERY:
SUBJECT_DOCUMENT
CROSS_DOCUMENT

These are different dimensions.

A direct commercial relationship found in another company's CAM is still DIRECT.

It is merely CROSS-DOCUMENT DISCOVERED.

Recalculate these counts.

==================================================
6. VALIDATE HISTORICAL / TERMINATED
==================================================

22,627 historical/terminated relationships is also suspicious.

Historical must require temporal evidence.

Examples of valid language:

- formerly
- previously
- terminated
- matured
- repaid
- exited
- sold
- ceased
- no longer
- prior relationship
- historical transaction

Do NOT classify a relationship as historical simply because:

- document is old
- source date is old
- another record is newer
- it appears in an annual review
- it is absent from another document

If the evidence does not explicitly or strongly establish historical status:

state = UNKNOWN or CURRENT where explicitly supported.

Recalculate.

==================================================
7. VALIDATE RELATIONSHIP TYPES
==================================================

There are currently 24 atomic relationship types.

For every type provide:

- relationship type
- total canonical records
- sample 5 records
- sources generating that type
- extraction rule used

Specifically scrutinize large classes such as:

- Lender
- Infrastructure Dependency
- Contracted Customer
- Guarantor
- Parent Company
- Sponsor
- M&A Target
- Regulator
- Advisor
- Agent Bank

Do not allow LLM-created labels to become truth without supporting evidence.

==================================================
8. VALIDATE ENTITY RECONCILIATION
==================================================

Audit entity resolution.

Find examples of:

- exact duplicates
- aliases
- same-name different companies
- SPV vs parent
- fund vs operating company
- facility vs borrower
- legal entity vs group name

Ensure we are not collapsing distinct legal entities.

Also ensure obvious aliases are not creating unnecessary duplicate nodes.

==================================================
9. MASTERFILES MUST NOT POLLUTE RELATIONSHIP EXTRACTION
==================================================

Pay special attention to:

- AI Economy Study_Masterfile.xlsx
- CAM Priority Population_Batch 1.xlsx
- Citi Data Layer_July ME 2026.xlsx
- Core AI CAMs.xlsx
- Customer_latest.parquet

For each one explicitly state:

PURPOSE
ENTITIES CONTRIBUTED
PORTFOLIO CLIENT FLAG CONTRIBUTED?
RELATIONSHIPS CONTRIBUTED?
EVIDENCE CONTRIBUTED?

If a file is merely population/reference data:

RELATIONSHIPS CONTRIBUTED = 0

unless the file explicitly contains relationship information.

==================================================
10. CREATE A DATABASE QUALITY REPORT
==================================================

After validation report:

FILES
- evidence documents
- portfolio/master files
- reference files

ENTITIES
- confirmed Lending portfolio clients
- external related entities
- unresolved/reference-only entities

RELATIONSHIPS
- evidence-backed canonical relationships
- direct
- indirect
- cross-document discovered
- current
- historical
- unknown state

QUALITY
- high/very-high confidence
- medium
- low/review
- multi-document corroborated
- records rejected during validation

Also calculate:

% canonical relationships with exact evidence
% with identifiable source location
% with multiple internal sources
% low-confidence
% unresolved entity identity

==================================================
11. GOLDEN SAMPLE
==================================================

Create a small "golden sample" of approximately 20–30 relationships from well-understood CAMs.

Prefer known examples such as relationships around:

- CoreWeave
- Anthropic
- other clearly documented subjects in the available CAM set

For every golden record manually/strictly verify:

entity pair
type
direction
state
source
excerpt

Use this as a regression test for future database rebuilds.

==================================================
12. DO NOT DELETE QUESTIONABLE RECORDS BLINDLY
==================================================

Create statuses:

VALIDATED
REVIEW_REQUIRED
REJECTED

Preserve provenance.

Questionable records should be moved out of the trusted canonical view rather than silently disappearing.

The user-facing canonical database should show VALIDATED records by default.

==================================================
13. FIX THE UI AFTER VALIDATION
==================================================

The top cards should report trustworthy metrics, not raw ingestion volume.

For example:

Validated relationships
Review required
Confirmed Lending clients
External connected entities
Cross-document discoveries
Multi-source corroborated

Do not headline "31,371 entities" if most are merely reference/masterfile rows.

==================================================
ACCEPTANCE CRITERIA
==================================================

PASS only if:

1. The exact reason for 29,255 portfolio clients is identified.
2. Portfolio/master rows are separated from relationship evidence.
3. Every canonical relationship has real supporting evidence.
4. Direct vs indirect is separated from cross-document discovery.
5. Historical status requires temporal evidence.
6. A random sample audit is produced with error rates.
7. Entity reconciliation is audited.
8. Masterfile contributions are explicitly documented.
9. Counts are rebuilt after quality filtering.
10. A golden relationship sample exists.
11. Canonical UI defaults to validated relationships.
12. No map/dashboard work is performed.

==================================================
FINAL RESPONSE
==================================================

Do not provide a long implementation narrative.

Report:

BEFORE VALIDATION:
- entities
- portfolio clients
- canonical relationships
- indirect
- historical

AFTER VALIDATION:
- confirmed Lending clients
- external related entities
- reference/unresolved entities
- validated canonical relationships
- review-required relationships
- rejected relationships
- direct
- indirect
- cross-document discovered
- current
- historical
- unknown
- multi-source corroborated

Then provide:

- sample audit accuracy
- major causes of false positives
- files responsible for population inflation
- golden sample status
- PASS/FAIL acceptance tests

STOP after validation.
