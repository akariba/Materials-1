IMPLEMENT WITH LUNA

CCR — CLIENT CORRELATION
V1 STAGE 4 — CORRELATION CONFIGURATION + CORRELATION ENGINE FOUNDATION

THIS IS THE FIRST STAGE WHOSE PRIMARY PURPOSE IS ACTUAL CCR CORRELATION.

Do not turn this into another general enrichment architecture stage.

The product objective is now:

Client Universe records
        ->
verified Legal Entity identity
        ->
accepted evidence-backed Legal Entity relationships
        ->
governed correlation definitions
        ->
derived Client-to-Client correlations

This stage must implement the configuration layer and the correlation execution engine together so that correlation semantics are configurable from the beginning rather than hard-coded and retrofitted later.

No frontend work in this stage.

No new relationship research.

No broad identity campaign.

No Stage 2A work.

--------------------------------------------------
1. VERIFIED BASELINE
--------------------------------------------------

Current relationship schema:

v10

Current Client Universe:

3,670,650 rows
3,670,650 unique GFCIDs

Authoritative source:

backend/Customer_latest.parquet

Current CCR V1 identity-resolution pilot result:

Status:
COMPLETED

Identity results:

4 VERIFIED identity links
0 PROBABLE
0 UNVERIFIED
0 REJECTED

Legal Entities:

2 created
2 reused

Existing V1 claims re-evaluated:

4

V1 relationships:

before: 0
after: 3 ACCEPTED

V1 relationship versions:

before: 0
after: 4

V1 qualifiers:

before: 0
after: 3

Known accepted facts include:

3M -> 3M India
relationship: owns
accepted
ownership_percentage: 75%

3M -> Solventum
relationship: owns
accepted
historical ownership percentage: 19.9%

3M -> Solventum
relationship: owns
later version
ownership percentage: 14.8%

3M -> Solventum
relationship: supplies
accepted

Cabot:

context only
no accepted V1 relationship

Existing SPIN_OFF event remains independent from relationship rows.

Solventum Client Universe match remains ambiguous.

Cabot Client Universe match remains ambiguous.

Historical Stage 2 rows remain unchanged.

Backend tests:

69 passed

Fuzzy merges:

0

Synthetic direct edges:

0

Client Universe modifications:

0

Source-master modifications:

0

--------------------------------------------------
2. CORE PRODUCT OBJECTIVE
--------------------------------------------------

This stage must make CCR capable of answering:

"How is Client A correlated with Client B?"

using governed structural definitions over accepted evidence-backed relationships.

The basic flow is:

CLIENT RECORD A
    ->
VERIFIED identity
    ->
LEGAL ENTITY A
    ->
accepted relationship graph
    ->
correlation definition
    ->
LEGAL ENTITY B
    ->
VERIFIED identity
    ->
CLIENT RECORD B

The output is:

CLIENT A
<->
CLIENT B

with an explicit correlation type and an explainable evidence path.

--------------------------------------------------
3. RELATIONSHIP FACTS AND CORRELATIONS ARE DIFFERENT
--------------------------------------------------

Do NOT alter relationship facts because a correlation configuration changes.

Example:

Supplier X -> supplies -> Client A Legal Entity
Supplier X -> supplies -> Client B Legal Entity

Those are factual relationship records.

A configuration may determine that this structure constitutes:

SHARED_SUPPLIER

Changing, disabling, or versioning SHARED_SUPPLIER must NOT change either supplies relationship.

Architecture:

FACTUAL V1 RELATIONSHIP GRAPH
        ↓
CORRELATION CONFIGURATION
        ↓
CORRELATION ENGINE
        ↓
DERIVED CLIENT-TO-CLIENT CORRELATION

--------------------------------------------------
4. TWO CLASSES OF CORRELATION
--------------------------------------------------

Do not model DIRECT as if it were exactly the same thing as a multi-hop derived pattern.

Support two definition kinds:

DIRECT_RELATION_VIEW

DERIVED_PATTERN

DIRECT_RELATION_VIEW means:

two qualifying Client Records are linked because their Legal Entities have a qualifying accepted direct relationship.

DERIVED_PATTERN means:

two qualifying Client Records are correlated because a governed structural graph pattern connects their Legal Entities.

This distinction should remain explicit in the model.

