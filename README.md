You are continuing the Lending Credit Relationship Workbench.

Act as the lead implementation engineer for a real Lending credit-intelligence solution.

This is NOT a UI-polish task.
This is NOT a demo task.
This is NOT another validation loop over the same 767 relationships.

The current trusted baseline already exists:

Baseline:
LENDING_INTERNAL_BASELINE_V1

Trusted canonical relationships:
767 VALIDATED

Review-required:
916

Rejected:
31,274

Golden sample:
PASS

The validated baseline must now be treated as a regression/reference set.

DO NOT keep rebuilding and revalidating the same baseline unless a code change directly affects extraction or reconciliation.

We are now moving from:

STATIC POC DATABASE

to:

REAL LENDING RELATIONSHIP INGESTION + UPDATE + GOVERNANCE PIPELINE


==================================================
CORE BUSINESS OBJECTIVE
==================================================

Build a sustainable Lending relationship data process that can:

1. know the full target Lending population
2. know which clients have CAM / credit documents available
3. know whether the CAM is current or stale
4. ingest new documents incrementally
5. extract relationships from the correct sections
6. reconcile them into the canonical database
7. preserve exact evidence and document versions
8. flag uncertain / conflicting relationships for review
9. avoid rebuilding everything from scratch
10. keep the relationship database current as new CAMs arrive

This is the main objective.

Do NOT prioritize map polish, dashboard styling, animations, R2D2, SEC, or web enrichment in this phase.


==================================================
1. TARGET LENDING POPULATION CONTROL
==================================================

The email / business context established that the target population is larger than the current parsed CAM set.

The population includes the CoreAI / Technology Lending names tracked in the masterfile.

The email discussion referenced:

- 75 CoreAI names
- 343 Technology CAGIDs
- 418 CAGIDs total

Do NOT hard-code 418 blindly.

Inspect the current masterfile / priority population / structured files and determine the actual target population now present.

Create a canonical population control table.

For every target client store at minimum:

client_id
CAGID
canonical_name
business_population
CAM_available
latest_CAM_date
latest_document_type
latest_document_file
document_status
stale_flag
ingestion_status
last_ingested_at
relationship_count
review_required_count

Possible document_status:

AVAILABLE_CURRENT
AVAILABLE_STALE
MISSING
PENDING_EXTRACTION
UNRESOLVED

Do not mark a client as covered just because it exists in a master workbook.


==================================================
2. CAM / CREDIT DOCUMENT FRESHNESS
==================================================

This is a hard requirement from the business emails.

For every Lending client:

identify all available relevant credit documents.

Examples may include:

- CAM
- CCM
- AR
- QR
- Credit Approval Memo
- Annual Review
- Quarterly Review
- Facility / financing memo

Determine:

- document type
- document date
- whether it is the latest available relevant document
- whether older documents still need to be retained for historical evidence

Do NOT simply ingest every document as equally current.

The pipeline must distinguish:

CURRENT SOURCE
HISTORICAL SOURCE

Never delete historical evidence.

But the latest relevant document should be clearly identifiable.


==================================================
3. SECTION-AWARE EXTRACTION
==================================================

Do not treat a CAM as one undifferentiated text blob.

The business explicitly referenced sections such as:

2. Recommendation
3. Approval Request
7. Relationship / Counterparty / Obligor Structure
8. Key Risks and Mitigants
9. Historical Financial Analysis
10. Outlook and Projections
11. Sources of Repayment
Risk Rating and Classification Assessment
ORR Overview
Support
FRR Overview
Cluster Analysis
Classification

Inspect the actual documents and identify section headings robustly.

Extract relationship information with section provenance.

Each evidence record should support:

source_document
document_type
document_date
section_name
page_or_location
exact_excerpt

This improves transparency and allows us to later answer:

"Where in the CAM did this relationship come from?"


==================================================
4. RELATIONSHIP EXTRACTION TARGETS
==================================================

Extract defensible credit-relevant relationships including, where supported:

COMMERCIAL
- contracted customer
- major customer
- supplier
- critical supplier
- service provider
- strategic partner

OWNERSHIP / CONTROL
- parent company
- subsidiary
- sponsor
- equity investor
- beneficial owner
- joint venture

FINANCING / SUPPORT
- guarantor
- parent guarantor
- lender
- financing provider
- backleverage provider
- agent bank
- collateral provider

DEPENDENCY / CONCENTRATION
- customer dependency
- supplier dependency
- revenue concentration
- technology dependency
- infrastructure dependency

OTHER
- legal relationship
- regulatory relationship
- acquisition / target relationship
- other explicit credit-relevant relationships supported by evidence

Do NOT classify simple co-mentions as relationships.


==================================================
5. INDIRECT EXPOSURE EXTRACTION
==================================================

This is an explicit business requirement.

The emails asked for examples where indirect exposure is mentioned.

Therefore add a distinct extraction capability for:

INDIRECT EXPOSURE / INDIRECT RELATIONSHIP

