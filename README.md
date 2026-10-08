FIX STRESS ANALYTICS WORLD MAP ONLY.

Do not redesign the Stress Analytics page.
Do not modify backend data.
Do not touch CCRIG recovery, DuckDB/Parquet, CAM, relationships, or demo logic.

The current map behavior is incorrect.

==================================================
PROBLEM
==================================================

The current implementation appears to:

1. take countries contained in the live API response
2. filter the GeoJSON to those countries
3. calculate geographic bounds from only those countries
4. fit those bounds to the entire SVG

Because the current live data primarily contains the United States,
the entire map becomes a large USA map.

That is NOT the intended design.

Stress Analytics is a GLOBAL country-of-risk map.

==================================================
EXPECTED MAP
==================================================

Always render the COMPLETE WORLD MAP.

All countries from:

frontend/public/countries.geojson

must remain visible regardless of whether they have live risk data.

Live API data should COLOR / annotate countries.

It must NOT determine the geographic viewport.

Conceptually:

FULL WORLD GEOJSON
      +
LIVE COUNTRY RISK DATA
      ↓
JOIN BY NORMALIZED COUNTRY / ISO CODE
      ↓
COLOR MATCHED COUNTRIES
      ↓
UNMATCHED COUNTRIES REMAIN NEUTRAL

==================================================
PROJECTION
==================================================

Use a normal professional world-map projection.

Preferred:

d3.geoNaturalEarth1()

or, if the current implementation already uses another appropriate
world projection, preserve it.

Use projection.fitExtent() / fitSize() against the FULL WORLD
FeatureCollection.

IMPORTANT:

NEVER calculate the projection extent from only countries returned by
the risk API.

Projection bounds must come from the complete world geometry.

==================================================
COUNTRY DISPLAY
==================================================

Render every country polygon.

Countries with live risk data:

RED
AMBER
GREEN
UNKNOWN

according to the existing stress-signal logic.

Countries without records:

neutral light grey / existing "No live row" styling.

Do not hide countries without exposure.

The purpose is to preserve geographic context.

==================================================
DATA JOIN
==================================================

Keep current country normalization / ISO matching.

Join the API records onto the world polygons.

Example:

United States risk row
        ↓
match USA polygon
        ↓
color USA

Poland has no row
        ↓
still render Poland
        ↓
neutral

China has no row
        ↓
still render China
        ↓
neutral

Do NOT remove Poland/China/etc. from the geometry.

==================================================
ENTITY MARKERS
==================================================

Entity markers may be shown on countries containing relevant entities.

Do not allow markers to alter map projection or bounds.

If multiple entities have the same country of risk, cluster/offset them
slightly if necessary rather than changing map extent.

==================================================
VIEWPORT
==================================================

The first view must show approximately:

North America
South America
Europe
Africa
Asia
Australia

in one global view.

Do not automatically zoom to USA or another active country.

Later interactive zoom/pan is fine, but initial state must be WORLD.

==================================================
RESPONSIVE SIZE
==================================================

Use the available Stress Analytics panel width.

Maintain the map aspect ratio.

Do not distort country geometry to fill the container.

Leave reasonable margins around the world geometry.

==================================================
DO NOT CHANGE
==================================================

Do not change:

- Stress Analytics business logic
- stress classifications
- API schema
- country-of-risk derivation
- backend
- Correlation page
- Portfolio Analytics
- Risk Heatmap
- overall CSS/theme

This is only a geographic rendering correction.

==================================================
ACCEPTANCE TEST
==================================================

With the current dataset containing mainly USA records:

[ ] complete world is visible
[ ] USA is visible in its correct geographic position
[ ] Europe is visible
[ ] Africa is visible
[ ] Asia is visible
[ ] South America is visible
[ ] Australia is visible
[ ] USA receives its live risk styling
[ ] countries without rows remain neutral
[ ] NVIDIA marker remains associated with USA if appropriate
[ ] map does not zoom automatically to USA
[ ] country shapes are not stretched/distorted
[ ] existing legend still works
[ ] compile passes

Take a browser screenshot after the fix.

STOP after the world-map rendering is corrected.