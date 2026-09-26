IMPLEMENT WITH LUNA

CCR — CLIENT CORRELATION
V1 STAGE 4 — SENIOR-REVIEW RECONCILIATION +
DERIVED CORRELATION FOUNDATION

RESUME FROM THE CURRENT STOPPED STAGE 4 CHECKPOINT.

This prompt supersedes the previous Stage 4 implementation instructions where they conflict.

Do NOT restart the project.
Do NOT revert completed CCR V1 Foundation work.
Do NOT revert Stage 1 / Stage 1.1.
Do NOT revert the 3M controlled revalidation.
Do NOT revert the Identity Resolution Pilot.
Do NOT modify historical Stage 2 data.
Do NOT modify the Client Universe.
Do NOT perform research.
Do NOT call external providers.
Do NOT modify the frontend.

The purpose of this task is:

1. cleanly remove/reconcile the unfinished Stage 4 implementation that was stopped before approval;

2. implement the corrected senior-reviewed correlation architecture;

3. create the first real CCR Direct Relationship View;

4. implement the bounded Derived Correlation Definition model;

5. implement the constrained pattern evaluator;

6. prove direct client-grain relationship projection using real 3M / 3M India data;

7. prove derived-pattern engine mechanics only with isolated test fixtures.

--------------------------------------------------
0. CURRENT STOPPED CHECKPOINT
--------------------------------------------------

Verified current checkpoint:

Execution status:
RUNNING_STOPPED

Schema before Stage 4:
10

Schema currently:
10

Stage 4 migration ledger entry:
NONE

Partial new tables already created:

ccr_correlation_definitions
ccr_correlation_definition_versions

Correlation definitions already persisted:
7

Correlation definition versions already persisted:
7

DIRECT persisted as a correlation definition:
YES

Endpoint identity policy stored as configurable definition field:
YES

Relationship acceptance policy stored as configurable definition field:
YES

Evidence drill-down stored as configurable definition field:
YES

Pattern kinds already started:

DIRECT
SHARED_INTERMEDIATE
DIRECTED_CHAIN

Depth bounded to:
2

Stage 4 tests added:
NONE

Existing CCR V1 relationships modified:
NO

Client Universe modified:
NO

Historical Stage 2 rows modified:
NO

External provider calls:
0

Frontend modifications:
0

The stopped Stage 4 implementation is NOT an approved baseline.

Its partial Stage 4 tables and data may be safely replaced only after verifying that no approved pre-Stage-4 object depends on them.

--------------------------------------------------
1. SENIOR-REVIEW ARCHITECTURE FREEZE
--------------------------------------------------

The approved conceptual architecture is:

CLIENT UNIVERSE
        +
CLIENT RECORD -> LEGAL ENTITY IDENTITY LINKS
        +
ACCEPTED LEGAL ENTITY RELATIONSHIP GRAPH
                         \
                          \
                           -> CONSTRAINED PATTERN EVALUATOR
                          /
CORRELATION DEFINITIONS
(independent governed/versioned configuration)

                         ↓

DERIVED CLIENT-TO-CLIENT CORRELATION RESULTS


Separately:

CLIENT UNIVERSE
        +
IDENTITY LINKS
        +
LEGAL ENTITY RELATIONSHIP GRAPH

        ↓

DIRECT RELATIONSHIP VIEW


Important:

Correlation Definition is NOT a processing stage between the graph and engine.

The relationship graph and a selected Correlation Definition Version are independent inputs to the evaluator.

Changing a Correlation Definition must NEVER modify factual relationships.

--------------------------------------------------
2. TERMINOLOGY FREEZE
--------------------------------------------------

Use these architectural terms consistently.

CLIENT RECORD

One authoritative record in the 3.67M Client Universe at GFCID grain.


LEGAL ENTITY

Real-world juridical entity represented in the Legal Entity / relationship graph.


RELATIONSHIP

A factual evidence-backed typed state between Legal Entities.

Examples:

owns
controls
supplies
lends_to


CORRELATION

A derived governed Client Record-to-Client Record structural finding produced from:

qualifying identity links
+
accepted factual relationships
+
an active Correlation Definition Version


DIRECT RELATIONSHIP VIEW

A client-grain projection of an existing direct Legal Entity relationship.

It is NOT a correlation.


CONNECTION

Do not use as a second architecture object.

"Connected clients" may later be used as informal UI wording only.


PATTERN

The bounded structural shape of a Correlation Definition.


DEFINITION

The governed/versioned configuration describing a derived correlation.


RESULT

One derived correlation instance found by evaluating one definition version against the graph.

--------------------------------------------------
3. STOP USING "GENERIC CORRELATION ENGINE"
--------------------------------------------------

Rename internal concepts where practical from:

generic correlation engine

to:

CONSTRAINED PATTERN EVALUATOR

The evaluator is intentionally NOT a general graph DSL.

Do not implement:

arbitrary graph expressions
Cypher-like syntax
recursive rule evaluation
user-written predicates
unbounded traversal
dynamic code execution

--------------------------------------------------
4. CLEAN UP THE ABORTED STAGE 4 ARTIFACTS
--------------------------------------------------