Do not treat "indirect" as a vague label.

Capture:

- subject entity
- intermediate entity if applicable
- ultimate related entity
- relationship chain / path
- relationship type
- evidence
- section
- confidence
- why it is indirect

Example conceptual structure:

Company A
  -> depends on Supplier X
  -> Supplier X depends on Company B

or:

Company A
  -> SPV
  -> Sponsor / Parent

If a relationship is direct but discovered in another document, do NOT mark it indirect.

Keep:

economic connectivity:
DIRECT / INDIRECT

separate from:

discovery origin:
SUBJECT_DOCUMENT / CROSS_DOCUMENT / MULTI_DOCUMENT


==================================================
6. INCREMENTAL INGESTION
==================================================

This is one of the most important requirements.

The system must not rebuild all files every time.

Implement incremental ingestion.

For every source document calculate a stable document fingerprint.

Use available metadata such as:

path
filename
size
modified time
hash

When ingestion runs:

NEW document:
process it

CHANGED document:
reprocess it

UNCHANGED document:
skip extraction

REMOVED document:
do NOT silently delete historical evidence
mark source status appropriately and require explicit governance decision

The ingestion job should report:

new files
changed files
unchanged files
failed files
relationships added
relationships updated
relationships sent to review
relationships retired / historical


==================================================
7. DOCUMENT VERSIONING
==================================================

Maintain document versions.

Example:

CoreWeave CAM — Jan 2026
CoreWeave CAM — Aug 2026

These are not duplicates.

The newer document may supersede the older one for current truth,
but the older document remains valid historical evidence.

Store:

document_id
document_version
subject_entity
document_type
document_date
file_hash
supersedes_document_id
is_latest_relevant_document


==================================================
8. PERSISTENT DATABASE MODEL
==================================================

Move away from using a single large JSON file as the operational data model.

The current frozen JSON baseline can remain for regression/reference.

Implement a proper persistent local database suitable for this POC and future Unix deployment.

Prefer a lightweight, transparent, portable option.

SQLite is acceptable for the current phase unless the repository already has a better proven database pattern.

Do NOT over-engineer with distributed infrastructure.

At minimum create normalized tables for:

ENTITIES
DOCUMENTS
DOCUMENT_VERSIONS
RELATIONSHIPS
RELATIONSHIP_EVIDENCE
POPULATION_CONTROL
ALIASES
REVIEW_DECISIONS
INGESTION_RUNS

Keep the data model simple and inspectable.


==================================================
9. CANONICAL RELATIONSHIP MODEL
==================================================

One economic relationship should remain canonical.

Example:

Entity A
Entity B
Relationship Type

Multiple documents may support it.

Do not create duplicate relationships for every source.

Instead:

RELATIONSHIP
    -> Evidence 1
    -> Evidence 2
    -> Evidence 3

Keep:

direction
state
connectivity
confidence
review_status
current/historical status

separate from evidence records.


==================================================
10. CHANGE DETECTION BETWEEN DOCUMENT VERSIONS
==================================================

When a new CAM arrives for an existing client:

compare the newly extracted relationships with the previous latest document.

Classify:

NEW_RELATIONSHIP
UNCHANGED_RELATIONSHIP
CHANGED_RELATIONSHIP
NO_LONGER_MENTIONED
EXPLICITLY_TERMINATED

Do NOT assume:

not mentioned = terminated.

Only mark historical / terminated when supported by evidence.

Otherwise:

NO_LONGER_MENTIONED / REVIEW_REQUIRED


==================================================
11. CONFIDENCE / QUALITY CONTROL
==================================================

Do not use pure LLM confidence.

Use explainable quality factors.

Examples:

- explicit relationship wording
- clear entity identity
- section relevance
- current vs stale source
- corroboration count
- multiple document support
- ambiguous language
- exact amount / contractual language
- entity matching certainty

Keep confidence conservative.

The existing validated baseline and golden sample should remain regression tests.


==================================================
12. REVIEW WORKFLOW
==================================================

Any new extraction that does not meet trusted canonical criteria should go to:

REVIEW_REQUIRED

Do not automatically promote it.

Analyst review should be able to:

CONFIRM
MODIFY
REJECT

Store:

reviewer
review_time
decision
notes

Do not overwrite original extraction/evidence.


==================================================
13. DATA COMPLETENESS / COVERAGE REPORT
==================================================

Create a useful operational coverage report.

The system should be able to answer:

How many target Lending clients exist?
How many have a current CAM?
How many have only stale CAMs?
How many have no CAM?
How many are pending extraction?
How many documents were processed?
How many relationships were validated?
How many require review?

This is much more important than another UI dashboard.


==================================================
14. INGESTION COMMAND / ENDPOINT
==================================================

Create one clean ingestion entry point.

For example:

python build/update command

or

one backend endpoint / admin action

The ingestion should:

1. inspect population
2. detect document changes
3. process only new / changed files
4. extract sections
5. extract relationships
6. reconcile entities
7. reconcile relationships
8. run validation
9. persist results
10. produce ingestion summary

Do not require manual multi-step developer intervention.


==================================================
15. UNIX COMPATIBILITY
==================================================

The solution is expected to move to a Unix server later.

Therefore:

- avoid Windows-only path assumptions
- use pathlib / platform-independent paths
- avoid hard-coded drive letters
- avoid PowerShell dependency in core processing
- use environment variables for configurable paths
- keep database/files portable

Do not redesign deployment now.
Just ensure the implementation is Unix-compatible.


==================================================
16. BASELINE REGRESSION
==================================================

The existing trusted baseline remains:

LENDING_INTERNAL_BASELINE_V1

Use it as a regression check.

Do NOT continually regenerate it.

After implementing the new ingestion architecture:

run the current corpus through the new pipeline once.

Compare:

existing validated baseline
vs
new persistent database output

Differences must be reported.

Do NOT automatically replace the frozen baseline.

==================================================
17. NO LOOPS
==================================================

This is critical.

Do NOT repeatedly:

- rebuild the same dataset
- re-run the same diagnostics
- revalidate unchanged files
- refactor after acceptance tests pass
- produce repeated reports

Proceed through the full scope once.

If a test fails:

fix the specific cause
rerun only the necessary test
continue

When all acceptance tests pass:

STOP.

No additional enhancements.
No speculative cleanup.
No "while I am here" refactoring.


==================================================
18. DO NOT WORK ON THESE YET
==================================================

Do NOT add:

- R2D2
- web search
- SEC
- AI Assist
- OSUC visual mapping
- advanced network centrality
- fancy map UI
- dashboard redesign
- scenario analysis
- risk scoring
- contagion modeling

Those are later phases.

==================================================
ACCEPTANCE TESTS
==================================================

TEST 1 — POPULATION CONTROL

System produces a target Lending population table with:

CAGID
client name
CAM availability
latest CAM date
document type
stale/current status

PASS / FAIL


TEST 2 — LATEST DOCUMENT LOGIC

For clients with multiple documents:

latest relevant document identified correctly
older versions preserved

PASS / FAIL


TEST 3 — SECTION EXTRACTION

At least 5 representative documents show:

identified business sections
section-specific evidence
page/location provenance

PASS / FAIL


TEST 4 — INDIRECT EXPOSURE

System can extract and represent at least real repository-supported indirect exposure examples if present.

If none are present:

prove none exist.

Do not fabricate.

PASS / FAIL


TEST 5 — INCREMENTAL INGESTION

Run ingestion twice.

First run:
process current files

Second run:
unchanged files skipped

Then modify/add one controlled test document/file metadata case and confirm:

only changed/new item reprocessed

PASS / FAIL


TEST 6 — DATABASE PERSISTENCE

Verify persistent database contains:

entities
documents
relationships
evidence
population
reviews
ingestion runs

PASS / FAIL


TEST 7 — DOCUMENT VERSIONING

Verify multiple document versions for same client remain distinguishable.

PASS / FAIL


TEST 8 — RELATIONSHIP RECONCILIATION

Multiple documents supporting the same relationship attach evidence to one canonical relationship.

PASS / FAIL


TEST 9 — CHANGE DETECTION

For a versioned document pair, verify:

new
unchanged
changed
no-longer-mentioned

logic works without falsely marking termination.

PASS / FAIL


TEST 10 — REVIEW GOVERNANCE

New uncertain relationships go to REVIEW_REQUIRED and do not enter trusted canonical view automatically.

PASS / FAIL


TEST 11 — BASELINE REGRESSION

Compare new persistent output with:

LENDING_INTERNAL_BASELINE_V1

Report differences.

Do NOT overwrite baseline.

PASS / FAIL


TEST 12 — UNIX COMPATIBILITY

Verify no core ingestion logic depends on:

Windows drive letters
PowerShell
Windows-only path assumptions

PASS / FAIL


==================================================
FINAL RESPONSE FORMAT
==================================================

When complete provide ONLY:

1. Actual target Lending population count
2. Current CAM available count
3. Stale CAM count
4. Missing CAM count
5. Documents processed
6. New/changed/unchanged document counts
7. Persistent database type/path
8. Entity count
9. Canonical relationship count
10. Review-required count
11. Real indirect-exposure examples found
12. Baseline regression differences
13. Files materially changed
14. TEST 1–12 PASS / FAIL
15. Genuine external blockers

No long architecture essay.

STOP immediately after acceptance criteria are satisfied.


==================================================
CORE OBJECTIVE
==================================================

Turn the current validated Lending POC into a maintainable Lending relationship data solution that knows the target population, tracks CAM availability and freshness, incrementally ingests new credit documents, extracts section-grounded credit relationships and indirect exposures, preserves exact evidence and document versions, reconciles everything into a persistent canonical database, and updates safely without repeatedly rebuilding the same corpus.
