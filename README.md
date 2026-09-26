IMPLEMENT WITH LUNA

CCR — CLIENT CORRELATION
V1 STAGE 3 — CONTROLLED LEGAL ENTITY IDENTITY RESOLUTION PILOT

This is an implementation/execution stage.

It is NOT another architecture audit.

The purpose is to resolve the identity blocker discovered during the completed 3M V1 controlled revalidation so that existing evidence-backed claims can become real CCR V1 relationships where the identity gate is satisfied.

Do not continue into correlation-engine development automatically after completing this stage.

==================================================
1. CURRENT VERIFIED BASELINE
==================================================

CCR V1 Foundation Stage 1:
COMPLETE

CCR V1 Foundation Stage 1.1:
COMPLETE

3M controlled V1 revalidation:
COMPLETE

Current relationship schema:
v10

Authoritative Client Universe:
backend/Customer_latest.parquet

Expected source properties:

3,670,650 rows
3,670,650 unique GFCIDs

Runtime Client Universe:

backend/data/client_universe.sqlite3

Expected:

3,670,650 client_master rows
3,670,650 unique GFCIDs

Current 3M root:

client_id:
437487

GFCID:
0000426083

legal_name:
3M CO

Current V1 3M revalidation result:

V1 documents:
2

V1 passages:
6

V1 atomic claims:
9

V1 coverage rows:
2

V1 events:
1

V1 identity links:
0

V1 relationships:
0

V1 relationship versions:
0

V1 qualifiers:
0

The reason there are zero V1 relationships is the Legal Entity identity gate.

Existing claims were intentionally not promoted where the Client Record -> Legal Entity identity had not been established.

Historical Stage 2 data remains immutable.

==================================================
2. PRIMARY OBJECTIVE
==================================================

Create production-quality CCR V1 identity links where defensible between selected Client Universe records and real-world Legal Entities.

Primary target:

3M Client Record
client_id 437487
GFCID 0000426083
legal_name 3M CO

Secondary target:

the exact Client Universe record representing 3M India Ltd used in the historical 3M pilot.

Additional match-back targets:

Solventum Corporation
Cabot Corporation

The goal is to determine whether these real-world Legal Entities are represented in the 3.67M Client Universe and, where evidence is strong enough, create governed V1 identity links.

After identity resolution, re-evaluate ONLY the already-existing V1 3M claims.

Do not perform new relationship discovery.

==================================================
3. THIS IS IDENTITY RESOLUTION, NOT RELATIONSHIP RESEARCH
==================================================

Allowed activity:

Legal Entity identity resolution
strong-identifier lookup
official-source entity verification
Client Universe exact identifier match-back
identity-support persistence
existing V1 claim re-evaluation after identity resolution

Not allowed:

supplier discovery
customer discovery
lender discovery
ownership discovery beyond already-persisted claims
dependency research
litigation research
partner research
new relationship research
frontier expansion
hidden-path discovery
Stage 2A.8
broad enrichment

Identity-provider information must not automatically become relationship evidence.

==================================================
4. IDENTITY MODEL
==================================================

Use the existing approved CCR V1 identity-link contract.

link_type:

EXACT
ASSOCIATED

link_state:

VERIFIED
PROBABLE
UNVERIFIED
REJECTED

EXACT means:

the Client Record and Legal Entity refer to the same real-world Legal Entity.

ASSOCIATED means:

the Client Record represents an explicitly evidenced branch, booking capacity, operating capacity, or other governed association with that Legal Entity.

ASSOCIATED must NOT mean:

same corporate group
subsidiary
parent
affiliate
shared CAGID
shared beneficial owner

Those are not identity.

==================================================
5. STRICT IDENTITY PRINCIPLES
==================================================

Do NOT assume:

1 GFCID = 1 Legal Entity

Do NOT automatically treat:

GFCID
CAGID
CAGID_NAME
beneficial_owner_gfcid
legal_entity_id
lei_legal_name
legal_name
alias
account type
customer type
GFCID type

as sufficient Legal Entity proof by themselves.

Do NOT use:

fuzzy name matching
edit distance
token similarity
embedding similarity
LLM similarity
name popularity

