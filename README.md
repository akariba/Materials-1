CLIENT CORRELATION — STAGE 2A.5
PROVIDER READINESS + BOUNDED UNRESOLVED RELATIONSHIP RECOVERY

Stage 2A.4 is complete.

Current bounded 3M state:

- 14 candidates
- 7 named candidates
- 6 generic descriptors retained unresolved
- 1 no-evidence finding
- 2 external entities
- 2 accepted relationship observations in bounded graph
- 4 named endpoints still unresolved
- 0 paths
- 0 fuzzy merges
- 0 synthetic shortcut edges

IMPORTANT PROVIDER STATE FROM STAGE 2A.4:

GLEIF: operational
SEC: NOT CALLED because SEC_USER_AGENT is not configured
Approved Web: NOT_CONFIGURED

OBJECTIVE

Do NOT broaden research to the 3.67M universe.

First make the preserved SEC and approved Web provider paths operational,
then rerun a tightly bounded recovery pass only against:

1. the four remaining named unresolved endpoints from Stage 2A.4;
2. the existing Solventum candidate findings;
3. the existing Cabot finding only as a regression/control case.

Do not perform new broad discovery.

==================================================
1. SEC READINESS
==================================================

Inspect the preserved SEC provider implementation and configuration.

Use environment/configuration only.

Do NOT hard-code identity credentials or personal secrets.

Configure the SEC User-Agent through the supported environment/config path.

The User-Agent must comply with the existing SEC provider implementation
and SEC access requirements.

Perform a minimal SEC connectivity/readiness test.

Report:

SEC configuration state
SEC transport state
HTTP status
TLS verification state
provider readiness

Do not disable TLS verification.
Do not bypass approved network/proxy configuration.

==================================================
2. APPROVED WEB READINESS
==================================================

Inspect the preserved approved Web provider implementation.

Determine exactly why it reports NOT_CONFIGURED.

Use the application's existing approved integration/configuration boundary.

Do NOT introduce direct arbitrary public-internet calls from business logic.

Do NOT create a parallel scraper.

If the provider requires configuration not available in the repository,
report the exact missing configuration.

If it can be activated safely from existing configuration/environment,
activate and perform one bounded readiness request.

Report:

Web provider state
transport state
configuration required
allowed source classes
successful bounded request YES/NO

==================================================
3. GLEIF REGRESSION
==================================================

Run one minimal GLEIF identity request to confirm the existing working path
has not regressed.

Do not redesign GLEIF.

==================================================
4. BOUNDED RECOVERY SET
==================================================

Read the Stage 2A.4 persisted resolution results.

Create an exact worklist containing ONLY:

- four remaining named unresolved endpoints;
- Solventum relationship candidates;
- Cabot accepted relationship as the positive control.

Do not send generic descriptors such as unnamed suppliers, unnamed lenders,
unnamed insurers, or unnamed technology providers to external providers.

==================================================
5. IDENTITY RECOVERY
==================================================

For each unresolved named endpoint:

first repeat exact Client Universe resolution;

then use, where applicable:

GLEIF
SEC
approved Web

Identity resolution and relationship evidence are separate gates.

Resolve identity using authoritative identifiers where possible:

LEI
CIK
official legal name
regulatory registration
official domain

No fuzzy merge.
No entity creation from similarity alone.

==================================================
6. RELATIONSHIP EVIDENCE RECOVERY
==================================================

For each named endpoint whose identity becomes sufficiently resolved:

retrieve evidence specifically for the EXISTING candidate relationship type.

Do not invent a new relationship type merely to obtain acceptance.

Search broadly enough to find admissible evidence but accept narrowly.

Apply the existing evidence hierarchy and Stage 2A.2 acceptance rules.

SEC filings should be preferred where the relationship is documented there.

Approved Web may provide independent corroboration from permitted sources.

GLEIF identity/parent data may support identity or ownership relationships
where explicitly supported, but must not be generalized to unrelated
relationship types.

==================================================
7. SOLVENTUM CONTROL
==================================================

The existing Solventum external identity is already resolved.

Re-evaluate the persisted Solventum candidates using the now-operational
SEC/Web source combination.

Do NOT promote merely because identity is known.

Promote only if the actual claimed relationship type, direction,
and semantics are directly supported.

If not, retain as candidate and state exactly which evidence requirement fails.

==================================================
8. CABOT CONTROL
==================================================

Replay the accepted Cabot relationship.

It must remain one observation.

No duplicate observation.
No duplicate external entity.
No duplicate evidence objects.

==================================================
9. GENERIC ENDPOINT SAFETY
==================================================

The six generic descriptors from Stage 2A.4 must remain unresolved descriptors.

Do not create entities for:

unnamed supplier groups
unnamed lender syndicates
unnamed insurers
unnamed ERP/IT vendors
generic counterparty descriptions

Generic descriptor entities created MUST equal 0.

==================================================
10. PATH RECALCULATION
==================================================

After the bounded recovery pass, recompute evidence-backed paths using only
accepted relationship observations.

Candidates may be visually/research connected later but cannot form accepted
hidden paths.

Do not create an A->C relationship simply because A->B->C exists.

Report:

accepted direct edges
candidate edges
evidence-backed paths
synthetic shortcut edges

Synthetic shortcut edges MUST equal 0.

==================================================
11. IDEMPOTENCE
==================================================

Replay this exact bounded Stage 2A.5 operation once.

Second execution must produce no duplicate:

external entities
identity records
relationship observations
candidate records
evidence objects
paths

==================================================
12. REPORT
==================================================

Create:

backend/data/PROVIDER_READINESS_RELATIONSHIP_RECOVERY_STAGE_2A5_REPORT.md

Include:

PROVIDER READINESS

GLEIF
SEC
Approved Web

For each:
configuration
connectivity
transport
readiness
failure reason if unavailable

BOUNDED ENTITY TABLE

Endpoint
Initial state
Internal client match
GLEIF result
SEC identity result
Web identity result
Final identity state
Strong identifiers

RELATIONSHIP TABLE

Subject
Related entity
Relationship type
Initial state
SEC evidence
Web evidence
GLEIF evidence where applicable
Evidence quality
Direction support
Final state
Reason

FINAL COUNTS

named endpoints tested
resolved internal endpoints
resolved external endpoints
remaining unresolved named endpoints
accepted observations before run
newly promoted observations
accepted observations after run
remaining candidates
generic descriptors retained
paths
synthetic shortcuts
fuzzy merges
duplicate records after replay

PASS REQUIREMENTS

Customer_latest.parquet modified = NO
fuzzy merges = 0
generic descriptor entities created = 0
synthetic shortcut edges = 0
duplicate records after replay = 0
Cabot regression = PASS
SEC readiness = report actual result
Web readiness = report actual result
GLEIF regression = PASS

STOP.

Do not research the full 3.67M universe.
Do not build the network UI.
Do not add AI workflows.
Do not redesign the relationship model.
