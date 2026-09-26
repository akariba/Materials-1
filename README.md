IMPLEMENT WITH LUNA

CCR — CLIENT CORRELATION
V1 STAGE 2 — CONTROLLED 3M HISTORICAL MIGRATION AND REVALIDATION
OFFLINE / EVIDENCE-BOUND / NON-DESTRUCTIVE

The CCR V1 Foundation is now complete through Stage 1.1.

Current verified baseline:

Relationship schema: v10

Client Universe:
3,670,650 rows
3,670,650 unique GFCIDs

Backend tests:
63 passed
0 failed
0 skipped

Historical 3M accepted observations:
4

Historical graph-visible accepted edges:
4

Canonical historical evidence resolver:
PASS

Cabot normalized ordinary evidence:
recognized

CCR V1 production-like tables:
empty

Historical Stage 2 rows:
preserved and unchanged

External provider calls during Stage 1.1:
0

This stage is now explicitly authorized.

The purpose is to perform the FIRST controlled migration/revalidation of historical CCR relationship evidence into the new CCR V1 model.

This is NOT new research.

This is NOT Stage 2A.8.

This is NOT frontier expansion.

This is NOT frontend work.

--------------------------------------------------
1. OBJECTIVE
--------------------------------------------------

Use the existing persisted 3M pilot data to prove the CCR V1 model end-to-end:

historical evidence
    ->
CCR V1 document representation
    ->
evidence passage
    ->
atomic claim
    ->
endpoint identity gate
    ->
deterministic acceptance policy
    ->
relationship / relationship version
    ->
qualifiers and/or events
    ->
coverage
    ->
auditable comparison with historical Stage 2 result

No historical record may be rewritten.

The V1 result may differ from the historical Stage 2 result.

That is expected.

The historical observations are inputs for revalidation, not V1 truth.

--------------------------------------------------
2. ABSOLUTE NO-RESEARCH RULE
--------------------------------------------------

Do NOT call:

SEC
GLEIF
Web
Stylus
provider recovery
frontier expansion
any external API
any external website

Do NOT attempt to refresh evidence.

Do NOT use model pretrained knowledge as evidence.

Do NOT infer facts from general knowledge.

Use only evidence already persisted locally.

External provider calls must remain:

0

--------------------------------------------------
3. HISTORICAL 3M ROOT
--------------------------------------------------

Verify the root from the current database.

Expected:

client_id:
437487

GFCID:
0000426083

legal_name:
3M CO

Do not assume the expected values if current persisted data differs.

Report the verified values.

--------------------------------------------------
4. HISTORICAL OBSERVATIONS TO REVALIDATE
--------------------------------------------------

The four historical accepted observations are expected to be:

OBSERVATION 1

3M
->
3M India Ltd

historical type:
subsidiary

endpoint:
internal Client Universe record

historical acceptance:
ACCEPTED


OBSERVATION 2

3M
<->
Cabot Corporation

historical type:
legal_counterparty

endpoint:
external legal entity

historical acceptance:
ACCEPTED


OBSERVATION 3

3M
->
Solventum Corporation

historical type:
equity_investor

endpoint:
external legal entity

historical acceptance:
ACCEPTED


OBSERVATION 4

3M
<->
Solventum Corporation

historical type:
strategic_partner

endpoint:
external legal entity

historical acceptance:
ACCEPTED

Verify these from the database.

Do not silently rely on the prompt.

--------------------------------------------------
5. HISTORICAL DATA IS IMMUTABLE
--------------------------------------------------

Do NOT modify:

research_runs
research_raw_results
research_findings
relationship_candidates
relationship_observations
relationship_evidence
relationship_observation_evidence
relationship_recovery_evidence
relationship_observation_recovery_evidence
external identity history
resolution history
provider attempt history
traversal history
frontier history

The Stage 2 dataset remains the historical audit record.

CCR V1 records must be new additive records.

--------------------------------------------------
6. USE THE CANONICAL EVIDENCE RESOLVER
--------------------------------------------------

For every historical observation use the Stage 1.1 canonical evidence resolver.

It must recognize:

DIRECT_ORDINARY

