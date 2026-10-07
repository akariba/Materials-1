You are auditing an existing application called **CCR Relationship Intelligence**.

DO NOT modify code yet.

Your first task is to inspect the entire repository and determine exactly how the current system works end-to-end. Do not assume that UI labels or existing implementation choices are correct.

The application is intended eventually to support a large entity universe (~3 million entities) and discover evidence-backed relationships between entities using:

1. Entity/client master data, currently available primarily as Parquet.
2. Identifier/reference data, including where available:
   - CAGID
   - GFCID
   - LEI
   - CIK
   - ISIN
   - CUSIP
   - ticker
   - Bloomberg or other identifiers
3. Credit Approval Memos (CAMs), approximately 1,600 documents, potentially in:
   - PDF
   - DOCX
   - TXT
   - JSON
   - other semi-structured formats
4. SEC filings.
5. Web/public-source evidence.

The purpose is NOT necessarily to calculate a conventional Pearson market correlation coefficient.

The primary objective is to discover and represent **entity relationships / dependencies**, including direct and derived network relationships, with strong evidence and traceability.

The frontend currently exposes concepts including:

- Correlation
- Direct
- Indirect
- Hidden
- Citi Indirect Exposure
- Hop Distance
- Jaccard Co-Exposure
- Weighted Path Distance
- Evidence Status
- Source Precedence
- CAM Upload
- Credit Risk Intelligence
- Live Market Data
- entity identifiers
- relationship records
- Stress Analytics
- Portfolio Analytics
- Risk Heatmap

I need you to determine whether the backend implementation supporting these concepts is logically, mathematically, and technically correct.

# PHASE 1 — REPOSITORY DISCOVERY

Inspect the complete repository.

Identify:

- frontend structure
- backend structure
- API routes
- database/storage implementation
- schemas/models
- CAM-processing code
- document parsers
- LLM calls
- prompts
- entity matching/resolution
- relationship extraction
- graph construction
- distance calculations
- relationship classification
- SEC integration
- web-search integration
- market-data integration
- caching
- persistence
- test suite
- configuration
- sample/mock data

Trace the complete flow:

`source data -> ingestion -> parsing -> extraction -> entity resolution -> relationship creation -> validation -> persistence -> API -> frontend`

For every important component, provide the exact file and function/class responsible.

Do not infer functionality from filenames. Verify it in code.

# PHASE 2 — ENTITY MASTER

Determine exactly what the application considers an "entity".

Answer:

1. What is the canonical entity schema?
2. What field is the primary/canonical entity ID?
3. Can one entity have multiple identifiers?
4. How are aliases represented?
5. How are parent companies and subsidiaries represented?
6. How are duplicate entities detected?
7. How are entity names normalized?
8. What happens when two companies have similar names?
9. What happens when an identifier disagrees with a company name?
10. Is CAGID treated as authoritative?
11. What precedence exists between:
    - CAGID
    - GFCID
    - LEI
    - CIK
    - ISIN
    - CUSIP
    - ticker
    - company name
12. Can securities such as an ISIN incorrectly become separate "companies"?
13. Does the implementation distinguish:
    - legal entity
    - obligor
    - borrower
    - issuer
    - counterparty
    - security
    - group
    - parent
    - subsidiary?

Very important:

Do NOT assume the 3-million-row client file contains "counterparties".

For the core data model, determine whether these should instead be treated as neutral **entities**, with roles assigned later according to exposure/context.

# PHASE 3 — CAM DATA STRUCTURE

This is one of the most important parts of the audit.

Find every piece of code that handles CAMs.

Determine:

1. What CAM file formats are currently supported?
2. How are PDFs processed?
3. How are DOCX files processed?
4. How are TXT files processed?
5. How are JSON CAMs processed?
6. Is structured JSON unnecessarily flattened into text?
7. Are PDF page numbers retained?
8. Are headings retained?
9. Are paragraphs retained?
10. Are tables preserved?
11. Are table rows/columns reconstructed correctly?
12. Are identifiers preserved exactly?
13. Are financial figures preserved?
14. Are document metadata and dates retained?
15. Are source document IDs assigned?
16. Can every extracted fact be traced back to the exact CAM?
17. Can evidence be traced to:
    - document
    - page
    - section
    - paragraph/table
    - exact supporting text?

Determine the actual current intermediate CAM representation.

Show me an example of the current internal representation after ingestion.

For example, establish whether the system currently creates something conceptually like:

```json
{
  "document_id": "...",
  "document_type": "CAM",
  "pages": [],
  "sections": [],
  "tables": [],
  "entities": [],
  "relationships": []
}
```

Do not propose a new schema until you show me what currently exists.

# PHASE 4 — CAM RELATIONSHIP EXTRACTION

Inspect precisely what the LLM is being asked to extract.

Find and reproduce the current extraction prompt(s).

Determine whether the CAM pipeline extracts:

- primary entity
- all legal entities mentioned
- entity identifiers
- relationship source
- relationship target
- relationship type
- direction
- exact evidence
- document/page/section reference
- confidence
- extraction/model version

Determine whether relationships are being **inferred without evidence**.

The following rule should generally hold:

> Two entities appearing in the same CAM does NOT by itself establish a relationship.

Check whether the implementation violates this rule.

Determine how it handles relationships such as:

- owns
- owned_by
- parent_of
- subsidiary_of
- controls
- controlled_by
- guarantor_of
- guaranteed_by
- borrower_from
- lender_to
- customer_of
- supplier_to
- sponsor_of
- SPV_of
- affiliate_of
- joint_venture_with
- partner_of
- investor_in
- acquired/acquired_by
- merged_with
- services
- distribution
- licensing
- major customer concentration
- major supplier concentration
- financing dependency
- shared guarantor
- shared parent
- shared ownership

Do not require the relationship taxonomy to be completely closed.

Determine whether the current design allows discovery of legitimate new relationship types while still normalizing them into a governed taxonomy.

# PHASE 5 — MAKER / CHECKER

Determine whether a genuine **maker-checker** mechanism currently exists.

I do NOT mean simply calling an LLM twice.

Identify:

### Maker

What component initially extracts:

`Entity A -> relationship -> Entity B`

### Checker

What independently verifies that proposed relationship?

Determine:

1. Does the checker receive the original source evidence?
2. Does it independently verify the relationship?
3. Can it reject the maker's output?
4. Can it correct:
   - source entity
   - target entity
   - relationship type
   - direction
   - evidence
5. Does it return an explicit status such as:
   - accepted
   - rejected
   - ambiguous
   - needs_review?
6. Is the maker output accidentally anchoring the checker?
7. Are maker and checker using the exact same prompt?
8. Are they using independent reasoning?
9. Is there deterministic validation in addition to LLM validation?
10. Are checker decisions persisted?

Explain whether the current implementation genuinely deserves to be called maker-checker.

If not, explain exactly why.

# PHASE 6 — RELATIONSHIP DATA MODEL

Find the actual relationship schema.

Show all fields.

Determine whether the system can represent at minimum:

```text
relationship_id
source_entity_id
target_entity_id
relationship_type
relationship_direction
source_document_id
source_type
evidence
page/section
extraction_confidence
validation_status
maker_model
checker_model
created_at
valid_from
valid_to
```

Do not assume these exact fields are required; compare this concept with the actual implementation.

Critically determine whether **evidence is attached to the relationship edge**, rather than only the entity.

# PHASE 7 — DIRECT, INDIRECT AND HIDDEN

The frontend has:

- Direct
- Indirect
- Hidden

Find the backend definitions.

For each, tell me exactly what it means mathematically/algorithmically.

Validate whether the current definitions make sense.

A likely conceptual model would be:

### Direct
An evidence-backed edge exists:

`A -> B`

### Indirect
No direct edge is required, but a path exists:

`A -> X -> B`

### Hidden
Potentially a non-obvious dependency discovered through graph topology, common exposure, common ownership, common guarantor, shared supplier/customer, etc.

But DO NOT assume these definitions are correct.

Tell me what the code actually does.

If "Hidden" is merely an arbitrary label produced by an LLM, flag it.

# PHASE 8 — DISTANCE

The frontend contains:

- Hop Distance
- Weighted Path Distance

Find their implementation.

For Hop Distance, verify whether it is effectively shortest graph path:

```text
A -> B = 1
A -> X -> B = 2
A -> X -> Y -> B = 3
```

Determine:

- directed or undirected?
- relationship-type aware?
- confidence aware?
- source-quality aware?
- disconnected behavior?
- maximum traversal depth?
- cycle handling?

Then inspect **Weighted Path Distance**.

Give me the exact formula used.

Explain what every weight represents.

Verify that stronger relationships result in a sensible distance.

Check for mathematically suspicious transformations.

For example, if relationship strength is `w`, distance may need some transformation such as:

`distance = 1 / w`

or

`distance = -log(w)`

