CCR RELATIONSHIP CORRELATION — PHASE 3
EXTERNAL IDENTITY + SEC / GLEIF / HIGH-QUALITY WEB EVIDENCE FOUNDATION

You are working inside the CURRENT CCR repository opened in VSCode.

CCR ONLY.

Do not inspect, import from, modify, or depend on:
- Lending
- CCRIG
- RPR
- any other repository

Read first:

backend/data/CCR_RELATIONSHIP_PHASE1_DATA_AUDIT.md
backend/data/CCR_RELATIONSHIP_PHASE2_FOUNDATION_REPORT.md
backend/data/CCR_EXPOSURE_DATA_DICTIONARY.md

Also inspect the actual Phase-2 database and builder rather than trusting report
numbers blindly:

backend/data/ccr_relationship_intelligence.sqlite3
backend/scripts/build_ccr_relationship_foundation.py

==================================================
1. OBJECTIVE
==================================================

Phase 2 created the canonical CCR identity/exposure foundation.

Current validated state is approximately:

- 16,769 unique source GFCIDs
- 16,755 canonical resolved CCR clients
- 14 unresolved source identities
- 25,000 normalized exposure rows
- 24,984 linked exposure rows
- 16 unresolved exposure rows
- 8,009 valid local LEIs
- 0 local CIKs
- 0 local tickers
- 0 local website/domain identifiers
- 0 explicit legal parents
- 0 explicit ultimate parents
- 8 beneficial-owner reference records NOT promoted to parents
- 0 synthetic relationships
- 0 relationship evidence
- 0 dense pair rows

RECOMPUTE important values from the database.
Do not hardcode them.

The purpose of Phase 3 is to create the authoritative external identity and
evidence-acquisition foundation required for later CCR relationship discovery.

Target:

CANONICAL CCR CLIENT
        ↓
EXTERNAL IDENTITY RESOLUTION
        ↓
GLEIF
SEC
HIGH-QUALITY WEB
        ↓
RAW SOURCE DOCUMENT
        ↓
EVIDENCE SNIPPET
        ↓
SOURCE QUALITY / ADMISSIBILITY
        ↓
EXTERNAL RELATIONSHIP OBSERVATION — FUTURE PHASE

PHASE 3 STOPS BEFORE automatic relationship extraction/scoring.

==================================================
2. HARD SCOPE BOUNDARY
==================================================

IN SCOPE:

- GLEIF identity enrichment
- GLEIF Level-2 hierarchy evidence
- SEC filer identity discovery
- SEC filing acquisition infrastructure
- SEC filing metadata
- controlled high-quality Web research infrastructure
- source-quality policy
- evidence storage
- caching
- provenance
- research run tracking
- external identity resolution
- controlled small acceptance/pilot execution
- tests

OUT OF SCOPE:

- AI relationship extraction
- relationship scoring
- relationship ranking
- relationship confidence model
- full graph construction
- candidate pair generation across all clients
- N×N comparison
- AI Create Relationship UI
- correlation UI
- frontend redesign
- Stylus modification
- exposure materiality scoring
- automatic research for all 16k clients

Do not create speculative business relationships.

==================================================
3. IMMUTABILITY
==================================================

DO NOT modify:

Customer_latest.parquet
thousandClients.csv
backend/data/ccr_clients.sqlite3

Do not destroy or rewrite Phase-2 canonical business data.

Extend:

backend/data/ccr_relationship_intelligence.sqlite3

using migrations / additive schema changes where appropriate.

Before modifying the Phase-2 database:

calculate and record a business-data fingerprint for the existing Phase-2
tables.

After Phase 3 prove Phase-2 business rows are unchanged.

Phase-2 tables that represent canonical/local business data are IMMUTABLE in
this phase.

External enrichment must live in new tables.

==================================================
4. CRITICAL DATA-GOVERNANCE RULE
==================================================

There is currently NO CAM relationship authority for CCR.

Therefore external relationship intelligence will ultimately depend primarily
on:

1. authoritative regulatory / registry evidence;
2. issuer / company primary-source disclosures;
3. approved high-quality secondary public sources.