NORMALIZED_ORDINARY

RECOVERY

and deduplicate evidence reachable by multiple mechanisms.

Do not create another evidence-resolution implementation.

All migrated evidence lineage must originate from this canonical resolution.

--------------------------------------------------
7. CREATE A DETERMINISTIC MIGRATION RUN
--------------------------------------------------

Introduce or use an existing run/audit mechanism to identify this controlled migration.

The run must have:

stable run identifier
stage identifier
policy version
ontology version
source database/schema version
input fingerprint
as-of date
created timestamp
status

Suggested stage name:

CCR_V1_3M_CONTROLLED_REVALIDATION

The same inputs + same policy version must produce the same V1 result.

Rerunning the migration must not create duplicate:

documents
passages
claims
identity links
relationships
relationship versions
qualifiers
events
coverage rows

Idempotence is required.

--------------------------------------------------
8. DOCUMENT MIGRATION RULE
--------------------------------------------------

For every historical evidence item used by the four observations, determine what is actually retained.

Do not invent content.

Possible cases include:

A. historical reference/excerpt only

Use:

retention_mode = LEGACY_REFERENCE

Replay capability must reflect reality:

PASSAGE_REPLAY
PARTIAL_REPLAY
or
NO_REPLAY

Never FULL_REPLAY.


B. retained cached body exists and can be deterministically tied to the evidence item

Only then may a stronger retention representation be used.

Do not automatically classify cached material as FULL_SNAPSHOT.

Verify:

body identity
content hash
source reference
lineage

before doing so.


C. evidence reference exists but exact excerpt cannot be verified

Represent honestly.

Do not fabricate a passage.

Do not mark verified excerpt if verification is impossible.

--------------------------------------------------
9. DOCUMENT DEDUPLICATION
--------------------------------------------------

The same underlying source document must not become multiple CCR V1 documents merely because:

SEC
Web
recovery
or historical ingestion

retrieved or referenced it differently.

Use deterministic source/document identity where possible.

Retrieval mechanism remains separate from source class.

Example:

retrieval mechanism:
WEB

underlying source:
SEC filing

source class:
REGULATORY_FILING

must not become independent corroboration.

--------------------------------------------------
10. PASSAGE MIGRATION
--------------------------------------------------

Create ccr_v1_passages only where an exact historical excerpt/text is actually retained.

Preserve:

exact excerpt
source reference
historical evidence identifier
hash if available
locator/page/offset only if actually known
verification capability
provenance

Do NOT invent:

page
offset
section
document position

when the old evidence does not contain it.

Historical excerpt-only passages should remain visibly legacy-limited.

--------------------------------------------------
11. ATOMIC CLAIM EXTRACTION
--------------------------------------------------

Convert the retained 3M evidence into atomic CCR V1 claims.

This is a deterministic migration/revalidation exercise.

Do not merely copy the historical relationship label into claim.relationship_type.

Read the persisted evidence/excerpt.

Represent exactly what the source states.

One passage may create multiple independent atomic claims.

Example:

a passage may separately state:

A retains a 19.9% interest in B

and

A and B entered transition service arrangements

Those are separate claims.

Do not collapse them into:

strategic_partner

unless the source itself makes a qualifying partnership claim and the V1 ontology permits it.

--------------------------------------------------
12. CLAIM DISCIPLINE
--------------------------------------------------

Each atomic claim must represent one assertion.

Do not create compound claims such as:

"A owns and controls and supplies B"

Create separate claims when separate facts are stated.

A claim may have:

resolved subject legal entity
resolved object legal entity

or:

unresolved subject/object mention

Do not create placeholder legal entities merely to complete a relationship.

Unresolved endpoints remain unresolved claims.

--------------------------------------------------
13. IDENTITY GATE COMES BEFORE CLIENT CONNECTION
--------------------------------------------------

A V1 relationship connects:

LEGAL ENTITY
to
LEGAL ENTITY

A client-to-client interpretation additionally requires qualifying Client Record <-> Legal Entity identity links.

Do NOT assume:

GFCID = legal entity

Do NOT infer VERIFIED identity from:

name equality alone
CAGID
CAGID_NAME
beneficial_owner_gfcid
legal_entity_id without established semantics
lei_legal_name alone
fuzzy similarity

No fuzzy merge.

--------------------------------------------------
14. INTERNAL CLIENT ENDPOINTS
--------------------------------------------------

3M and 3M India are represented in the Client Universe.

That fact alone does not establish their legal-entity identity.

For each, inspect existing local deterministic identifiers and historical/provider identity evidence.

If existing evidence is sufficient for an EXACT or ASSOCIATED legal-entity link under current CCR rules, create the corresponding link with explicit provenance.

Otherwise use:

UNVERIFIED

or:

PROBABLE

as appropriate.

Do NOT promote to VERIFIED merely so a V1 relationship can be created.

If the subject identity remains insufficient for an accepted entity relationship, report:

IDENTITY_BLOCKED

rather than weakening the identity gate.

--------------------------------------------------
15. EXISTING CABOT AND SOLVENTUM ENTITY RECORDS
--------------------------------------------------

The existing external_entities rows for Cabot and Solventum remain the current legal-entity storage boundary.

Reuse them when appropriate.

Do not create duplicate legal entities.

Preserve their existing:

external_entity_id
canonical name
provider identifiers
identity evidence
resolution history

Create CCR V1 identity-link/support records only when justified by existing deterministic evidence.

Do not convert historical AMBIGUOUS internal-match status into VERIFIED.

--------------------------------------------------
16. V1 RELATIONSHIP TYPES
--------------------------------------------------

ACTIVE V1 relationship types:

owns
controls
lends_to
provides_credit_support
supplies
depends_on_products_of

PASSIVE / OPPORTUNISTIC ontology-supported types:

manages
licenses_to
partners_with
litigates_against

Deferred:

provides_professional_services_to
broad passive equity harvesting
regulatory relationships
natural-person external enrichment
organisation-grain relationships

The historical Stage 2 labels:

subsidiary
legal_counterparty
equity_investor
strategic_partner

are NOT V1 relationship types.

They must be revalidated.

--------------------------------------------------
17. HISTORICAL `subsidiary` REVALIDATION
--------------------------------------------------

Do not simply rename:

subsidiary
->
controls

Inspect the source evidence.

`controls` may be accepted only when the evidence explicitly establishes control through something such as:

subsidiary/consolidation statement
controlled-by statement
accounting consolidation
voting control
general-partner structure
explicit contractual control

If the source is an SEC Exhibit 21 or equivalent and identifies the entity as a subsidiary, that may support:

controls

with:

control_basis = SUBSIDIARY_DISCLOSURE

Do not infer ownership percentage.

`owns` must remain independent.

Only create an owns claim/version if the source actually provides sufficient ownership evidence.

Do not assume:

subsidiary = 100% owned

--------------------------------------------------
18. HISTORICAL `equity_investor` REVALIDATION
--------------------------------------------------

Do not preserve `equity_investor` as a V1 relationship type.

Inspect the actual evidence.

If the source explicitly states that 3M owns/retains a stake in Solventum, create:

owns

Direction:

3M -> Solventum

If a percentage is explicitly stated, create an independently evidenced qualifier:

ownership_percentage

Preserve direct/indirect basis exactly as stated.

Never invent a percentage.

An accepted owns relationship must satisfy the frozen V1 evidence rule.

Primary evidence is sufficient.

Single secondary evidence alone is not sufficient for ACCEPTED.

--------------------------------------------------
19. HISTORICAL `strategic_partner` REVALIDATION
--------------------------------------------------

`strategic_partner` is not a V1 relationship type.

Do not map it automatically to:

partners_with

Read the actual retained evidence.

Possible decompositions include:

supplies
licenses_to
partners_with
event/context only
no supported V1 relationship

Examples:

transition services agreement
may support:
supplies

licensing agreement
may support:
licenses_to

specifically scoped collaboration agreement
may support:
partners_with

generic wording such as:
strategic partner
technology partner
ecosystem partner

without described scope is NOT sufficient for an accepted V1 relationship.

One historical strategic_partner observation may produce:

0
1
or multiple

V1 atomic claims/relationships.

