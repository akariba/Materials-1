CONTINUE THE LENDING POC.

The approved local world-country geometry asset is now available at:

frontend/public/countries.geojson

IMPORTANT:
- Use this LOCAL asset only.
- Do NOT install D3.
- Do NOT install Leaflet.
- Do NOT install topojson-client.
- Do NOT use Mapbox, Google Maps, OpenStreetMap tiles, CDN map tiles, or any external runtime map/API call.
- Render the GeoJSON directly with React/SVG.
- Do not fabricate coordinates or geometry.

SCOPE

Implement the real interactive Lending Portfolio Geography map using the
existing validated Portfolio API data and the local GeoJSON.

Do not redesign the rest of the Lending application.

DO NOT modify:
- V1/V2/V3
- relationship extraction
- canonical/review relationship data
- portfolio calculations
- OSUC calculations
- external overlay
- Stylus/R2D2/SEC
- backend governance
- CCR

1. GEOJSON VALIDATION

Read:

frontend/public/countries.geojson

Confirm:
- valid GeoJSON FeatureCollection
- number of country features
- available country-name property
- available ISO2 property
- available ISO3 property

Determine the exact property names from the file itself.
Do not assume them.

2. COUNTRY RECONCILIATION

Reconcile the existing governed Portfolio API country labels against the
GeoJSON using deterministic matching.

Preferred matching order:

1. ISO code where available
2. exact normalized country name
3. explicit controlled alias table only where necessary

Examples of labels already present in the portfolio may include:

UNITED STATES OF AMERICA (THE)
UNITED KINGDOM OF GREAT BRITAIN
KOREA THE REPUBLIC OF
RUSSIAN FEDERATION (THE)

Create explicit aliases only where required.

Do NOT use fuzzy matching that could assign a client to the wrong country.

Produce:
- matched country count
- unmatched portfolio country labels
- client total reconciliation
- OSUC total reconciliation

The map must not silently drop exposure.

3. MAP

Replace the current "Geographic analytics not available" placeholder with a
real world choropleth.

Use the existing Lending light visual design.

Map behavior:

- countries with portfolio exposure are filled according to Reported OSUC
- countries without portfolio exposure remain neutral/light
- use the current dashboard palette:
  teal / blue / violet / amber accents
- do not use an aggressive rainbow heatmap

The map should visually feel consistent with the existing Lending UI.

4. INTERACTIONS

Hover on country:

show a clean tooltip containing:

Country
Client count
Reported OSUC
Portfolio share
Clients with CAM
Clients without CAM
CAM client coverage %
CAM-covered OSUC if available
CAM OSUC coverage % if available

Click country:

- select the country
- give the selected country a visible glow/pulse/highlight
- filter the associated country analytics/client list
- preserve selected state until cleared
- provide "Reset country" action

Use a subtle professional pulse, not decorative flashing.

5. GEOGRAPHY ANALYTICS

Keep the existing country ranking beside/below the map.

Selecting a country either from:
- map
or
- country ranking

must update the same selected-country state.

Show top-country metrics using actual API values only.

Do not hard-code geography values.

6. OVERVIEW INTEGRATION

On the main Lending Overview, upgrade the Geography section so that it shows:

- real compact world map
- top countries by Reported OSUC
- selected-country summary when clicked

The full Geography interaction can expand within the existing analytics
experience.

Do NOT make the Overview crowded.

7. CLIENT FILTER INTEGRATION

When a country is selected and the user chooses "View clients":

navigate/filter the existing Clients view using that exact country.

Do not create a duplicate client dataset.

8. VISUAL INTERACTION

Implement professional interaction states:

- hover country: slight brightness/lift
- selected country: glowing outline/pulse
- changing selected country: smooth transition
- tooltip follows/anchors to hovered country
- accessible selected state

No excessive animation.

9. DATA GOVERNANCE

Geography represents PORTFOLIO EXPOSURE geography.

It is NOT relationship-network geography.

Do not imply causal risk, relationship location, or geographic dependency.

Reported OSUC remains marked supplemental according to the existing
governance metadata.

10. ACCEPTANCE TEST

Verify:

- local GeoJSON loads successfully
- external map calls = 0
- map renders
- all mapped values come from validated Portfolio API
- portfolio client reconciliation = 2,484
- CAM-covered = 1,698
- without CAM = 786
- reported OSUC reconciles to approximately $349.27B
- clicking country filters correctly
- hover tooltip works
- reset works
- selected-country glow/pulse works
- Overview map works
- Clients country filter works
- no automatic external research call
- V1/V2/V3 unchanged
- CCR untouched

If any country labels cannot be matched, DO NOT invent a match.
Report them explicitly.

FINAL RESPONSE ONLY:

GEOJSON VALID: PASS / FAIL
COUNTRY FEATURES: X
PORTFOLIO COUNTRIES: X
MATCHED COUNTRIES: X
UNMATCHED COUNTRIES: <list>
CLIENT RECONCILIATION: X / 2484
OSUC RECONCILIATION: <value>
WORLD MAP: PASS / FAIL
HOVER TOOLTIP: PASS / FAIL
COUNTRY CLICK/FILTER: PASS / FAIL
SELECTED COUNTRY ANIMATION: PASS / FAIL
CLIENT FILTER INTEGRATION: PASS / FAIL
EXTERNAL MAP CALLS: 0 / <number>
V1/V2/V3 UNCHANGED: PASS / FAIL
CCR UNCHANGED: PASS / FAIL

Then STOP.
