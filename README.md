CONTINUE ONLY THE LENDING GEOGRAPHY MAP TASK.

The required local GeoJSON asset is now available at:

frontend/public/countries.geojson

Use this local file only.

DO NOT:
- install D3 or any new npm package
- make external map/API/tile calls
- use OpenStreetMap, Mapbox, Google Maps, Leaflet, or external CDN assets
- fabricate coordinates or geometry
- change V1/V2/V3
- change backend calculations
- change relationship data
- change external research / Stylus / R2D2 / SEC
- touch CCR
- redesign the rest of the Lending UI

TASK

1. Validate frontend/public/countries.geojson:
   - valid GeoJSON FeatureCollection
   - country polygons present
   - identify available country properties such as ADMIN, ISO_A2, ISO_A3

2. Build the Lending portfolio world map directly with React + SVG using the supplied GeoJSON geometry.

3. Match the governed Lending portfolio country labels from the Portfolio API to the GeoJSON countries.
   Create explicit normalization aliases where required, for example:
   - UNITED STATES OF AMERICA (THE) -> United States of America
   - UNITED KINGDOM OF GREAT BRITAIN... -> United Kingdom
   - KOREA THE REPUBLIC OF -> South Korea
   etc.
   Do not guess silently. Record every normalization.

4. Geography map behavior:
   - world choropleth
   - country fill intensity based on Reported OSUC
   - optional toggle: Reported OSUC / Client count
   - hover tooltip:
       country
       client count
       CAM-covered client count
       clients without CAM
       Reported OSUC
       portfolio share
   - click country filters the Lending client population
   - selected country gets a visible highlighted/glow state
   - smooth hover/highlight transition
   - Reset geography filter action

5. Keep the same light-blue / white Lending visual system already used in the application.

6. Replace the current text-only "Portfolio geography" fallback with the actual interactive map.
   Keep the ranked country list beside or below the map as supporting analytics.

7. Reconcile totals. The map aggregation must reconcile back to the current Portfolio API totals. Do not create or alter exposure numbers.

8. Verify no external network request is made for map rendering after application load.

FINAL RESPONSE ONLY:

GEOJSON VALID: PASS / FAIL
COUNTRIES IN GEOJSON: X
PORTFOLIO COUNTRY LABELS: X
MATCHED: X
UNMATCHED: X

WORLD MAP RENDERED: PASS / FAIL
HOVER TOOLTIP: PASS / FAIL
COUNTRY FILTER: PASS / FAIL
SELECTED COUNTRY HIGHLIGHT: PASS / FAIL
RESET FILTER: PASS / FAIL
OSUC RECONCILIATION: PASS / FAIL
EXTERNAL MAP CALLS: 0 / <number>

V1/V2/V3 UNCHANGED: PASS / FAIL
CCR UNCHANGED: PASS / FAIL
BACKEND CALCULATIONS UNCHANGED: PASS / FAIL

Then STOP.