That is acceptable.

--------------------------------------------------
20. HISTORICAL `legal_counterparty` REVALIDATION
--------------------------------------------------

`legal_counterparty` is not a V1 relationship type.

Do not migrate it directly.

Inspect the actual Cabot evidence.

Potential outcomes include:

A. litigates_against

Only if evidence clearly establishes:

plaintiff/claimant
->
defendant/respondent

for an identifiable case.

Direction must be explicit.

Regulatory enforcement is excluded.


B. event-only

If the retained evidence describes a:

settlement
legal resolution
transaction
indemnity event

without a qualifying persistent V1 relationship, represent the appropriate event/context only.


C. unsupported V1 relationship

If the historical evidence merely establishes that Cabot is a legal counterparty but does not satisfy a V1 relationship type:

do not create a relationship.

Preserve the claim/evidence and classify the historical observation as revalidation-rejected or not-mappable.

Do not manufacture a V1 edge simply to preserve historical graph density.

--------------------------------------------------
21. `supplies` ACCEPTANCE RULE
--------------------------------------------------

For any 3M evidence that may support supplies:

Direction:

supplier -> customer

Accept existence if:

PRIMARY evidence explicitly states supply relationship

OR

two independent approved secondary sources corroborate it.

Examples sufficient:

"X supplies Y to A"

"X is our supplier"

named filed supply agreement

Named supplier list may support existence but not unstated qualifiers.

Insufficient:

co-mention
product use
compatibility
generic relationship wording

--------------------------------------------------
22. `depends_on_products_of` RULE
--------------------------------------------------

Direction:

dependent -> producer

Requires explicit dependency language such as:

rely on
depend on
critical input
essential component
sole-source
single-source
no readily available substitute

Mere usage or incorporation is insufficient.

The producer must resolve to a Legal Entity.

--------------------------------------------------
23. `partners_with` RULE
--------------------------------------------------

V1 passive type.

Requires:

named agreement

or:

specifically described scoped collaboration

in PRIMARY evidence.

Generic marketing partnership wording is not sufficient.

Do not use `partners_with` as a catch-all for any commercial agreement.

--------------------------------------------------
24. `licenses_to` RULE
--------------------------------------------------

V1 passive type.

Only migrate if the retained source demonstrates a meaningful named IP/technology licence.

Ordinary enterprise/software/SaaS usage does not qualify.

Direction:

licensor -> licensee

--------------------------------------------------
25. `litigates_against` RULE
--------------------------------------------------

Direction:

plaintiff/claimant -> defendant/respondent

Requires PRIMARY evidence such as:

court record
filed litigation disclosure

Parties and roles must be sufficiently clear.

Settlement itself is an event, not automatically a persistent litigation relationship.

--------------------------------------------------
26. EVIDENCE BASIS
--------------------------------------------------

Use only:

PRIMARY
CORROBORATED
SINGLE_SECONDARY
INSUFFICIENT

No HIGH/MEDIUM/LOW numerical or ordinal confidence controls acceptance.

Historical confidence may remain in lineage metadata but must not decide V1 acceptance.

PRIMARY includes appropriate:

REGISTRY
REGULATORY_FILING
ISSUER_FILING
ISSUER_IR where allowed by type
OFFICIAL_TRANSACTION_DOCUMENT
GOVERNMENT
EXCHANGE_FILING

CORROBORATED requires at least two genuinely independent approved secondary sources.

Do not double-count syndicated or derivative sources.

--------------------------------------------------
27. RELATIONSHIP VERSION STATES
--------------------------------------------------

Use:

CANDIDATE
ACCEPTED
DISPUTED
REJECTED

Freshness is separate.

Temporal validity is separate.

Evidence basis is separate.

Do not create a relationship version merely because the historical Stage 2 observation was ACCEPTED.

The new V1 version must satisfy V1 rules.

--------------------------------------------------
28. QUALIFIERS
--------------------------------------------------

Qualifiers must be evaluated separately from the base relationship.

Potential relevant 3M qualifiers include:

ownership_percentage
ownership_basis
control_basis
agreement_name
product_or_service_category
described_as_critical
described_as_strategic
sole_source
single_source
revenue_share
spend_share