Before implementing the corrected architecture:

inspect the two partial Stage 4 tables:

ccr_correlation_definitions
ccr_correlation_definition_versions

and all current partial Stage 4 code.

Because:

- schema version remains 10;
- no Stage 4 migration ledger entry exists;
- Stage 4 was explicitly stopped before approval;
- no approved historical object depends on these records;

treat the current 7 definitions / 7 versions as ABORTED STAGE 4 SCRATCH DATA.

If verification confirms they have no approved dependency:

drop/recreate or otherwise cleanly replace ONLY:

ccr_correlation_definitions
ccr_correlation_definition_versions

Do NOT touch:

CCR V1 identity links
documents
passages
claims
events
relationships
relationship versions
qualifiers
coverage
Stage 2 historical tables
Client Universe
source master

Record exactly what was removed/rebuilt in the Stage 4 report.

Do not create a migration ledger record for the aborted implementation.

The corrected implementation should become the first approved Stage 4 migration.

--------------------------------------------------
5. DIRECT IS NOT A CORRELATION DEFINITION
--------------------------------------------------

Remove DIRECT from:

ccr_correlation_definitions

Remove DIRECT from:

ccr_correlation_definition_versions

Remove DIRECT from:

derived pattern kinds

There must be:

NO DIRECT correlation definition
NO DIRECT correlation version
NO DIRECT configuration fingerprint

DIRECT is implemented as:

DIRECT RELATIONSHIP VIEW

It has no authored lifecycle.

It is:

always available
not authorable
not activatable
not disableable as a business definition
not versioned as a correlation definition
not creatable by future AI Create Correlation

A display filter may later choose which factual relationship types to show.

That is UI/query filtering, not correlation semantics.

--------------------------------------------------
6. DIRECT RELATIONSHIP VIEW
--------------------------------------------------

Implement a first-class service/domain result for:

Direct Relationship View

Conceptually:

Client Record A
    ->
VERIFIED identity
    ->
Legal Entity A
    ->
ACCEPTED relationship
    ->
Legal Entity B
    ->
VERIFIED identity
    ->
Client Record B

Return the actual factual relationship.

Example:

3M
    ->
owns
    ->
3M India

The result must preserve:

Client Record A
Client Record B

Legal Entity A
Legal Entity B

identity-link IDs

identity-link type

identity-link state

relationship ID

relationship-version ID

relationship type

canonical direction

acceptance state

freshness

qualifiers

evidence basis

evidence/support lineage

as-of/current resolution metadata

No synthetic Client-to-Client relationship row is created.

--------------------------------------------------
7. HARD IDENTITY INVARIANT
--------------------------------------------------

Identity eligibility is NOT a Correlation Definition field.

Remove from the configurable definition surface:

endpoint_identity_policy

or equivalent author-controlled field.

For accepted V1 correlations:

both Client Record endpoints require:

link_state = VERIFIED

and

link_type = EXACT

This is a HARD GLOBAL PLATFORM INVARIANT.

Definitions cannot weaken it.

Definitions cannot request:

PROBABLE
UNVERIFIED
REJECTED

PROBABLE must never appear in accepted correlation results.

PROBABLE may support a future separate analyst-review/exploration capability, but do not implement that now.

VERIFIED + ASSOCIATED:

preserve architectural capability for a future GLOBAL governance switch.

It is NOT configurable per definition.

For this initial Stage 4 implementation:

global accepted-correlation endpoint rule remains:

VERIFIED + EXACT

ASSOCIATED acceptance:
OFF

Any future enabling of VERIFIED + ASSOCIATED must be:

global
explicit
governed
clearly labeled

never silently equivalent to EXACT.

--------------------------------------------------
8. HARD RELATIONSHIP INVARIANT
--------------------------------------------------

Relationship acceptance eligibility is NOT a Correlation Definition field.

Remove from the configurable definition surface:

relationship_acceptance_policy

or equivalent.

For every accepted derived correlation:

every relationship hop MUST use:

relationship-version state = ACCEPTED

This is a HARD GLOBAL PLATFORM INVARIANT.

Definitions may NOT enable:

CANDIDATE
DISPUTED
REJECTED

No AI-created definition may ever override this.

Candidate exploration, if built later, must be a completely separate capability and result stream.

Do not mix candidate exploration with accepted correlations.

--------------------------------------------------
9. EVIDENCE DRILL-DOWN IS A HARD INVARIANT
--------------------------------------------------

Remove:

evidence_drilldown_required

or equivalent configurable toggle.

Every direct relationship result and every derived correlation result must be traceable through:

relationship version
support
atomic claim
passage
document/source evidence

where such V1 evidence is retained.

Evidence drill-down is mandatory platform behavior.

Because it is mandatory, it must NOT be configurable.

--------------------------------------------------
10. DERIVED CORRELATION PATTERN SHAPES
--------------------------------------------------

V1 supports exactly TWO derived pattern shapes:

SHARED_INTERMEDIATE

DIRECTED_CHAIN

Do not include DIRECT as a pattern kind.

Do not create additional graph-shape kinds.

Maximum derived pattern depth:

2 relationship hops

No recursive traversal.

No arbitrary graph DSL.

--------------------------------------------------
11. PER-HOP TYPING
--------------------------------------------------

Pattern configuration must be typed per hop.

A pattern contains:

hop_1:
    relationship_type
    direction

hop_2:
    relationship_type
    direction

Each hop may use different governed relationship types if allowed by the definition.

Directions must conform to the canonical relationship ontology.

A definition cannot redefine the underlying relationship direction.

Examples:

SHARED_SUPPLIER:

hop 1:
Supplier X -> supplies -> Client A

hop 2:
Supplier X -> supplies -> Client B


SUPPLY_CHAIN:

hop 1:
Client A -> supplies -> X

hop 2:
X -> supplies -> Client B

The shared shape model must allow these without creating new engine code for each named definition.

--------------------------------------------------
12. DERIVED CORRELATION DEFINITION
--------------------------------------------------

Create/retain an approved model equivalent to:

CCRCorrelationDefinition

Fields should include:

definition_id
code
display_name
description
category
pattern_kind
status
created_at
created_by

Allowed pattern_kind:

SHARED_INTERMEDIATE
DIRECTED_CHAIN

Suggested statuses:

DRAFT
ACTIVE
DISABLED
RETIRED

Category is descriptive/governance metadata.

Initial useful categories may include:

GROUP_STRUCTURE
COMMERCIAL_DEPENDENCY
FINANCING
PRODUCT_DEPENDENCY

Do not make category an acceptance rule.

--------------------------------------------------
13. CORRELATION DEFINITION VERSION
--------------------------------------------------

Create immutable versions containing the configurable semantics only.

Suitable fields include:

definition_id
version

effective_from
effective_to

hop_1 relationship type
hop_1 direction

hop_2 relationship type
hop_2 direction

intermediate entity rules

qualifier predicates

coverage presentation policy

hub/noise default policy

default visibility

canonical configuration JSON

configuration fingerprint

created_at
created_by

Do NOT include as configuration:

identity acceptance state
identity link type policy
relationship acceptance state
evidence drill-down requirement
maximum arbitrary depth
free-form graph expressions

Maximum depth is a platform invariant derived from pattern kind.

--------------------------------------------------
14. DEFINITION VERSION IMMUTABILITY
--------------------------------------------------

Once a definition version becomes ACTIVE:

do not mutate its executable semantics.

A changed configuration creates a new version.

Old versions remain auditable.

Configuration fingerprint is:

system-derived
deterministic
not user-editable

Equivalent canonical configuration must generate the same fingerprint.

Changed executable semantics must generate a different fingerprint.

--------------------------------------------------
15. QUALIFIER PREDICATES
--------------------------------------------------

Support a small closed predicate form.

Allowed operators:

EXISTS
EQUALS

and numeric ordered comparisons:

GREATER_THAN
GREATER_THAN_OR_EQUAL
LESS_THAN
LESS_THAN_OR_EQUAL

Numeric comparisons may only be used on qualifier types defined by the ontology as numeric.

Examples:

ownership_percentage >= 20

Only qualifier names from the governed ontology may be referenced.

Predicate combination:

flat AND list only

Do NOT implement:

OR
NOT
nested expressions
free-form expressions
scripts
user-written SQL
arbitrary formula evaluation

This is a bounded form, not a DSL.

--------------------------------------------------
16. CORRELATION TRUTH VS USEFULNESS
--------------------------------------------------

Keep these concepts strictly separate.

CORRELATION TRUTH requires:

qualifying endpoint identity
+
ACCEPTED relationship hops
+
structural pattern match
+
required qualifier predicates

That determines whether the correlation exists.


USEFULNESS / NOISE may use:

intermediate client degree
hub degree
qualifier presence
coverage
default visibility policy

These factors must NOT alter whether the underlying correlation is true.

Do not create:

correlation score
importance score
risk score
strength score
materiality score

--------------------------------------------------
17. HUB / NOISE POLICY
--------------------------------------------------

Support deterministic default-display policy such as:

NONE
WARN
SUPPRESS

with optional factual threshold:

max_role_specific_client_degree

Important:

SUPPRESS means:

hidden/collapsed by default presentation

NOT:

delete the correlation
invalidate the correlation
remove it from auditable query results

The result contract must retain a flag such as:

would_be_suppressed_by_default = true / false

The user must be able to retrieve suppressed correlations explicitly later.

--------------------------------------------------
18. COVERAGE RULE
--------------------------------------------------

Coverage must accompany:

positive correlation results

and

empty correlation queries.

A positive structural correlation remains valid even if broader research coverage is partial.

Coverage does NOT invalidate a found result.

For absence statements:

Only state an unqualified:

"no known connection of this type"

when the relevant governed research scope is sufficiently complete for BOTH endpoints.

Where coverage is:

PARTIAL
NOT_RESEARCHED
UNAVAILABLE

the system must instead say conceptually:

"No qualifying correlation was found within current research coverage."

Do not imply:

no shared supplier exists
no common customer exists
no dependency exists

when coverage is incomplete.

--------------------------------------------------
19. TEMPORAL MODEL
--------------------------------------------------