External evidence must never become canonical merely because an LLM says so.

AI may later:

- extract
- classify
- summarize
- compare evidence

AI must NOT manufacture evidence.

==================================================
5. SOURCE AUTHORITY MODEL
==================================================

Implement an explicit source-policy registry.

Use concepts such as:

TIER_1_AUTHORITATIVE
TIER_2_HIGH_QUALITY_SECONDARY
TIER_3_CORROBORATIVE
INADMISSIBLE

--------------------------------------------------
TIER 1 — AUTHORITATIVE
--------------------------------------------------

Examples:

SEC / EDGAR
GLEIF
official regulatory registries
official company filings
issuer investor-relations disclosures
official company annual reports
official press releases where relationship information is explicit

Tier 1 evidence may independently support a future relationship proposal
provided the text itself supports it.

--------------------------------------------------
TIER 2 — HIGH-QUALITY SECONDARY
--------------------------------------------------

Examples:

major financial wire services
major established financial/business publications
reputable global news organizations

Examples may include Reuters, Bloomberg, Financial Times, Wall Street Journal
and similarly governed sources.

Do NOT rely on domain-name matching alone.

Store publisher/source-policy decision explicitly.

Tier 2 may independently support ordinary public factual relationships where
evidence is explicit, but high-impact/ambiguous ownership or legal-control
claims should preferably require Tier 1 or corroboration.

--------------------------------------------------
TIER 3 — CORROBORATIVE
--------------------------------------------------

Examples:

reputable specialist industry publications
recognized trade associations
high-quality specialist research/publications

Normally use as supporting evidence rather than sole authority for critical
legal/control relationships.

--------------------------------------------------
INADMISSIBLE
--------------------------------------------------

Examples:

social media posts
anonymous forums
content farms
SEO aggregators
unsourced company databases
scraped reposting sites
AI-generated answer pages
random blogs
search-result snippets without source retrieval
Wikipedia as sole relationship evidence

These may help discovery only if explicitly allowed in the future.

They must not enter relationship evidence as admissible proof.

==================================================
6. DATABASE EXTENSION
==================================================

Add appropriate tables.

Preserve the existing Phase-2 schema.

Preferred logical structures follow.

Exact physical names may vary slightly if repository conventions require it.

--------------------------------------------------
6A. external_identity
--------------------------------------------------

One or multiple external identity candidates per CCR client.

Fields should support:

external_identity_id
ccr_client_key

source_system:
- SEC
- GLEIF
- WEB_DOMAIN
- OTHER_AUTHORITATIVE

identifier_type
identifier_value

external_legal_name
external_country
external_address

resolution_status
resolution_method
match_quality
match_reasons
conflict_reasons

verified
review_required

source_reference
retrieved_at
research_run_id

Statuses:

VERIFIED
CANDIDATE
AMBIGUOUS
NOT_FOUND
CONFLICT
ERROR

Do not force ambiguous matches.

--------------------------------------------------
6B. research_runs
--------------------------------------------------

Every external operation must belong to a research run.

Fields:

research_run_id
requested_at
started_at
completed_at

run_type:
GLEIF_LOOKUP
GLEIF_DISCOVERY
SEC_IDENTITY_DISCOVERY
SEC_FILING_RESEARCH
WEB_RESEARCH
COMBINED_RESEARCH

requested_client_count
executed_client_count

mode:
DRY_RUN
PILOT
EXPLICIT

provider
configuration_snapshot
status

network_request_count
cache_hit_count
cache_miss_count
error_count

initiated_by
notes

No anonymous untracked network activity.

--------------------------------------------------
6C. source_documents
--------------------------------------------------

Store external-source metadata.

Fields:

source_document_id
ccr_client_key if known
external_identity_id if relevant

source_channel:
SEC_FILING
GLEIF_RECORD
GLEIF_RELATIONSHIP
OFFICIAL_WEB
HIGH_QUALITY_WEB

publisher
domain
source_title

filing_type
accession_number
filing_date
period_of_report

