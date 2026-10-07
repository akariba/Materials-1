You are continuing work on the existing **CCR Relationship Intelligence / CCR Correlation** repository.

The architecture audit is complete.

The current design has been assessed as a credible POC foundation. Do NOT redesign the entire application.

The immediate objective is now:

> **Prove whether the existing CAM → entity → relationship → evidence → checker pipeline is accurate before scaling to ~1,600 CAMs or adding further enrichment.**

Proceed autonomously through the scope below.

Do not stop for confirmation unless there is a genuine external blocker.

---

# PHASE 0 — FREEZE THE BASELINE

Before changing any production logic:

1. Record the current Git commit/hash if available.
2. Record:
   - current extraction prompt/version
   - current model configuration
   - checker configuration
   - important confidence thresholds
   - canonical entity artifact path/version
3. Record the current relevant test results.

Create a benchmark metadata file containing these values.

The objective is reproducibility.

Do NOT modify the production extraction logic during this phase.

---

# PHASE 1 — CREATE A 10-CAM BENCHMARK SAMPLE

Build a reproducible benchmark of approximately **10 CAM documents**.

Use a fixed random seed where randomness is involved.

However, do NOT simply choose 10 fully random documents.

The sample should deliberately cover several useful situations.

Where possible include:

- PDF
- DOCX
- simple CAM
- complex CAM
- multiple entities in one CAM
- parent/subsidiary discussion
- ownership relationship
- guarantee relationship
- lender/borrower relationship
- customer/supplier or other commercial dependency
- entity aliases/name variations
- ambiguous entity resolution
- directional relationship
- entities co-mentioned with **no actual relationship**
- at least one CAM where few or no usable relationships exist

Do not manually cherry-pick only easy examples.

Create:

`benchmarks/cam10/manifest.json`

For every selected CAM record:

- benchmark_document_id
- original filename
- source path
- format
- file size
- document hash
- selection reason
- parser expected
- notes

Do not copy or alter the original CAMs unnecessarily.

---

# PHASE 2 — RUN PARSING ONLY

Run the existing ingestion/parser on the 10 selected CAMs.

Do not run SEC or web enrichment.

For every CAM produce:

- parser used
- number of pages if available
- sections identified
- paragraphs/text blocks
- tables detected
- extracted character count
- warnings
- parsing failures

Persist the parsed intermediate representation.

Create something similar to:

`benchmarks/cam10/parsed/`

Also produce a compact parsing report.

Very important:

Verify preservation of:

- document identity
- page number
- section
- source location
- relevant table information
- exact text

Do NOT fix parser behavior yet.

Record failures first.

---

# PHASE 3 — RUN THE EXISTING CAM PIPELINE UNCHANGED

Run the CURRENT pipeline on those 10 CAMs.

No SEC.

No web.

No market-data enrichment.

Use:

`CAM only`

For every document capture all intermediate stages, not only the final output.

Capture:

### Entity extraction
- entity name exactly as extracted
- entity type if available
- identifiers
- source location
- confidence

### Entity resolution
- extracted entity
- canonical entity ID
- CAGID
- GFCID
- matching method
- identifier used
- normalized-name score if applicable
- resolution status
- ambiguity/conflict flags

### Relationship maker output
- source entity
- relationship type
- target entity
- direction
- exact evidence
- page
- section
- confidence
- model/version

### Checker output
- accepted
- rejected
- review_required
- warnings/errors
- grounding result
- taxonomy result
- entity-anchor result

### Final output
- final relationship record
- evidence status
- whether persisted/eligible
- reason if excluded

Create machine-readable artifacts, preferably JSONL/Parquet.

Do not change production results to make the benchmark look better.

---

# PHASE 4 — CREATE THE HUMAN GOLD-LABEL REVIEW PACK

This is extremely important.

Do NOT let the same LLM generate "gold truth" and then measure itself against that gold truth.

Create a human-review file/template.

Prefer:

`benchmarks/cam10/gold_labels.csv`

or XLSX if the repository already has a suitable spreadsheet dependency.

For each potential relationship / relevant entity pair provide fields such as:

```text
benchmark_document_id
filename

source_entity_name
source_entity_canonical_id

target_entity_name
target_entity_canonical_id

system_relationship_type
system_direction

evidence_page
evidence_section
evidence_excerpt

GOLD_relationship_exists
GOLD_relationship_type
GOLD_source_entity
GOLD_target_entity
GOLD_direction
GOLD_evidence_correct
GOLD_entity_resolution_correct

reviewer_comment
review_status
```

Gold-label fields must initially be EMPTY.

The system must not pre-fill them as truth.

The purpose is for a human reviewer to establish ground truth independently.

---

# PHASE 5 — INCLUDE NEGATIVE CASES

Do not evaluate only extracted relationships.

Create explicit candidate pairs for cases where:

- two entities occur in the same CAM
- but no evidence-backed relationship exists.

These are necessary to detect hallucinated relationships.

Mark these for human review as potential negative examples.

The benchmark must test the system's ability to correctly say:

`NO RELATIONSHIP`

---

# PHASE 6 — BUILD THE BENCHMARK SCORING HARNESS

Create benchmark scoring code that runs ONLY after human gold labels have been completed.

Do not invent missing labels.

If labels are missing, report:

`BENCHMARK_NOT_READY_FOR_SCORING`

The scoring harness should calculate:

### Entity extraction

- precision
- recall
- F1

### Entity resolution

- exact entity-resolution accuracy
- ambiguous/unresolved rate

### Relationships

- relationship precision
- relationship recall
- relationship F1