Do not create a qualifier unless supported by evidence.

A base relationship can be ACCEPTED while a qualifier is:

CANDIDATE
DISPUTED
UNKNOWN

Do not hold back a valid base relationship merely because an optional qualifier is weak.

--------------------------------------------------
29. EVENT USE
--------------------------------------------------

Use the new event model where historically retained evidence actually describes an event.

Potential 3M examples may include:

spin-off
settlement
agreement signing
transition arrangement
transaction completion

Do not create an event simply because one is expected from general knowledge.

Use only persisted evidence.

Creating an event must not automatically create a relationship.

--------------------------------------------------
30. COVERAGE
--------------------------------------------------

This stage is not a complete research campaign.

Therefore do NOT claim systematic:

RESEARCHED_NONE_FOUND

for any active family merely because the four historical observations did not contain that family.

Coverage for this controlled migration should explicitly indicate its bounded scope.

Appropriate states may include:

NOT_RESEARCHED

or:

PARTIAL

depending on what the migrated evidence represents.

This migration is:

historical-evidence revalidation

not:

complete 3M enrichment research.

Do not claim full ownership/control/financing/supply coverage.

--------------------------------------------------
31. HISTORICAL-TO-V1 DISPOSITION
--------------------------------------------------

For each of the four historical observations assign one or more migration dispositions.

Use:

CONFIRMED
RECLASSIFIED
DOWNGRADED
REJECTED
EVENT_ONLY
IDENTITY_BLOCKED
EVIDENCE_LIMITED

Definitions:

CONFIRMED
The same factual relationship survives and maps directly enough to a V1 relationship.

RECLASSIFIED
The underlying fact survives but maps to a different V1 type or multiple V1 claims.

DOWNGRADED
Historical accepted observation becomes only CANDIDATE under V1.

REJECTED
Historical observation does not meet any V1 relationship rule.

EVENT_ONLY
Evidence supports an event but not a persistent V1 relationship.

IDENTITY_BLOCKED
Relationship evidence may be adequate but endpoint identity gate prevents accepted relationship creation.

EVIDENCE_LIMITED
Stored historical evidence is insufficient for deterministic V1 acceptance and no refetch is allowed in this stage.

Multiple dispositions may be recorded where necessary, but explain them.

--------------------------------------------------
32. EXPECT DIFFERENT COUNTS
--------------------------------------------------

Do NOT target:

4 historical observations
=
4 V1 relationships

The correct V1 count may be:

less than 4
equal to 4
greater than 4

because:

one historical observation may produce no V1 relationship

or:

one historical observation may decompose into multiple atomic V1 relationships.

Correct evidence semantics matter more than preserving historical graph density.

--------------------------------------------------
33. MIGRATION LINEAGE
--------------------------------------------------

Every V1 object created from historical data must preserve lineage sufficient to trace back to:

historical observation ID
historical candidate ID if relevant
historical evidence ID
recovery evidence ID if relevant
research run
source reference
migration run
policy version
ontology version

Do not require an analyst to reverse-engineer lineage from free text.

If existing provenance JSON is sufficient, use it consistently.

If a tiny additive crosswalk structure is necessary, add the minimum schema required.

Do not redesign the whole schema.

--------------------------------------------------
34. IDEMPOTENCE
--------------------------------------------------

Run this controlled migration at least twice or use the repository's deterministic replay mechanism.

Second execution must create:

0 duplicate documents
0 duplicate passages
0 duplicate claims
0 duplicate identity links
0 duplicate relationships
0 duplicate relationship versions
0 duplicate qualifiers
0 duplicate events
0 duplicate coverage rows

Report replay results.

--------------------------------------------------
35. NO BROAD ONTOLOGY MIGRATION
--------------------------------------------------

Only migrate/revalidate evidence connected to the 3M pilot.

Do NOT migrate all historical relationship observations.

Do NOT migrate all 14 candidates beyond what is necessary to preserve the four-observation evidence lineage.

Do NOT perform Client Universe-wide enrichment.

Do NOT bulk-create identity links.