--------------------------------------------------
5. CORRELATION DEFINITION OBJECT
--------------------------------------------------

Introduce a first-class versioned object conceptually equivalent to:

CCRCorrelationDefinition

and:

CCRCorrelationDefinitionVersion

A definition represents the stable business concept.

A version represents the exact executable configuration.

At minimum a definition requires:

definition_id
code
display_name
description
definition_kind
status
created_at
created_by

Suggested status model:

DRAFT
ACTIVE
DISABLED
RETIRED

A definition version requires at minimum:

definition_id
version
effective_from
effective_to if any
pattern specification
endpoint identity policy
relationship acceptance policy
relationship type restrictions
direction rules
maximum depth
intermediate-node rules
qualifier predicates if any
coverage policy
hub/noise policy
visibility policy
evidence drill-down policy
canonical configuration hash
created_at
created_by

Versions should be immutable after activation.

A changed configuration creates a new version.

--------------------------------------------------
6. DO NOT BUILD AN UNBOUNDED GRAPH DSL
--------------------------------------------------

Do not create a general-purpose arbitrary graph-programming language.

V1 configuration must be constrained and validateable.

Support only the structural pattern shapes required by CCR V1.

Suggested pattern kinds:

DIRECT

SHARED_INTERMEDIATE

DIRECTED_CHAIN

This is enough for the first correlation catalogue.

Examples:

DIRECT

Client A
    -- relationship -->
Client B


SHARED_INTERMEDIATE

Client A <- supplies - Supplier X - supplies -> Client B


DIRECTED_CHAIN

Client A -> supplies -> Entity X -> supplies -> Client B

Do not create arbitrary recursive pattern execution.

V1 configured depth must remain bounded.

Maximum supported derived pattern depth for this stage:

2 relationship hops.

--------------------------------------------------
7. CORRELATION CONFIGURATION MUST BE DATA, NOT CODE
--------------------------------------------------

Do not implement each correlation using custom if-statements such as:

if shared_supplier:
    ...

The engine should execute governed definitions stored through the configuration model.

Adding a new valid supported correlation pattern later should primarily require:

new configuration

not:

new relationship-graph business logic

provided the configuration uses an already supported pattern shape.

This is essential for the future:

AI Create Correlation

feature.

--------------------------------------------------
8. AI CREATE CORRELATION — DESIGN FOR IT, DO NOT IMPLEMENT IT
--------------------------------------------------

The future product will support:

Create Correlation
    ->
Manual
or
AI Create Correlation

AI will eventually be allowed to propose correlation configuration.

It must NOT directly activate arbitrary graph semantics.

Future flow:

AI proposal
    ->
DRAFT correlation definition/version
    ->
schema validation
    ->
preview against graph
    ->
result/noise review
    ->
authorized approval
    ->
ACTIVE version

Therefore the configuration contract created now must be serializable, validateable, versioned, and able to represent a DRAFT.

Do NOT implement:

LLM calls
AI proposal generation
approval UI
configuration UI

in this stage.

--------------------------------------------------
9. STRICT DEFAULT IDENTITY POLICY
--------------------------------------------------

Default Client-to-Client correlation endpoint policy:

link_state = VERIFIED

link_type = EXACT

Do not allow by default:

PROBABLE
UNVERIFIED
REJECTED

A definition may structurally support ASSOCIATED in the future, but initial system definitions should use EXACT unless there is an explicit reason otherwise.

Do not silently convert an ASSOCIATED link into EXACT.

--------------------------------------------------
10. INTERMEDIATE LEGAL ENTITIES
--------------------------------------------------

Derived correlations may use Legal Entities that are not Client Universe records as intermediate nodes.

Example:

Client A
    <- supplies -
External Supplier X
    - supplies ->
Client B

Supplier X does NOT have to be a client.

But both correlation endpoints:

Client A
Client B

must satisfy the configured Client Record -> Legal Entity identity policy.

Do not manufacture Client Records for intermediate entities.

--------------------------------------------------
11. RELATIONSHIP ELIGIBILITY
--------------------------------------------------

Default relationship-hop eligibility:

relationship version state = ACCEPTED

Do not traverse:

CANDIDATE
DISPUTED
REJECTED

unless a future explicitly governed configuration permits a different display-only mode.

For active V1 correlation definitions in this stage:

ACCEPTED only.

