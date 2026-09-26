CCR V1 — STAGE 5
CORRELATION QUERY API + CLIENT CORRELATION READ MODEL

IMPLEMENTATION TASK

This is an implementation stage.

Implement the Stage 5 read/query layer on top of the approved CCR V1 Stage 4.1 baseline.

Do NOT perform new external research.
Do NOT call SEC, GLEIF, Web, Stylus, or any external provider.
Do NOT perform frontier expansion.
Do NOT create synthetic relationships.
Do NOT create fuzzy identity matches.
Do NOT modify the Client Universe.
Do NOT modify the authoritative source parquet.
Do NOT build the frontend.
Do NOT build AI Create Correlation.
Do NOT implement correlation-definition authoring yet.
Do NOT start broad enrichment.
Do NOT introduce recursive graph traversal.
Do NOT migrate to PostgreSQL.
Do NOT introduce a graph database.

This stage is a READ MODEL + API stage.

==================================================
1. APPROVED BASELINE
==================================================

Use the completed Stage 4.1 implementation as the authoritative baseline.

Relevant report:

backend/data/
CCR_V1_STAGE_4_1_FINAL_CONTRACT_PATCH_REPORT.md

Approved database:

backend/data/relationship_ingestion.sqlite3

Current relationship schema version:

11

Client Universe:

3,670,650 rows
3,670,650 unique GFCIDs

The Client Universe must remain unchanged.

Stage 4.1 has already established:

- VERIFIED + EXACT identity endpoint gate
- ACCEPTED relationship-version gate
- mandatory evidence lineage
- symmetric explicitly named client resolution
- discovered-entity ambiguity handling
- separate Direct Relationship View
- separate Derived Correlation Evaluator
- six approved derived definitions
- two allowed pattern kinds:
    SHARED_INTERMEDIATE
    DIRECTED_CHAIN
- maximum derived depth:
    2 relationship hops
- query-time-only derived results
- no DIRECT correlation definition
- no persisted derived-result table
- execution-status vs enrichment-coverage distinction
- truth vs hub/default-visibility separation

Preserve those contracts exactly.

==================================================
2. STAGE 5 OBJECTIVE
==================================================

Create a clean read model and public FastAPI query surface so a consumer can select a Client Record and retrieve:

1. factual direct relationships;
2. derived Client correlations;
3. pairwise Client-to-Client results;
4. the structural explanation/path;
5. endpoint identity lineage;
6. relationship evidence lineage;
7. qualifiers;
8. temporal state;
9. query execution status;
10. research/enrichment coverage;
11. visibility / hub suppression metadata;
12. correlation-definition metadata.

This is the first product-facing backend read layer.

The output must be designed so the frontend can later render:

CLIENT
  |
  +-- DIRECT RELATIONSHIPS
  |
  +-- DERIVED CORRELATIONS
  |
  +-- WHY / PATH / EVIDENCE
  |
  +-- COVERAGE

without confusing a factual relationship with a derived correlation.

==================================================
3. CRITICAL SEMANTIC RULE
==================================================

There are TWO distinct result families.

A. DIRECT RELATIONSHIP

A factual projection of an accepted Legal Entity relationship to Client Record grain.

Example:

3M
  --owns 75%-->
3M India

This is NOT a correlation definition.

B. DERIVED CORRELATION

A governed structural result computed from multiple accepted factual relationship hops.

Example:

Client A
  <- supplied by -
Supplier X
  - supplies ->
Client B

Result:

SHARED_SUPPLIER

Do not combine these into one generic result object.

Do not introduce a generic DIRECT correlation.

==================================================
4. PUBLIC STATUS CONTRACT
==================================================

Stage 5 MUST eliminate ambiguity in public API terminology.

Expose:

execution_status

with only:

COMPLETE
PARTIAL
FAILED

Semantics:

COMPLETE =
the bounded evaluator finished over all currently eligible facts available to the query.

PARTIAL =
the intended bounded evaluator could not fully evaluate the requested query.

FAILED =
the evaluator did not produce a reliable result.

CRITICAL:

COMPLETE MUST NEVER mean:

"the real world was comprehensively researched."

==================================================
5. RESEARCH / ENRICHMENT COVERAGE CONTRACT
==================================================

Expose research/enrichment coverage separately.

Use the existing governed coverage model:

NOT_ELIGIBLE
NOT_RESEARCHED
RESEARCHED_FOUND
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE

Freshness:

CURRENT
STALE

Do not expose the old convenience field:

coverage_state = COMPLETE

as if it were authoritative research coverage.

If legacy/internal convenience fields are needed for compatibility, they may remain internally, but the new Stage 5 API must expose a clearly named structure such as:

research_coverage

or:

enrichment_coverage

Example:

{
  "execution_status": "COMPLETE",
  "research_coverage": {
      "outcome": "PARTIAL",
      "freshness": "STALE",
      "as_of_date": "...",
      "relationship_family": "...",
      "scope_key": "...",
      "source_set": [...]
  }
}

There may be multiple coverage records for one result/query.

Do not collapse them into a fake single complete/not-complete flag when multiple families/scopes are relevant.

==================================================
6. ZERO-RESULT CONTRACT
==================================================

For any zero-result query, expose a structured flag:

zero_is_not_universal_negative = true

or equivalent explicit contract field.

The API/read model must support wording equivalent to:

"No qualifying correlation was found in the currently available eligible graph."

It must NOT imply:

"No correlation exists."

If:

execution_status = COMPLETE

and research coverage is:

PARTIAL
NOT_RESEARCHED
or UNAVAILABLE

the result is still not evidence of universal non-existence.

Test this explicitly.

==================================================
7. DIRECT RELATIONSHIP READ MODEL
==================================================

Create an explicit Direct Relationship result contract.

Suggested conceptual fields:

result_family:
DIRECT_RELATIONSHIP

query_source_client
query_target_client if pairwise

canonical_relationship_id
relationship_version_id

relationship_type

canonical_direction

query_relative_direction

acceptance_state

effective_from
effective_to
observed_at
last_verified_at
date precision where available

source_legal_entity
target_legal_entity

source_identity_link
target_identity_link

qualifiers[]

evidence[]

execution_status

research_coverage[]

coverage_warnings[]

visibility metadata if applicable

as_of_date

The actual names may follow repository conventions, but preserve these semantics.

==================================================
8. QUERY-RELATIVE DIRECTION
==================================================

The reverse query behavior validated in Stage 4.1 must remain explicit.

Example:

3M -> 3M India

returns canonical factual relationship:

3M owns 3M India

with query-relative direction:

A_TO_B

Query:

3M India -> 3M

must return the SAME canonical relationship.

Do NOT fabricate:

3M India owns 3M.

Instead report the original canonical fact relative to the reverse query, such as:

B_TO_A

The read model should make both:

canonical direction

and

query-relative direction

clear enough that a future UI cannot accidentally invert the fact.

==================================================
9. DERIVED CORRELATION READ MODEL
==================================================

Create a separate Derived Correlation result contract.

Suggested conceptual fields:

result_family:
DERIVED_CORRELATION

definition_id
definition_code
definition_version
definition_category
pattern_kind

source_client
target_client

source_legal_entity
target_legal_entity

intermediate_entity / entities

path_hops[]

Each hop should expose:

relationship_id
relationship_version_id
relationship_type
canonical direction
path-relative direction
qualifiers
identity lineage
evidence lineage
temporal fields

Also expose:

execution_status
research_coverage[]
coverage_warnings[]
visibility_state
suppression_reason
as_of_date

The correlation result itself must NOT become a stored relationship.

Do not persist derived result rows.

==================================================
10. EXPLANATION / PATH CONTRACT
==================================================

Every positive derived result must be explainable without recomputing an opaque graph traversal.

Return a deterministic bounded explanation.

Example:

{
  "definition_code": "SHARED_SUPPLIER",
  "source_client": ...,
  "target_client": ...,
  "intermediate_entity": ...,
  "path": [
      {
        "relationship_type": "supplies",
        ...
      },
      {
        "relationship_type": "supplies",
        ...
      }
  ]
}

The path must reference the exact accepted relationship versions used.

Do not return a synthetic summary edge in place of the underlying path.

==================================================
11. EVIDENCE LINEAGE CONTRACT
==================================================

For Direct Relationship results and for every derived path hop, return enough evidence metadata for a later UI to drill down.

At minimum include available:

claim_id
relationship_support_id
document_id
passage_id
source class
source reference
title
publication date
excerpt/reference
evidence basis
admissibility
retention/replay capability
content/source hashes where available

Do not invent missing body text, offsets, hashes, dates, or source metadata.

Historical evidence may legitimately be LEGACY_REFERENCE / PASSAGE_REPLAY.

Expose what exists.

Do not silently upgrade historical evidence to FULL_REPLAY.

==================================================
12. IDENTITY LINEAGE CONTRACT
==================================================

For every Client endpoint in a returned Direct Relationship or Derived Correlation result expose:

client_id
GFCID where permitted by existing contract
legal entity ID
identity_link_id
link_type
link_state
identity evidence/support references

Hard eligibility remains:

link_state = VERIFIED

AND

link_type = EXACT

Do not allow PROBABLE.

Do not allow ASSOCIATED while the global associated-link acceptance policy remains disabled.