published_date
retrieved_at

source_reference
canonical_reference

source_tier
admissibility

content_hash
cache_path or cached_content_reference

http_status if relevant

research_run_id

Do not redistribute unnecessary full copyrighted secondary articles.

For Web/news sources store metadata and bounded evidence excerpts only.

Official regulatory/public records may be cached according to normal technical
requirements where appropriate.

--------------------------------------------------
6D. evidence_snippets
--------------------------------------------------

Evidence must be separately persisted.

Fields:

evidence_id
source_document_id
ccr_client_key

evidence_type
section
location_reference

evidence_excerpt
excerpt_hash

source_tier
admissibility

extraction_method:
DIRECT_TEXT
RULE
AI_FUTURE
MANUAL

quality_status

created_at

IMPORTANT:

Phase 3 should populate evidence only where retrieval/parsing itself produces
bounded useful excerpts.

Do NOT run AI relationship extraction.

--------------------------------------------------
6E. sec_entity_map
--------------------------------------------------

Fields:

ccr_client_key
cik
sec_name
ticker
exchange

match_method
match_status
match_quality
match_reasons

source_snapshot
retrieved_at

Do not create CIK matches from loose fuzzy-name matching alone.

--------------------------------------------------
6F. gleif_entity_map
--------------------------------------------------

Fields:

ccr_client_key
lei
gleif_legal_name
jurisdiction
entity_status

match_method
match_status
match_quality

retrieved_at
source_reference

--------------------------------------------------
6G. gleif_relationship_observations
--------------------------------------------------

GLEIF Level-2 relationships are real authoritative external structural
observations.

Store them separately from the future CCR canonical relationship graph.

Fields:

observation_id

child_ccr_client_key if mapped
child_lei

parent_lei
parent_name

relationship_type

Use exact GLEIF semantics, such as concepts representing:

DIRECT_ACCOUNTING_CONSOLIDATING_PARENT
ULTIMATE_ACCOUNTING_CONSOLIDATING_PARENT

Do not relabel these loosely as generic beneficial ownership.

Fields also include:

relationship_status
relationship_start_date if available
relationship_end_date if available
validation_status
reporting_exception if applicable
source_reference
retrieved_at
research_run_id

Do NOT promote them into a general PARENT_OF graph in this phase.

--------------------------------------------------
6H. source_policy_registry
--------------------------------------------------

Persist:

source_policy_id
channel
publisher/domain pattern where appropriate
tier
allowed
independent_evidence_allowed
requires_corroboration
allowed_relationship_categories
notes
version

Keep this editable/configurable.

Do not bury source governance in Python conditionals only.

==================================================
7. GLEIF PROVIDER
==================================================

Build a dedicated provider/service.

Preferred concept:

GLEIFProvider

It must support:

A. lookup by existing LEI

B. retrieve Level-1 entity information

C. retrieve Level-2 direct parent

D. retrieve Level-2 ultimate parent

E. retrieve/report parent-reporting exceptions

F. optional controlled entity discovery by:
   legal name + jurisdiction/country

The current dataset has approximately 8,009 valid local LEIs.

These are the strongest initial authoritative external-identity anchors.

For an existing local LEI:

local LEI
    ↓
GLEIF record
    ↓
legal name / status / jurisdiction
    ↓
Level-2 relationships
    ↓
external identity + hierarchy observations

Never silently replace the local CCR legal name.

Store external values alongside local values.

If names disagree:
record discrepancy.

Do not overwrite canonical identity.

==================================================
8. GLEIF DISCOVERY WITHOUT EXISTING LEI
==================================================

Approximately 8,746 canonical clients may lack a local LEI.

Do NOT automatically perform thousands of fuzzy searches in this phase.

Implement discovery capability but place it behind explicit execution.

Use bounded matching features such as:

legal name
country/jurisdiction
address where available

Statuses:

VERIFIED
CANDIDATE
AMBIGUOUS
NOT_FOUND

A name-only fuzzy match cannot automatically become VERIFIED unless the
provider response and multiple identity attributes make it defensible.

