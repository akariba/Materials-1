# CoreAI Relationship Intelligence — Full Backend, Prompt and Data-Integrity Audit

## OBJECTIVE

Perform a comprehensive, READ-ONLY technical investigation of the existing **CoreAI Relationship Intelligence** application.

This is a separate colleague-developed application.

Do not confuse it with our CCR Correlation / CCR Relationship Intelligence project.

Our own CCR production implementation is being developed independently and must remain untouched.

The purpose of this investigation is to understand the colleague's complete implementation, identify its useful technical approaches and establish whether any displayed relationships, financial figures, confidence ratings or supporting evidence are fabricated, unsupported, incorrectly attributed or misleading.

**Do not redesign, rebuild or modify the colleague's application.**

Produce a detailed implementation reconstruction, including the actual LLM prompts used by the application.

---

## 1. LOCATE THE REAL PROJECT

Identify the project responsible for generating:

`CoreAI_relationship_report_20260928.html`

The report is described as a counterparty relationship intelligence report containing approximately 43 relationship records, using credit approval memos, SEC filings and news sources.

Potential relevant local workspace:

`C:\Users\ak54743\Downloads\phr-tool-main`

However, do not assume this workspace contains the report's backend. It may only be where the report is being viewed.

Locate the actual generating application using a bounded search of relevant local project folders, configuration files, Git history, scripts and report metadata.

Search for:

- CoreAI
- relationship intelligence
- relationship extraction
- Credit Approval Memo
- relationship report generation
- maker/checker
- MapReduce
- LLM prompts
- report templates
- relationship records
- source evidence
- confidence scoring
- XLSX/CSV exports

Find the original backend, not merely the generated HTML file.

If the source project cannot be located, clearly distinguish what can be established from the report from what remains unknown.

Do not invent an architecture based on filenames.

---

## 2. RECONSTRUCT THE ENTIRE BACKEND ARCHITECTURE

Identify all backend components and the actual execution sequence.

Trace the complete flow:

Input documents
→ document ingestion
→ text extraction
→ entity identification
→ relationship extraction
→ AI processing
→ evidence checking
→ aggregation/deduplication
→ confidence calculation
→ output persistence
→ HTML/report generation.

Determine whether this is the real sequence or whether the implementation differs.

For each actual component, document:

- Module/file name
- Function/class
- Purpose
- Input schema
- Output schema
- Data transformations
- AI/model dependency
- Validation behavior
- Error handling
- Storage location
- Downstream consumer

Identify whether the implementation uses:

- Python
- FastAPI or another backend
- LangChain
- Google ADK
- R2D2
- Claude
- OpenAI models
- Custom LLM gateway
- MapReduce
- Parallel processing
- Agent orchestration
- Maker/checker validation
- Deterministic validation
- Human review

Report only components found in the actual project.

Do not infer an agent architecture merely because the report contains AI-generated text.

Create an accurate end-to-end architecture diagram in Mermaid.

---

## 3. RECOVER ALL ACTUAL LLM PROMPTS

**This is a priority requirement.**

Find every prompt involved in creating the relationship intelligence output.

Inspect:

- Python prompt constants
- Prompt templates
- Markdown/TXT prompt files
- JSON/YAML configurations
- Agent instructions
- Model request builders
- System messages
- User messages
- Critic/checker instructions
- Refinement prompts
- Aggregation prompts
- Report generation prompts

Recover prompts for any implemented stages such as:

1. CAM document understanding
2. Entity identification
3. Corporate hierarchy extraction
4. Ownership extraction
5. Relationship discovery
6. Relationship classification
7. Evidence extraction
8. SEC filing analysis
9. Web/news investigation
10. Relationship verification
11. Contradiction checking
12. Confidence assessment
13. Relationship aggregation
14. Portfolio summarization
15. HTML report construction

Do not invent prompts for stages that do not exist.

For every discovered prompt, document:

**PROMPT ID**

**SOURCE FILE AND LINE RANGE**

**PURPOSE**

**MODEL USED**

**SYSTEM PROMPT — EXACT TEXT**

**USER PROMPT TEMPLATE — EXACT TEXT**

**VARIABLES AND THEIR SOURCES**

**EXPECTED OUTPUT FORMAT**

**JSON SCHEMA, IF ANY**

**VALIDATION APPLIED**

**RETRY/ERROR HANDLING**

**NEXT PIPELINE STAGE**

Preserve the original wording in a local technical appendix, subject to applicable information-handling restrictions.

Redact credentials, tokens and secrets, but do not replace actual prompt logic with generic descriptions.

If prompts are generated dynamically, reconstruct their templates and variable binding from code.

If the model receives the full CAM, selected sections, chunks, retrieval results or summarized context, identify exactly which.

Determine whether models are allowed to use general knowledge or must rely strictly on supplied evidence.

---

## 4. INVESTIGATE DOCUMENT INGESTION

Determine exactly how the application processes credit approval memos.

Identify:

- Original document directories
- PDF/DOCX support
- Number of actual unique documents
- Document parsing libraries
- Table extraction
- Text extraction
- Chunking and chunk sizes
- Document section recognition
- Context-window handling
- Metadata retention
- Page references
- Source hashing
- Duplicate handling
- Parsing failures

The generated report claims a corpus of approximately 49 credit approval memos.

Verify this independently.

Report:

- Documents discovered
- Unique document hashes
- Documents successfully parsed
- Documents skipped
- Documents partially parsed
- Documents used in relationship extraction
- Documents actually cited in final records

Check whether source documents are truncated before reaching the LLM.

Check whether numeric fields, names, tables or contractual clauses are lost during extraction.

Investigate whether CAM evidence was extracted from actual document text or from intermediate AI summaries.

---

## 5. TRACE RELATIONSHIP DATA POPULATION

For every output relationship, establish the complete lineage:

Original document
→ extracted text
→ specific evidence passage
→ model input
→ model output
→ checker/validator
→ normalized relationship
→ stored record
→ displayed report row.

Identify all locations where data can be introduced or modified.

Pay special attention to:

- Hardcoded sample relationships
- Static JSON datasets
- Fallback records
- Test fixtures
- Example outputs
- Prepopulated dictionaries
- Cached LLM responses
- Manual edits
- Synthetic enrichment
- Default values
- Missing-value substitutions
- Generated financial figures

Determine whether the final report combines genuine extracted relationships with manually entered or preloaded relationships.

If manual records exist, identify how they are labeled and validated.

Inspect whether relationship descriptions are verbatim source facts, source-grounded paraphrases, AI interpretations or unsupported assertions.

---

## 6. AUDIT EVERY RELATIONSHIP RECORD

Perform a record-by-record investigation of the generated relationship report.

Do not check only a small sample.

For each physical relationship record, retrieve:

- Record ID
- Entity A
- Entity B
- Canonical identifiers
- Relationship type
- Relationship direction
- Contract/deal description
- Claimed financial amount
- Citi indirect exposure
- Source document
- Source location
- Evidence excerpt
- Source date
- Confidence
- Validation result
- Generation method
- AI-processing status

Compare the record against its actual underlying source.

Test:

**Entity accuracy**

Do both legal entities exist and match the source?

**Relationship accuracy**

Does the source actually support the claimed relationship type?

**Directionality**

Is ownership, guarantee, financing or customer/supplier direction correct?

**Financial accuracy**

Are disclosed amounts represented correctly, including currency, scale and units?

**Date accuracy**

Are transaction dates, source dates and effective dates distinguished?

**Source accuracy**

Does the claimed source exist and contain the asserted information?

**Evidence accuracy**

Does the supporting excerpt contain the relevant claim?

**Confidence accuracy**