Relationship evidence must remain available through the CCR V1 support/evidence lineage.

No synthetic relationships.

--------------------------------------------------
12. TEMPORAL SEMANTICS
--------------------------------------------------

The engine must execute with an explicit:

as_of_date

or a clearly defined current-time mode.

For relationship versions with temporal information:

select versions valid/observed for the requested as-of interpretation according to existing V1 fields.

Do not flatten:

19.9%
and
14.8%

Solventum ownership observations into one timeless fact.

Correlation explanation must identify the relationship version(s) used.

If exact temporal validity is unknown, preserve the available observation/as-of semantics rather than inventing dates.

--------------------------------------------------
13. CORRELATION RESULT IS DERIVED
--------------------------------------------------

Do NOT persist correlation results as authoritative facts in this stage.

Correlation results should be derived/query results from:

relationship facts
identity links
correlation definition version
as-of date

Do not create a giant precomputed client-pair table.

Do not materialize all possible 3.67M x 3.67M pairs.

Persist configuration.

Derive correlation results.

Caching may be considered later.

--------------------------------------------------
14. CORRELATION RESULT CONTRACT
--------------------------------------------------

Create a domain result object conceptually equivalent to:

CCRCorrelationResult

It must contain at least:

correlation definition ID
correlation code
definition version
definition kind
Client A client_id
Client A GFCID
Client A Legal Entity
Client B client_id
Client B GFCID
Client B Legal Entity
as_of_date
ordered path
relationship IDs
relationship-version IDs
intermediate Legal Entity IDs
direction information
qualifying identity-link IDs
relevant qualifiers
evidence-basis metadata
coverage warnings
configuration hash
deterministic result fingerprint

Do not include an opaque correlation score.

--------------------------------------------------
15. CORRELATION EXPLANATION
--------------------------------------------------

Every result must be explainable.

Example output conceptually:

Correlation:
SHARED_SUPPLIER

Client A:
...

Client B:
...

Intermediate:
Supplier X

Path:

Supplier X
    -> supplies -> Client A Legal Entity

Supplier X
    -> supplies -> Client B Legal Entity

Endpoint identity:

Client A:
VERIFIED / EXACT

Client B:
VERIFIED / EXACT

Relationship evidence:

hop 1:
ACCEPTED
PRIMARY

hop 2:
ACCEPTED
PRIMARY

Definition:

SHARED_SUPPLIER
version 1

As of:

...

The user must be able to understand why CCR says the clients are correlated.

--------------------------------------------------
16. CORRELATION CONFIGURATION V1 CATALOGUE
--------------------------------------------------

Seed the following governed definitions.

Do not create fake graph results.

Definitions may legitimately return zero against the current pilot.

A. DIRECT

definition kind:

DIRECT_RELATION_VIEW

Meaning:

two qualifying Client Records whose Legal Entities have an eligible accepted relationship.

The result must preserve the actual underlying relationship type.

Examples:

owns
controls
supplies
lends_to
provides_credit_support
depends_on_products_of

Do not flatten them into an unexplained generic direct edge.


B. SHARED_CONTROLLER

definition kind:

DERIVED_PATTERN

Pattern:

Controller X
    -> controls -> Client A Legal Entity

Controller X
    -> controls -> Client B Legal Entity

Intermediate:

LEGAL_ENTITY

Depth:

2


C. SHARED_SUPPLIER

Pattern:

Supplier X
    -> supplies -> Client A Legal Entity

Supplier X
    -> supplies -> Client B Legal Entity


D. SHARED_CUSTOMER

Pattern:

Client A Legal Entity
    -> supplies -> Customer X

Client B Legal Entity
    -> supplies -> Customer X


E. SUPPLY_CHAIN

Pattern:

Client A Legal Entity
    -> supplies -> Intermediate X

Intermediate X
    -> supplies -> Client B Legal Entity

Direction matters.


F. SHARED_LENDER

Pattern:

Lender X
    -> lends_to -> Client A Legal Entity

Lender X
    -> lends_to -> Client B Legal Entity


G. SHARED_PRODUCT_DEPENDENCY

Pattern:

Client A Legal Entity
    -> depends_on_products_of -> Producer X

Client B Legal Entity
    -> depends_on_products_of -> Producer X


Do not add SHARED_SPONSOR yet unless the current manages semantics are fully implemented and tested.