Default V1 query mode:

latest known current ACCEPTED relationship state

evaluated as of the query execution date/time.

Every returned result must record the effective:

as_of_date

used by the evaluator.

Do not require the analyst to manually provide historical as-of date for ordinary V1 queries.

Preserve architecture for explicit historical as-of queries later.

Do not flatten multiple relationship versions.

Example:

3M -> Solventum ownership

19.9%
and later
14.8%

must remain separate relationship/qualifier history.

STALE ACCEPTED relationships may still participate but must be marked:

freshness = STALE

Freshness is not itself an acceptance gate.

--------------------------------------------------
20. RESULT PERSISTENCE
--------------------------------------------------

Persist:

Correlation Definitions
Correlation Definition Versions

Do NOT persist derived correlation results as authoritative pair rows.

Do NOT create:

giant Client A x Client B table

Do NOT materialize all possible correlations.

Derived results are query-time results.

A future query cache may be introduced only after measured need.

--------------------------------------------------
21. CONSTRAINED PATTERN EVALUATOR
--------------------------------------------------

Implement one bounded evaluator.

Inputs:

selected Client Record
active Correlation Definition Version
current/as-of relationship graph

The evaluator must:

1. validate the definition;

2. resolve the selected Client Record through the hard identity invariant;

3. load eligible ACCEPTED relationship versions;

4. execute exactly the configured bounded pattern shape;

5. enforce per-hop canonical direction;

6. enforce per-hop governed relationship type;

7. evaluate flat qualifier predicates;

8. identify the opposite Client Record endpoint through qualifying VERIFIED + EXACT identity;

9. compute role-specific intermediate client degree;

10. identify whether intermediate entity is itself a qualifying Client Record;

11. attach coverage metadata;

12. apply default noise/visibility policy without altering truth;

13. construct an ordered explainable path;

14. return deterministic results.

No provider call.

No research call.

No recursive traversal.

--------------------------------------------------
22. RESULT CONTRACT
--------------------------------------------------

Each derived correlation result must include at least:

correlation definition ID
correlation code
definition version
definition category
pattern kind
configuration fingerprint

Client A client_id
Client A GFCID
Client A Legal Entity

Client B client_id
Client B GFCID
Client B Legal Entity

Client A identity-link ID
Client A identity-link type
Client A identity-link state

Client B identity-link ID
Client B identity-link type
Client B identity-link state

as_of_date

ordered path

hop 1 relationship ID
hop 1 relationship-version ID
hop 1 type
hop 1 direction
hop 1 acceptance state
hop 1 freshness
hop 1 evidence basis

hop 2 relationship ID
hop 2 relationship-version ID
hop 2 type
hop 2 direction
hop 2 acceptance state
hop 2 freshness
hop 2 evidence basis

intermediate Legal Entity ID

intermediate role-specific qualifying-client degree

intermediate_is_client:
true / false

intermediate_client_reference:
nullable client_id/GFCID if qualifying

qualifiers used by the definition

coverage metadata

would_be_suppressed_by_default:
true / false

visibility-policy reason

deterministic result fingerprint

Do not add an opaque numeric score.

--------------------------------------------------
23. DIRECT RELATIONSHIP RESULT CONTRACT
--------------------------------------------------

Direct Relationship View has a separate result object.

It must NOT require:

definition_id
definition_version
configuration fingerprint

because DIRECT is not a correlation definition.

It should include:

Client A
Client B

their Legal Entities

their identity-link IDs/types/states

relationship ID
relationship-version ID

relationship type
canonical direction

acceptance state
freshness

qualifiers

evidence basis
support lineage

as_of_date

deterministic direct-view fingerprint if useful

This result family may later be rendered beside correlations in the same workspace.

--------------------------------------------------
24. INITIAL DERIVED CORRELATION CATALOGUE
--------------------------------------------------

Seed only DERIVED definitions.

Do NOT seed DIRECT.

Seed:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN
SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY

--------------------------------------------------
25. SHARED_CONTROLLER
--------------------------------------------------

Code:

SHARED_CONTROLLER

Category:

GROUP_STRUCTURE

Pattern:

SHARED_INTERMEDIATE

Structure:

Controller X
    -> controls -> Client A

Controller X
    -> controls -> Client B

Status:

ACTIVE

Default visibility:

VISIBLE

Report role-specific intermediate client degree.

This is structurally distinct from dependency patterns.

Do not call it a dependency correlation.

--------------------------------------------------
26. SHARED_SUPPLIER
--------------------------------------------------

Code:

SHARED_SUPPLIER

Category:

COMMERCIAL_DEPENDENCY

Pattern:

SHARED_INTERMEDIATE

Structure:

Supplier X
    -> supplies -> Client A

Supplier X
    -> supplies -> Client B

Status:

ACTIVE

Use deterministic hub/default-visibility policy capability.

Do not invent a numerical threshold unless required by a fixture/test.

Base truth exists independently of hub visibility.

--------------------------------------------------
27. SHARED_CUSTOMER
--------------------------------------------------

Code:

SHARED_CUSTOMER

Category:

COMMERCIAL_DEPENDENCY

Pattern:

SHARED_INTERMEDIATE

Structure:

Client A
    -> supplies -> Customer X

Client B
    -> supplies -> Customer X

Status:

ACTIVE

Because generic/common customers can create noise:

support hub/default-visibility handling.

Do not require revenue-share qualifier in base V1 definition unless already supported by factual data.

Qualifier-enriched variants can be created later.

--------------------------------------------------
28. SUPPLY_CHAIN
--------------------------------------------------

Code:

SUPPLY_CHAIN

Category:

COMMERCIAL_DEPENDENCY

Pattern:

DIRECTED_CHAIN

Structure:

Client A
    -> supplies -> Intermediate X

Intermediate X
    -> supplies -> Client B

Status:

ACTIVE

Direction is mandatory.

The result explanation must preserve:

upstream
intermediate
downstream

roles where derivable from direction.

Do not infer financial/risk propagation.

It is a structural supply-chain correlation only.

--------------------------------------------------
29. SHARED_LENDER
--------------------------------------------------

Code:

SHARED_LENDER

Category:

FINANCING

Pattern:

SHARED_INTERMEDIATE

Structure:

Lender X
    -> lends_to -> Client A

Lender X
    -> lends_to -> Client B

Status:

ACTIVE

Default visibility:

HIDDEN_BY_DEFAULT

Reason:

large lenders can create high-degree hub results.

Additionally expose whether the intermediate lender is itself:

a Client Record
or
an internally governed institution requiring later display-policy review.

Do NOT implement special Citi hard-coding.

Add a report note:

Citi-as-intermediate display/governance policy remains an external governance decision.

Do not solve that by silently suppressing facts.

--------------------------------------------------
30. SHARED_PRODUCT_DEPENDENCY
--------------------------------------------------

Code:

SHARED_PRODUCT_DEPENDENCY

Category:

PRODUCT_DEPENDENCY

Pattern:

SHARED_INTERMEDIATE

Structure:

Client A
    -> depends_on_products_of -> Producer X

Client B
    -> depends_on_products_of -> Producer X

Status:

ACTIVE

Default visibility:

HIDDEN_BY_DEFAULT

Because the underlying relationship itself requires explicit dependency evidence, preserve its strict evidence semantics.

Do not weaken depends_on_products_of acceptance.

--------------------------------------------------
31. DO NOT ADD SHARED_SIGNIFICANT_INVESTOR YET
--------------------------------------------------

Senior review noted a possible future pattern:

SHARED_SIGNIFICANT_INVESTOR

Do not implement it in this stage.

Record it as a future candidate only.

--------------------------------------------------
32. CONFIGURATION VALIDATION
--------------------------------------------------

Reject any definition/version that tries to:

use DIRECT as a derived pattern

use an unknown pattern kind

reference an unknown relationship type

use depth greater than 2

override identity eligibility

enable PROBABLE endpoints

enable UNVERIFIED endpoints

enable REJECTED endpoints

override ACCEPTED-only relationship eligibility

enable CANDIDATE hops

enable DISPUTED hops

enable REJECTED hops

disable evidence lineage

invent a new relationship direction

reference an unknown qualifier

apply numeric comparison to a non-numeric qualifier

use OR

use nested expressions

use arbitrary graph expressions

use arbitrary code

--------------------------------------------------
33. FUTURE AI CREATE CORRELATION SUPPORT
--------------------------------------------------

Do NOT implement AI Create Correlation now.

But ensure the schema can safely support it later.

The future AI should only be able to fill bounded slots:

definition name
description
category
pattern kind
hop relationship types
hop directions
bounded qualifier predicates
hub/default visibility settings

It must never be able to author:

identity acceptance rules

relationship acceptance states

evidence requirements

arbitrary traversal

new ontology types

new qualifier operators

arbitrary executable expressions

Activation must remain separate from creation.

A DRAFT must later be previewable through the same evaluator with no side effect except storing the draft.

No LLM code in this stage.

--------------------------------------------------
34. QUERY METHODS
--------------------------------------------------

Implement service/repository methods conceptually equivalent to:

direct_relationships_for_client(
    client_id,
    optional relationship types,
    current/as_of,
    limit
)

derived_correlations_for_client(
    client_id,
    optional definition codes,
    current/as_of,
    include_hidden,
    limit
)

derived_correlations_between_clients(
    client_id_a,
    client_id_b,
    optional definition codes,
    current/as_of
)

Do not expose unrestricted public configuration mutation APIs yet.

Public API work is the next stage.

--------------------------------------------------
35. BOUNDED EXECUTION
--------------------------------------------------

Enforce:

derived depth exactly as required by supported pattern shape

maximum 2 hops

bounded results

bounded intermediate expansion

no frontier research

no recursive graph expansion

no provider calls

no research initiation

--------------------------------------------------
36. REAL 3M DIRECT RELATIONSHIP PROOF
--------------------------------------------------

Use current real V1 data.

Known qualifying case:

3M Client Record
    ->
VERIFIED EXACT
    ->
3M Legal Entity
    ->
ACCEPTED owns
    ->