--------------------------------------------------
36. OPTIONAL CANDIDATE CONTEXT
--------------------------------------------------

The 14 historical candidates may be inspected when required to understand lineage of evidence supporting the four accepted observations.

Do not migrate unrelated candidate relationships into V1 production records during this stage.

If a candidate contains evidence essential to an accepted historical observation, preserve that lineage.

--------------------------------------------------
37. DO NOT PERFORM NEW PATH DISCOVERY
--------------------------------------------------

No:

traversal expansion
frontier research
hidden relationship mining
client-connection pattern calculation
shared-supplier calculation
shared-controller calculation
shared-lender calculation

This stage validates V1 facts for one known pilot.

Client connections come later.

--------------------------------------------------
38. API
--------------------------------------------------

Do not build broad V1 APIs yet.

If necessary, add a minimal read-only diagnostic endpoint only if repository conventions genuinely require one.

Prefer repository/report/test validation over adding an API.

No frontend integration.

--------------------------------------------------
39. DATABASE SCHEMA
--------------------------------------------------

Current schema is v10.

Do not increment the schema merely because data is populated.

Only migrate to v11 if a genuinely necessary small structural addition is required for deterministic historical lineage or migration-run metadata.

If no schema change is needed:

remain at v10.

Explain the decision.

--------------------------------------------------
40. REQUIRED TESTS
--------------------------------------------------

Preserve all 63 existing tests.

Add focused migration/revalidation tests covering:

1. migration is deterministic.

2. migration is idempotent.

3. historical Stage 2 rows remain unchanged.

4. LEGACY_REFERENCE evidence cannot become FULL_REPLAY.

5. document deduplication works across retrieval mechanisms.

6. passage requires actual retained excerpt.

7. passage locator is not fabricated.

8. one passage may generate multiple atomic claims.

9. claim is distinct from accepted relationship.

10. unresolved endpoint does not create placeholder Legal Entity.

11. weak identity blocks client-to-client acceptance.

12. PROBABLE identity does not behave as VERIFIED.

13. REJECTED identity is excluded.

14. no fuzzy merge.

15. subsidiary label is not automatically converted to owns.

16. subsidiary evidence can support controls only when evidence satisfies the rule.

17. ownership percentage is not inferred.

18. equity_investor label is not preserved as V1 type.

19. strategic_partner is not automatically mapped to partners_with.

20. legal_counterparty is not a V1 relationship type.

21. settlement event does not automatically create litigates_against.

22. accepted relationship requires sufficient evidence basis.

23. SINGLE_SECONDARY does not satisfy a PRIMARY-required rule.

24. qualifier state is independent of base relationship state.

25. event does not automatically create relationship.

26. controlled migration does not produce RESEARCHED_NONE_FOUND for unsearched families.

27. no provider call occurs.

28. Client Universe remains unchanged.

29. source master remains unchanged.

30. canonical historical evidence resolver remains aligned with graph/API behavior.

--------------------------------------------------
41. 3M COMPARISON REPORT
--------------------------------------------------

Produce a clear before/after table:

HISTORICAL OBSERVATION
HISTORICAL TYPE
HISTORICAL ACCEPTANCE
HISTORICAL EVIDENCE
V1 ATOMIC CLAIM(S)
IDENTITY GATE
V1 RELATIONSHIP TYPE
V1 VERSION STATE
V1 EVIDENCE BASIS
QUALIFIERS
EVENTS
DISPOSITION
RATIONALE

Do this for all four observations.

Do not hide a rejected or downgraded result.

--------------------------------------------------
42. V1 OBJECT COUNTS
--------------------------------------------------

Report exact created counts for:

ccr_v1_identity_links
ccr_v1_documents
ccr_v1_passages
ccr_v1_claims
ccr_v1_identity_link_support
ccr_v1_relationships
ccr_v1_relationship_versions
ccr_v1_relationship_support
ccr_v1_qualifiers
ccr_v1_enrichment_coverage
ccr_v1_events

Also report counts by:

relationship type
relationship acceptance state
evidence basis
identity state
retention mode
migration disposition

--------------------------------------------------
43. SOURCE MASTER INTEGRITY
--------------------------------------------------