to create a VERIFIED identity link.

Search candidate != identity proof.

==================================================
6. STRONG IDENTIFIER PRIORITY
==================================================

Resolve identity using strong identifiers first.

Potential strong identity evidence includes, where semantics are established:

LEI
CIK
official registry identifier
official incorporation/company identifier
other approved stable Legal Entity identifier

For every identifier used as proof, validate:

identifier type
identifier value
issuing/source authority
entity legal name
entity status where relevant
jurisdiction where relevant
consistency with the Client Record

Do not assume the Client Universe field:

legal_entity_id

is an LEI merely because it contains an LEI-shaped value.

Validate what it actually represents.

==================================================
7. EXTERNAL SOURCES AUTHORIZED
==================================================

Unlike the previous offline stages, this stage MAY use external identity sources.

Authorized providers:

GLEIF
SEC

Web may be used only as a narrowly scoped fallback for official/primary Legal Entity identity evidence.

Web must NOT be used for broad relationship discovery.

All provider calls must be recorded.

==================================================
8. GLEIF ROLE
==================================================

GLEIF is an identity source.

Use GLEIF for:

LEI lookup
official Legal Entity name
entity status
registered address/jurisdiction where relevant
identifier verification

GLEIF search ranking is not identity proof.

A candidate returned from GLEIF becomes VERIFIED only when deterministic evidence supports the match.

Do not use GLEIF Level 2 to create ownership relationships in this stage.

Do not create:

owns
controls

from GLEIF relationship data during this identity stage.

==================================================
9. SEC ROLE
==================================================

SEC is an identity source where applicable.

Use:

CIK
registrant legal name
filing entity metadata
official ticker/CIK mapping where appropriate

Do not use:

ticker alone
filing co-mention
subsidiary mention
brand mention

as standalone identity proof.

Ensure SEC User-Agent and transport configuration are correct before making calls.

Persist provider-attempt audit records.

==================================================
10. WEB FALLBACK ROLE
==================================================

Web is permitted only when GLEIF/SEC cannot resolve the identity and an official primary identity source is required.

Allowed examples:

official company registry
official issuer legal page
government corporate registry
official exchange filing identity page

Do not use general news or search-result snippets as VERIFIED identity proof.

Do not perform broad open-web research.

==================================================
11. RESOLVE 3M FIRST
==================================================

For:

client_id 437487
GFCID 0000426083
legal_name 3M CO

Inspect all current Client Universe identity context first.

Report:

GFCID
legal_name
legal_entity_id
lei_legal_name
CAGID
CAGID_NAME
aliases
GFCID type
customer type
account type
other normalized identifiers

Then resolve the corresponding real-world Legal Entity.

Try to establish:

link_type = EXACT

link_state = VERIFIED

only if deterministic evidence supports it.

If evidence supports only a weaker state:

use PROBABLE or UNVERIFIED.

Do not promote for convenience.

==================================================
12. 3M LEGAL ENTITY RECORD
==================================================

Before creating a new external Legal Entity:

search existing external_entities using strong identifiers and existing canonical identity data.

If the Legal Entity already exists:

reuse it.

If no valid record exists and the identity is sufficiently established:

create exactly one Legal Entity record using the existing legal-entity storage boundary.

Preserve:

canonical legal name
strong identifier(s)
source
jurisdiction if known
status if available
identity provenance

Do not create a generic "3M group" organization node.

==================================================
13. IDENTITY SUPPORT
==================================================

Every created CCR V1 identity link must have explicit support.

Use:

ccr_v1_identity_link_support

or the current approved support contract.

Persist enough information to answer:

Which source proved this?
Which identifier was used?
What identifier type?
What Legal Entity did it identify?
What Client Record was linked?
What decision rule was used?
Which policy version?
Which provider?
When was the decision made?
What was the as-of date?
Why was the state VERIFIED / PROBABLE / UNVERIFIED?

Do not rely on free-text explanation alone.

==================================================
14. RESOLVE 3M INDIA
==================================================

Identify the exact internal Client Universe record used by historical observation 1.

Verify from current persisted data:

client_id
GFCID
legal_name
legal_entity_id
lei_legal_name
aliases
other available identifiers

Then resolve the real-world Legal Entity represented by that Client Record.

Do not rely solely on the name "3M India Ltd".

Attempt strong-identifier identity proof.

If deterministic evidence supports it:

create:

EXACT + VERIFIED

Otherwise preserve the appropriate weaker state.

Do not create a relationship simply because the historical relationship said subsidiary.

==================================================
15. SOLVENTUM — REUSE EXISTING LEGAL ENTITY
==================================================

An external Solventum Legal Entity already exists.

Do not create another one.

Inspect its:

external_entity_id
canonical legal name
provider identifiers
identity evidence
resolution history
LEI if available
CIK if available
other strong identifiers

Use this existing Legal Entity as the real-world entity anchor.

==================================================
16. SOLVENTUM CLIENT UNIVERSE MATCH-BACK
==================================================

Determine whether the exact Solventum Legal Entity is represented in the 3.67M Client Universe.

Search using:

strong identifiers first

Then exact deterministic supporting metadata.

Possible outcomes:

VERIFIED
PROBABLE
AMBIGUOUS
NO_MATCH
INSUFFICIENT

If exactly one Client Universe record is proven to represent the same Legal Entity:

create:

EXACT + VERIFIED

identity link.

If several Client Records are plausible:

do not choose arbitrarily.

Report:

AMBIGUOUS

unless evidence proves the role of each record.

==================================================
17. CABOT — REUSE EXISTING LEGAL ENTITY
==================================================

An external Cabot Legal Entity already exists.

Do not create another one.

Inspect the existing Legal Entity identity evidence and strong identifiers.

Then determine whether the same Legal Entity is represented in the Client Universe.

Use the same outcomes:

VERIFIED
PROBABLE
AMBIGUOUS
NO_MATCH
INSUFFICIENT

No fuzzy auto-link.

==================================================
18. MULTIPLE CLIENT RECORDS FOR ONE LEGAL ENTITY
==================================================

This is a critical rule.

If one Legal Entity appears to match several Client Universe records:

do not silently collapse them.

Do not assume duplicate GFCIDs.

Do not assume branch semantics.

Do not assume account-role semantics.

Create VERIFIED identity links only where the relationship between each Client Record and the Legal Entity is explicitly supportable.

Otherwise:

PROBABLE
UNVERIFIED
or no link

is acceptable.

==================================================
19. IDENTITY CONFLICTS
==================================================

If:

GLEIF
SEC
Client Universe identifiers
official registry data

conflict:

do not silently prefer one.

Record the conflict.

Use:

PROBABLE
UNVERIFIED
REJECTED

as appropriate.

Do not allow unresolved conflict to produce an accepted client-to-client correlation path.

==================================================
20. DO NOT USE RELATIONSHIP CLAIMS AS IDENTITY SHORTCUTS
==================================================

Existing evidence saying:

3M owns 75% of 3M India

does not automatically prove that:

Client Record 437487 = the Legal Entity described in that filing.

Identity must have its own support.

Likewise:

relationship evidence
!=
identity evidence

unless the same source passage explicitly and independently establishes Legal Entity identity.

==================================================
21. RE-EVALUATE EXISTING V1 CLAIMS AFTER IDENTITY
==================================================

Once identity resolution is complete, re-evaluate ONLY the existing claims created during:

CCR_V1_3M_CONTROLLED_REVALIDATION

Do not discover new claims.

Existing claims include ownership and commercial-context assertions.

For each claim previously marked:

IDENTITY_BLOCKED

re-evaluate the identity gate.

Possible outcomes:

remains blocked
becomes CANDIDATE relationship version
becomes ACCEPTED relationship version

depending on:

endpoint identity
relationship evidence
evidence basis
current V1 acceptance rules

==================================================
22. 3M -> 3M INDIA `owns`
==================================================

The controlled revalidation found evidence stating approximately:

75% ownership

Do not trust this prompt.

Use the already-persisted V1 claim/evidence.

If:

3M Legal Entity identity passes

and:

3M India Legal Entity identity passes