Store candidate alternatives.

==================================================
9. SEC PROVIDER
==================================================

Build:

SECProvider

or a similarly clean provider abstraction.

Use official SEC/EDGAR sources only for SEC channel.

SEC public data APIs do not require an API key.

Configuration must include environment/config variables such as:

SEC_USER_AGENT
SEC_CONTACT_EMAIL
SEC_REQUESTS_PER_SECOND
SEC_TIMEOUT_SECONDS
SEC_CACHE_DIR

Never print secrets/contact details unnecessarily.

Request-rate policy:

SEC's current fair-access ceiling is 10 requests/second.

Configure the application BELOW that limit.

Use a conservative default such as:

5 requests/second

and never allow configuration > 10.

Implement:

rate limiting
retry with backoff
429 handling
5xx handling
timeout
cache
request logging

Every automated request must send a declared User-Agent.

==================================================
10. SEC IDENTITY DISCOVERY
==================================================

There are currently zero local CIKs.

Therefore separate:

SEC_IDENTITY_DISCOVERY

from:

SEC_FILING_RESEARCH.

Use official SEC reference datasets first where practical.

Examples:

SEC ticker / CIK / exchange mapping files
SEC filer/company-name indexes

Do not make one live search request per CCR client if a bounded official
reference file can be downloaded once and matched locally.

Preferred process:

download/cache official SEC filer mapping snapshot
        ↓
normalize SEC filer names
        ↓
compare CCR legal identity
        ↓
candidate CIK
        ↓
validate using additional attributes
        ↓
VERIFIED / CANDIDATE / AMBIGUOUS / NOT_FOUND

Do not auto-verify weak name-only matches.

Record:

local legal name
SEC legal name
former SEC names if available
country/context if available
ticker
exchange
CIK

and exact match reasons.

==================================================
11. SEC SUBMISSIONS
==================================================

Once a CIK has been VERIFIED, support retrieving official submission metadata.

Use the official SEC submissions JSON endpoint pattern for:

CIK##########.json

with zero-padded 10-digit CIK.

Persist filing metadata.

Relevant forms for FUTURE relationship research should include configurable
support for:

10-K
10-Q
8-K
20-F
40-F
6-K
S-1 / F-1 where relevant
DEF 14A
SC 13D / 13D/A
SC 13G / 13G/A
13F where relevant to institutional holdings

Do not assume every form has the same evidentiary meaning.

Create configurable form policy.

==================================================
12. SEC FILING TEXT ACQUISITION
==================================================

Implement infrastructure to retrieve primary filing documents using official
EDGAR references.

Cache by:

CIK
accession number
document name
content hash

Never re-download unchanged filings unnecessarily.

For future relationship extraction, priority filing sections include concepts
such as:

Business
Customers
Suppliers
Dependencies
Risk Factors
Related Party Transactions
Principal Stockholders
Security Ownership
Material Agreements
Acquisitions
Joint Ventures
Strategic Agreements

But PHASE 3 does NOT classify relationships from them yet.

It may index/segment sections for later use.

==================================================
13. SEC COMPANYFACTS
==================================================

Do NOT use CompanyFacts as a relationship engine.

CompanyFacts may be supported for future quantitative/reference use.

It is not required to establish:

supplier
customer
strategic partner
parent
technology dependency

Do not confuse XBRL financial facts with relationship evidence.

==================================================
14. HIGH-QUALITY WEB PROVIDER
==================================================

Create a provider abstraction such as:

WebResearchProvider

DO NOT silently assume a provider exists.

Detect whether there is an approved runtime/provider already configured in the
CCR repository/environment.

If none exists:

WEB_PROVIDER_STATUS = NOT_CONFIGURED

Do not add a random scraping/search dependency merely to make the test pass.

The architecture must still support future providers cleanly.

Required request contract:

subject_ccr_client_key
subject_legal_name

optional related_entity
relationship_scope

as_of_date

source_policy
research_instruction

max_sources
max_age_days where relevant

No unconstrained "search everything on the internet" behavior.

