I am building an internal Lending Portfolio Intelligence POC in a React/Vite frontend.

I need to add an interactive geographic portfolio map using existing governed country-level data.

IMPORTANT:
This is Lending only. Ignore CCR.

The application currently has:
- client CAGID
- client name
- country / country-of-risk label
- reported OSUC
- CAM count / CAM coverage
- sector
- relationship information

We DO NOT currently have governed latitude/longitude coordinates for individual clients.

Therefore the map should initially work at COUNTRY LEVEL only:
- country choropleth or country bubble/centroid visualization
- aggregate Reported OSUC by country
- aggregate client count by country
- CAM-covered vs non-CAM clients
- click country to filter the portfolio
- hover country to show metrics
- no invented client coordinates

Please tell me which mapping libraries/frameworks are actually APPROVED and AVAILABLE for use inside Citi internal applications in this environment.

For each approved option provide:

1. exact library/package name
2. whether npm installation is allowed
3. whether it requires an external API key
4. whether it requires internet access at runtime
5. whether map tiles are fetched externally
6. whether OpenStreetMap tiles are approved for internal use
7. whether local/offline GeoJSON or TopoJSON country boundaries are permitted
8. whether Leaflet is approved
9. whether OpenLayers is approved
10. whether D3 geographic maps are approved
11. whether ECharts maps are approved
12. whether Mapbox is approved
13. whether any Citi-approved internal map component/library already exists

Most importantly:

Recommend the APPROVED option for a React/Vite application that can render a world/country map without sending client data externally.

If external public tile services are not permitted, identify the approved approach for rendering a local country-level map from bundled GeoJSON/TopoJSON.

Do not provide generic open-source recommendations.
I need Citi-specific approved/available options only.