depending on the model.

Do not change anything yet; tell me what is actually implemented and whether it is defensible.

# PHASE 9 — JACCARD CO-EXPOSURE

The UI explicitly contains **Jaccard Co-Exposure**.

Find the implementation and exact formula.

Determine what the sets actually represent.

For example, if:

`N(A)` = counterparties/entities connected to A

and

`N(B)` = counterparties/entities connected to B

then a Jaccard similarity might be:

```text
J(A,B) = |N(A) ∩ N(B)| / |N(A) ∪ N(B)|
```

But do NOT assume that is what the code implements.

Show:

- actual formula
- actual sets
- empty-set handling
- whether relationship types are considered
- whether edge strengths are considered
- whether direct exposure and graph neighbors are being mixed incorrectly

Assess whether this metric is meaningful for CCR.

# PHASE 10 — "CORRELATION" TERMINOLOGY

This is critical.

Determine whether the system calculates an actual statistical correlation coefficient from time-series observations.

For example:

- equity returns
- CDS spread changes
- bond-spread changes
- PD changes
- market factors

If there is NO such time-series calculation, then determine whether the UI term **Correlation** is misleading.

We may actually be modeling:

- relationship
- dependency
- interconnectedness
- co-exposure
- network proximity

rather than statistical correlation.

Flag every place where "correlation" is used in a way that could mislead users or model-risk reviewers.

Do not rename anything yet.

# PHASE 11 — SEC FILINGS

Inspect current SEC implementation.

Determine:

1. How is an entity mapped to a CIK?
2. What happens when CIK is missing?
3. What filings are retrieved?
4. What sections are processed?
5. Does the SEC pipeline extract relationships between the registrant and other entities?
6. Does it retain filing/accession/date/page/section evidence?
7. Are subsidiary lists processed?
8. Are guarantees processed?
9. Are ownership disclosures processed?
10. Are major customers/suppliers extracted when explicitly disclosed?
11. Are exhibits processed?
12. Is SEC evidence kept separate from CAM evidence?

The fact that an SEC filing belongs to one registrant must NOT imply that every company appearing in it has a relationship.

Verify this.

# PHASE 12 — WEB RELATIONSHIPS

Inspect web-based discovery.

Determine:

- what search queries are generated
- which sources are permitted
- whether web results are treated as evidence or fact
- how source reliability is scored
- whether source URLs/titles/dates/passages are stored
- whether multiple sources can support the same relationship
- whether conflicting evidence is handled
- whether stale relationships expire
- whether web evidence can override CAM/SEC evidence

Find the implementation of **Source Precedence**.

Show the exact precedence rules.

Assess whether those rules are defensible.

# PHASE 13 — CITI INDIRECT EXPOSURE

The UI contains **Citi Indirect Exposure — CAM disclosure only**.

Find exactly what this means in backend code.

Explain:

- what constitutes indirect exposure
- how it is extracted
- whether it means financial exposure or merely an entity relationship
- whether amounts are captured
- whether currencies are normalized
- whether dates/maturities are captured
- whether indirect exposure can be double counted
- why CAM is the only accepted source, if that is an intentional rule

Flag any ambiguity.

# PHASE 14 — DATA STORAGE

Determine exactly where data currently lives.

Check whether the application uses:

- flat JSON
- CSV
- Parquet
- SQLite
- DuckDB
- PostgreSQL
- graph database
- in-memory structures
- browser/local storage

Show me the actual architecture.

Assess separately:

### Analytical processing
Would DuckDB/Parquet be appropriate?

### Production/front-end serving
Would PostgreSQL or another persistent database be more appropriate?

### Graph analytics
Can graph calculations reasonably be performed in Python/PostgreSQL, or is a dedicated graph database actually justified?

Do NOT recommend distributed technology such as Hadoop/MapReduce merely because the final entity universe is 3 million rows.

Assess actual workload first.

# PHASE 15 — PERFORMANCE AND SCALE

The target universe is approximately:

- 3 million entities
- ~1,600 CAMs initially
- potentially substantial SEC/web enrichment
- potentially millions of relationship edges

Assess:

- expected entity table size
- relationship table growth
- indexing
- entity lookup latency
- graph traversal performance
- CAM ingestion throughput
- LLM cost
- duplicate processing
- caching
- incremental processing

Determine whether processing each request by scanning all CAMs would be a design error.

The intended architecture should likely process each CAM once and persist extracted relationships for reuse.

Verify whether the current application already does this.

# PHASE 16 — DATA QUALITY

