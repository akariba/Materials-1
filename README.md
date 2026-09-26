CCR — CLIENT CORRELATION
V1 STAGE 4.1 — FINAL CONTRACT PATCH BEFORE STAGE 5

PURPOSE

Apply the two required senior-review correctness patches to the already-approved CCR V1 Stage 4 implementation before any Stage 5 public query/read API is built.

This is a SMALL PATCH.

Do not redesign Stage 4.
Do not add new correlation patterns.
Do not perform enrichment or research.
Do not call providers.
Do not modify the frontend.
Do not begin Stage 5.
Do not add AI Create Correlation.
Do not add persisted derived-result tables.
Do not modify the Client Universe.
Do not modify historical Stage 2 data.
Do not modify existing factual relationships except where test fixtures are isolated.

The existing Stage 4 foundation remains approved except for the two contract defects described below.

--------------------------------------------------
1. CURRENT APPROVED BASELINE
--------------------------------------------------

Current schema version:
11

Current approved derived definitions:
6

Current approved definition versions:
6

Persisted DIRECT definitions:
0

Direct Relationship View:
implemented

Derived Correlation evaluator:
implemented

Persisted derived-result table:
none

Current real proof:

3M -> 3M India

relationship:
owns

ownership:
75%

Direct Relationship View:
1 factual result

3M -> Solventum:

blocked by identity ambiguity

All six derived real-data queries currently return:
0 results

Stage 4 fixture suite:
passing

Full backend suite:
passing

No provider calls:
confirmed

--------------------------------------------------
2. SENIOR REVIEW DECISION
--------------------------------------------------

Senior review decision:

STAGE 4 APPROVED AFTER PATCH — THEN PROCEED TO STAGE 5

Only two blocking changes are required:

1. identity resolution symmetry for explicitly named client_id endpoints;

2. separation of evaluator execution status from research/enrichment coverage.

Do not introduce unrelated architecture changes.

--------------------------------------------------
3. PATCH 1 — IDENTITY RESOLUTION SYMMETRY
--------------------------------------------------

The current Stage 4 implementation permits an explicitly selected source client to use its persisted identity link even when a provider identifier is shared, but explicitly selected target clients may still be forced through provider-identifier uniqueness resolution.

This is incorrect.

Resolution must depend on:

EXPLICITLY NAMED CLIENT
versus
DISCOVERED ENTITY

not:

SOURCE
versus
TARGET

Freeze this invariant:

Any Client Record explicitly identified in the query by client_id, regardless of whether it is source or target, resolves through that Client Record's own persisted identity link.

Required accepted endpoint identity gate remains:

link_state = VERIFIED
AND
link_type = EXACT

Lookup path:

client_id
    ->
persisted CCR V1 identity link
    ->
Legal Entity

Do NOT re-derive an explicitly named client's identity by raw provider identifier matching.

Do NOT require provider identifier uniqueness when the query caller has already explicitly named a client_id that has an approved VERIFIED+EXACT identity link.

--------------------------------------------------
4. DISCOVERED ENTITY RESOLUTION
--------------------------------------------------

Provider-identifier matching and ambiguity rules remain required only when the evaluator discovers a Legal Entity and must determine whether that entity maps to a Client Record.

Examples:

- two-hop intermediate entity;
- discovered counterparty;
- graph-found endpoint not explicitly supplied by client_id.

For discovered entities:

provider identifier ambiguity may legitimately result in:

IDENTITY_UNRESOLVED

or equivalent governed status.

Do not weaken this rule.

--------------------------------------------------
5. SOURCE/TARGET ROLE MUST NOT CHANGE ELIGIBILITY
--------------------------------------------------

For two explicitly named clients A and B:

query:
A -> B

and query:
B -> A

must resolve the same two Client Record identity links.

Changing which client is syntactically called "source" or "target" must never make an otherwise identical factual relationship or derived correlation become identity-eligible in one direction and identity-blocked in the reverse direction.

Relationship direction itself must still remain factual and canonical.

Example:

A owns B

does not become:

B owns A