==================================================
15. WEB SOURCE QUALITY
==================================================

For every Web result evaluate:

publisher
domain
article/title
publication date
retrieval date
primary vs secondary
source tier
admissibility
duplicate/canonical URL
evidence accessibility

Do not accept a search-engine snippet as evidence.

Retrieve the underlying source.

If underlying source cannot be retrieved:

SOURCE_NOT_VERIFIED

Do not treat it as admissible relationship evidence.

==================================================
16. OFFICIAL COMPANY SITES
==================================================

Support the concept:

OFFICIAL_COMPANY_SOURCE

Examples:

investor relations
annual-report pages
official press release
official corporate disclosures

However:

Do NOT trust a domain merely because it contains a similar company name.

Future identity/domain resolution must establish that the domain belongs to
the subject entity.

==================================================
17. CACHE DESIGN
==================================================

External research must be cache-first.

A normal read/query must NEVER cause hidden external execution.

Implement separate concepts:

GET/READ CACHED RESULT
vs
RUN EXTERNAL RESEARCH

If API endpoints are added:

read endpoint:
NO NETWORK

run endpoint:
EXPLICIT NETWORK EXECUTION

A cache miss from a read endpoint must return:

NOT_CACHED

It must not trigger external research.

==================================================
18. API CONTRACT
==================================================

Add clean backend API support if consistent with current FastAPI structure.

Possible routes:

GET /api/ccr/research/status

GET /api/ccr/research/client/{ccr_client_key}

GET /api/ccr/research/client/{ccr_client_key}/identities

GET /api/ccr/research/client/{ccr_client_key}/sources

GET /api/ccr/research/client/{ccr_client_key}/evidence

POST /api/ccr/research/run

POST /api/ccr/research/run/gleif

POST /api/ccr/research/run/sec

POST /api/ccr/research/run/web

Exact routing may follow existing repo conventions.

CRITICAL:

GET endpoints must perform zero external network calls.

Only explicit POST/run operations may execute providers.

==================================================
19. EXPLICIT EXECUTION CONTROL
==================================================

CLI scripts should default to:

DRY RUN

Network calls should require an explicit flag such as:

--execute

Bulk execution should also require:

--limit N

Do not provide an accidental "research all 16,755 clients" default.

Require explicit batch size.

Hard-cap pilot mode.

==================================================
20. CONTROLLED PILOT
==================================================

After infrastructure/tests are complete, run only a bounded pilot if network
access is available.

Do not run across the full portfolio.

Create a deterministic acceptance cohort.

Preferred cohort:

GROUP A
10 canonical clients with valid existing LEI
→ test GLEIF direct lookup + Level 2

GROUP B
10 canonical clients without local CIK but strong SEC-discovery identity
→ test official SEC identity discovery

GROUP C
up to 5 Web-ready clients
→ test Web provider ONLY if an approved Web provider is actually configured

Avoid duplicate clients across groups where practical.

Do not hardcode famous company names purely to make the demo work.

Select deterministically from actual CCR data using documented criteria.

Store the cohort definition.

==================================================
21. PILOT SAFETY
==================================================

For the pilot report:

Do NOT report a relationship merely because:

GLEIF identity matched
SEC identity matched
a filing was found
a Web page mentioned the company

Those establish identity/source coverage.

Only GLEIF Level-2 records may be persisted as actual structural relationship
OBSERVATIONS in Phase 3 because they are explicit registry relationship data.

Even those remain:

EXTERNAL STRUCTURAL OBSERVATIONS

not canonical CCR graph edges yet.

==================================================
22. IDENTITY MATCH RULES
==================================================

Implement transparent matching.

Strong match dimensions:

existing exact LEI
exact verified CIK
legal name
former legal name
jurisdiction
address
ticker/exchange where available

Do not use one opaque scalar confidence only.

Persist a feature/reason vector such as:

EXACT_LEI
EXACT_NORMALIZED_NAME
COUNTRY_MATCH
ADDRESS_MATCH
FORMER_NAME_MATCH
TICKER_MATCH
NAME_ONLY
COUNTRY_CONFLICT
MULTIPLE_CANDIDATES