Does the assigned confidence correspond to the actual quality of evidence?

**Duplicate accuracy**

Are bidirectional representations and repeated evidence counted appropriately?

Do not count the reverse direction of the same relationship as an independent supporting fact.

---

## 7. DETECT FABRICATED OR UNSUPPORTED INFORMATION

Search specifically for:

- Invented relationships
- Invented company identifiers
- Fabricated CAM references
- Fake source citations
- Unsupported financial amounts
- Unsupported guarantees
- Incorrect ownership statements
- Hallucinated partnerships
- Misattributed exposures
- Fabricated dates
- Invented confidence scores
- LLM-generated excerpts not present in source documents
- Information introduced through static/demo fallback paths

Also detect subtler failures:

- Real company but wrong legal entity
- Real transaction but wrong participant
- Real source but unsupported conclusion
- Real agreement but incorrect financing amount
- Source mentions two companies without establishing a relationship
- Parent-company exposure incorrectly assigned to subsidiary
- Bidirectional relationship counted twice
- Missing source labeled as verified
- AI summary promoted into evidence
- Expired or superseded relationships presented as current

Use explicit findings:

**SUPPORTED**

The original source supports the stated relationship and material attributes.

**PARTIALLY_SUPPORTED**

The main relationship exists, but some details or classifications are unsupported.

**UNSUPPORTED**

The cited source does not establish the claim.

**CONTRADICTED**

The source conflicts with the stated relationship or attribute.

**UNVERIFIABLE**

The necessary source is unavailable or cannot be independently examined.

**SYNTHETIC_OR_HARDCODED**

The record comes from test, mock, demonstration or manually constructed data without appropriate production-evidence treatment.

**DUPLICATE**

The record repeats an existing fact or direction without adding independent evidence.

Do not label a record fabricated merely because a document is inaccessible.

Reserve a finding of fabrication for evidence of generated or invented content, not simple verification failure.

Keep all original records unchanged.

---

## 8. FINANCIAL AND EXPOSURE VALIDATION

Inspect all numerical values in the report.

In particular examine:

- Syndicated financing amounts
- Facility commitments
- Credit facilities
- Guarantees
- Investment values
- Ownership percentages
- Citi indirect exposure
- Revenue dependencies
- Maturity dates
- Currency denominations

Trace each reported figure to its original evidence.

Examples requiring particular care include reported financing commitments above USD 900 million and descriptions of syndicated financing arrangements.

Confirm whether these values represent:

- Entire syndicated facility
- Citi participation
- Borrower exposure
- Parent guarantee
- Total project financing
- Historical facility amount
- Undrawn commitment

These values are not interchangeable.

Check whether the report's `Not Quantifiable` field reflects an actual inability to quantify Citi exposure or simply missing calculations.

Do not generate missing values.

Document units and currency conversions where used.

---

## 9. INVESTIGATE AI CONFIDENCE CALCULATION

The report displays confidence labels including HIGH and VERY HIGH.

Find the exact implementation responsible for assigning them.

Determine whether confidence comes from:

- Model self-assessment
- Rule-based calculation
- Source reliability
- Evidence count
- Cross-source corroboration
- Entity-resolution confidence
- Maker/checker agreement
- Manually assigned values

Retrieve the actual formula, thresholds or prompt instructions.

Determine whether confidence is evidence-based or merely requested from the LLM.

Check for default HIGH or VERY HIGH values.

A model's self-reported confidence must not be treated as proof of relationship accuracy.

Report cases where the confidence appears overstated.

---

## 10. ANALYZE THE MAKER/CHECKER AND MAPREDUCE DESIGN

Determine whether the implementation genuinely uses a multi-stage extraction and checking pipeline.

If present, explain each stage in detail:

**MAP**

How relationship candidates are extracted from individual CAMs or chunks.

**SEMANTIC CHECKER**

Whether another model reviews candidates against original evidence.

