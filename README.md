You are now the lead engineer and credit-data analyst for the CCRIG Credit Relationship Workbench.

IMPORTANT: CHANGE OF PRIORITY.

STOP prioritizing dashboards, exposure visualizations, R2D2 enrichment, or sophisticated network-map design.

The PRIMARY objective for this iteration is:

BUILD THE STRONGEST POSSIBLE LENDING CREDIT RELATIONSHIP DATABASE FROM ALL AVAILABLE INTERNAL FILES.

Everything else depends on the quality of this database.

==================================================
PHASE 1 — DATABASE FIRST
==================================================

We have many CAMs, credit approval memos, review memos, Excel files, Word files, PDFs, and other credit documents already available in the project folders.

Examples visible in the repository include folders such as:

- CLFU
- CLM
- CRMPS
- RESCU
- other CAM / credit-document folders

and structured files such as:

- Core AI CAMs.xlsx
- CAM Priority Population_Batch 1.xlsx
- AI Economy Study_Masterfile.xlsx
- Citi Data Layer_July ME 2026.xlsx
- Customer_latest.parquet

These names are examples only.

FIRST inspect the complete repository and identify ALL potentially useful internal credit files.

Do not limit extraction to three CAMs.

Do not limit extraction to currently demonstrated CoreWeave / Anthropic examples.

The goal is to create a reusable Lending relationship database covering as much of the available internal population as possible.

==================================================
WHAT THE DATABASE MUST ANSWER
==================================================

For every client/entity, we want to know:

1. What other entities are connected to it?
2. What exactly is the relationship?
3. What is the direction of the relationship?
4. Is it current, historical, or indirect/hidden?
5. What internal document supports it?
6. What exact text supports the conclusion?
7. Is there an amount / percentage / facility value associated with it?
8. How confident are we that the relationship was extracted correctly?
9. Is the related entity itself another Citi/Lending client?
10. Does the same relationship appear in another CAM/document?
11. Are multiple portfolio clients connected to the same external company?

This database will later power:

- hidden-correlation discovery
- network mapping
- concentration analysis
- exposure overlays
- R2D2 / SEC / web enrichment

But NOT YET.

First make the internal database strong.

==================================================
STEP 1 — INVENTORY ALL SOURCE FILES
==================================================

Inspect all relevant project folders and classify available files.

Identify:

- CAM
- CCM
- Credit Approval Memo
- Annual Review
- Quarterly Review
- Financing / Facility memo
- Lending approval document
- other useful internal credit documents
- structured portfolio files
- masterfiles

Build an internal source inventory.

For every source file preserve at least:

source_file
source_folder
document_type
subject_company if identifiable
CAGID/internal identifier if identifiable
document_date if identifiable

Do NOT modify the original files.

==================================================
STEP 2 — IDENTIFY SUBJECT ENTITY OF EACH DOCUMENT
==================================================

Before extracting relationships, identify the primary subject/client of each document.

Example:

Document:
CoreWeave CAM

Subject:
CoreWeave

Then relationships mentioned inside it could include:

CoreWeave -> Microsoft
CoreWeave -> NVIDIA
CoreWeave -> Blackstone
etc.

Be careful with project/facility/SPV names.

Where possible distinguish:

legal entity
facility / SPV
parent
operating company
sponsor

Do not automatically assume they are the same entity.

==================================================
STEP 3 — EXTRACT ALL CREDIT-RELEVANT RELATIONSHIPS
==================================================

Read the available internal documents and extract every defensible relationship between entities.

Do NOT limit extraction to a tiny predefined list.

Capture relationships such as, where supported by the documents:

COMMERCIAL
- customer
- contracted customer
- major customer
- supplier
- critical supplier
- service provider
- distributor
- strategic partner

OWNERSHIP / CONTROL
- parent
- subsidiary
- sponsor
- equity investor
- beneficial owner
- joint venture

