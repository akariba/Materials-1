LENDING — PORTFOLIO / MATERIALITY API

Build the read-only Lending portfolio analytics layer required by the final
POC UI.

This stage is BACKEND/API ONLY.

Do NOT redesign or modify the frontend yet.

==================================================
TRUSTED DATA BOUNDARIES
==================================================

Keep these populations distinct.

A. CAM-priority / credit-portfolio population
Source:
CAM CAGIDs List_20260918.xlsx

Validated:
- 2,484 distinct CAGIDs
- 1,698 with CAM data
- 786 without CAM data
- 928 with exactly 1 CAM
- 770 with exactly 2 CAMs
- 0 with >2 CAMs
- total supplied OSUC approximately $349.27B
- CAM-covered supplied OSUC approximately $259.93B

IMPORTANT:
This is scope-limited.
It is NOT proven to be the complete Lending universe.

OSUC is SUPPLEMENTAL because:
- explicit as-of date is unavailable
- unit definition is not encoded in workbook metadata
- hedge treatment is not established

Never label this field "OSUC Net of Hedges".

Use wording such as:
"Reported OSUC"
or
"Portfolio OSUC"
and preserve the source limitation.

B. AI Economy Masterfile
- 418 clients
- separate analytical population
- overlap with 2,484 = 330
- absent from 2,484 = 88

Do not silently merge these populations.

C. V3 CAM relationship layer
Frozen:
- 13 canonical relationships
- 28 review-required relationships
- 0 unresolved CAM document subjects

V3 remains authoritative internal relationship evidence.

D. External overlay
The external-research overlay backend has PASSED.

External intelligence remains separate from V3 CAM truth.

==================================================
HARD RULES
==================================================

LENDING ONLY.

Do NOT:
- modify V1
- modify V2
- modify V3
- rerun extraction
- modify CAM source documents
- modify source workbooks
- modify Stylus preset
- call SEC/R2D2/Web
- modify CCR
- rebuild frontend
- create fake/demo portfolio values
- infer relationship facts from structured portfolio workbooks

This stage is read-only analytics/API.

==================================================
OBJECTIVE
==================================================

Expose clean backend endpoints for:

1. portfolio overview
2. portfolio clients
3. client detail
4. exposure/materiality analytics
5. CAM coverage
6. sectors
7. V3 relationship summaries
8. external overlay summaries
9. review queue statistics

Use actual repository data only.

==================================================
PORTFOLIO OVERVIEW
==================================================

Provide an endpoint conceptually similar to:

GET /lending/portfolio/overview

Return:

population_name
population_scope_description
client_count
clients_with_cam
clients_without_cam
one_cam_count
two_cam_count

reported_osuc_total
reported_osuc_cam_covered
reported_osuc_no_cam

cam_coverage_pct_by_clients
cam_coverage_pct_by_osuc

sector_count

canonical_relationship_count
review_required_relationship_count

external_proposal_count
external_conflict_count

data_quality / limitation flags

Include explicit metadata:

osuc_authority = SUPPLEMENTAL
osuc_as_of_date = null if unknown
osuc_net_of_hedges = UNKNOWN
population_authority = SCOPE_LIMITED

Do not hide these limitations.

==================================================
CLIENT LIST
==================================================

Provide:

GET /lending/portfolio/clients

Support:
- search by CAGID
- search by name
- sector filter
- CAM coverage filter
- relationship-risk-rating filter if available
- credit-classification filter if available
- country/exclusion filter if available
- sorting
- pagination

Return per client:

CAGID
client name
sector L1
sector L2
sector L3
country risk
reported OSUC
portfolio share
exposure rank
CAM count
CAM coverage flag
relationship risk rating
credit classification
country exclusion flag

V3 relationship counts:
- canonical
- review-required

External overlay counts:
- corroborations
- proposals
- conflicts

Do not execute external research from this endpoint.

==================================================
EXPOSURE MATERIALITY
==================================================

Compute exposure materiality only.

Do NOT create a generic "risk score".

For each client calculate where possible:

reported_osuc
portfolio_share
exposure_rank
exposure_percentile
cumulative_portfolio_share

Materiality is based on exposure only.

Call it:

EXPOSURE MATERIALITY

Do not call it:
- overall risk
- credit risk score
- relationship risk score

Do not invent business thresholds.

Expose raw metrics first.

If tiers are needed for UI convenience, make them configurable and label
them clearly as UI analytical bands, not approved risk policy.

==================================================
TOP EXPOSURES
==================================================

Provide:

GET /lending/portfolio/top-exposures

Support a configurable limit.

Return:
- rank
- CAGID
- client
- reported OSUC
- portfolio %
- cumulative portfolio %
- sector
- CAM count
- canonical relationship count
- review relationship count

==================================================
SECTOR ANALYTICS
==================================================