**DETERMINISTIC VALIDATOR**

Whether exact evidence, identifiers, taxonomy and source fields are programmatically checked.

**REDUCE**

How individual CAM findings are aggregated.

**DEDUPLICATION**

How parallel relationships, bidirectional records and repeated sources are handled.

**FINAL SYNTHESIS**

How the report combines entity-level and portfolio-level information.

For each stage, identify the exact code, prompt, model and output.

Verify that the checker receives independent access to source evidence rather than only the maker's JSON.

Check whether rejected relationships can reappear during aggregation or HTML generation.

If there is no genuine independent checker, report that clearly.

---

## 11. INSPECT STORAGE AND EXPORTS

Determine where final relationship records are stored.

Identify:

- JSON files
- CSV files
- XLSX files
- SQLite or other databases
- Parquet files
- In-memory structures
- HTML-embedded JSON
- Browser-local data
- Generated reports

Inspect whether the HTML is:

- Standalone/static
- Loaded from a backend API
- Populated by embedded JSON
- Dynamically querying a database

Inspect the CSV/XLSX export implementation.

Determine whether exports contain exactly the displayed validated records or a different underlying dataset.

Test whether filtering affects export correctly.

Check if the displayed count of approximately 43 records represents:

- Physical relationship records
- Unique entity pairs
- Bidirectional entries
- Deduplicated facts
- Aggregated report rows

Explain any difference.

---

## 12. VERIFY REPRODUCIBILITY

Determine whether the same inputs and existing saved responses can reproduce the final report.

Inspect:

- Run configuration
- Model names and versions
- Prompts
- Temperature
- Token limits
- Retries
- Parallelism
- Intermediate artifacts
- Execution logs
- Timestamps
- Human review interventions

If an offline replay using existing artifacts is safe and available, run it without changing the colleague's original files.

Do not initiate a large new LLM job or repeatedly call internal providers.

Do not overwrite original outputs.

If complete reproduction is impossible, explain why.

---

## 13. COMPARE WITH OUR CCR ARCHITECTURE

After completing the independent audit, provide a concise technical comparison against our current CCR Relationship Intelligence design.

Compare only relevant concepts:

- CAM extraction
- Canonical entity resolution
- Relationship discovery
- Source validation
- LLM prompting
- Semantic checking
- Deterministic checking
- Confidence
- Relationship deduplication
- Hierarchy extraction
- Direct/indirect classification
- Exposure attribution
- Data persistence
- Report rendering

Classify each useful colleague-project technique as:

- REUSABLE
- REUSABLE_WITH_CHANGES
- NOT_RECOMMENDED
- INSUFFICIENT_EVIDENCE

Do not copy or integrate any code into our CCR project.

Do not introduce dependencies on the colleague's repository.

Do not assume their report contains verified facts without completing the audit.

---

## 14. DELIVER A DETAILED TECHNICAL REPORT

Create a local report:

`COREAI_TECHNICAL_IMPLEMENTATION_AND_DATA_AUDIT.md`

Include:

### Part A — Executive findings

What the application actually does, what works, and what cannot be verified.

### Part B — Architecture

Real pipeline diagram and component-by-component implementation.

### Part C — Prompt inventory

Every actual prompt, its source location, model, variables, schema and role in the processing pipeline.

### Part D — Document processing

Actual CAM inventory, extraction, parsing, retrieval and evidence lineage.

### Part E — Relationship generation

Exact relationship extraction, classification, scoring, deduplication and validation logic.

### Part F — Data population

How records enter the output and how manual, cached, hardcoded or generated values are handled.

### Part G — Record-by-record authenticity audit

A table covering every final physical relationship record, including source verification and identified defects.

### Part H — Financial integrity

Findings about financing amounts, ownership percentages and Citi exposure values.

### Part I — Confidence methodology

Actual scoring or confidence assignment and whether labels are justified.

### Part J — Storage and frontend