FINANCING / CREDIT SUPPORT
- guarantor
- parent guarantor
- lender
- agent bank
- debt investor
- backleverage provider
- collateral provider
- financing vehicle

DEPENDENCY
- technology dependency
- infrastructure dependency
- hardware dependency
- revenue dependency
- customer concentration
- supplier concentration

OTHER CREDIT-RELEVANT
- competitor
- acquisition target
- potential acquirer
- legal counterparty
- regulator
- rating agency
- other relationship explicitly relevant to the credit assessment

Do NOT invent a relationship merely because two companies are mentioned in the same document.

There must be supporting text.

==================================================
STEP 4 — RELATIONSHIP TYPE MUST BE ATOMIC
==================================================

Do NOT store:

Supplier / Investor / Customer

as one relationship type.

If the document supports three relationships, create three records:

CoreWeave | NVIDIA | Supplier
CoreWeave | NVIDIA | Equity Investor
CoreWeave | NVIDIA | Customer

One pair of entities may legitimately have multiple relationship types.

==================================================
STEP 5 — CANONICAL DATABASE MODEL
==================================================

Build one canonical relationship dataset.

At minimum each canonical relationship should support:

relationship_id
subject_entity_id
subject_entity_name
related_entity_id
related_entity_name
relationship_family
relationship_type
direction
relationship_state
direct_or_indirect
subject_category
related_entity_category
amount
amount_currency
percentage
other_quantitative_context
source_document
source_document_type
source_subject
source_date
source_page_or_location
evidence_excerpt
extraction_confidence
evidence_quality
review_state
notes

Possible relationship_state:

CURRENT
HISTORICAL
EMERGING
TERMINATED
UNKNOWN

Possible connectivity:

DIRECT
INDIRECT

Avoid using "hidden" as an underlying database value.

"Hidden relationship" can be a UI/business label for an INDIRECT relationship or a relationship discovered from another client's document.

==================================================
STEP 6 — EXACT EVIDENCE IS MANDATORY
==================================================

Transparency is critical.

Every extracted relationship MUST preserve evidence.

For example:

Subject:
CoreWeave

Related Entity:
Microsoft

Relationship Type:
Contracted Customer

Source:
CoreWeave CAM

Evidence excerpt:
exact supporting passage or concise source-grounded excerpt

Page / location:
page number / section / identifiable location where technically available

Amount:
67% FY25 revenue

Confidence:
High

Never save a relationship with no supporting evidence.

If evidence is weak or ambiguous, mark it clearly rather than pretending certainty.

==================================================
STEP 7 — CONFIDENCE MUST BE DEFENSIBLE
==================================================

Do not let the LLM arbitrarily call everything Very High.

Use conservative extraction confidence.

Suggested logic:

VERY HIGH
- explicit relationship statement
- entity identities clear
- direct internal source evidence
- potentially corroborated by another internal document

HIGH
- explicit or very strong relationship wording
- clear entities
- strong internal evidence

MEDIUM
- relationship is reasonably supported but some interpretation is necessary

LOW
- weak / ambiguous evidence
- retain only as a proposed relationship requiring review

INSUFFICIENT
- do not include as a canonical relationship

Confidence must be explainable from evidence.

==================================================
STEP 8 — CROSS-DOCUMENT CORROBORATION
==================================================

This is extremely important.

The same relationship may appear in:

- Company A CAM
- Company B CAM
- financing memo
- annual review
- another portfolio company's CAM

Detect that.

Example:

CoreWeave CAM:
CoreWeave -> NVIDIA = Supplier

NVIDIA-related document:
NVIDIA -> CoreWeave = Customer

These may represent the SAME economic relationship from opposite perspectives.

Do not create unrelated duplicate economic relationships.

Attach multiple evidence records to the same canonical relationship where appropriate.

Increase evidence strength when independently supported.

==================================================
STEP 9 — HIDDEN RELATIONSHIPS
==================================================

This is one of the most valuable features.

A relationship may NOT appear in Company A's own CAM but may appear in another company's CAM.