A relationship match should consider:

- source entity
- target entity
- relationship existence
- normalized relationship type

### Direction

Calculate direction accuracy separately.

### Relationship type

Calculate relationship-type accuracy separately.

### Evidence grounding

Calculate:

- exact/acceptable evidence rate
- wrong-evidence rate
- missing-evidence rate

### Negative cases

Calculate false-positive rate for cases where no relationship exists.

### Checker

Calculate:

- accepted relationships that are actually correct
- accepted relationships that are incorrect
- rejected relationships that were actually correct
- review-required cases
- checker agreement with human gold

Pay special attention to:

**incorrect relationships that pass the checker.**

Those are particularly important.

---

# PHASE 7 — CREATE ERROR TAXONOMY

For every benchmark failure, classify the root cause into one of:

```text
PARSING
ENTITY_EXTRACTION
ENTITY_RESOLUTION
RELATIONSHIP_EXTRACTION
RELATIONSHIP_TYPE
RELATIONSHIP_DIRECTION
EVIDENCE_GROUNDING
CHECKER_FAILURE
SCHEMA
OTHER
```

Allow secondary causes where necessary.

Generate an error-analysis report grouped by root cause.

Do not propose architectural changes until the root causes are known.

---

# PHASE 8 — VERIFY THREE SPECIFIC RISKS FROM THE ARCHITECTURE AUDIT

The previous audit identified three areas needing particular attention.

## A. Maker-checker

Current implementation appears to be:

`LLM maker + deterministic checker`

rather than independent semantic LLM-vs-LLM verification.

For the 10-CAM benchmark, quantify:

- semantic relationship errors generated by maker
- how many deterministic checker catches
- how many incorrect relationships survive checker

Do NOT add a second LLM checker yet.

First measure whether it is necessary.

---

## B. Hidden relationships

Do NOT include topology/Jaccard candidates as verified relationships in CAM benchmark accuracy.

Keep separate concepts:

```text
EVIDENCE_BACKED_RELATIONSHIP
TOPOLOGY_CANDIDATE
```

A high Jaccard score does NOT prove that A and B have an actual relationship.

For this CAM benchmark, evaluate evidence-backed edges only.

---

## C. Correlation terminology

Do not calculate Pearson correlation because no time-series statistical correlation model currently exists.

For this benchmark:

`correlation` means nothing mathematically unless explicitly supported by implemented time-series data.

Treat current graph outputs as:

- relationship
- dependency
- proximity
- co-exposure
- graph distance

Do NOT alter UI terminology during this phase.

---

# PHASE 9 — DO NOT CHANGE THESE YET

Do NOT yet:

- migrate to PostgreSQL
- introduce Neo4j
- introduce Hadoop
- introduce MapReduce
- introduce Spark
- process all 1,600 CAMs
- enable broad web enrichment
- enable SEC enrichment for this benchmark
- redesign the frontend
- rewrite the entity canonicalizer
- change relationship thresholds to improve benchmark results
- change prompts after seeing individual benchmark results

We need an unbiased baseline first.

---

# PHASE 10 — RELATIONSHIP CONTRACT ASSESSMENT

Do not refactor it yet.

Using the 10-CAM output, determine whether all final relationships can consistently populate the following conceptual contract:

```text
relationship_id

source_entity_id
source_entity_name

target_entity_id
target_entity_name

relationship_type
relationship_direction

source_type
source_document_id
source_document_name

evidence_page
evidence_section
evidence_excerpt

confidence
validation_status

maker_model
checker_type
checker_model_or_version

valid_from
valid_to

created_at
updated_at
```

For every field classify:

```text
AVAILABLE
PARTIAL
MISSING
NOT_APPLICABLE
```

This will inform the next architecture change after validation.

---

# PHASE 11 — OUTPUTS

Create:

```text
benchmarks/cam10/
    manifest.json
    benchmark_metadata.json

    parsed/
    baseline_outputs/

    gold_labels.csv
    negative_cases.csv

    benchmark_metrics.py
    README.md
```

If appropriate also generate:

```text
cam10_baseline_summary.json
cam10_error_analysis.json
```

Do not overwrite normal production artifacts.

---

# FINAL REPORT

At the end, give me a concise report with:

## 1. Selected 10 CAMs

Filename, format and why selected.

## 2. Parsing results

Which parsed successfully and any structural problems.

## 3. Baseline extraction results

For each CAM:

```text
entities extracted
entities resolved
relationships proposed
relationships accepted
relationships rejected
review required
```

## 4. Evidence quality

Count relationships with:

- exact usable evidence
- weak evidence
- missing evidence

## 5. Checker behavior

How many maker outputs were blocked or flagged.

## 6. Gold dataset status

Clearly state that accuracy cannot be calculated until human gold labels are completed.

Do NOT invent accuracy numbers.

## 7. Human review instructions

Explain exactly which columns I need to fill in.

## 8. Structural gaps observed

Only factual findings from the benchmark.

## 9. Recommendation

Answer only:

- READY_FOR_HUMAN_LABELING
- BLOCKED_BY_PARSING
- BLOCKED_BY_PIPELINE_ERROR

with reasons.

---

# STOP CONDITION

Once:

1. the 10 CAMs have been processed,
2. the baseline artifacts exist,
3. the blank human gold-label pack exists,
4. the scoring harness exists,
5. the summary has been produced,

STOP.

Do not start fixing extraction behavior.

Do not scale beyond the 10 CAMs.

The next phase will begin only after human gold labels have been completed and baseline accuracy has been measured.