Actual backend persistence, report data loading and export implementation.

### Part K — Reproducibility

Whether results can be reconstructed from available evidence.

### Part L — CCR comparison

Which design elements are worth reusing conceptually in our existing CCR project.

### Part M — Implementation blueprint

Produce a faithful technical blueprint of how the colleague's system is implemented, including module interfaces, stage sequencing, prompts, schemas, model routing and validation gates.

Distinguish IMPLEMENTED behavior from PROPOSED improvements.

Do not create hypothetical prompts and present them as original prompts.

---

## 15. REQUIRED STRUCTURED OUTPUTS

Alongside the Markdown report, produce where feasible:

`coreai_prompt_inventory.md`

Containing complete recovered prompt templates, their source code locations and invocation details.

`coreai_relationship_evidence_audit.csv`

Containing one row per physical relationship with authenticity classification and source evidence findings.

`coreai_architecture.mmd`

Containing the actual end-to-end architecture.

`coreai_data_lineage.json`

Containing source-to-output lineage for every traceable relationship record.

Save these as local audit artifacts only, without changing the colleague's source project.

Do not include secrets or restricted raw document contents in an unauthorized output location.

---

## 16. STRICT EXECUTION RULES

- READ ONLY on the colleague's project.
- Do not modify the existing CCR Correlation project.
- Do not edit the generated HTML report.
- Do not change source relationships.
- Do not add fake data to complete missing records.
- Do not run broad AI enrichment.
- Do not initiate an expensive reprocessing of all CAMs.
- Do not expose credentials or tokens.
- Do not weaken certificate verification.
- Do not assume a reporting claim is true without locating its evidence.
- If sources are unavailable, classify them UNVERIFIABLE.
- Do not claim an internal or external data source was checked unless it actually was.
- Document all unresolved questions.

Use actual code and source evidence to support every technical conclusion.

## 17. FINAL SUMMARY

Return:

```text
COREAI RELATIONSHIP INTELLIGENCE — AUDIT

ACTUAL BACKEND LOCATED: YES/NO
PROJECT ROOT:
PRIMARY ENTRY POINT:
MODEL PROVIDERS:

CAM DOCUMENTS CLAIMED:
CAM DOCUMENTS FOUND:
CAM DOCUMENTS ACTUALLY PROCESSED:

PROMPTS RECOVERED:
PROMPTS FULLY DOCUMENTED:

PHYSICAL RELATIONSHIP RECORDS:
UNIQUE ENTITY PAIRS:

SUPPORTED:
PARTIALLY_SUPPORTED:
UNSUPPORTED:
CONTRADICTED:
UNVERIFIABLE:
SYNTHETIC_OR_HARDCODED:
DUPLICATE:

FINANCIAL AMOUNT ISSUES:
EXPOSURE ATTRIBUTION ISSUES:
IDENTITY RESOLUTION ISSUES:
CONFIDENCE SCORING ISSUES:

MAKER/CHECKER:
MAPREDUCE:
DETERMINISTIC VALIDATION:
SOURCE TRACEABILITY:
REPRODUCIBILITY:

REUSABLE CCR DESIGN ELEMENTS:
HIGH-RISK IMPLEMENTATION PATTERNS:

TECHNICAL REPORT PATH:
PROMPT INVENTORY PATH:
RECORD AUDIT PATH:
ARCHITECTURE PATH:
DATA LINEAGE PATH:

FILES MODIFIED IN SOURCE PROJECT: 0
```

**EXECUTE THE INVESTIGATION, RECOVER THE REAL IMPLEMENTATION AND ORIGINAL PROMPTS, TRACE EVERY RELATIONSHIP TO ITS EVIDENCE, AND IDENTIFY UNSUPPORTED OR FABRICATED CONTENT.**

Do not implement a replacement application.

Do not modify our CCR project.

Stop after delivering the complete technical and data-integrity audit.