Example:

CoreWeave CAM does not mention Supermicro.

Another internal CAM says:

Supermicro -> CoreWeave

When an analyst searches CoreWeave, this relationship should still appear as:

CoreWeave <-> Supermicro

Discovery context:
INDIRECT / CROSS-DOCUMENT DISCOVERY

Source:
the other company's CAM

This is what we mean by finding hidden relationships from the internal database.

Do not confuse hidden with low confidence.

It may be a very high-confidence relationship discovered from another document.

==================================================
STEP 10 — ENTITY RECONCILIATION
==================================================

We need one company represented once.

Examples:

NVIDIA
NVIDIA Corp.
NVIDIA Corporation

should resolve to one canonical entity when evidence supports it.

Prefer:

1. CAGID/internal identifier
2. available legal identifiers
3. known structured-data identifiers
4. normalized legal name
5. aliases

Do NOT merge purely on fuzzy name similarity if uncertain.

Preserve aliases.

Also distinguish:

company
subsidiary
SPV
financing vehicle
facility
fund
parent

where those distinctions matter for credit.

==================================================
STEP 11 — RELATED ENTITIES OUTSIDE OUR CLIENT POPULATION
==================================================

DO NOT restrict the database to Citi/Lending clients.

This is critical.

Suppose our starting population contains:

90 lending clients.

If their CAMs identify:

Microsoft
NVIDIA
Blackstone
Dell
Supermicro
AWS
Google
etc.

those entities MUST also enter the entity database.

Mark whether:

is_portfolio_client = YES / NO

This enables future analysis such as:

"Show me all Citi Lending clients connected to NVIDIA."

That is one of the main business values of the project.

==================================================
STEP 12 — STRUCTURED ENTITY TABLE
==================================================

Create/maintain an entity master alongside the relationship table.

Example fields:

entity_id
canonical_name
aliases
CAGID
entity_type
entity_category
country
industry
is_portfolio_client
source_count
relationship_count

Only populate attributes supported by available data.

==================================================
STEP 13 — QUANTITATIVE RELATIONSHIP INFORMATION
==================================================

Extract quantities when they appear in the internal documents.

Examples:

$ amount
facility size
percentage ownership
percentage revenue
customer concentration %
supplier concentration %
loan amount
commitment
financing size

IMPORTANT:

Do not add unrelated dollar values together.

Preserve semantic meaning.

For example:

"$7.6bn facility"
and
"$400mm Citi commitment"

are different measures.

Store:

amount_value
amount_currency
amount_context

where possible.

==================================================
STEP 14 — BUILD THE DATABASE BEFORE FANCY UI
==================================================

This iteration is successful if the database becomes significantly stronger.

Do NOT spend most of the effort designing:

- complex dashboards
- OSUC visualizations
- R2D2 Assist
- SEC integration
- fancy category bubbles
- large portfolio reports

Those come later.

First create the trusted internal relationship foundation.

==================================================
STEP 15 — SIMPLE DATABASE EXPLORER
==================================================

Once the database is built, provide a clean way to inspect it.

At minimum:

Search entity / company / CAGID

Results:
- relationship count
- connected entities
- current relationships
- indirect / hidden relationships
- historical relationships

Relationship table:

Related entity
Relationship type
Direction
State
Source
Confidence
Amount/context
Evidence excerpt
Inspect

==================================================
STEP 16 — SIMPLE NETWORK MAP
==================================================

AFTER the database is working, add/retain a SIMPLE network map.

Do not make map sophistication the priority.

The useful interaction is:

1. Search/select Company A
2. Company A appears in the center
3. Draw relationship lines to connected entities
4. Different edge labels/colors may represent relationship type
5. Click Company B
6. Pivot the map so Company B becomes the selected entity
7. Display all known relationships of Company B

This should allow the user to visually "walk" through the relationship network.

Example:

CoreWeave
     |
     | Supplier
     |
NVIDIA
     |
     | Strategic / Customer / other supported links
     |