3M India Legal Entity
    ->
VERIFIED EXACT
    ->
3M India Client Record

Run:

Direct Relationship View

Expected conceptual output:

3M
    -- owns -->
3M India

with:

actual Client IDs
actual GFCIDs
actual Legal Entity IDs
identity-link IDs
identity-link types/states
relationship ID
relationship-version ID
ownership_percentage = 75% where available
evidence basis
freshness
support lineage

This must NOT be returned as:

DIRECT correlation

It is:

DIRECT RELATIONSHIP VIEW

--------------------------------------------------
37. SOLVENTUM DIRECT SAFETY CASE
--------------------------------------------------

3M has accepted Legal Entity relationships with Solventum.

But Solventum's Client Universe match-back remains ambiguous.

Therefore:

Legal Entity relationship:
YES

Direct Client Relationship View:
NO

unless a qualifying VERIFIED + EXACT Client Record identity link exists.

Do not create such an identity during this stage.

Do not perform identity research.

--------------------------------------------------
38. CABOT SAFETY CASE
--------------------------------------------------

Cabot currently has:

no accepted V1 relationship

and
ambiguous Client Universe candidate match

Therefore:

Direct Client Relationship View:
NO

Derived correlation:
NO

Do not reopen Cabot research.

--------------------------------------------------
39. REAL DERIVED RESULTS
--------------------------------------------------

Run all ACTIVE derived correlation definitions against current real V1 pilot data.

Do not fabricate matches.

Likely real counts may be zero.

That is acceptable.

For each zero result distinguish:

NO_STRUCTURAL_MATCH

ENDPOINT_IDENTITY_GAP

INSUFFICIENT_COVERAGE

or combinations where supportable.

Do not assert non-existence beyond coverage.

--------------------------------------------------
40. TEST FIXTURES
--------------------------------------------------

Derived-pattern mechanics must be validated using structurally isolated test data.

Fixtures must use:

temporary database
or
separate test-only repository/database

They must NOT be inserted into the real relationship_ingestion.sqlite3 production-like store.

Fixture tests prove:

engine mechanics

NOT:

real-world product-value density.

State this clearly in the report.

--------------------------------------------------
41. REQUIRED TESTS — CLEANUP
--------------------------------------------------

Add tests proving:

1. aborted DIRECT definition removed.

2. exactly no DIRECT derived definition exists.

3. aborted Stage 4 rows do not survive corrected bootstrap.

4. corrected bootstrap is idempotent.

5. no approved pre-Stage-4 object was deleted.

--------------------------------------------------
42. REQUIRED TESTS — HARD INVARIANTS
--------------------------------------------------

6. VERIFIED + EXACT endpoint passes.

7. PROBABLE endpoint fails accepted correlation evaluation.

8. UNVERIFIED endpoint fails.

9. REJECTED endpoint fails.

10. ASSOCIATED fails while global associated toggle is OFF.

11. definition cannot override identity gate.

12. ACCEPTED relationship hop passes.

13. CANDIDATE hop fails.

14. DISPUTED hop fails.

15. REJECTED hop fails.

16. definition cannot override relationship acceptance gate.

17. evidence drill-down cannot be disabled by a definition.

--------------------------------------------------
43. REQUIRED TESTS — DIRECT RELATIONSHIP VIEW
--------------------------------------------------

18. accepted direct factual relationship between two VERIFIED+EXACT Client-linked Legal Entities appears in Direct Relationship View.

19. underlying relationship type is preserved.

20. relationship direction is preserved.

21. relationship-version ID is returned.

22. qualifiers are returned.

23. evidence lineage is available.

24. DIRECT creates no correlation definition.

25. DIRECT creates no synthetic Client relationship row.

26. ambiguous Solventum Client match prevents Direct Client Relationship View.

27. Cabot does not appear.

--------------------------------------------------
44. REQUIRED TESTS — PATTERN MODEL
--------------------------------------------------

28. only SHARED_INTERMEDIATE and DIRECTED_CHAIN pattern kinds accepted.

29. DIRECT pattern rejected.

30. depth > 2 impossible/rejected.

31. hop 1 and hop 2 types are independently configurable.

32. canonical direction constraints enforced.

33. unsupported relationship type rejected.

--------------------------------------------------
45. REQUIRED TESTS — DERIVED PATTERNS
--------------------------------------------------

34. SHARED_CONTROLLER positive fixture.

35. SHARED_CONTROLLER wrong direction negative.

36. SHARED_SUPPLIER positive fixture.

37. SHARED_CUSTOMER positive fixture.

38. SUPPLY_CHAIN positive fixture.

39. SUPPLY_CHAIN wrong direction negative.

40. SHARED_LENDER positive fixture.

41. SHARED_PRODUCT_DEPENDENCY positive fixture.

42. intermediate does not need to be a Client Record.

43. both result endpoints require qualifying Client Records.

44. intermediate-is-client field populated correctly when appropriate.

45. role-specific intermediate degree returned.

--------------------------------------------------
46. REQUIRED TESTS — QUALIFIERS
--------------------------------------------------

46. EXISTS works.

47. EQUALS works.

