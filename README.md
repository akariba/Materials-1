A compliant local world-country SVG asset has now been supplied.

DO NOT install D3 or any other map package.
DO NOT call any external tile service.
DO NOT modify backend calculations, V1/V2/V3, relationship extraction,
external research, Stylus/R2D2/SEC, or CCR.

TASK

Inspect the supplied local world SVG.

First verify:
- every country is represented by an individual path
- country identifiers are available through ISO2, ISO3, path id, or country name
- no external runtime resources exist
- no remote scripts, images, fonts, tiles, or URLs are required

Then integrate it into the existing Lending Portfolio Geography section.

Use the existing governed Portfolio API country statistics.

MAP BEHAVIOR

Render a real interactive world map.

For every country successfully matched:

- fill intensity based on Reported OSUC
- hover highlight
- smooth glow/flash transition
- tooltip containing:
    country
    client count
    CAM-covered count
    without-CAM count
    Reported OSUC
    portfolio OSUC share
    CAM coverage %
- click country filters the Lending client population
- clicking the selected country again clears the filter
- selected country gets a stronger outline/glow
- keep the existing country ranking/list synchronized with map selection

COUNTRY MATCHING

Build an explicit normalization table between Portfolio API country labels
and SVG country identifiers.

Do not silently fuzzy-match ambiguous countries.

Produce:
- matched country count
- unmatched country count
- explicit unmatched list

Expected portfolio country labels: 88.

Do not fabricate coordinates or country boundaries.

VISUAL STYLE

Use the existing Lending visual language:

- light background
- soft blue base countries
- deeper blue for increasing OSUC
- teal selection/glow
- subtle animated highlight on hover/selection
- clean institutional style
- no dark-map redesign
- no unnecessary map controls

Do not redesign the rest of the page.

VALIDATION

Confirm:
- total client count remains 2,484
- reported OSUC remains approximately $349.27B
- CAM-covered count remains 1,698
- no API or analytics calculations changed
- no external runtime calls
- country click correctly filters clients
- clearing selection restores all 2,484 clients

Final response:

LOCAL SVG VALIDATION: PASS / FAIL
COUNTRIES IN SVG: X
PORTFOLIO COUNTRY LABELS: 88
COUNTRIES MATCHED: X
COUNTRIES UNMATCHED: X
EXTERNAL MAP CALLS: 0 / NOT 0
PORTFOLIO RECONCILIATION: PASS / FAIL
COUNTRY FILTER: PASS / FAIL
HOVER TOOLTIP: PASS / FAIL
SELECTION GLOW: PASS / FAIL
V1/V2/V3 UNCHANGED: PASS / FAIL
CCR UNCHANGED: PASS / FAIL

Then STOP.