But identity eligibility must be role-symmetric.

--------------------------------------------------
6. DIRECT RELATIONSHIP VIEW PATCH
--------------------------------------------------

Apply the same named-client identity invariant to Direct Relationship View.

For pairwise direct query:

client_id_a
client_id_b

if both clients have:

VERIFIED + EXACT

persisted identity links,

use those links directly.

Do not rerun provider-id uniqueness resolution for either named endpoint.

For broad discovery queries from one client:

the selected client uses its persisted identity link;

discovered target Legal Entities still require governed entity-to-client match-back.

This distinction is expected and correct.

--------------------------------------------------
7. SOLVENTUM CONSEQUENCE
--------------------------------------------------

Re-test the current 3M / Solventum case carefully.

Important:

If the Solventum client_id supplied in the explicit pairwise query already has its own persisted VERIFIED+EXACT identity link, the pairwise identity gate must use that link and must NOT be blocked merely because other Client Universe records share the same provider identifier.

If Solventum does NOT have a persisted qualifying VERIFIED+EXACT identity link for that explicit client_id, it remains blocked.

Do not assume the result.

Read the current persisted CCR V1 identity links and report the actual state.

The broad discovery behavior may still differ:

3M broad direct discovery
    ->
Solventum Legal Entity discovered
    ->
ambiguous client match-back

may legitimately surface:

IDENTITY_UNRESOLVED / PARTIAL coverage

if the evaluator does not already know a specific client_id.

That is not the same operation as an explicit pairwise query.

Document the difference.

--------------------------------------------------
8. IDENTITY TESTS
--------------------------------------------------

Add regression tests proving:

1. explicitly named source client resolves through its persisted VERIFIED+EXACT identity link.

2. explicitly named target client resolves through its persisted VERIFIED+EXACT identity link.

3. raw provider-identifier ambiguity does not invalidate either explicitly named client when both already have approved identity links.

4. A-to-B and B-to-A pairwise queries resolve identical endpoint identity links.

5. factual relationship direction remains canonical despite symmetric identity resolution.

6. discovered entity match-back still applies provider identifier ambiguity rules.

7. discovered ambiguous entity is not auto-attached to a Client Record.

8. PROBABLE identity still fails accepted-correlation eligibility.

9. ASSOCIATED remains ineligible while global ASSOCIATED acceptance is OFF.

10. no fuzzy identity merge introduced.

--------------------------------------------------
9. PATCH 2 — EXECUTION STATUS VS COVERAGE
--------------------------------------------------

Separate:

EVALUATOR EXECUTION COMPLETENESS

from:

RESEARCH / ENRICHMENT COVERAGE

These must be distinct in domain objects and Stage 4 evaluator results before Stage 5 public API work begins.

--------------------------------------------------
10. EXECUTION STATUS
--------------------------------------------------

Introduce or normalize:

execution_status

Allowed values:

COMPLETE
PARTIAL
FAILED

Semantics:

COMPLETE

The evaluator finished processing all currently eligible graph facts within the bounded query.

It does NOT mean:

- external research was comprehensive;
- the real world was exhaustively checked;
- no undiscovered relationship exists;
- enrichment coverage is complete.

PARTIAL

The evaluator itself could not complete its intended bounded evaluation.

Examples may include:

internal evaluation interruption
missing required local inputs
bounded execution failure affecting result completeness

Do not misuse PARTIAL merely because enrichment coverage is partial.

FAILED

The evaluator failed to produce a reliable execution result.

--------------------------------------------------
11. COVERAGE OBJECT
--------------------------------------------------

Coverage must remain a separate structured object.

Do not flatten all coverage into execution_status.

Coverage should be represented at appropriate granularity by:

endpoint
relationship family / research family
scope
as_of_date
policy_version

using existing governed coverage outcomes:

NOT_ELIGIBLE
NOT_RESEARCHED
RESEARCHED_FOUND
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE

Freshness remains separate:

CURRENT
STALE

Do not invent additional coverage truth states unless already required by the existing domain contract.