and:

existing evidence satisfies V1 owns acceptance

then create:

ccr_v1_relationships

relationship_type:
owns

direction:
3M Legal Entity -> 3M India Legal Entity

Create a relationship version with the correct:

acceptance state
evidence basis
dates/as-of metadata
policy version
ontology version

If the evidence explicitly states:

75%

then create:

ownership_percentage = 75%

as a qualifier supported by its own claim/evidence.

Do not infer:

controls

unless a separate controls claim exists and passes.

==================================================
23. 3M -> SOLVENTUM `owns`
==================================================

Existing V1 claims include explicit historical ownership assertions such as:

19.9%

and a later:

14.8%

Use only persisted claims.

If 3M identity passes and Solventum is already a resolved Legal Entity:

re-evaluate the ownership claims.

Do not overwrite the percentages.

Preserve temporal context.

Possible correct representation:

stable relationship:
owns

relationship versions / qualifier history:

ownership_percentage = 19.9
observed/effective context A

ownership_percentage = 14.8
observed/effective context B

Do not invent exact effective dates when the source only gives observation/reporting context.

==================================================
24. SOLVENTUM COMMERCIAL / SUPPLY CLAIM
==================================================

The controlled revalidation found transition-services / commercial context.

Do not recreate historical:

strategic_partner

Do not automatically create:

partners_with

If an existing V1 atomic claim already explicitly satisfies:

supplies

then evaluate that existing claim under the V1 supplies rule after identity passes.

Direction must reflect:

supplier -> customer

based on the actual evidence.

Do not guess direction.

If evidence is insufficient:

leave it as a claim/candidate.

==================================================
25. CABOT RELATIONSHIP CLASSIFICATION
==================================================

Do NOT perform new Cabot legal research.

The previous revalidation found:

indemnification/legal context

but not sufficient evidence for:

litigates_against

Do not change that conclusion merely because identity becomes resolved.

This stage may resolve Cabot identity only.

No new Cabot relationship should be created unless an already-existing V1 claim independently qualifies under an already-existing acceptance rule.

==================================================
26. EVENT HANDLING
==================================================

Existing V1 event:

SPIN_OFF

must remain independent of relationships.

Do not let identity resolution automatically convert the event into:

owns
controls
partners_with
or any other relationship.

Preserve event/relationship separation.

==================================================
27. COVERAGE
==================================================

This stage is:

IDENTITY RESOLUTION
+
LIMITED RE-EVALUATION OF EXISTING CLAIMS

It is NOT a full relationship enrichment campaign.

Do not create:

RESEARCHED_NONE_FOUND

for broad relationship families.

Preserve:

PARTIAL

where appropriate.

==================================================
28. CORRELATION READINESS ASSESSMENT
==================================================

At the end, explicitly assess readiness for the next stage.

Answer these questions:

A.
Do we have at least one:

VERIFIED Client Record -> Legal Entity link?

B.
Do we have at least one:

ACCEPTED V1 Legal Entity relationship?

C.
Do we have any accepted relationship where BOTH Legal Entity endpoints map to Client Universe records through qualifying identity links?

D.
Can we demonstrate:

DIRECT correlation?

E.
Do we have sufficient accepted relationship topology to demonstrate any real two-hop derived correlation?

Examples:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN

Do not fabricate readiness.

Expected possible outcome:

DIRECT = READY

DERIVED MULTI-HOP = NOT_READY

That is acceptable.

==================================================
29. IMPORTANT — DO NOT BUILD CORRELATION YET
==================================================

Do NOT implement:

correlation definition tables
correlation configuration
correlation engine
shared-supplier logic
shared-controller logic
shared-customer logic
supply-chain logic
shared-lender logic
correlation API
correlation UI
AI Create Correlation

Those are the immediately following authorized design direction, but they are not part of this stage.

==================================================
30. SCHEMA
==================================================

Current schema:

v10

Prefer to stay at:

v10

unless a genuinely missing identity-audit structure requires an additive migration.

Do not increment the schema unnecessarily.

If a migration is required:

keep it minimal
additive
idempotent
replay-safe
foreign-key safe