48. numeric >= works on numeric qualifier.

49. numeric <= works on numeric qualifier.

50. numeric comparison rejected for non-numeric qualifier.

51. flat AND list works.

52. OR rejected.

53. nested predicate rejected.

54. candidate qualifier cannot satisfy ACCEPTED qualifier requirement where acceptance is required.

--------------------------------------------------
47. REQUIRED TESTS — HUB / VISIBILITY
--------------------------------------------------

55. hub policy never changes correlation truth.

56. WARN preserves result.

57. SUPPRESS preserves result in auditable query.

58. SUPPRESS sets would_be_suppressed_by_default=true.

59. include_hidden query can retrieve suppressed/default-hidden results.

--------------------------------------------------
48. REQUIRED TESTS — COVERAGE
--------------------------------------------------

60. positive result remains valid under PARTIAL broader coverage.

61. empty result with PARTIAL coverage does not assert universal absence.

62. sufficiently completed scope can support governed "no known correlation found" wording.

--------------------------------------------------
49. REQUIRED TESTS — TEMPORAL
--------------------------------------------------

63. current mode selects latest known applicable accepted state.

64. older relationship version remains preserved.

65. stale accepted relationship may participate but is explicitly marked STALE.

66. result records actual as_of_date used.

--------------------------------------------------
50. REQUIRED TESTS — RESULT CONTRACT
--------------------------------------------------

67. correlation result contains definition version and configuration fingerprint.

68. identity link type returned for both endpoints.

69. acceptance state returned per hop.

70. freshness returned per hop.

71. role-specific intermediate degree returned.

72. intermediate-is-client flag returned.

73. default-suppression flag returned.

74. deterministic result fingerprint stable for identical inputs.

--------------------------------------------------
51. REQUIRED TESTS — INTEGRITY
--------------------------------------------------

75. no persisted derived-correlation result table exists.

76. no synthetic Client-to-Client relationship rows.

77. no fuzzy merges.

78. no external calls.

79. Client Universe unchanged.

80. source master unchanged.

81. historical Stage 2 unchanged.

82. existing CCR V1 relationships unchanged.

83. test fixtures do not exist in real production-like relationship database.

Run full backend suite after focused tests.

--------------------------------------------------
52. DATABASE MIGRATION
--------------------------------------------------

Current approved schema:
v10

After aborted Stage 4 artifacts are reconciled, create the first approved Stage 4 migration.

Expected resulting schema:
v11

Migration must be:

additive relative to approved v10
idempotent
replay-safe
non-destructive to all approved pre-Stage-4 data

Create only the corrected derived-correlation configuration structures required by this prompt.

Do not create a persisted result table.

Record one Stage 4 migration-ledger entry.

--------------------------------------------------
53. EXPECTED CONFIGURATION TABLES
--------------------------------------------------

Expected approved persistent structures:

ccr_correlation_definitions

ccr_correlation_definition_versions

They contain DERIVED correlation configuration only.

DIRECT must not appear in either table.

If another tiny table is genuinely required for platform-wide correlation governance settings, such as future ASSOCIATED global enablement, justify it before use.

Prefer configuration/code constant for this stage if no persistent governance need exists.

Do not over-engineer.

--------------------------------------------------
54. SEEDED DEFINITION COUNT
--------------------------------------------------

Expected derived definitions:

6

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN
SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY

DIRECT is excluded.

Expected initial versions:

6

unless a technically justified versioning/bootstrap detail requires otherwise.

Report exact counts.

--------------------------------------------------
55. EXTERNAL ACTIVITY
--------------------------------------------------

Required:

GLEIF calls:
0

SEC calls:
0

Web calls:
0

Stylus calls:
0

new identity research:
0

new relationship research:
0

frontier research:
0

Stage 2A.8:
0

--------------------------------------------------
56. CLIENT UNIVERSE INTEGRITY
--------------------------------------------------

Verify:

client_master rows:
3,670,650

unique GFCIDs:
3,670,650

inserts:
0

updates:
0

deletes:
0

--------------------------------------------------
57. SOURCE MASTER INTEGRITY
--------------------------------------------------

Verify:

backend/Customer_latest.parquet

rows:
3,670,650

unique GFCIDs:
3,670,650

modifications:
0

--------------------------------------------------
58. FRONTEND
--------------------------------------------------

Frontend files modified:

0

Do not implement:

Correlation Configuration UI
AI Create Correlation
Network Map
Client Workspace
Correlation Explorer

Those come later.

--------------------------------------------------
59. CREATE REPORT
--------------------------------------------------

Create:

backend/data/CCR_V1_STAGE_4_CORRELATION_FOUNDATION_REPORT.md

Required sections:

1. Executive result
2. Stopped Stage 4 checkpoint
3. Aborted-artifact reconciliation
4. Senior-review architecture changes
5. Terminology freeze
6. Direct Relationship View
7. Derived Correlation Definition model
8. Definition Version model
9. Hard identity invariant
10. Hard relationship invariant
11. Mandatory evidence lineage
12. Pattern model
13. Per-hop configuration
14. Qualifier predicate model
15. Coverage semantics
16. Truth vs hub/noise semantics
17. Temporal semantics
18. Result persistence decision
19. Constrained Pattern Evaluator
20. Result contract
21. Seeded definitions
22. SHARED_CONTROLLER
23. SHARED_SUPPLIER
24. SHARED_CUSTOMER
25. SUPPLY_CHAIN
26. SHARED_LENDER
27. SHARED_PRODUCT_DEPENDENCY
28. Real 3M Direct Relationship View
29. Solventum negative identity-gate case
30. Cabot negative case
31. Real derived correlation counts
32. Test-fixture derived validation
33. Configuration bootstrap replay
34. Migration replay
35. Backend tests
36. SQLite integrity
37. Client Universe integrity
38. Source-master integrity
39. External-call verification
40. Remaining product-validation gap
41. Recommended next action

--------------------------------------------------
60. PRODUCT-VALIDATION GAP
--------------------------------------------------

The report must explicitly distinguish:

ENGINE CORRECTNESS

from

PRODUCT VALUE VALIDATION

Fixture-derived patterns prove only:

pattern execution
identity gating
relationship gating
direction
qualifier predicates
coverage handling
hub/noise handling

They do NOT prove that real, useful, non-obvious correlations exist at sufficient volume.

Record as a near-term product milestone:

obtain at least one real evidence-backed derived two-hop correlation through controlled enrichment after the query/API foundation is stable.

Do not perform that enrichment in this stage.

--------------------------------------------------
61. FINAL STATUS FORMAT
--------------------------------------------------

At completion output exactly:

CCR V1 — STAGE 4 CORRELATION FOUNDATION

Status:
PASS / PARTIAL / FAIL

Schema before:
10

Schema after:

Aborted Stage 4 scratch definitions removed:
YES / NO

Aborted DIRECT definition removed:
YES / NO

Approved correlation definitions:

Approved correlation definition versions:

DIRECT persisted as correlation definition:
0

Direct Relationship View:
PASS / PARTIAL / FAIL

Hard identity invariant:
PASS / FAIL

Accepted endpoint identity policy:
VERIFIED + EXACT

ASSOCIATED global acceptance:
OFF

PROBABLE accepted correlation eligibility:
NO

Hard relationship invariant:
PASS / FAIL

Eligible relationship state:
ACCEPTED ONLY

Evidence drill-down configurable:
NO

Pattern kinds:

SHARED_INTERMEDIATE:
SUPPORTED / NOT_SUPPORTED

DIRECTED_CHAIN:
SUPPORTED / NOT_SUPPORTED

Other pattern kinds:
0

Max derived depth:
2

Qualifier operators:

EXISTS:
EQUALS:
GREATER_THAN:
GREATER_THAN_OR_EQUAL:
LESS_THAN:
LESS_THAN_OR_EQUAL:

Flat AND only:
YES / NO

Correlation definitions:

SHARED_CONTROLLER:
status:
default visibility:
category:

SHARED_SUPPLIER:
status:
default visibility:
category:

SHARED_CUSTOMER:
status:
default visibility:
category:

SUPPLY_CHAIN:
status:
default visibility:
category:

SHARED_LENDER:
status:
default visibility:
category:

SHARED_PRODUCT_DEPENDENCY:
status:
default visibility:
category:

Real Direct Relationship View:

3M -> 3M India:
FOUND / NOT_FOUND

Underlying relationship:
owns / other

Ownership qualifier:
75% / other / none

3M -> Solventum Client Direct Relationship View:
FOUND / BLOCKED_BY_IDENTITY / NOT_FOUND

Cabot Direct Relationship View:
FOUND / NOT_FOUND

Real derived correlations:

SHARED_CONTROLLER:
SHARED_SUPPLIER:
SHARED_CUSTOMER:
SUPPLY_CHAIN:
SHARED_LENDER:
SHARED_PRODUCT_DEPENDENCY:

Test-only fixture correlations persisted into real DB:
0

Persisted derived correlation-result rows:
0

Synthetic relationship rows:
0

Fuzzy merges:
0

External provider calls:
0

New identity research:
0

New relationship research:
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

Focused Stage 4 tests:
passed / failed / skipped

Full backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Migration replay:
PASS / FAIL

Configuration bootstrap replay:
PASS / FAIL

Direct Relationship View readiness:
READY / PARTIAL / FAIL

Derived Correlation Definition readiness:
READY / PARTIAL / FAIL

Constrained Pattern Evaluator readiness:
READY / PARTIAL / FAIL

Real derived product-value proof:
NOT_YET_DEMONSTRATED / DEMONSTRATED

Correlation API:
NOT_IMPLEMENTED

Correlation UI:
NOT_IMPLEMENTED

AI Create Correlation:
NOT_IMPLEMENTED

Report:
backend/data/CCR_V1_STAGE_4_CORRELATION_FOUNDATION_REPORT.md

Recommended next action:

If:

Direct Relationship View = READY

and

Derived Correlation Definition = READY

and

Constrained Pattern Evaluator = READY

then recommend:

CCR V1 — CORRELATION QUERY API + CLIENT CORRELATION READ MODEL

Do not start it automatically.
