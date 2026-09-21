CCR RELATIONSHIP CORRELATION — PHASE 4B
LOCAL CORRELATION ENGINE + RESEARCH-CANDIDATE NETWORK

You are working in the CURRENT Windows-local CCR application.

The Phase 4A local POC is working.

DO NOT:
- work on Unix
- debug Windows DNS
- require SEC/GLEIF/Web connectivity
- fabricate business relationships
- convert similarity into relationship evidence
- modify source datasets
- modify Phase-2 canonical identities
- modify Stylus preset
- build a dense N×N matrix

This phase makes the application into an actual CCR CORRELATION TOOL using
local data while preserving the distinction:

CORRELATION / CANDIDATE SIGNAL
!=
RELATIONSHIP EVIDENCE

==================================================
1. OBJECTIVE
==================================================

When the user selects one CCR client, produce a bounded ranked set of entities
that are reasonable candidates for relationship research.

The application should answer:

"Which other entities should I investigate in relation to this client, and
why?"

It must NOT answer:

"What relationships definitely exist?"

unless evidence exists.

Target:

SELECTED CLIENT
    ↓
LOCAL CANDIDATE GENERATION
    ↓
MULTIPLE EXPLAINABLE SIGNALS
    ↓
CONFIG-AWARE SCORING
    ↓
TOP RESEARCH CANDIDATES
    ↓
NETWORK / TABLE / MAP
    ↓
FUTURE EXTERNAL RESEARCH
    ↓
EVIDENCE-BACKED RELATIONSHIP

==================================================
2. CURRENT VALIDATED STATE
==================================================

Read:

backend/data/CCR_PHASE4A_WINDOWS_LOCAL_POC_REPORT.md

Inspect the actual current implementation.

Do not rely only on documentation.

Preserve approximately:

canonical clients: 16,755
exposure rows: 25,000
linked exposure rows: 24,984
valid LEIs: 8,009
confirmed evidence-backed relationships: 0
evidence records: 0

Recompute all important counts.

==================================================
3. PRINCIPLE — THREE DIFFERENT OBJECTS
==================================================

The system must distinguish:

A. CLIENT / ENTITY

B. RESEARCH CANDIDATE

C. EVIDENCE-BACKED RELATIONSHIP

Never merge B and C.

A candidate says:

"research this pair"

A relationship says:

"evidence supports this relationship"

==================================================
4. CREATE LOCAL CORRELATION ENGINE
==================================================

Preferred module:

backend/app/core/ccr_correlation.py

or equivalent consistent project location.

The engine should take:

subject_ccr_client_key
analysis_config_id
top_k

and return:

candidate entities
signal components
score
reason codes
explanation
candidate provenance

No external calls.

==================================================
5. CANDIDATE GENERATION BEFORE SCORING
==================================================

DO NOT score all 16,755 × 16,755 combinations.

Candidate generation must happen FIRST.

Use bounded blocking/indexing.

Possible blocking dimensions, only where fields actually exist:

same sector
same industry
related industry
same country
same region
same legal/client type
shared parent identifier where actually available
shared ultimate-parent identifier where actually available
same beneficial-owner reference where explicitly present
shared identifier-domain signal
similar normalized entity classification

Do not assume fields exist.

Use actual database schema.

==================================================
6. CANDIDATE POOLS
==================================================

Build independently explainable candidate pools.

Examples:

SECTOR_POOL
INDUSTRY_POOL
GEOGRAPHY_POOL
HIERARCHY_POOL
OWNER_REFERENCE_POOL
ENTITY_TYPE_POOL
NAME_STRUCTURE_POOL
EXPOSURE_CONTEXT_POOL

But only implement pools justified by actual available data.

Each candidate must retain:

which pool(s) generated it.

==================================================
7. NAME SIMILARITY
==================================================

Name similarity can help entity research but must be handled carefully.

Use it primarily for:

possible group / alias / related-name discovery

Examples:

ABC HOLDINGS LLC
ABC OPERATING COMPANY LLC

But do NOT automatically infer:

PARENT
SUBSIDIARY
COMMON_OWNER

Name similarity is only a candidate signal.

Normalize names using explainable deterministic rules.

Avoid expensive all-pairs fuzzy matching.

Apply fuzzy comparison only inside already bounded blocks.

==================================================
8. LOCAL SIGNAL COMPONENTS
==================================================

Create explainable component scores in range 0–1 where appropriate.

Potential components:

sector_similarity
industry_similarity
geography_similarity
entity_type_similarity
name_similarity
hierarchy_signal
owner_reference_signal
identifier_signal
exposure_context_similarity

Only calculate components that are defensible from local data.

Missing component:

NULL / NOT_AVAILABLE

not zero unless mathematically justified.

==================================================
9. IMPORTANT — EXPOSURE
==================================================

Exposure units remain UNKNOWN.

Therefore:

DO NOT use monetary exposure amounts.

You MAY use non-monetary structural attributes such as:

exposure_record_count

only if clearly labelled.

Exposure record count must not imply:

economic materiality
credit importance
relationship strength

Possible use:

activity_context_signal

not:

materiality_score.

==================================================
10. CONFIG-AWARE CORRELATION
==================================================

Use the Phase-4A AI Create Relationship configuration.

Different analyses should choose different local candidate signals.

Example:

SUPPLY CHAIN DEPENDENCY

use candidate generation emphasizing:

industry compatibility
sector adjacency
geography where useful
entity type
known structural signals

Do not turn these into supplier relationships.

Example:

PARENT / SUBSIDIARY

emphasize:

LEI availability
name/group structure
existing hierarchy fields
owner references

Example:

CUSTOMER RELATIONSHIP

emphasize:

sector/industry compatibility
commercial/entity type
geography where relevant

Again:

candidate only.

==================================================
11. PRESET CANDIDATE SIGNAL POLICY
==================================================

Extend each AI relationship preset with:

candidate_signal_weights

For example:

Supply Chain Dependency:

industry = high
sector = medium
geography = low
name similarity = low
hierarchy = low

Parent / Subsidiary:

hierarchy = very high
owner reference = high
name structure = medium
industry = low
geography = low

Customer Relationship:

industry compatibility = medium
sector compatibility = medium
geography = medium
entity type = medium

Do not present these as empirically calibrated probabilities.

They are configurable heuristic research weights.

==================================================
12. SCORE TERMINOLOGY
==================================================

Never call the local candidate score:

relationship confidence

Use:

RESEARCH RELEVANCE SCORE

or

CANDIDATE SCORE

Prefer 0–100 for display.

Example:

Candidate Score: 78

Explain:

Industry similarity      25
Sector compatibility     20
Country signal            8
Name/group signal        15
Other supported signal   10

Do not imply 78% probability of a relationship.

==================================================
13. SCORE CALCULATION
==================================================

Implement an explainable weighted normalized score.

Conceptually:

available_weight =
sum(weight_i for available components)

score =
sum(weight_i * component_i)
/
available_weight

Then convert to 0–100.

Do not penalize entities merely because a field is missing.

Persist:

component values
component weights
available components

==================================================
14. CANDIDATE SCORE BANDS
==================================================

For user readability only:

80–100  Strong research candidate
60–79   Relevant research candidate
40–59   Secondary research candidate
<40     normally exclude from default results

These labels describe research priority.

They do NOT describe relationship truth.

Make thresholds configurable.

==================================================
15. MAXIMUM RESULTS
==================================================

Default:

top 20 candidates

Allow:

10
20
50

Hard cap:

100

Never render hundreds/thousands around one node by default.

==================================================
16. PERSIST CANDIDATE RUNS
==================================================

Add additive structures such as:

correlation_runs

Fields:

correlation_run_id
subject_ccr_client_key
analysis_config_id
analysis_config_version
executed_at
top_k
candidate_count
engine_version