--------------------------------------------------
12. COVERAGE SUMMARY
--------------------------------------------------

Optionally expose a deterministic convenience field:

coverage_summary

Allowed presentation-oriented values may be:

COMPREHENSIVE
PARTIAL
MINIMAL
UNKNOWN

But only if this is implemented as a derived convenience summary.

It must never replace detailed coverage records.

If the existing code does not need this field yet, do not force it into persistence.

Stage 5 can derive it in the read model.

--------------------------------------------------
13. ZERO RESULT SEMANTICS
--------------------------------------------------

For:

execution_status = COMPLETE

and coverage including PARTIAL / NOT_RESEARCHED / UNAVAILABLE

a zero result means only:

the evaluator found zero qualifying matches in the currently available graph.

It must NOT mean:

no such real-world correlation exists.

Preserve this exact conceptual distinction.

Required report wording example:

"0 [pattern] correlations found under [definition] against the currently available relationship graph (execution: COMPLETE). [Family] coverage is PARTIAL for [client]. This does not confirm no such relationship exists — it reflects current enrichment coverage as of [date]."

Do not hardcode user-facing prose into low-level evaluator logic unless already part of the architecture.

Prefer returning structured fields from which Stage 5 can build this wording.

--------------------------------------------------
14. POSITIVE RESULT SEMANTICS
--------------------------------------------------

A valid positive correlation remains valid even if broader enrichment coverage is PARTIAL.

Example:

A qualifying SHARED_SUPPLIER result was found.

That structural result remains true under current evidence.

Partial research coverage only means:

there may be additional suppliers/correlations not yet found.

Coverage does not invalidate an already proven positive result.

--------------------------------------------------
15. REAL 3M DERIVED QUERY PATCH
--------------------------------------------------

Rerun the six real derived definitions after the patch.

Their evaluator execution may legitimately report:

execution_status = COMPLETE

with:

results = 0

But attach or expose the real coverage metadata separately.

Do not describe the zero results as proof that no real correlation exists.

Definitions:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN
SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY

--------------------------------------------------
16. CATEGORY NORMALIZATION — SMALL NON-BLOCKING CLEANUP
--------------------------------------------------

While touching the Stage 4 contract, normalize the six seeded definition categories to the senior-reviewed stable labels.

Category is:

UI grouping metadata
+
governance metadata

It is NOT evaluator semantics.

Changing only the category must never change matching behavior.

Use:

SHARED_CONTROLLER
category = GROUP_STRUCTURE

SHARED_SUPPLIER
category = COMMERCIAL_DEPENDENCY

SHARED_CUSTOMER
category = COMMERCIAL_DEPENDENCY

SUPPLY_CHAIN
category = COMMERCIAL_DEPENDENCY

SHARED_LENDER
category = FINANCING

SHARED_PRODUCT_DEPENDENCY
category = PRODUCT_DEPENDENCY

Do not add additional categories.

Do not make category part of correlation truth.

If definition immutability means changing the existing active version would violate the current version contract, perform the smallest correct versioned/configuration migration necessary and document it.

Do not silently mutate immutable executable semantics.

Because category is non-executable metadata, explicitly document whether it belongs to definition metadata or versioned configuration in the current implementation.

--------------------------------------------------
17. HARD GATES REMAIN UNCHANGED
--------------------------------------------------

Do NOT change:

accepted endpoint identity:
VERIFIED + EXACT

ASSOCIATED global acceptance:
OFF

eligible relationship version state:
ACCEPTED only

mandatory evidence lineage:
required

maximum derived depth:
2

pattern kinds:
SHARED_INTERMEDIATE
DIRECTED_CHAIN

persisted derived result rows:
none

--------------------------------------------------
18. DIRECT VS DERIVED REMAIN DISTINCT
--------------------------------------------------

Preserve separate domain result families for:

Direct Relationship View

and

Derived Correlation Result

Do not merge them into one generic "correlation result" object.

Stage 5 will expose separate API response types.

--------------------------------------------------
19. HUB / VISIBILITY REMAINS UNCHANGED
--------------------------------------------------