It can remain deferred.

--------------------------------------------------
17. CONFIGURATION ENABLEMENT
--------------------------------------------------

Each seeded correlation definition must explicitly support:

ACTIVE
DISABLED

or equivalent governed enablement.

Initial recommendation:

DIRECT:
ACTIVE

SHARED_CONTROLLER:
ACTIVE

SHARED_SUPPLIER:
ACTIVE

SHARED_CUSTOMER:
ACTIVE

SUPPLY_CHAIN:
ACTIVE

SHARED_LENDER:
ACTIVE

SHARED_PRODUCT_DEPENDENCY:
ACTIVE

"ACTIVE" does not mean results must exist.

It means the engine is permitted to evaluate the pattern.

--------------------------------------------------
18. COVERAGE IS NOT PROOF OF NON-CORRELATION
--------------------------------------------------

A correlation query returning zero results does not mean:

no correlation exists.

The result should expose relevant enrichment coverage where available.

Example:

SHARED_SUPPLIER result count = 0

but supply enrichment coverage = PARTIAL

must be distinguishable from:

SHARED_SUPPLIER result count = 0

with complete governed supply coverage.

Do not convert zero result into a universal negative.

--------------------------------------------------
19. HUB / NOISE CONFIGURATION
--------------------------------------------------

Support a configuration section for hub/noise handling.

Do not implement opaque importance scores.

The configuration should be able to express factual constraints such as:

maximum intermediate linked-client degree
minimum evidence requirements
default visibility
suppress high-degree intermediate nodes
warn instead of suppress

For Stage 4, implement only simple deterministic degree handling if needed.

Suggested model:

hub_policy:
    mode = NONE | WARN | SUPPRESS
    max_client_degree = nullable integer

Default:

NONE

Do not invent thresholds for the seeded definitions unless required for tests.

--------------------------------------------------
20. VISIBILITY CONFIGURATION
--------------------------------------------------

Definitions should support:

VISIBLE
HIDDEN_BY_DEFAULT

This controls presentation/query default behavior.

It must not alter factual relationships.

No frontend is being built yet.

--------------------------------------------------
21. QUALIFIER PREDICATES
--------------------------------------------------

The configuration contract should be capable of requiring an accepted qualifier.

Example future configuration:

SHARED_CRITICAL_SUPPLIER

requires:

supplies

plus:

described_as_critical = ACCEPTED

Do not seed this correlation yet.

Do not implement a complicated general expression language.

Support a constrained qualifier predicate shape such as:

qualifier_type
allowed_states
operator
value where appropriate

V1 can initially support simple:

EXISTS
EQUALS

only.

--------------------------------------------------
22. CONFIGURATION VALIDATION
--------------------------------------------------

A correlation definition/version must be validated before activation.

Reject invalid configurations such as:

unknown relationship type
unknown pattern kind
depth > supported V1 depth
candidate hops for an ACTIVE V1 definition
REJECTED identity endpoints
missing direction semantics
unsupported qualifier operator
missing endpoint identity policy
synthetic relationship requirement
unknown entity grain

Validation errors must be explicit.

--------------------------------------------------
23. VERSIONING
--------------------------------------------------

Correlation definitions must be versioned.

Example:

SHARED_SUPPLIER v1

later:

SHARED_SUPPLIER v2

may change:

hub policy
visibility
identity policy
qualifier requirement

Existing result fingerprints/explanations must identify which version was used.

Do not mutate ACTIVE v1 in place.

--------------------------------------------------
24. CONFIGURATION FINGERPRINT
--------------------------------------------------

Canonicalize the executable configuration and compute a deterministic configuration fingerprint/hash.

The same semantic version/configuration should produce the same fingerprint.

A changed executable configuration must produce a different fingerprint.

Use this in:

result fingerprints
audit/debug output
tests

--------------------------------------------------
25. GENERIC CORRELATION ENGINE
--------------------------------------------------

Implement one engine/service that:

1. loads an ACTIVE correlation definition version;

2. validates the configuration;

3. resolves the selected Client Record to qualifying Legal Entity identity;

4. queries accepted V1 relationship versions;

5. executes the configured pattern;

6. validates the opposite client endpoint identity;

7. applies direction rules;

8. applies qualifier predicates;

9. applies hub policy;