==================================================
13. EXPLICIT CLIENT VS DISCOVERED ENTITY MODE
==================================================

Preserve Stage 4.1 distinction.

For an explicitly named Client Record:

client_id
  -> persisted CCR V1 VERIFIED + EXACT identity link
  -> Legal Entity

This rule is symmetric for source and target.

For a Legal Entity encountered through broad discovery:

Legal Entity
  -> provider identifier / approved identity information
  -> deterministic Client Universe match-back
  -> ambiguity checks

Ambiguous discovered entities must not be auto-attached to a Client Record.

Expose enough metadata for consumers to understand the resolution mode.

Suggested field:

endpoint_resolution_mode:

NAMED_CLIENT_PERSISTED_LINK
DISCOVERED_ENTITY_MATCHBACK

Do not make source/target role itself alter identity eligibility.

==================================================
14. VISIBILITY / HUB CONTRACT
==================================================

Truth and default display suppression must remain separate.

A structurally valid correlation may have:

is_match = true

visibility_state = SUPPRESSED_HUB

suppression_reason = ...

Do not delete the result because of hub/noise policy.

Stage 5 API must expose the structural truth and visibility state separately.

==================================================
15. CORRELATION DEFINITION CATALOG API
==================================================

Expose the six approved read-only derived definitions.

Expected definitions:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN
SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY

Expected normalized categories:

SHARED_CONTROLLER
    GROUP_STRUCTURE

SHARED_SUPPLIER
    COMMERCIAL_DEPENDENCY

SHARED_CUSTOMER
    COMMERCIAL_DEPENDENCY

SUPPLY_CHAIN
    COMMERCIAL_DEPENDENCY

SHARED_LENDER
    FINANCING

SHARED_PRODUCT_DEPENDENCY
    PRODUCT_DEPENDENCY

Expose useful metadata such as:

definition_id
code
version
category
pattern_kind
description if already governed
hop contract
qualifier predicates
visibility/hub metadata
as-of behavior

Do not expose arbitrary executable predicates.

Do not add mutation endpoints.

Do not add Create/Update/Delete definition APIs yet.

Do not add AI Create Correlation yet.

==================================================
16. SUGGESTED API SURFACES
==================================================

Implement a coherent bounded API surface.

Exact route naming may follow the current FastAPI conventions, but it should cover at least:

GET /api/ccr/correlation-definitions

GET /api/ccr/clients/{client_id}/summary

GET /api/ccr/clients/{client_id}/relationships

GET /api/ccr/clients/{client_id}/correlations

GET /api/ccr/clients/{source_client_id}/relationships/{target_client_id}

GET /api/ccr/clients/{source_client_id}/correlations/{target_client_id}

If a better REST shape fits the current repository conventions, use it, but preserve these six capabilities.

Do not break existing Client Universe APIs.

==================================================
17. CLIENT CORRELATION SUMMARY
==================================================

The selected-client summary should be designed as the future workspace bootstrap call.

Return bounded summary information such as:

Client Record identity/context

resolved Legal Entity identity

direct relationship count

derived correlation count

counts by correlation definition

coverage summary

warnings

as_of_date

available correlation definitions

Do NOT trigger research in order to populate the summary.

Counts must reflect only currently available eligible CCR facts.

==================================================
18. PAGINATION AND BOUNDS
==================================================

All list endpoints must be bounded.

Use deterministic ordering.

Suggested:

default limit: 25
maximum limit: 100

Use a stable continuation/cursor approach where practical.

Do not introduce unbounded graph queries.

Do not return the entire 3.67M Client Universe.

==================================================
19. AS-OF DATE
==================================================

The API must accept an as-of date where the underlying Stage 4 contracts support it.

Temporal filtering must preserve:

effective_from
effective_to
observed dates
acceptance state

Do not reinterpret `observed_to` as relationship termination.

Do not fabricate effective dates.

==================================================
20. REAL-DATA ACCEPTANCE TESTS
==================================================

Use the existing real local 3M data.

At minimum test:

A. 3M -> 3M India direct query

Expected:

FOUND

relationship:
owns

ownership:
75%

identity:
VERIFIED + EXACT for both endpoints

factual result family:
DIRECT_RELATIONSHIP

B. 3M India -> 3M direct query

Expected:

same canonical relationship

no fabricated inverse ownership

query-relative direction should reflect reversal.

C. explicit 3M -> Solventum direct query

Stage 4.1 now establishes qualifying persisted EXACT links.

Expected current factual relationships include:

owns

supplies

Do not re-run provider resolution for the named Solventum Client endpoint.

D. broad 3M direct relationship list

Expected:

existing valid results retained

ambiguous discovered Client match-backs remain warnings