And:

correlation_candidates

candidate_id
correlation_run_id
subject_ccr_client_key
candidate_ccr_client_key

candidate_score
candidate_band

signal_components_json
reason_codes_json

candidate_status

Candidate status:

RESEARCH_CANDIDATE
DISMISSED
PROMOTED_TO_RESEARCH

Never use:

CONFIRMED

in this table.

==================================================
17. CORRELATION API
==================================================

Create endpoints such as:

POST /api/ccr/correlation/run

GET /api/ccr/correlation/runs/{run_id}

GET /api/ccr/correlation/client/{client_key}

GET /api/ccr/correlation/client/{client_key}/latest

Request example:

{
  "subject_ccr_client_key": "...",
  "analysis_config_id": "...",
  "top_k": 20
}

No network calls.

==================================================
18. NETWORK PAGE — MAKE IT USEFUL
==================================================

Update the Network page.

Current selected center node remains.

Default layers:

[✓] Evidence-backed relationships
[✓] Research candidates
[ ] External structural observations
[ ] Indirect paths

Because there are currently no confirmed relationships, show research
candidates by default after a candidate run exists.

If no candidate run exists show:

"Generate research candidates"

button.

==================================================
19. NETWORK CANDIDATE DESIGN
==================================================

Center:
selected CCR client

Candidate nodes:
bounded top candidates

Candidate edges:
dotted / visually lighter

Label example:

RESEARCH CANDIDATE · 78

Hover:

Candidate score
Analysis preset
Top 3 signal reasons

Example:

Industry similarity
Same jurisdiction
Entity-type compatibility

Never label:

SUPPLIER
CUSTOMER
PARTNER

without evidence.

==================================================
20. NETWORK EDGE INSPECTOR
==================================================

Candidate edge inspector:

RESEARCH CANDIDATE

Candidate Score:
78 / 100

Analysis:
Supply Chain Dependency

Why proposed:
- industry compatibility
- sector similarity
- same operating geography

Evidence:
NONE

Relationship Status:
NOT ESTABLISHED

Action:

Research This Pair

==================================================
21. RESEARCH THIS PAIR
==================================================

Add button:

Research This Pair

For now, while external providers are unavailable:

it should create/prepare an explicit research request record.

Do not make network calls automatically.

Store:

subject
candidate
analysis_config
requested source channels
research instruction

Status:

WAITING_FOR_PROVIDER

or:

READY_TO_RUN

depending provider state.

==================================================
22. AI CREATE RELATIONSHIP — ADD RUN CAPABILITY
==================================================

The Phase-4A page currently configures presets.

Add:

Run Analysis

Workflow:

Select:
Subject Client

Select:
Analysis Preset

Select:
Top K

Click:

Generate Research Candidates

Result:

ranked candidate table.

This is LOCAL ANALYSIS.

Do not call it:

AI-confirmed relationship generation.

==================================================
23. AI ANALYSIS RESULT TABLE
==================================================

Columns:

Rank
Candidate Entity
Candidate Score
Country
Sector
Industry
Signals
LEI
Research Readiness
Action

Action:

Open Network
Research Pair
Dismiss

==================================================
24. CUSTOM ANALYSIS
==================================================

The Custom Analysis preset should allow the analyst to adjust local candidate
signal weights.

Example controls:

Industry importance
Sector importance
Geography importance
Entity type importance
Hierarchy importance
Name/group importance

Do not expose unsupported signals.

Weights should normalize automatically.

==================================================
25. RELATIONSHIP EXPLORER
==================================================

Maintain two clearly separate tabs:

RELATIONSHIPS

RESEARCH CANDIDATES

Relationships currently may remain empty.

Research Candidates should show candidate runs.

Columns:

Subject
Candidate
Analysis
Candidate Score
Top Signals
Run Date
Research Status

