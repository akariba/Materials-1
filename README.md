DO NOT IMPLEMENT OR REDESIGN ANYTHING YET.

The Lending world-map attempt stopped correctly because:
- no local GeoJSON/TopoJSON/SVG country-boundary asset was found
- D3 is not installed
- approved internal npm registry returned HTTP 401

Perform READ-ONLY discovery only.

SCOPE: LENDING MAP DEPENDENCY DISCOVERY.

Do not modify:
- frontend code
- backend code
- V1/V2/V3
- portfolio calculations
- relationship data
- Stylus/R2D2/SEC
- CCR
- package.json
- package-lock.json
- npm configuration

SEARCH FOR EXISTING LOCAL MAP CAPABILITY

Inspect the current repository and available local frontend dependencies for:

1. d3
2. d3-geo
3. topojson-client
4. world-atlas
5. react-simple-maps
6. echarts geographic/map support
7. any existing geographic/map package already installed
8. any local:
   - .geojson
   - .topojson
   - world*.json
   - countries*.json
   - country*.json
   - world*.svg
   - map*.svg
   - geographic boundary asset

Also inspect:
- frontend/node_modules
- npm cache if locally accessible
- repository public/assets directories
- existing HTML prototype/reference files
- any bundled static assets already included in the application

Do not search the public internet.
Do not install anything.
Do not authenticate or modify npm configuration.

SPECIFIC FALLBACK CHECK

Determine whether an existing LOCAL world SVG exists where countries have
stable identifiers such as:
- ISO2
- ISO3
- country name
- path id

If such SVG exists, report whether the map can be implemented directly using
React/SVG WITHOUT D3.

Also determine whether an already-installed charting library can render a
locally supplied map WITHOUT runtime external calls.

INTERNAL NPM

Inspect current npm configuration READ-ONLY and report:

- configured registry URL
- whether authentication appears missing/expired
- exact HTTP 401 source
- whether other packages from that same internal registry are already installed

Do not attempt to fix credentials.

FINAL RESPONSE ONLY:

LOCAL D3: YES / NO
LOCAL D3-GEO: YES / NO
LOCAL TOPOJSON CLIENT: YES / NO
LOCAL WORLD ATLAS: YES / NO

EXISTING MAP LIBRARY:
<name or NONE>

LOCAL GEOJSON/TOPOJSON:
<paths or NONE>

LOCAL WORLD SVG:
<path or NONE>

SVG DIRECT RENDER POSSIBLE:
YES / NO

NPM REGISTRY:
<registry>

NPM 401 CAUSE:
<what can be established without guessing>

MAP CAN BE BUILT WITHOUT NEW PACKAGE:
YES / NO

MINIMUM MISSING ASSET:
<exact asset/package needed>

RECOMMENDED NEXT STEP:
<one concise recommendation>

Then STOP.
