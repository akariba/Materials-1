I understand you are providing internal documentation/knowledge, not executing queries against the database.
Based only on the available Citi/AMC Confluence documentation, prepare the exact technical integration specification needed for a developer in VS Code to consume:
- AMCDATA.LEI_GENERAL_INFO
- AMCDATA.LEI_LEI_REL
I need implementation details, not another conceptual assessment.
For each dataset provide:
1. Exact platform/system where the table physically resides.
2. Exact database/catalog/schema/table or view name.
3. Supported access mechanism:
   - JDBC
   - ODBC
   - internal API
   - Spark
   - data service
   - file/extract
   - other
4. Connection/service name if documented.
5. Required entitlement/access group if documented.
6. Exact column names and types relevant to:
   - GFCID
   - LEI
   - legal name
   - entity status
   - jurisdiction
   - relationship type
   - child LEI/GFCID
   - parent LEI/GFCID
   - relationship status
   - effective/start/end dates
   - source/update/version dates
7. Exact join keys between LEI_GENERAL_INFO and LEI_LEI_REL.
8. Exact documented mapping to GFCID / Client Universe.
9. Meaning of DIRECTPARENT and ULTIMATEPARENT.
10. Whether rows are current-state or historical/versioned.
11. Refresh frequency.
12. Any known duplicate/cardinality rules.
13. Any documented data-quality caveats.
14. Read-only example SQL for:
    - lookup by GFCID
    - lookup by LEI
    - retrieve direct parent
    - retrieve ultimate parent
15. Existing internal service/API/view that should be preferred over direct table access, if one exists.
Do not claim that you queried live data unless you actually did.
Clearly mark each item as:
- DOCUMENTED
- NOT DOCUMENTED
- INFERRED
The output will be handed to a developer implementing this in VS Code.