Preserve:

correlation truth

separately from:

default suppression / visibility metadata.

A hub-suppressed result remains a true match.

Do not filter it out at the evaluator level when the caller requests hidden/suppressed results.

--------------------------------------------------
20. NO STAGE 5 WORK
--------------------------------------------------

Do not add:

public Stage 5 APIs
new FastAPI routes
frontend
network UI
AI Create Correlation
new enrichment workflows
provider orchestration
real two-hop research

This patch must leave Stage 5 as a clean next stage.

--------------------------------------------------
21. MIGRATION / SCHEMA GUIDANCE
--------------------------------------------------

First inspect whether these two patches require a schema migration.

Prefer no schema migration if:

- the identity fix is evaluator/service logic only;
- execution_status and structured coverage already fit existing in-memory/domain contracts;
- category normalization can be handled without violating persistence contracts.

If a schema migration is genuinely necessary, justify it clearly.

Do NOT increment schema version merely for convenience.

Current schema:
v11

Expected schema after patch:
prefer v11

If schema changes are necessary:
use the next version and make it additive/replay-safe.

--------------------------------------------------
22. REQUIRED TESTS — STATUS/COVERAGE
--------------------------------------------------

Add tests proving:

11. execution_status=COMPLETE means evaluator completion only.

12. execution_status is independent from coverage state.

13. COMPLETE + PARTIAL coverage is valid.

14. COMPLETE + NOT_RESEARCHED coverage is valid where applicable.

15. COMPLETE + UNAVAILABLE coverage is valid where applicable.

16. zero results + partial coverage does not produce a universal non-existence assertion in structured result semantics.

17. positive correlation + partial broader coverage remains a valid positive result.

18. coverage remains endpoint/family scoped rather than one global truth value.

19. coverage as-of metadata preserved.

20. coverage policy version preserved where available.

--------------------------------------------------
23. REQUIRED TESTS — CATEGORY
--------------------------------------------------

21. SHARED_CONTROLLER category = GROUP_STRUCTURE.

22. SHARED_SUPPLIER category = COMMERCIAL_DEPENDENCY.

23. SHARED_CUSTOMER category = COMMERCIAL_DEPENDENCY.

24. SUPPLY_CHAIN category = COMMERCIAL_DEPENDENCY.

25. SHARED_LENDER category = FINANCING.

26. SHARED_PRODUCT_DEPENDENCY category = PRODUCT_DEPENDENCY.

27. category changes do not alter evaluator matching semantics.

--------------------------------------------------
24. REQUIRED REGRESSION TESTS
--------------------------------------------------

Confirm all existing Stage 4 tests still pass for:

DIRECT absent from derived catalog

exactly six derived definitions

exactly two derived pattern shapes

depth <= 2

ACCEPTED-only relationship hops

VERIFIED+EXACT identity gates

mandatory evidence lineage

qualifier predicates

temporal filtering

hub suppression metadata

query-time-only derived results

no persisted correlation results

no synthetic client edges

no fuzzy merges

--------------------------------------------------
25. REAL-DATA REGRESSION
--------------------------------------------------

Re-run current real checks.

Report separately:

A. explicit pairwise Direct Relationship View:

3M -> 3M India

B. reverse explicit pairwise query:

3M India -> 3M

Identity resolution should be symmetric.

The factual relationship direction must remain:

3M owns 3M India

Do not fabricate inverse ownership.

C. explicit pairwise 3M -> Solventum

Read actual current persisted identity-link state before deciding outcome.

D. broad 3M discovery query

Report discovered-entity identity ambiguity separately.

E. all six derived definitions

Report:

execution_status
result_count
coverage metadata

separately.

--------------------------------------------------
26. INTEGRITY
--------------------------------------------------

Verify:

Client Universe rows:
3,670,650

Client Universe modifications:
0

source-master modifications:
0

historical Stage 2 modifications:
0

CCR V1 factual relationship modifications:
0 unless category metadata/config migration explicitly requires no fact changes

external provider calls:
0

new research:
0

frontend modifications:
0