10. attaches coverage information;

11. builds explanation path;

12. returns deterministic correlation results.

Do not implement separate engines for every correlation type.

--------------------------------------------------
26. QUERY MODES
--------------------------------------------------

Support at least:

A. correlations_for_client

Input:

client_id
optional definition code(s)
as_of_date
limit

Output:

bounded correlation results from the selected Client Record.


B. correlation_between_clients

Input:

client_id_a
client_id_b
optional definition code(s)
as_of_date

Output:

all qualifying configured correlations between the two Client Records.

These may initially be service/repository methods.

A public API is not required in this stage.

--------------------------------------------------
27. BOUNDED EXECUTION
--------------------------------------------------

All correlation execution must be bounded.

No unbounded graph walk.

For this stage:

maximum supported depth:
2 relationship hops

bounded result limit required

intermediate-node fan-out must be query-bounded

no recursive frontier expansion

no provider calls

no research initiation

--------------------------------------------------
28. CURRENT REAL PILOT — DIRECT CORRELATION
--------------------------------------------------

The current CCR V1 graph should be used to prove the engine with real data.

Expected real candidate:

3M Client Record

and

3M India Client Record

because the identity pilot established qualifying identities and the V1 graph contains:

3M Legal Entity
    -> owns ->
3M India Legal Entity

with an ACCEPTED relationship.

Run the DIRECT definition.

Expected conceptual result:

3M
<- DIRECT / owns ->
3M India

with:

relationship ID
relationship-version ID
identity-link IDs
ownership percentage where applicable
evidence basis
definition version
configuration fingerprint
as-of date
explanation

Do NOT hard-code client IDs into the engine.

This must emerge from the generic configuration and graph query.

--------------------------------------------------
29. SOLVENTUM SAFETY TEST
--------------------------------------------------

Solventum has accepted Legal Entity relationships with 3M but its Client Universe match remains ambiguous.

Therefore:

3M -> Solventum

must NOT automatically become a Client-to-Client DIRECT correlation unless Solventum has a qualifying identity link satisfying the active DIRECT definition.

Use this as a critical regression test.

Legal Entity relationship:

YES

Client-to-Client correlation:

NO

when endpoint Client identity is ambiguous/non-qualifying.

--------------------------------------------------
30. CABOT SAFETY TEST
--------------------------------------------------

Cabot currently has:

no accepted V1 relationship

and an ambiguous Client Universe match.

It must not appear as a client correlation.

This provides another negative control.

--------------------------------------------------
31. DERIVED PATTERN PILOT RESULT
--------------------------------------------------

Run the seeded derived definitions against the existing 3M-centered V1 data.

Do not expect fabricated results.

It is acceptable and likely that:

SHARED_CONTROLLER = 0

SHARED_SUPPLIER = 0

SHARED_CUSTOMER = 0

SUPPLY_CHAIN = 0

SHARED_LENDER = 0

SHARED_PRODUCT_DEPENDENCY = 0

for this small pilot.

Report the result honestly.

Also report whether the reason is:

no matching graph pattern

insufficient Client endpoint identity

insufficient relationship coverage

or a combination.

Zero derived correlations is not a failure of the engine.

--------------------------------------------------
32. DO NOT RESEARCH TO CREATE A DERIVED RESULT
--------------------------------------------------

Do not call providers just because the pilot lacks a shared supplier or shared controller.

Do not create test production data.

Do not fabricate relationships.

Use unit-test fixtures for pattern tests.

Use the real 3M data only for real validation.

--------------------------------------------------
33. TEST FIXTURES FOR ALL PATTERNS
--------------------------------------------------

Create temporary/test-only graph fixtures sufficient to verify each correlation definition mechanically.

Fixtures must not enter the production-like local relationship database.

Test:

DIRECT

SHARED_CONTROLLER

SHARED_SUPPLIER

SHARED_CUSTOMER

SUPPLY_CHAIN

SHARED_LENDER

SHARED_PRODUCT_DEPENDENCY

Verify directionality exactly.

--------------------------------------------------
34. DIRECT IS NOT A SYNTHETIC EDGE
--------------------------------------------------

A DIRECT correlation result is a derived client view of an existing accepted Legal Entity relationship.

Do not persist a new relationship edge between Client Records.

The relationship fact remains:

Legal Entity A
-> relationship ->
Legal Entity B

DIRECT correlation exposes that fact at the Client Record layer.

--------------------------------------------------
35. DERIVED CORRELATION IS NOT A RELATIONSHIP FACT
--------------------------------------------------

Example:

Client A and Client B share Supplier X.

Do NOT create a relationship row:

Client A -> shared_supplier -> Client B

in:

ccr_v1_relationships

SHARED_SUPPLIER is a derived correlation result.

This distinction is mandatory.

--------------------------------------------------
36. NO CORRELATION SCORE
--------------------------------------------------

Do not introduce:

correlation score
relationship score
materiality score
importance score
risk score
connection strength score

The engine returns:

correlation type
path
facts
evidence basis
coverage
degree/noise facts
configuration version

Any future ranking can be designed separately.

--------------------------------------------------
37. CORRELATION CATALOGUE REPOSITORY
--------------------------------------------------

Provide repository/service methods for at least:

create_definition
create_definition_version
get_definition
list_definitions
get_active_version
activate_version
disable_definition
validate_version

Writes may be used by tests/bootstrap only.

No admin UI yet.

Do not expose unrestricted public configuration mutation APIs in this stage.

--------------------------------------------------
38. SEEDED DEFINITIONS MUST BE IDEMPOTENT
--------------------------------------------------

Application initialization/bootstrap must not duplicate seeded definitions.

Repeated initialization must produce:

same definition IDs where deterministic
same active versions
same fingerprints
zero duplicate versions

Test this.

--------------------------------------------------
39. AUDITABILITY
--------------------------------------------------

A correlation result must be reproducible from:

definition ID
definition version
configuration fingerprint
as-of date
Client IDs
identity-link IDs
relationship-version IDs
qualifier IDs where used

Do not require hidden model reasoning to reproduce a result.

--------------------------------------------------
40. CORRELATION CONFIGURATION VS RELATIONSHIP CONFIGURATION
--------------------------------------------------

Keep this architectural separation explicit.

RELATIONSHIP CONFIGURATION answers:

What is an owns / controls / supplies / lends_to relationship?
What evidence is required?
What direction does it have?
What qualifiers are valid?

CORRELATION CONFIGURATION answers:

How can accepted relationships combine into a meaningful Client-to-Client structural connection?

Do not merge these two concepts into one configuration table.

--------------------------------------------------
41. NO LEGACY STATISTICAL CORRELATION REUSE
--------------------------------------------------

Do NOT reuse old Phase 4A constructs such as:

SAME_CAGID
SAME_BENEFICIAL_OWNER
statistical similarity signals
exposure correlation
old correlation score logic

as V1 correlation definitions.

Those remain legacy.

The new correlation engine is structural and evidence-backed.

--------------------------------------------------
42. NO EXPOSURE AUTHORITY
--------------------------------------------------

Do not use:

historical CCR exposure population
thousandClients
exposure amount
credit-managed flags

as correlation eligibility requirements.

All Client Universe records remain potentially eligible subject to identity and enrichment coverage.

--------------------------------------------------
43. DATABASE SCHEMA
--------------------------------------------------

Current schema:

v10

A small additive schema migration is authorized for correlation configuration.

Expected:

v11

Suggested new tables:

ccr_correlation_definitions

ccr_correlation_definition_versions

Use existing repository naming conventions.

Do not create a persisted correlation-result table in this stage.

If one additional small audit/bootstrap table is genuinely necessary, justify it in the report.

No destructive migration.

--------------------------------------------------
44. CONFIGURATION STORAGE
--------------------------------------------------

Prefer explicit scalar columns for core governance fields and canonical JSON for bounded pattern/policy structures where appropriate.

Do not store the entire definition as opaque free-form JSON only.

The database should make basic governance fields queryable:

code
kind
status
version
effective dates
configuration fingerprint

Pattern JSON must be schema validated.

--------------------------------------------------
45. NO FRONTEND
--------------------------------------------------

Frontend modifications:

0

Do not implement yet:

Correlation Configuration page
network map
client workspace
AI Create Correlation
configuration editor
preview UI

The backend model must, however, be suitable for those features later.

--------------------------------------------------
46. NO EXTERNAL ACTIVITY
--------------------------------------------------

During this stage:

GLEIF calls = 0

SEC calls = 0