Verify:

backend/Customer_latest.parquet

Expected:

3,670,650 rows
3,670,650 unique GFCIDs

Verify source hash if available.

Modifications:

0

--------------------------------------------------
44. CLIENT UNIVERSE INTEGRITY
--------------------------------------------------

Verify:

backend/data/client_universe.sqlite3

Expected:

3,670,650 client_master rows
3,670,650 unique GFCIDs

No rows inserted
No rows updated
No rows deleted

--------------------------------------------------
45. NO FRONTEND
--------------------------------------------------

Frontend files modified:

0

Do not build:

network map
relationship workspace
evidence panel
dashboard
client connection UI

--------------------------------------------------
46. CREATE REPORT
--------------------------------------------------

Create:

backend/data/CCR_V1_3M_CONTROLLED_REVALIDATION_REPORT.md

Required sections:

1. Executive result
2. Scope and non-actions
3. Migration run identity
4. Historical 3M baseline
5. Evidence inventory used
6. Document migration
7. Passage migration
8. Atomic claims produced
9. Identity-link evaluation
10. 3M India revalidation
11. Cabot revalidation
12. Solventum ownership revalidation
13. Solventum strategic-partner revalidation
14. Event migration
15. Relationship/version results
16. Qualifier results
17. Coverage results
18. Historical-to-V1 disposition table
19. V1 object counts
20. Idempotence/replay result
21. Test result
22. SQLite integrity
23. Client Universe integrity
24. Source-master integrity
25. External-call verification
26. Remaining evidence limitations
27. Remaining identity limitations
28. Recommended next action

--------------------------------------------------
47. IMPORTANT INTERPRETATION RULE
--------------------------------------------------

If existing evidence cannot support a V1 relationship without refetching:

do not refetch.

Mark the result:

EVIDENCE_LIMITED

or:

DOWNGRADED

or:

REJECTED

as appropriate.

The purpose of this stage is to discover what the stored historical evidence can defensibly support under V1.

It is NOT to preserve the old result.

--------------------------------------------------
48. ABSOLUTE CONSTRAINTS
--------------------------------------------------

External provider calls:
0

New external research:
0

New frontier research:
0

Stage 2A.8:
0

Fuzzy merges:
0

Synthetic path edges:
0

Historical Stage 2 row modifications:
0

Client Universe modifications:
0

Source-master modifications:
0

Frontend modifications:
0

No relationship may be accepted merely because Stage 2 historically accepted it.

--------------------------------------------------
49. FINAL STATUS FORMAT
--------------------------------------------------

At completion output exactly:

CCR V1 — 3M CONTROLLED REVALIDATION

Status:
PASS / PARTIAL / FAIL

Relationship schema version:

Migration run:

Historical Stage 2 rows modified:

Client Universe rows:
Client Universe modifications:
Source-master modifications:

External provider calls:

Historical 3M accepted observations:
4

Historical graph-visible edges:
4

Historical observations revalidated:

V1 documents created:

V1 passages created:

V1 atomic claims created:

V1 identity links created:

VERIFIED identity links:
PROBABLE identity links:
UNVERIFIED identity links:
REJECTED identity links:

V1 relationships created:

V1 relationship versions created:

ACCEPTED:
CANDIDATE:
DISPUTED:
REJECTED:

V1 qualifiers created:

V1 events created:

Disposition counts:

CONFIRMED:
RECLASSIFIED:
DOWNGRADED:
REJECTED:
EVENT_ONLY:
IDENTITY_BLOCKED:
EVIDENCE_LIMITED:

3M India result:

Cabot result:

Solventum ownership result:

Solventum strategic-partner result:

RESEARCHED_NONE_FOUND rows created:
0 unless a completed defined research scope genuinely exists

Migration replay/idempotence:
PASS / FAIL

Duplicate V1 objects after replay:

Fuzzy merges:

Synthetic direct edges:

New paths:

Frontend files modified:

Backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Report:
backend/data/CCR_V1_3M_CONTROLLED_REVALIDATION_REPORT.md

Recommended next action:

Do not perform new research, client-connection mining, or frontend work automatically.
