LENDING — REMOVE ALL CCR CONTAMINATION BEFORE PROMPT 4D

Work only in the CURRENT Lending repository/worktree.

This is a Lending-only correction.

DO NOT implement Prompt 4D yet.

OBJECTIVE

The Lending product must contain no CCR dependency, CCR runtime path, CCR data dependency,
CCR product semantics, CCR route ownership, CCR customer-master dependency, or CCR-derived
authority.

CCR is a completely separate product.

The Lending application must stand independently without requiring, importing, reading,
routing through, or reasoning from CCR assets.

IMPORTANT

Do not modify the CCR product itself.

Do not delete legitimate CCR repository assets merely because they coexist in the monorepo.

The requirement is:

    CCR MUST NOT PARTICIPATE IN LENDING.

Existing CCR files may remain elsewhere in the repository if they belong to the separate CCR
product, but Lending code, Lending APIs, Lending routes, Lending loaders, Lending reports,
Lending frontend, Lending tests, and Lending authority contracts must not depend on them.

--------------------------------------------------
1. FIRST — AUDIT ALL CCR REFERENCES
--------------------------------------------------

Search the complete Lending implementation for:

    CCR
    ccr
    Customer_latest
    Customer_latest.parquet
    customer master
    customer_master
    /ccr
    portfolio/ccr
    ccr_clients
    ccr relationship
    relationships.py

Inspect at minimum:

    backend/app/
    backend/data/
    backend/tests/
    frontend/src/
    scripts/
    Lending reports and architecture documents

Classify every occurrence as one of:

A. Separate CCR product asset
B. Historical documentation only
C. Shared legacy code
D. Active Lending dependency
E. Active Lending import
F. Active Lending route
G. Active Lending data read
H. Active Lending API behavior
I. Active Lending frontend behavior
J. Test-only dependency

Do not assume that a file is harmless simply because its name is legacy.

Trace actual imports, calls, routes, readers, and runtime paths.

--------------------------------------------------
2. LENDING RUNTIME MUST HAVE ZERO CCR DEPENDENCIES
--------------------------------------------------

Verify and enforce that ordinary Lending runtime paths do NOT:

- import CCR-specific modules;
- read backend/data/ccr;
- read Customer_latest.parquet;
- read CCR customer-master files;
- read ccr_clients.sqlite3;
- use CCR identifiers as Lending entity authority;
- call CCR relationship engines;
- use CCR relationship tables;
- use CCR source discovery;
- use CCR normalization;
- use CCR proposal logic;
- route through CCR endpoints;
- redirect Lending users into CCR routes;
- use CCR counts in Lending metrics;
- use CCR entity populations in Lending denominators;
- use CCR evidence in Lending relationship truth;
- use CCR taxonomy as Lending taxonomy.