Web calls = 0

Stylus calls = 0

new relationship research = 0

new identity research = 0

frontier expansion = 0

Stage 2A.8 = 0

The engine queries only existing local V1 data.

--------------------------------------------------
47. CLIENT UNIVERSE INTEGRITY
--------------------------------------------------

Verify:

3,670,650 client_master rows

3,670,650 unique GFCIDs

No inserts.
No updates.
No deletes.

--------------------------------------------------
48. SOURCE MASTER INTEGRITY
--------------------------------------------------

Verify:

backend/Customer_latest.parquet

Rows:
3,670,650

Unique GFCIDs:
3,670,650

No modifications.

--------------------------------------------------
49. REQUIRED TESTS
--------------------------------------------------

Preserve all current tests.

Add focused tests covering at least:

CONFIGURATION

1. correlation definition can be persisted.

2. correlation definition version can be persisted.

3. ACTIVE version is immutable.

4. changed config creates new version.

5. deterministic config fingerprint.

6. invalid relationship type rejected.

7. invalid pattern kind rejected.

8. depth > 2 rejected.

9. missing endpoint identity policy rejected.

10. candidate-hop ACTIVE configuration rejected.

11. unsupported qualifier operator rejected.

12. seeded definitions are idempotent.

IDENTITY GATING

13. VERIFIED EXACT endpoint passes default gate.

14. PROBABLE endpoint fails.

15. UNVERIFIED endpoint fails.

16. REJECTED endpoint fails.

17. ambiguous Client Universe candidate does not become correlation endpoint.

DIRECT

18. accepted direct relationship between two qualifying client-linked Legal Entities yields DIRECT result.

19. underlying relationship type remains visible.

20. candidate relationship version does not yield DIRECT result.

21. disputed relationship version does not yield DIRECT result.

22. rejected relationship version does not yield DIRECT result.

23. Solventum ambiguous match does not yield a client-to-client DIRECT result.

24. Cabot does not yield DIRECT result.

DERIVED PATTERNS

25. SHARED_CONTROLLER positive fixture.

26. SHARED_CONTROLLER direction-negative fixture.

27. SHARED_SUPPLIER positive fixture.

28. SHARED_CUSTOMER positive fixture.

29. SUPPLY_CHAIN positive fixture.

30. SUPPLY_CHAIN wrong-direction negative fixture.

31. SHARED_LENDER positive fixture.

32. SHARED_PRODUCT_DEPENDENCY positive fixture.

33. intermediate entity need not be a Client Record.

34. both endpoints must qualify as Client Records.

35. no synthetic relationship row is created.

QUALIFIERS

36. EXISTS qualifier predicate works.

37. EQUALS qualifier predicate works.

38. candidate qualifier fails an ACCEPTED-only predicate.

TEMPORAL

39. as-of query uses qualifying relationship version.

40. later ownership version does not erase historical version.

COVERAGE

41. zero correlation result with PARTIAL coverage does not assert no correlation exists.

BOUNDS

42. result limit enforced.

43. maximum depth enforced.

44. no recursive provider/research call occurs.

REPLAY

45. configuration bootstrap replay creates no duplicates.

INTEGRITY

46. Client Universe unchanged.

47. source master unchanged.

48. existing V1 relationships unchanged.

49. no fuzzy merge.

50. no synthetic direct relationship.

--------------------------------------------------
50. REAL 3M VALIDATION
--------------------------------------------------

Run the correlation engine against current real V1 data.

Required real checks:

A. correlations_for_client(3M)

with:

DIRECT

Report exact results.

Expected:

at least the 3M / 3M India ownership correlation if the current verified identity links and accepted relationship satisfy the configured policy.

Do not force the expectation.


B. correlation_between_clients(3M, 3M India)

Expected conceptual result:

DIRECT
underlying relation = owns

Include:

identity links
relationship
relationship version
75% qualifier where available
evidence basis
definition/version
as-of date
configuration fingerprint


C. 3M / Solventum

Legal Entity relationship exists.

Client-to-Client correlation must be absent if Solventum still lacks a qualifying Client Record identity link.


D. derived patterns

Run all ACTIVE derived definitions.

Report actual counts.

Zero is acceptable.

--------------------------------------------------
51. CORRELATION READINESS
--------------------------------------------------

At the end assess:

CONFIGURATION MODEL:
READY / PARTIAL / FAIL

DIRECT CORRELATION:
READY / PARTIAL / FAIL

DERIVED PATTERN ENGINE:
READY / PARTIAL / FAIL

REAL DIRECT PILOT:
READY / NOT_READY

REAL DERIVED PILOT DATA:
AVAILABLE / INSUFFICIENT

CORRELATION API:
NOT YET IMPLEMENTED

CORRELATION UI:
NOT YET IMPLEMENTED

AI CREATE CORRELATION:
NOT YET IMPLEMENTED

--------------------------------------------------
52. CREATE REPORT
--------------------------------------------------

Create:

backend/data/CCR_V1_CORRELATION_CONFIGURATION_ENGINE_FOUNDATION_REPORT.md

Required sections:

1. Executive result
2. Baseline
3. Product boundary
4. Relationship facts vs correlations
5. Schema changes
6. Correlation definition model
7. Definition version model
8. Configuration validation
9. Configuration fingerprinting
10. Seeded correlation catalogue
11. Generic execution engine
12. Identity gates
13. Relationship gates
14. Qualifier predicates
15. Temporal/as-of behavior
16. Coverage behavior
17. Hub/noise policy
18. Correlation explanation contract
19. DIRECT execution
20. SHARED_CONTROLLER execution
21. SHARED_SUPPLIER execution
22. SHARED_CUSTOMER execution
23. SUPPLY_CHAIN execution
24. SHARED_LENDER execution
25. SHARED_PRODUCT_DEPENDENCY execution
26. Real 3M validation
27. Solventum negative identity-gate test
28. Derived-pattern pilot results
29. Replay/idempotence
30. Tests
31. SQLite integrity
32. Client Universe integrity
33. Source-master integrity
34. External-call verification
35. Remaining limitations
36. Recommended next action

--------------------------------------------------
53. FINAL STATUS FORMAT
--------------------------------------------------

At completion output exactly:

CCR V1 — CORRELATION CONFIGURATION + ENGINE FOUNDATION

Status:
PASS / PARTIAL / FAIL

Schema before:
Schema after:

Client Universe rows:
Client Universe modifications:
Source-master modifications:

External provider calls:
0

New relationship research:
0

New identity research:
0

Correlation definitions created:

Correlation definition versions created:

Seeded definitions:

DIRECT:
SHARED_CONTROLLER:
SHARED_SUPPLIER:
SHARED_CUSTOMER:
SUPPLY_CHAIN:
SHARED_LENDER:
SHARED_PRODUCT_DEPENDENCY:

Configuration validation:
PASS / PARTIAL / FAIL

Configuration fingerprinting:
PASS / PARTIAL / FAIL

Generic correlation engine:
PASS / PARTIAL / FAIL

DIRECT correlation engine:
PASS / PARTIAL / FAIL

Derived correlation engine:
PASS / PARTIAL / FAIL

Real 3M DIRECT correlations:

3M -> 3M India DIRECT:
FOUND / NOT_FOUND

Underlying relationship type:

3M -> Solventum Client-to-Client correlation:
FOUND / BLOCKED_BY_IDENTITY / NOT_FOUND

Real derived-pattern results:

SHARED_CONTROLLER:
SHARED_SUPPLIER:
SHARED_CUSTOMER:
SUPPLY_CHAIN:
SHARED_LENDER:
SHARED_PRODUCT_DEPENDENCY:

Synthetic relationship rows created:
0

Persisted correlation-result rows created:
0

Fuzzy merges:
0

Frontend files modified:
0

Backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Configuration bootstrap replay:
PASS / FAIL

Correlation configuration readiness:
READY / PARTIAL / FAIL

Correlation engine readiness:
READY / PARTIAL / FAIL

Correlation API:
NOT_IMPLEMENTED

Correlation UI:
NOT_IMPLEMENTED

AI Create Correlation:
NOT_IMPLEMENTED

Report:
backend/data/CCR_V1_CORRELATION_CONFIGURATION_ENGINE_FOUNDATION_REPORT.md

Recommended next action:

If correlation configuration and engine are READY and the real 3M/3M India DIRECT result is produced correctly, recommend:

CCR CORRELATION API + QUERY LAYER

Do not begin API, frontend, AI Create Correlation, or new enrichment research automatically.