Provide:

GET /lending/portfolio/sectors

Return by sector:

client count
reported OSUC
portfolio share
CAM-covered client count
CAM-covered OSUC
no-CAM OSUC
1-CAM count
2-CAM count

Validate that the CAM-covered sector totals reconcile to the validated
1,698-client / approximately $259.93B population.

==================================================
CAM COVERAGE
==================================================

Provide:

GET /lending/portfolio/cam-coverage

Return:

with CAM
without CAM
1 CAM
2 CAMs

and corresponding reported OSUC values.

IMPORTANT:

"CAM data available" does NOT mean:
- physical PDF/DOCX CAM exists locally
- CAM is current
- CAM type is known
- CCM is proven
- annual review is proven

Expose those caveats in response metadata.

==================================================
CLIENT DETAIL
==================================================

Provide:

GET /lending/portfolio/client/{cagid}

Return:

identity
portfolio metadata
reported OSUC
portfolio share
rank
sector
country
CAM count
risk rating
credit classification

Then relationship intelligence:

V3 canonical relationships
V3 review-required relationships
external overlay results

Keep sections separate:

cam_relationships
cam_review_relationships
external_intelligence

Never merge external intelligence into CAM truth.

==================================================
RELATIONSHIP SUMMARY
==================================================

Provide a lightweight endpoint for UI network/overview use.

Conceptually:

GET /lending/portfolio/client/{cagid}/relationships

Allow filters:

canonical
review_required
external
relationship_type
direct/indirect
current/emerging/historical/terminated

Do not expose the old 32,957 noisy candidate population.

Only use:
- V3 canonical 13
- V3 review-required 28
- governed external overlay

==================================================
REVIEW QUEUE SUMMARY
==================================================

Provide:

GET /lending/review/summary

Return counts for:

V3 review-required
external proposals pending review
external conflicts
external insufficient evidence
unresolved entity matches

==================================================
POPULATION METADATA
==================================================

Provide:

GET /lending/populations

Return each population independently:

CAM Priority / Credit Portfolio
AI Economy Masterfile
Technology
CoreAI
CoreAI tracker
physical CAM subject population

For each:
- count
- description
- source
- authority
- overlap information where available

Do not pretend one is the universal denominator.

==================================================
PERFORMANCE
==================================================

Do not load multi-million-row Customer_latest.parquet on every API call.

Use existing indexed/reference mechanisms or load only what is required.

POC implementation:
simple, deterministic, fast.

Avoid enterprise-scale refactoring.

==================================================
TESTS
==================================================

Add tests for:

- overview population count = 2,484
- CAM count = 1,698
- no-CAM = 786
- 1 CAM = 928
- 2 CAMs = 770
- no >2 CAM rows
- exposure arithmetic reconciles
- sector totals reconcile
- search/filter/pagination
- portfolio shares sum appropriately
- exposure ranking deterministic
- client drill-down
- canonical V3 count remains 13
- review-required remains 28
- rejected/noisy 32,957 candidates are NOT exposed
- external overlay remains separate
- read endpoints trigger zero SEC/R2D2 calls
- CCR inaccessible from Lending routes

==================================================
REGRESSION
==================================================

Verify:

V1 unchanged
V2 unchanged
V3 unchanged
external overlay tests still pass
Stylus preset unchanged
frontend unchanged
CCR untouched

==================================================
FINAL REPORT
==================================================

Generate:

backend/data/LENDING_PORTFOLIO_API_VALIDATION_REPORT.md

Final response:

LENDING PORTFOLIO API: PASS / FAIL

Portfolio clients:
Clients with CAM:
Clients without CAM:
1 CAM:
2 CAMs:

Reported OSUC total:
Reported CAM-covered OSUC:
Reported no-CAM OSUC:

OSUC authority:
SUPPLEMENTAL

Portfolio overview endpoint:
PASS / FAIL

Client list endpoint:
PASS / FAIL

Client detail endpoint:
PASS / FAIL

Top exposure endpoint:
PASS / FAIL

Sector endpoint:
PASS / FAIL

CAM coverage endpoint:
PASS / FAIL

Relationship endpoint:
PASS / FAIL

Review summary endpoint:
PASS / FAIL

Population metadata endpoint:
PASS / FAIL

V3 canonical exposed:
13

V3 review-required exposed:
28

32,957 noisy candidates exposed:
0

Automatic external calls from read endpoints:
0

Tests passed:
Tests failed:

V1 unchanged:
PASS / FAIL

V2 unchanged:
PASS / FAIL

V3 unchanged:
PASS / FAIL

External overlay unchanged:
PASS / FAIL

Frontend unchanged:
PASS / FAIL

CCR untouched:
PASS / FAIL

READY FOR FINAL UI REBUILD:
YES / NO

Then STOP.