Find all current data-quality checks.

Evaluate:

### Entity resolution
- exact identifier match
- normalized-name match
- alias match
- ambiguity detection
- duplicate detection

### Relationship extraction
- evidence required
- correct direction
- valid entities
- relationship normalization
- duplicate edge detection

### Document processing
- parsing completeness
- page preservation
- table preservation
- unreadable content handling

### Graph
- orphan nodes
- self-loops
- impossible relationships
- duplicate/reversed relationships
- cycle behavior

### Provenance
Can every displayed relationship be traced back to its source?

# PHASE 17 — TESTING / GOLD DATASET

Find existing tests.

Determine whether there is a real validation dataset.

If not, propose a small first benchmark using approximately:

- 10 CAMs
- ~10–20 entities
- positive relationship examples
- difficult aliases
- multiple entities in one CAM
- negative examples where no relationship exists
- at least one ambiguous relationship
- at least one parent/subsidiary case
- at least one guarantee or ownership case

The benchmark should allow us to calculate at least:

- entity precision
- entity recall
- relationship precision
- relationship recall
- direction accuracy
- relationship-type accuracy
- evidence-grounding accuracy
- entity-resolution accuracy
- checker acceptance/rejection accuracy

Also test that the system correctly returns **no relationship** rather than hallucinating one.

# PHASE 18 — FRONTEND/BACKEND CONSISTENCY

Inspect every item visible in the frontend and determine whether it is backed by real production logic.

Specifically trace:

- Unique Companies
- Unique Relationships
- Database Records
- Reference Entities
- Citi Indirect Exposure
- Search company/CAGID/GFCID/LEI/CIK/BBG
- All / Direct / Indirect / Hidden
- CAM Upload
- Reset
- Rotate
- Credit Risk Intelligence
- Rating
- Financials
- Identity
- Relationships
- Distance
- Live Market Data
- Filterable Relationship Database
- Hop Distance
- Jaccard Co-Exposure
- Weighted Path Distance
- Evidence Status
- Source Precedence

For each item classify it as:

`REAL`
`PARTIAL`
`MOCK`
`PLACEHOLDER`
`BROKEN`
`UNVERIFIED`

Provide backend evidence supporting the classification.

# PHASE 19 — SECURITY AND GOVERNANCE

Check:

- uploaded CAM storage
- temporary files
- sensitive-data logging
- document deletion
- prompt logging
- LLM data transmission
- API authentication
- path traversal
- arbitrary file upload
- malformed PDFs/JSON
- prompt injection from CAM documents
- web-source prompt injection
- model output validation

Because CAM text is untrusted model input, check whether document content could instruct the LLM to ignore extraction rules.

# FINAL DELIVERABLE

Do NOT give me a generic architecture essay.

Produce an evidence-based audit from this repository.

Structure the response as:

## 1. Current architecture
A compact end-to-end diagram and explanation.

## 2. Current data model
Entity, identifier, CAM/document, relationship and evidence schemas.

## 3. CAM processing
Exactly what happens to PDF / DOCX / TXT / JSON.

## 4. Maker-checker
What exists, what does not, and whether it is genuinely independent.

## 5. Relationship logic
Direct / indirect / hidden definitions and implementation.

## 6. Mathematics
Exact formulas for:
- hop distance
- weighted path distance
- Jaccard co-exposure
- any score called correlation

## 7. Source enrichment
CAM / SEC / web / market-data behavior and source precedence.

## 8. Database/storage
Current implementation and scalability assessment.

## 9. Frontend-to-backend verification
For every visible frontend feature, classify:
REAL / PARTIAL / MOCK / PLACEHOLDER / BROKEN / UNVERIFIED.

## 10. Accuracy risks
Rank as:
- Critical
- High
- Medium
- Low

## 11. Missing definitions
Anything that the existing implementation uses without a precise business or mathematical definition.

## 12. Recommended target architecture
Only after documenting the current implementation.

## 13. Minimal 10-CAM pilot
Give the exact workflow we should use to validate this architecture before scaling.

## 14. Questions that require business clarification
Only ask questions that cannot be answered from the repository.

For every material conclusion, cite the exact file path and relevant function/class/code section.

Do not make code changes.

Do not silently assume that something is correct because it already exists.

Pay particular attention to the difference between:

**statistical correlation**

and

**entity relationship / dependency / network proximity**.

The objective of this audit is to determine whether what has already been built is genuinely defensible for a CCR relationship-intelligence application before we scale it.