broad discovery coverage remains distinguishable from explicit pairwise behavior.

E. six derived 3M / 3M India definitions

Expected current real derived result count:

0

The API must return this without asserting universal non-existence.

F. definition catalog

Expected:

6 definitions

0 DIRECT definitions.

==================================================
21. FIXTURE DERIVED TESTS
==================================================

Retain and extend existing isolated Stage 4 fixtures.

Stage 5 API serialization tests must include at least:

positive SHARED_INTERMEDIATE result

positive DIRECTED_CHAIN result

wrong direction rejected

wrong hop type rejected

identity blocked endpoint

PROBABLE identity rejected

ASSOCIATED identity rejected while global policy disabled

non-ACCEPTED relationship rejected

missing mandatory evidence rejected

effective-date filtering

SUPPRESSED_HUB positive result retained

zero-result + partial coverage semantics

query-time result not persisted

==================================================
22. READ-ONLY GUARANTEE
==================================================

Normal Stage 5 GET requests must not write:

Client Universe rows

source master rows

relationships

relationship versions

identity links

claims

qualifiers

coverage rows

events

correlation result rows

provider attempts

research runs

No network request should occur.

Add tests where practical confirming query paths are read-only.

==================================================
23. SCHEMA POLICY
==================================================

Prefer NO schema migration for Stage 5.

This should principally be:

domain contracts
repository/read-model methods
service layer
FastAPI routes
serialization
tests
report

If a schema migration is genuinely unavoidable, stop and explain why before implementing it.

Do not add a derived-result persistence table.

==================================================
24. EXISTING APIS
==================================================

Preserve existing Client Universe and historical relationship APIs unless a compatibility fix is essential.

Do not repurpose old Stage 2 routes to silently mean CCR V1 Stage 5.

Create explicit CCR V1 query surfaces.

Avoid ambiguous old terminology.

==================================================
25. FRONTEND BOUNDARY
==================================================

Do not modify frontend files.

However, design the Stage 5 responses so a later UI can directly render:

Client header

Direct Relationships

Derived Correlations

Correlation reason/path

Evidence panel

Coverage state

Warnings

No-results-with-partial-coverage message

without performing graph logic in the browser.

==================================================
26. FUTURE CORRELATION CONFIGURATION
==================================================

Do not implement configuration editing now.

However, Stage 5 must preserve the architecture needed later for:

Correlation Configuration

and:

AI Create Correlation

That future capability will author/version governed definition contracts.

Therefore:

- keep definition IDs/versioning stable;
- keep category separate from executable semantics;
- do not hard-code UI labels throughout service logic;
- make the read-only definition catalog reusable by the future configuration UI;
- do not allow future definition metadata to override platform hard gates.

==================================================
27. VALIDATION
==================================================

Run:

focused Stage 5 tests

full backend suite

Python compile/static checks

SQLite foreign-key check

SQLite quick_check

Verify:

schema remains v11

Client Universe row count remains 3,670,650

unique GFCIDs remain 3,670,650

source master unchanged

historical Stage 2 data unchanged

CCR V1 Stage 1-4.1 data unchanged

provider calls = 0

new research = 0

fuzzy merges = 0

synthetic edges = 0

persisted derived-result rows = 0

frontend files modified = 0

==================================================
28. REQUIRED IMPLEMENTATION REPORT
==================================================

Create:

backend/data/
CCR_V1_STAGE_5_CORRELATION_QUERY_API_REPORT.md

The report must include:

1. Executive status

2. Files changed

3. Routes added

4. Read-model/domain contracts

5. Direct Relationship result contract

6. Derived Correlation result contract

7. Execution-status contract

8. Research/enrichment coverage contract

9. Zero-result semantics

10. Identity-lineage contract

11. Evidence-lineage contract

12. Visibility/hub contract

13. Definition catalog result

14. Real 3M -> 3M India API examples

15. Real reverse 3M India -> 3M example

16. Real explicit 3M -> Solventum example

17. Broad 3M relationship result/coverage behavior

18. Real six-definition derived result counts

19. Fixture-derived positive examples

20. Read-only verification

21. Test results

22. SQLite integrity

23. Client Universe integrity

24. Source-master integrity

25. Known limitations

26. Exact recommended next stage

==================================================
29. STOP BOUNDARY
==================================================

STOP after Stage 5 API/read-model implementation and validation.

Do NOT:

- perform controlled two-hop enrichment;
- start Stage 6 frontend;
- add provider research;
- add correlation authoring;
- add AI Create Correlation;
- broaden the ontology;
- create persisted correlation-result tables.

At completion, report whether Stage 5 is:

PASS
PARTIAL
FAIL

and give the exact route examples needed for us to inspect the first product-facing CCR results.