Other Company

Clicking NVIDIA should immediately show NVIDIA's network from the database.

==================================================
STEP 17 — MULTIPLE RELATIONSHIPS BETWEEN TWO ENTITIES
==================================================

If two companies have several relationship types, represent them clearly.

Example:

CoreWeave <-> NVIDIA

Supplier
Equity Investor
Customer

The map may show:
- multiple small edge labels
OR
- one edge with "3 relationships"

Clicking the edge should open the complete relationship list.

Do not collapse the database records into one ambiguous label.

==================================================
STEP 18 — MAP MUST BE DRIVEN ONLY BY DATABASE
==================================================

The network map should not invent information.

It should simply visualize canonical relationships already stored in the database.

Database first.
Visualization second.

==================================================
STEP 19 — DATABASE QUALITY SUMMARY
==================================================

Add a simple summary showing:

- documents processed
- documents successfully parsed
- unique entities
- portfolio clients
- external/non-client entities
- canonical relationships
- relationship types
- current relationships
- indirect/cross-document relationships
- historical relationships
- relationships with multiple internal sources
- low-confidence relationships requiring review
- documents that failed extraction

This is very important for transparency.

==================================================
STEP 20 — EXTRACTION FAILURE HANDLING
==================================================

Do not silently skip files.

If a PDF/DOCX/XLSX cannot be parsed:

record:

file
reason
status = extraction_failed

We need to know how complete the database actually is.

==================================================
ACCEPTANCE TESTS
==================================================

TEST 1
All relevant internal Lending folders/files are inventoried.

TEST 2
Available CAM / credit documents are processed rather than only the original demo CAMs.

TEST 3
Canonical entity master exists.

TEST 4
Canonical relationship database exists.

TEST 5
Each relationship has source provenance and evidence.

TEST 6
Multiple relationship types can exist for the same entity pair.

TEST 7
Duplicate/reverse representations do not inflate canonical relationship counts.

TEST 8
Cross-document corroboration works.

TEST 9
A relationship discovered in another client's CAM appears when searching either entity.

TEST 10
External/non-client entities are retained in the database.

TEST 11
Current / indirect / historical status is retained where supported.

TEST 12
Amounts/percentages are retained with correct context when present.

TEST 13
Search an entity and retrieve all known relationships.

TEST 14
Simple network map is driven by the database.

TEST 15
Clicking a connected entity pivots/explores that entity's relationships.

TEST 16
Extraction statistics and failures are visible.

TEST 17
No fabricated evidence / entities / relationships are introduced.

==================================================
IMPORTANT ENGINEERING RULES
==================================================

Inspect before modifying.

Reuse existing code.

Do not broadly refactor the application.

Do not rebuild working components.

Do not create fake data.

Do not use R2D2/Web/SEC in this iteration unless an existing internal file itself contains that evidence.

We are proving the INTERNAL DATABASE first.

Do not stop repeatedly to ask for approval.

Proceed autonomously through this approved scope.

If an individual document cannot be parsed, record the failure and continue with the remaining files.

Do not let one bad document block the entire batch.

==================================================
FINAL RESPONSE
==================================================

When finished, report only:

1. Number of files discovered
2. Number successfully processed
3. Number failed + why
4. Number of unique entities
5. Number of portfolio clients
6. Number of external/non-client entities
7. Number of canonical relationships
8. Relationship types discovered
9. Current / indirect / historical counts
10. Number of relationships with multiple-source corroboration
11. Exact database files/tables created or updated
12. Exact source files used
13. Acceptance-test PASS/FAIL
14. Genuine blockers

Do not give me a long theoretical discussion.

IMPLEMENT FIRST.

==================================================
CORE OBJECTIVE
==================================================

Extract the maximum defensible credit-relationship information from the complete available internal Lending document population, preserve exact evidence and provenance, reconcile it into a strong canonical entity/relationship database, and only then expose that database through a simple interactive network explorer.
