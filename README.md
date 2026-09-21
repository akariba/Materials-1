==================================================
47. ANALYTICS EXPERIENCE — REQUIRED
==================================================

The final POC must be a genuine analytics application.

Do not interpret this specification as primarily tables and KPI cards.

The Overview and analytical pages must include visual analytics wherever the
validated backend supports them.

A. PORTFOLIO ANALYTICS

Required on Overview:

1. Exposure ranking
   - ranked clients by Reported OSUC
   - rank number
   - portfolio share
   - CAM status
   - sector
   - click client -> Client Detail

2. Sector concentration
   - horizontal ranked bar chart
   - toggle:
       Reported OSUC
       Client Count
   - click sector -> filtered Clients view

3. CAM coverage analytics
   - With CAM vs Without CAM
   - 1 CAM vs 2 CAMs
   - client coverage %
   - OSUC coverage %
   - use a clean stacked bar / donut / equivalent visual

4. Exposure concentration
   - Top 10 / Top 20 exposure contribution where deterministically calculated
   - cumulative portfolio share if available/calculable
   - no invented materiality thresholds

B. GEOGRAPHIC MAP

If validated country/geographic data is available through the Portfolio API,
include an interactive geographic portfolio map.

The geographic map should represent:

- client count by country
or
- Reported OSUC by country

Provide a toggle where both are available.

Clicking a country should filter/drill into the underlying clients.

IMPORTANT:

The geographic map represents portfolio geography/exposure.

It is NOT the relationship network.

Do not fabricate geographic coordinates or countries.

If the API does not expose sufficient geographic data, show a clean
"Geographic analytics not available in current POC" state rather than fake
data.

C. RELATIONSHIP NETWORK MAP

Keep a separate relationship network visualization.

Overview:
small network preview only.

Dedicated Network page:
full interactive network.

The relationship network should visually communicate:

- entities = nodes
- relationships = edges
- CAM canonical = authoritative solid edge
- review-required = clearly distinct dashed edge
- external proposal = supplemental distinct edge
- indirect/hidden path = path representation only when backend-supported
- node size may represent Reported OSUC when Exposure lens is active

Required interactions:

- pan
- zoom
- fit view
- search entity
- select node
- select relationship
- evidence drilldown
- filters
- lens switching

Do not render the entire population as a network.

Only render relevant evidence-backed relationships.

D. ANALYTICS LENSES

Dedicated Network page must support these working lenses where data exists:

1. CAM
   authoritative relationship structure

2. Exposure
   node size / context based on Reported OSUC

3. Hidden / Indirect
   evidence-backed multi-hop paths only

4. External SEC/Web
   external corroborations / proposals / conflicts

Prepare but DO NOT fabricate:

5. Market & News
6. AI Ecosystem
7. Potential Impact

If those datasets are not yet connected, display them as disabled
"Future capability".

E. RANKINGS

Provide useful rankings without creating a fake risk score.

Examples:

- Exposure Rank
- Sector Exposure Rank
- Portfolio Share
- CAM Coverage by sector
- largest uncovered exposure clients
- clients with highest exposure and review-required relationships

Rankings must be based only on available deterministic data.

Do NOT create an opaque composite ranking.

F. ANALYTICS STORY

The Overview should visually flow:

PORTFOLIO SCALE
    ↓
CAM COVERAGE
    ↓
EXPOSURE / SECTOR CONCENTRATION
    ↓
GEOGRAPHIC DISTRIBUTION
    ↓
CLIENT RANKING
    ↓
RELATIONSHIP INTELLIGENCE
    ↓
ITEMS REQUIRING REVIEW

The user should understand the portfolio before opening the detailed
relationship network.

G. DRILLDOWN

Every major analytics visual should lead somewhere useful:

Sector bar -> filtered Clients
Country map -> filtered Clients
Exposure ranking -> Client Detail
CAM segment -> filtered Clients
Network node -> Client/Entity Detail
Network edge -> Relationship Detail
Review metric -> Review Queue

Avoid dead visualizations.

H. VISUAL BALANCE

Do NOT place all analytics on one enormous screen.

Use clear sections and progressive disclosure.

Overview:
executive analytics summary.

Clients:
population analytics and ranking.

Network:
relationship analytics.

Relationship Explorer:
record/evidence analytics.

Review Queue:
exception analytics.

The result must feel like a professional Lending portfolio intelligence
workbench rather than a collection of charts.