==================================================
26. WORLD MAP — REPLACE CURRENT ABSTRACT SHAPE
==================================================

The current Overview footprint visualization is useful but does not read
clearly enough as a world map.

Replace/upgrade it with a recognizable geographic world map.

Use a proper geographic world outline / GeoJSON / SVG map.

Do not require online map tiles for local Windows operation.

Prefer an offline-compatible map asset/library.

Show country-level bubbles using actual CCR country data.

Bubble size:
client count

Tooltip:

Country
Client count
% of CCR population

==================================================
27. MAP — SELECTED CLIENT
==================================================

When a client is selected:

highlight its country.

Show:

Selected Client
Country
CCR clients in country
% of CCR population

==================================================
28. MAP — CANDIDATE CONNECTIONS
==================================================

If a candidate run exists:

optional toggle:

Research Candidate Connections

Draw only top candidate arcs.

Use dotted arcs.

Do not present them as real relationship routes.

Legend:

Research Candidate — not evidence

When confirmed relationships eventually exist:

use a separate solid arc style.

==================================================
29. MAP PERFORMANCE
==================================================

Do not plot 16,755 individual points.

Aggregate at country level for Overview.

For selected-client analysis:

maximum same top-K candidate connections as the network.

==================================================
30. OVERVIEW — ADD RELATIONSHIP INTELLIGENCE PANEL
==================================================

Add:

RELATIONSHIP INTELLIGENCE

Show:

Evidence-backed relationships
Research candidates generated
Clients researched
External observations
Pending research requests
Evidence records

Real database values only.

==================================================
31. OVERVIEW — TOP RESEARCH SIGNALS
==================================================

Optional useful panel:

Top Local Candidate Signals

Examples:

Industry
Sector
Geography
Hierarchy
Owner reference
Entity type

Show how frequently each signal contributed to stored candidate runs.

Do not present these as relationship counts.

==================================================
32. CLIENT DETAIL — CORRELATION
==================================================

Add section:

RELATIONSHIP RESEARCH

Show:

Latest Analysis
Candidate Count
Top Candidate Score
Research Requests
Evidence-backed Relationships

Button:

Run Relationship Analysis

==================================================
33. CLIENT DETAIL — TOP CANDIDATES
==================================================

Show top 5 research candidates after a run.

Each shows:

name
score
top reasons
relationship status:

NOT ESTABLISHED

Button:

Open Network

==================================================
34. CANDIDATE DEDUPLICATION
==================================================

One candidate entity may appear from many pools.

Deduplicate by canonical client key.

Merge reason codes.

Example:

generated by:
SECTOR_POOL
INDUSTRY_POOL
GEOGRAPHY_POOL

becomes one candidate with multiple signals.

==================================================
35. SELF RELATIONSHIPS
==================================================

Never create:

client → same client

as candidate.

Exclude aliases resolving to same canonical entity.

==================================================
36. ENTITY IDENTITY QUALITY
==================================================

Prefer HIGH identity-quality candidates.

Allow MEDIUM where useful.

Normally exclude:

UNRESOLVED

unless user explicitly enables unresolved research.

Persist identity-quality context.

==================================================
37. RESEARCH READINESS
==================================================

Candidate ranking may display:

GLEIF lookup ready
SEC discovery required
Web ready

But provider availability must not alter local similarity score.

Separate:

Candidate Relevance

from:

Researchability

==================================================
38. PERFORMANCE
==================================================

Target local candidate generation:

<2 seconds typical

for one client / top 20.

Avoid scanning 16k records repeatedly when indexes can be used.

Add database indexes as justified.

Do not prematurely introduce:

Neo4j
Elasticsearch
vector database

SQLite remains sufficient for this POC.

==================================================
39. DETERMINISM
==================================================

Given:

same data
same subject
same preset version
same top_k

candidate ranking should be deterministic.

Tie break using stable canonical key.

==================================================
40. AUDITABILITY
==================================================

Every candidate must explain:

WHY WAS THIS ENTITY RETURNED?

No opaque embedding-only score.

If future embeddings are added, they become another explainable signal, not
the sole decision mechanism.

==================================================
41. TEST ACCEPTANCE CLIENTS
==================================================

Choose actual clients from CCR dynamically.

Test at least:

A. one Technology client

B. one Financial / Investment client

C. one client with LEI

D. one client without LEI

Do not hardcode names unless selected from the actual database as test
fixtures.

==================================================
42. ACCEPTANCE TEST — NETWORK
==================================================

For a selected client:

run Supply Chain Dependency candidate analysis.

Verify:

candidate run created
<=20 candidates
no duplicate candidates
no self node
score deterministic
signals visible
network shows candidates
candidate edge dotted
edge inspector says NOT EVIDENCE

==================================================
43. ACCEPTANCE TEST — CUSTOM ANALYSIS
==================================================

Run default custom analysis.

Then change signal weights materially.

Run again.

Verify:

configuration version changes

and where data permits:

ranking changes or component contributions change.

Do not fake ranking change merely to satisfy test.

==================================================
44. ACCEPTANCE TEST — MAP
==================================================

Verify:

recognizable world map
country aggregation equals canonical country counts
selected country highlight
candidate arcs <= top_k
candidate arcs labelled not evidence
zero external calls

==================================================
45. REGRESSION
==================================================

Must preserve:

Phase-2 foundation
Phase-3 external architecture
Phase-4A UI functionality

Tests must prove:

canonical data unchanged
source data unchanged
confirmed relationships remain 0 unless actual evidence already exists
evidence rows remain genuine only
external calls from correlation engine = 0
dense N×N rows = 0

==================================================
46. REPORT
==================================================

Generate:

backend/data/CCR_PHASE4B_LOCAL_CORRELATION_REPORT.md

Include:

CANDIDATE ENGINE
SIGNALS USED
SIGNALS NOT AVAILABLE
PRESET WEIGHTS
CANDIDATE COUNTS
PERFORMANCE
NETWORK
WORLD MAP
AI CREATE RELATIONSHIP
RELATIONSHIP EXPLORER
AUDITABILITY
TESTS
REGRESSION
KNOWN LIMITATIONS

==================================================
47. FINAL RESPONSE
==================================================

Return exactly:

CCR PHASE 4B LOCAL CORRELATION: PASS / FAIL

CORRELATION ENGINE
Implemented:
Available signals:
Unavailable signals:
Default top_k:
Dense pair matrix created: 0 / FAIL

AI CREATE RELATIONSHIP
Run Analysis: PASS / FAIL
Preset-aware ranking: PASS / FAIL
Custom weights: PASS / FAIL
Config versioning: PASS / FAIL

CANDIDATES
Stored runs:
Stored candidates:
Maximum candidates per run:
Duplicate candidates: 0 / FAIL
Self candidates: 0 / FAIL
Candidates labelled as relationships: 0 / FAIL

NETWORK
Center-client view: PASS / FAIL
Candidate layer: PASS / FAIL
Evidence layer separate: PASS / FAIL
Edge inspector: PASS / FAIL
Research Pair action: PASS / FAIL

WORLD MAP
Recognizable geographic map: PASS / FAIL
Country aggregation: PASS / FAIL
Selected-client highlight: PASS / FAIL
Candidate arcs: PASS / FAIL
Candidate/evidence distinction: PASS / FAIL

PERFORMANCE
Typical candidate runtime:
Worst acceptance runtime:

SAFETY
External calls during correlation: 0 / FAIL
Synthetic relationships: 0 / FAIL
Canonical mutations: 0 / FAIL
Exposure monetary scoring: 0 / FAIL

TESTS
Passed:
Failed:

REPORT:
backend/data/CCR_PHASE4B_LOCAL_CORRELATION_REPORT.md

WINDOWS CORRELATION TOOL READY:
YES / NO

STOP.