Explain why.

==================================================
31. IDEMPOTENCE
==================================================

The identity-resolution run must be deterministic where inputs and external identity evidence are unchanged.

Run/replay the local persistence stage twice where practical.

Second execution must create:

0 duplicate Legal Entities
0 duplicate identity links
0 duplicate identity-support rows
0 duplicate relationships
0 duplicate relationship versions
0 duplicate qualifiers

Report all duplicate counts.

==================================================
32. PROVIDER AUDIT
==================================================

Record every external identity-provider call.

For each:

provider
entity target
query/identifier
purpose
HTTP/result status
cache status
network attempted
result
whether the result contributed to identity proof

Do not treat provider failure as:

NO_MATCH

Use:

UNAVAILABLE
or
INSUFFICIENT

where appropriate.

==================================================
33. REQUIRED TESTS
==================================================

Preserve all current backend tests.

Add focused tests covering at minimum:

1.
strong exact identifier can support VERIFIED EXACT identity.

2.
name-only match cannot create VERIFIED identity.

3.
alias-only match cannot create VERIFIED identity.

4.
CAGID cannot create VERIFIED identity.

5.
CAGID_NAME cannot create VERIFIED identity.

6.
beneficial_owner_gfcid cannot create VERIFIED identity.

7.
legal_entity_id is not assumed to be an LEI.

8.
lei_legal_name alone is not identity proof.

9.
FTS/search result is candidate discovery only.

10.
existing Legal Entity is reused by strong identifier.

11.
duplicate Legal Entity creation is prevented.

12.
ambiguous Client Universe matches remain non-VERIFIED.

13.
PROBABLE identity cannot satisfy strict client-correlation identity gate.

14.
UNVERIFIED identity cannot satisfy the strict gate.

15.
REJECTED identity cannot satisfy the gate.

16.
identity support is distinct from relationship support.

17.
identity-provider evidence cannot automatically create relationship claims.

18.
existing identity-blocked claim can be re-evaluated after VERIFIED identity exists.

19.
no new relationship claim is created by identity lookup.

20.
3M ownership qualifier is not fabricated.

21.
Solventum percentages remain separately evidenced.

22.
event does not automatically become relationship.

23.
Client Universe remains unchanged.

24.
source master remains unchanged.

25.
no fuzzy merge.

26.
identity resolution replay creates zero duplicates.

==================================================
34. CLIENT UNIVERSE INTEGRITY
==================================================

Verify:

backend/data/client_universe.sqlite3

Expected:

client_master rows:
3,670,650

unique GFCIDs:
3,670,650

No rows inserted.
No rows updated.
No rows deleted.

==================================================
35. SOURCE MASTER INTEGRITY
==================================================

Verify:

backend/Customer_latest.parquet

Expected:

rows:
3,670,650

unique GFCIDs:
3,670,650

Verify SHA-256 against the current established source hash.

No modifications.

==================================================
36. HISTORICAL STAGE 2 IMMUTABILITY
==================================================

Do not modify historical Stage 2 relationship/research rows.

Expected modification count:

0

Existing historical data remains audit history only.

==================================================
37. FRONTEND
==================================================

Frontend files modified:

0

Do not build any UI.

==================================================
38. CREATE REPORT
==================================================

Create:

backend/data/CCR_V1_IDENTITY_RESOLUTION_PILOT_REPORT.md

Required sections:

1. Executive result
2. Scope and non-actions
3. Input baseline
4. Identity policy
5. Provider activity summary
6. 3M Client Record identity context
7. 3M Legal Entity resolution
8. 3M identity-link decision
9. 3M India Client Record identification
10. 3M India Legal Entity resolution
11. 3M India identity-link decision
12. Solventum existing Legal Entity
13. Solventum Client Universe match-back
14. Cabot existing Legal Entity
15. Cabot Client Universe match-back
16. Strong identifiers used
17. Ambiguous matches
18. Identity conflicts
19. Identity-support records
20. Existing V1 claims re-evaluated
21. 3M -> 3M India ownership result
22. 3M -> Solventum ownership result
23. Solventum supply/transition-services result
24. Cabot result
25. Relationship/version counts
26. Qualifier counts
27. Coverage
28. Correlation-readiness assessment
29. Replay/idempotence
30. Tests
31. SQLite integrity
32. Client Universe integrity
33. Source-master integrity
34. Remaining identity limitations
35. Remaining GFCID-semantic unknowns
36. Recommended next action

