IMPLEMENT ONLY THE LENDING GEOGRAPHIC MAP ENHANCEMENT.

Do not redesign the rest of the application.

SCOPE: LENDING ONLY.
Do not touch CCR.

HARD BOUNDARIES

Do NOT modify:
- V1 / V2 / V3 relationship data
- extraction
- CAM relationship logic
- portfolio calculations
- OSUC calculations
- external-overlay logic
- Stylus / R2D2 / SEC
- backend relationship governance
- existing Lending navigation
- existing Network implementation except where country filtering already integrates naturally

Do not use mock data.

CURRENT STATE

The Lending Overview already contains a Portfolio Geography section showing
country names and horizontal exposure bars.

The governed Portfolio API already provides country-level portfolio data.

We currently DO NOT have governed client latitude/longitude coordinates.

Therefore:
- DO NOT invent client coordinates
- DO NOT geocode client addresses
- DO NOT place individual clients on guessed centroids
- DO NOT make external map/tile/API calls

MAP ARCHITECTURE

Implement a COUNTRY-LEVEL world map using:

Preferred:
- D3 geographic rendering
- locally bundled GeoJSON or TopoJSON country boundaries

No runtime external dependency calls.

Before implementation:
1. Check whether D3 is already available in the project.
2. Check whether the required package is available through the existing
   approved/internal npm configuration.
3. Do NOT pull from a public CDN.
4. Do NOT fetch GeoJSON/TopoJSON at runtime.
5. The country-boundary asset must be stored locally in the frontend bundle.

If D3 cannot be obtained through the current approved/internal environment,
STOP and report the blocker. Do not silently substitute Mapbox, Google Maps,
Leaflet + public tiles, OpenStreetMap tiles, or another external service.

GEOGRAPHY DATA

Use ONLY the existing governed portfolio API country field.

Aggregate by country:

- client count
- Reported OSUC
- CAM-covered client count
- non-CAM client count
- CAM client coverage %
- CAM-covered OSUC
- CAM OSUC coverage % where already available/derivable from governed values

Do not invent missing metrics.

COUNTRY NORMALIZATION

Create a small deterministic normalization layer only where necessary to match
portfolio country names to the local geographic boundary dataset.

Examples may include formatting differences such as:
- UNITED STATES OF AMERICA (THE)
- UNITED KINGDOM OF GREAT BRITAIN...
- KOREA THE REPUBLIC OF

Do not alter the underlying source data.
Normalization is visualization-only.

MAP DESIGN

Use the same visual language as the existing Lending application:

- white / very-light-blue canvas
- blue / teal geographic palette
- subtle purple accents where already used
- orange only for attention / uncovered exposure
- thin boundaries
- clean institutional appearance
- no dark basemap
- no street tiles

Default map metric:
REPORTED OSUC

Country fill intensity:
larger Reported OSUC = stronger blue/teal intensity.

Provide metric selector:

[ Reported OSUC ]
[ Client Count ]
[ CAM Coverage ]

CAM Coverage may use a teal intensity scale.

INTERACTION

Hover over a country:
show compact tooltip:

Country
Reported OSUC
Portfolio share
Clients
CAM-covered clients
Without CAM
CAM client coverage %
CAM OSUC coverage % if available

Click a country:
- visually select it
- use a subtle glow/pulse highlight
- filter the existing Lending client population to that country
- update the corresponding client table/list
- show a small country summary panel

Click selected country again or press Clear:
remove geography filter.

Do NOT trigger external research from map interaction.

VISUAL EFFECTS

Use restrained animation:

- smooth 200–350 ms fill transitions
- selected country outline/glow
- subtle one-time pulse when selected
- tooltip fade
- no continuous distracting animation

The “flash/light” effect should communicate selection only.

MAP CONTROLS

Include:

Metric:
Reported OSUC | Client Count | CAM Coverage

CAM:
All | With CAM | Without CAM

Optional sector selector:
All sectors + values already supplied by API

Reset map

Do not create filters based on fields not currently available.

LAYOUT

On Lending Overview:

Replace the existing long Portfolio Geography bar-list presentation with:

----------------------------------------------------
| PORTFOLIO GEOGRAPHY                             |
| Interactive geographic concentration           |
|                                                  |
|       LARGE WORLD MAP              | SUMMARY    |
|                                    | Country    |
|                                    | OSUC       |
|                                    | Clients    |
|                                    | CAM cov.   |
----------------------------------------------------

The world map should be visually significant, not a tiny widget.

Below the map retain a compact ranked list:
Top countries by current selected metric.

Do not duplicate the existing giant country list.

EMPTY / UNMATCHED DATA

If a portfolio country cannot be matched to the boundary asset:
- keep it in portfolio totals
- display it under “Unmapped country labels”
- never silently drop its exposure
- do not fabricate geography

DATA INTEGRITY

Reconcile map aggregates against existing portfolio totals.

Specifically ensure map/filter implementation does not change:

Portfolio clients = 2,484
CAM-covered clients = 1,698
Without CAM = 786
Exactly 1 CAM = 928
Exactly 2 CAMs = 770
Reported OSUC ≈ $349.27B
CAM-covered OSUC ≈ $259.93B
V3 canonical relationships = 13
V3 review-required = 28

The map is a visualization/filter layer only.

VALIDATION

Verify:

1. Lending frontend compiles.
2. /lending loads.
3. Overview renders.
4. World map renders from LOCAL geographic asset.
5. Browser network inspection shows NO map tile/API requests.
6. Country hover works.
7. Country click filtering works.
8. Reset works.
9. Portfolio totals remain unchanged.
10. No external research call occurs.
11. CCR unchanged.
12. V1/V2/V3 unchanged.

Final response only:

LENDING WORLD MAP: PASS / FAIL
LOCAL GEO ASSET: PASS / FAIL
EXTERNAL MAP CALLS: 0 / <number>
COUNTRY MATCHED: X
COUNTRY UNMATCHED: X
PORTFOLIO RECONCILIATION: PASS / FAIL
COUNTRY FILTER: PASS / FAIL
HOVER TOOLTIP: PASS / FAIL
SELECTED COUNTRY ANIMATION: PASS / FAIL
V1/V2/V3 UNCHANGED: PASS / FAIL
CCR UNCHANGED: PASS / FAIL

List any unmatched country labels.

Then STOP.