synthetic direct edges:
0

fuzzy merges:
0

persisted derived result rows:
0

--------------------------------------------------
27. CREATE PATCH REPORT
--------------------------------------------------

Create:

backend/data/CCR_V1_STAGE_4_1_FINAL_CONTRACT_PATCH_REPORT.md

Required sections:

1. Executive result
2. Senior review decision
3. Identity asymmetry defect
4. Correct named-client identity invariant
5. Discovered-entity resolution invariant
6. Direct Relationship View pairwise behavior
7. Broad discovery behavior
8. Execution status contract
9. Coverage contract
10. Zero-result semantics
11. Positive-result semantics
12. Catalog category normalization
13. Hard-gate regression
14. Direct vs derived regression
15. Hub/visibility regression
16. Real 3M pairwise validation
17. Reverse-direction identity validation
18. Solventum validation
19. Broad 3M discovery validation
20. Real six-definition derived results
21. Focused tests
22. Full backend tests
23. SQLite integrity
24. Client Universe integrity
25. Source-master integrity
26. External-call verification
27. Stage 5 readiness

--------------------------------------------------
28. FINAL OUTPUT FORMAT
--------------------------------------------------

At completion output exactly:

CCR V1 — STAGE 4.1 FINAL CONTRACT PATCH

Status:
PASS / PARTIAL / FAIL

Schema before:
11

Schema after:

Identity symmetry patch:
PASS / FAIL

Named source client uses persisted VERIFIED+EXACT link:
YES / NO

Named target client uses persisted VERIFIED+EXACT link:
YES / NO

Named endpoint resolution depends on source/target role:
YES / NO

Discovered entity provider-ambiguity checks retained:
YES / NO

Reverse pairwise identity resolution:
PASS / FAIL

3M -> 3M India explicit pairwise result:
FOUND / NOT_FOUND

3M India -> 3M explicit pairwise identity resolution:
PASS / FAIL

Canonical factual relationship direction preserved:
YES / NO

3M -> Solventum explicit pairwise result:
FOUND / BLOCKED_BY_IDENTITY / NOT_FOUND

Solventum qualifying persisted identity link:
YES / NO

Broad 3M discovery coverage:
status:

Execution/Coverage split:
PASS / FAIL

execution_status field:
SUPPORTED / NOT_SUPPORTED

coverage structured separately:
YES / NO

COMPLETE may coexist with PARTIAL coverage:
YES / NO

COMPLETE means comprehensive real-world research:
NO

Zero-result partial-coverage semantics:
PASS / FAIL

Categories:

SHARED_CONTROLLER:
GROUP_STRUCTURE

SHARED_SUPPLIER:
COMMERCIAL_DEPENDENCY

SHARED_CUSTOMER:
COMMERCIAL_DEPENDENCY

SUPPLY_CHAIN:
COMMERCIAL_DEPENDENCY

SHARED_LENDER:
FINANCING

SHARED_PRODUCT_DEPENDENCY:
PRODUCT_DEPENDENCY

Category affects matching semantics:
NO

Hard endpoint identity gate:
VERIFIED + EXACT

Eligible relationship state:
ACCEPTED ONLY

Mandatory evidence lineage:
YES

Persisted DIRECT correlation definitions:
0

Derived definitions:
6

Derived pattern kinds:
2

Persisted derived result rows:
0

Synthetic direct edges:
0

Fuzzy merges:
0

External provider calls:
0

New research:
0

Client Universe rows:
3,670,650

Client Universe modifications:
0

Source-master modifications:
0

Historical Stage 2 modifications:
0

Frontend modifications:
0

Focused Stage 4.1 tests:
passed / failed / skipped

Full backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Stage 5 readiness:
READY / NOT_READY

Report:
backend/data/CCR_V1_STAGE_4_1_FINAL_CONTRACT_PATCH_REPORT.md

Recommended next action:

If all blocking patches pass:

CCR V1 — STAGE 5
CORRELATION QUERY API + CLIENT CORRELATION READ MODEL

Do not start Stage 5 automatically.