==================================================
39. ABSOLUTE CONSTRAINTS
==================================================

New relationship discovery:
0

New frontier research:
0

Stage 2A.8:
0

Fuzzy identity merges:
0

Synthetic direct edges:
0

Historical Stage 2 modifications:
0

Client Universe modifications:
0

Source-master modifications:
0

Frontend modifications:
0

Do not create a VERIFIED identity merely to unblock correlation.

==================================================
40. FINAL STATUS FORMAT
==================================================

At completion output exactly:

CCR V1 — IDENTITY RESOLUTION PILOT

Status:
PASS / PARTIAL / FAIL

Schema version:

Client Universe rows:
Client Universe modifications:
Source-master modifications:
Historical Stage 2 modifications:

External identity-provider calls:

GLEIF:
SEC:
Web:

3M Client Record:
client_id:
GFCID:

3M Legal Entity:
external_entity_id:
canonical legal name:
LEI:
CIK:

3M identity link:
EXACT / ASSOCIATED / NONE

3M identity state:
VERIFIED / PROBABLE / UNVERIFIED / REJECTED / NONE

3M identity support count:

3M India Client Record:
client_id:
GFCID:

3M India Legal Entity:
external_entity_id:
canonical legal name:
LEI:
other strong identifier:

3M India identity link:
EXACT / ASSOCIATED / NONE

3M India identity state:
VERIFIED / PROBABLE / UNVERIFIED / REJECTED / NONE

Solventum existing Legal Entity reused:
YES / NO

Solventum Client Universe match:
VERIFIED / PROBABLE / AMBIGUOUS / NO_MATCH / INSUFFICIENT

Cabot existing Legal Entity reused:
YES / NO

Cabot Client Universe match:
VERIFIED / PROBABLE / AMBIGUOUS / NO_MATCH / INSUFFICIENT

New Legal Entities created:

Identity links created:

VERIFIED:
PROBABLE:
UNVERIFIED:
REJECTED:

Identity-support records created:

Existing V1 claims re-evaluated:

V1 relationships before:
V1 relationships after:

V1 relationship versions before:
V1 relationship versions after:

V1 ACCEPTED relationships:

V1 CANDIDATE relationships:

V1 qualifiers created:

3M -> 3M India owns:
ACCEPTED / CANDIDATE / IDENTITY_BLOCKED / EVIDENCE_BLOCKED / NOT_SUPPORTED

3M -> Solventum owns:
ACCEPTED / CANDIDATE / IDENTITY_BLOCKED / EVIDENCE_BLOCKED / NOT_SUPPORTED

3M -> Solventum supplies:
ACCEPTED / CANDIDATE / IDENTITY_BLOCKED / EVIDENCE_BLOCKED / NOT_SUPPORTED

Cabot relationship:
result:

External relationship research performed:
0

Fuzzy merges:
0

Synthetic direct edges:
0

Frontend files modified:
0

Correlation readiness:

At least one VERIFIED Client Record -> Legal Entity link:
YES / NO

At least one ACCEPTED V1 relationship:
YES / NO

At least one accepted relationship with qualifying Client Universe identity at both endpoints:
YES / NO

DIRECT correlation:
READY / NOT_READY

DERIVED multi-hop correlation:
READY / NOT_READY

Backend tests:
passed / failed / skipped

SQLite foreign-key check:

SQLite quick check:

Replay/idempotence:
PASS / FAIL

Duplicate objects on replay:

Report:
backend/data/CCR_V1_IDENTITY_RESOLUTION_PILOT_REPORT.md

Recommended next action:

If identity and at least one V1 relationship are sufficiently proven, recommend:

CCR V1 — CORRELATION CONFIGURATION + CORRELATION ENGINE FOUNDATION

Do not begin that next stage automatically.