This applies to:

    /lending
    /lending/clients
    /lending/client/{cagid}
    /lending/network
    /lending/relationships
    /lending/workbench
    /lending/review
    /lending/external-research
    all /api/lending/* routes

--------------------------------------------------
3. REMOVE LEGACY CCR ROUTING FROM LENDING
--------------------------------------------------

Inspect frontend/src/App.tsx and all router definitions.

Lending must not own, advertise, redirect, alias, or expose routes such as:

    /ccr
    /portfolio/ccr

If those routes belong to the separate CCR product, leave the CCR application itself intact,
but remove them from the Lending route family.

No Lending navigation item should point to CCR.

No Lending fallback route should silently redirect CCR URLs into Lending.

--------------------------------------------------
4. REMOVE SHARED CCR BUSINESS LOGIC FROM LENDING
--------------------------------------------------

Inspect:

    backend/app/core/relationships.py

and any equivalent shared relationship modules.

If that module contains mixed Lending and CCR business logic:

- identify exactly what Lending currently imports;
- isolate Lending behavior behind Lending-specific modules/contracts;
- remove Lending dependence on CCR-specific branches;
- do not rewrite or destroy CCR behavior;
- do not create another duplicate relationship database.

The end state must make the product boundary explicit:

    Lending logic -> Lending modules/data/contracts
    CCR logic     -> CCR modules/data/contracts

No Lending execution path should need a CCR conditional branch.

--------------------------------------------------
5. DATA AUTHORITY
--------------------------------------------------

Lending authority remains:

    CAM/V3 = authoritative relationship truth.

Other currently governed Lending lanes may remain as previously established:

    V2 fallback/history
    normalized operational projection
    external research supplemental lane
    governed AI lane

But these must remain Lending-specific.

CCR customer master is NOT a Lending population source.

Customer_latest.parquet is NOT a Lending source.

CCR entity resolution is NOT Lending entity resolution.

CCR relationship evidence is NOT Lending relationship evidence.

Do not use CCR data to fill gaps in Lending.

--------------------------------------------------
6. REPORT CLEANUP
--------------------------------------------------

The current:

    LENDING_IMPLEMENTATION_REBASELINE.md

contains CCR-specific material.

Rewrite the Lending baseline so it describes Lending only.

Remove sections such as:

    CCR contamination check
    CCR/shared surfaces
    CCR customer-master analysis
    Customer_latest.parquet discussion
    CCR-specific route discussion

unless a single short architectural boundary statement is necessary.

If retained at all, the only permitted statement is conceptually:

    "Lending is isolated from other product data domains."

Do not make CCR part of the Lending architecture narrative.

The Lending implementation report should be understandable without knowing CCR exists.

--------------------------------------------------
7. VERIFY ZERO ACTIVE REFERENCES
--------------------------------------------------

After remediation, run searches demonstrating that active Lending code contains no CCR
dependency.

Report separately:

1. CCR references remaining in separate CCR-owned directories.
2. CCR references remaining in historical/archive documentation.
3. CCR references remaining in ACTIVE Lending runtime code.

The required value for #3 is:

    0

Also report:

- active Lending imports of CCR code = 0
- Lending reads of CCR data = 0
- Lending API calls into CCR = 0
- Lending frontend CCR routes = 0
- Lending CCR redirects = 0
- Lending tests depending on CCR fixtures = 0
- Customer_latest.parquet Lending reads = 0

--------------------------------------------------
8. REGRESSION VALIDATION
--------------------------------------------------

Run the existing Lending regression suites.

At minimum validate:

- Home
- Portfolio
- Client Detail
- Network
- Lending status
- CAM/V3 relationship projection
- review summary
- existing Prompt 4A
- existing Prompt 4B
- existing Prompt 4C

Confirm that removal of CCR coupling does not change legitimate Lending counts or authority.

Do not alter CAM/V3 authority.

Do not fabricate replacement data.

Do not broaden the Lending population.

--------------------------------------------------
9. OUTPUT REPORT
--------------------------------------------------

Create:

    backend/data/LENDING_CCR_ISOLATION_REPORT.md

Include:

1. every CCR reference discovered;
2. classification of each reference;
3. whether it was removed, isolated, or retained outside Lending;
4. files changed;
5. runtime dependency verification;
6. route verification;
7. data-read verification;
8. test results;
9. final Lending authority statement.

The report must end with exactly one of:

    LENDING CCR ISOLATION: PASS
    LENDING CCR ISOLATION: FAIL

PASS requires zero active Lending dependency on CCR.

If PASS, the final line must be:

    READY FOR PROMPT 4D

If FAIL, stop and identify the exact remaining dependency.

--------------------------------------------------
STRICT NON-GOALS
--------------------------------------------------

Do NOT:

- implement Prompt 4D;
- redesign CCR;
- modify CCR business data;
- migrate CCR databases;
- use Customer_latest.parquet;
- merge CCR and Lending;
- build a shared universal customer master;
- create a universal relationship denominator;
- call external providers;
- perform SEC/GLEIF/web research;
- change CAM/V3 authority;
- invent replacement Lending data.

The sole purpose of this task is to make Lending completely independent from CCR and to
establish a clean Lending baseline before Prompt 4D.