Then derive:

VERIFIED
CANDIDATE
AMBIGUOUS
CONFLICT

with explicit rules.

==================================================
23. NO AI IDENTITY HALLUCINATION
==================================================

Do not ask an LLM:

"What is this company's CIK?"
"What is its LEI?"
"What is its parent?"

and then store the answer.

Identifiers and ownership data must come from authoritative external sources.

AI may later interpret documents but cannot originate registry facts.

==================================================
24. EXTERNAL EVIDENCE QUALITY
==================================================

Create explicit fields:

source_quality
admissibility
identity_match_quality
evidence_quality

Do not misuse percentages such as:

"93% confidence"

unless a statistically validated model exists.

Preferred categorical values:

HIGH
MEDIUM
LOW
INSUFFICIENT

with reason arrays.

==================================================
25. RESEARCH FAILURE STATES
==================================================

Persist normal failure states.

Examples:

NOT_FOUND
AMBIGUOUS_IDENTITY
RATE_LIMITED
TIMEOUT
SOURCE_UNAVAILABLE
PARSE_FAILED
INADMISSIBLE_SOURCE
INSUFFICIENT_IDENTITY
CACHE_ONLY
PROVIDER_NOT_CONFIGURED

Do not turn operational failures into empty successful results.

==================================================
26. OBSERVABILITY
==================================================

For every external request record:

research_run_id
provider
endpoint class
status
duration
cache hit/miss
HTTP status
retry count
error type

Do not store secret credentials.

Provide aggregate run statistics.

==================================================
27. TESTS — SEC
==================================================

Add mocked/unit tests proving:

1. SEC requests include declared User-Agent.

2. configured rate cannot exceed 10 req/sec.

3. default rate is conservative.

4. 429 invokes backoff.

5. cache hit causes no network call.

6. GET API causes no external call.

7. explicit POST/run can invoke provider.

8. name-only ambiguous CIK is not VERIFIED.

9. exact/strong identity can be verified.

10. filing metadata preserves accession/form/date.

11. no CompanyFacts value becomes relationship evidence automatically.

==================================================
28. TESTS — GLEIF
==================================================

Prove:

1. exact local LEI lookup maps to correct client.

2. GLEIF legal name does not overwrite canonical CCR name.

3. name disagreement is persisted.

4. direct parent and ultimate parent are distinguished.

5. reporting exception is preserved.

6. no reporting exception is converted to a fake parent.

7. fuzzy/name discovery does not auto-verify ambiguous candidates.

8. GLEIF structural observations remain separate from future canonical graph.

==================================================
29. TESTS — WEB
==================================================

Prove:

1. provider-not-configured is handled normally.

2. search snippet alone is not evidence.

3. inadmissible source cannot become evidence.

4. underlying source metadata is required.

5. source tier is persisted.

6. GET/cache reads cause zero external calls.

7. Web result cannot silently mutate canonical identity.

==================================================
30. REGRESSION TESTS
==================================================

Prove Phase-2 values remain unchanged for:

canonical_clients
identity_resolution
exposure_records
client_exposure_summary
exposure field semantics
candidate signal registry

Also prove:

Customer_latest.parquet unchanged

thousandClients.csv unchanged

ccr_clients.sqlite3 unchanged

No dense pair generation.

No synthetic relationship creation.

==================================================
31. EXTERNAL RESEARCH CONFIGURATION FILES
==================================================

Create config artifacts rather than scattering constants.

Preferred examples:

backend/config/ccr_source_policy.json
backend/config/ccr_sec_research.json
backend/config/ccr_relationship_evidence_policy.json

or equivalent project-appropriate location.

SEC config should include:

allowed forms
form priorities
rate setting
cache policy
recency policy
section priorities

Source policy should include:

tiers
admissibility
corroboration requirements

Do not include credentials.

==================================================
32. FUTURE AI CREATE RELATIONSHIP COMPATIBILITY
==================================================

Design Phase 3 so Phase 4 can introduce configurable analysis presets such as:

SUPPLY_CHAIN_DEPENDENCY
TECHNOLOGY_DEPENDENCY
CUSTOMER_RELATIONSHIP
PARENT_SUBSIDIARY
INVESTOR_SPONSOR
LENDER_FINANCING
STRATEGIC_PARTNER
SERVICE_PROVIDER
INFRASTRUCTURE_DEPENDENCY
JOINT_VENTURE
NEWS_EVENT_DRIVEN
CUSTOM_ANALYSIS

Do NOT implement the AI presets yet.

But make evidence queryable by:

source channel
source tier
filing type
publication date
entity
evidence text

so configurations can select appropriate sources later.

==================================================
33. DO NOT USE EXPOSURE FOR RELATIONSHIP MATERIALITY
==================================================

Phase 2 established:

exposure units = UNKNOWN
additivity = UNKNOWN

Therefore Phase 3 MUST NOT:

rank relationships by exposure
call a relationship "material" because of an exposure field
sum exposure values
derive relationship confidence from exposure

Until exposure semantics are independently confirmed.

==================================================
34. PERFORMANCE
==================================================

Do not call GLEIF/SEC/Web serially for the entire population.

Use:

cache
bounded workers
provider rate limits
batch reference downloads where available
local matching before network matching

No external call should occur when existing cached authoritative data suffices.

==================================================
35. PHASE 3 REPORT
==================================================

Generate:

backend/data/CCR_RELATIONSHIP_PHASE3_EXTERNAL_RESEARCH_REPORT.md

Include:

ARCHITECTURE
DATABASE TABLES ADDED
SOURCE POLICY
SEC CONFIGURATION
GLEIF CONFIGURATION
WEB CONFIGURATION
CACHE DESIGN
IDENTITY MATCH RULES
PILOT COHORT
PILOT RESULTS
GLEIF LEVEL-2 RESULTS
SEC IDENTITY RESULTS
WEB RESULTS
NETWORK REQUEST COUNTS
CACHE COUNTS
ERRORS
TEST RESULTS
REGRESSION
OPEN ISSUES

Do not dump complete filing text into the report.

==================================================
36. FINAL RESPONSE
==================================================

Return exactly:

CCR PHASE 3 EXTERNAL FOUNDATION: PASS / FAIL

PHASE-2 REGRESSION:
PASS / FAIL

NEW TABLES:
<names>

SOURCE POLICY:
Tier 1 sources:
Tier 2 sources:
Tier 3 sources:
Inadmissible policy: PASS / FAIL

GLEIF
Existing local LEIs:
Pilot attempted:
Verified:
Not found:
Ambiguous:
Direct-parent observations:
Ultimate-parent observations:
Reporting exceptions:
Network requests:
Cache hits:

SEC
Local CIK before Phase 3:
Discovery pilot attempted:
Verified CIK:
Candidate CIK:
Ambiguous:
Not found:
Submission records retrieved:
Filing metadata rows:
Network requests:
Cache hits:
Configured requests/sec:

WEB
Provider configured: YES / NO
Pilot attempted:
Sources retrieved:
Admissible Tier 1:
Admissible Tier 2:
Tier 3:
Inadmissible:
Network requests:
Cache hits:

EVIDENCE
Source documents:
Evidence snippets:
Synthetic evidence: 0 / FAIL
AI-generated relationship claims: 0 / FAIL

GLEIF STRUCTURAL OBSERVATIONS
Direct accounting parent:
Ultimate accounting parent:
Canonical CCR graph edges created: 0 / FAIL

SAFETY
Automatic research on GET/read: 0 / FAIL
Dense pair rows: 0 / FAIL
Exposure materiality scoring: 0 / FAIL
Canonical Phase-2 mutations: 0 / FAIL
Source files modified: 0 / FAIL

TESTS:
X passed / Y failed

REPORT:
backend/data/CCR_RELATIONSHIP_PHASE3_EXTERNAL_RESEARCH_REPORT.md

PHASE 4 READY:
YES / NO

If NO:
list only genuine blockers.

STOP.
