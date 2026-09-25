CCR CLIENT CORRELATION — CLEAN RESET

This is a CONTROLLED CLEANUP task.

The product is being reset around ONE primary objective:

3.6M CLIENT MASTER
→ CLIENT CORRELATION
→ RELATIONSHIP DISCOVERY
→ SEC / WEB / GLEIF EVIDENCE
→ INTERACTIVE NETWORK MAP

The previous ~16k CCR-centered application is no longer the product foundation.

Do not build anything new yet.

Do not redesign anything yet.

First remove/archive the accumulated product noise while preserving valuable
source data and reusable infrastructure.

==================================================
0. SAFETY FIRST
==================================================

Before deleting anything:

1. Confirm this is a Git repository.
2. Record current branch and commit.
3. Create a recoverable Git checkpoint/tag or clean reset branch.
4. Do not destroy uncommitted user work without preserving it.
5. Produce an inventory of what will be kept and what will be removed.

Do NOT delete any authoritative source data.

Do NOT delete Git history.

==================================================
1. PRESERVE THESE ASSETS
==================================================

Identify and preserve:

A. REAL MASTER CLIENT DATA

Especially inspect and preserve:

Customer_latest.parquet

and any database that genuinely contains the complete ~3.6M client/master
population.

Do not assume the existing database is correct.
Just preserve it until validated.

B. SOURCE FILES

Preserve original:

parquet
csv
source extracts

that contain real business/client data.

C. EXTERNAL PROVIDER INFRASTRUCTURE

Preserve working reusable implementation for:

SEC
GLEIF
approved Web provider
Windows/ZSA proxy handling
TLS verification
provider request normalization
source-document retrieval

Only preserve code that is actually reusable and not coupled to the old UI.

D. EVIDENCE UTILITIES

Preserve reusable utilities for:

source-document storage
content hashing
evidence snippets
source provenance
provider audit logging

Do not preserve old workflow complexity merely because it exists.

==================================================
2. OLD PRODUCT SURFACES TO REMOVE FROM ACTIVE PRODUCT
==================================================

Remove from the ACTIVE application architecture:

Portfolio dashboard
old Entities UI
old CCR entity intelligence page
old Network implementation
Radar
Events
Research dashboard
Evidence dashboard
Review dashboard
old inspector implementation
old AI drawer
old KPI surfaces
old map implementation
old candidate starburst graph
old UI reports
old experimental UI components
legacy CSS/design systems
unused routes

The new application will NOT be rebuilt during this task.

If deletion creates unnecessary risk, move obsolete code under a clearly
isolated:

legacy/

directory that is NOT imported, routed, built or executed.

Prefer actual deletion when Git already provides recovery and dependencies are
clearly dead.

==================================================
3. REMOVE OLD CCR-CENTERED PRODUCT ASSUMPTIONS
==================================================

The new product must not be architected around:

16,769 CCR subjects
16,767 entity_registry rows
25,000 exposure rows

Those datasets may remain available as legacy/reference data but must no longer
define:

application population
entity universe
search universe
network universe
primary API architecture
frontend navigation

Do not delete authoritative data solely because it belongs to the old CCR
subset.

Just disconnect it from the new core product.

==================================================
4. DATABASE CLEANUP
==================================================

Inventory every SQLite/database artifact.

Classify each as:

AUTHORITATIVE SOURCE
MASTER CLIENT DATABASE
DERIVED DATABASE
LEGACY CCR DATABASE
TEST DATABASE
EMPTY/INVALID
DUPLICATE
UNKNOWN

Do not delete the database containing the ~3.6M master population.

Do not delete source databases before verifying their content.

Remove only databases that are conclusively:

empty
test-only
temporary
duplicate generated artifacts
obsolete UI/experimental databases

Old relationship-intelligence databases may be moved to:

legacy/data/

if they contain prior research/evidence we may want to inspect later.

The new system should eventually have one clearly named primary master client
database.

Do NOT build it yet.

==================================================
5. REPORT / GENERATED FILE CLEANUP
==================================================

Old generated reports have accumulated heavily.

Move obsolete reports to:

legacy/reports/

or remove them if Git history already preserves them.

The active backend/data directory should not contain dozens of obsolete
implementation reports.

Keep only raw/authoritative data and files needed for the new build.

==================================================
6. FRONTEND RESET
==================================================

Reduce the frontend to the smallest possible application shell.

For now it may contain only:

App
router
base styles
one temporary placeholder route

Example:

/

CLIENT CORRELATION
New application foundation

No dashboard.
No cards.
No fake graph.
No old navigation.

Do not begin the new visual design yet.

==================================================
7. BACKEND RESET
==================================================

Do NOT delete reusable provider/data utilities.

But remove old application routing from the active API where it exists solely
to support obsolete UI surfaces.

The new backend should ultimately focus on:

client universe
client search
relationship discovery
evidence
network

Do not implement those APIs yet.

Keep health/status functionality if useful.

==================================================
8. AI
==================================================

Remove AI from the active UI for now.

Do not delete reusable HELIX integration code if it is valid.

The new product will introduce AI only after the core correlation/evidence
workflow works.

AI is extra, not the product.

==================================================
9. FINAL ACTIVE REPOSITORY SHAPE
==================================================

After cleanup, the ACTIVE product should be easy to understand.

Conceptually:

data/
    authoritative master sources

backend/
    reusable core
    providers
    source/evidence utilities
    minimal API

frontend/
    minimal application shell

legacy/
    old CCR application artifacts that we intentionally retain temporarily

tests/
    only tests relevant to preserved infrastructure

There should be no ambiguity about which frontend is active.

==================================================
10. VERIFY NOTHING IMPORTANT WAS LOST
==================================================

Before completing:

verify master client source still exists

verify its size/hash did not change

verify reusable SEC code remains

verify reusable GLEIF code remains

verify approved proxy configuration/code remains

verify authoritative source datasets remain unchanged

verify Git can recover deleted legacy files

==================================================
11. DO NOT DO YET
==================================================

DO NOT:

build the 3.6M database
create relationships
run SEC discovery
run Web discovery
create correlation configuration
create network graph
create AI functionality
create dashboards

This task is CLEANUP ONLY.

==================================================
12. CREATE ONE REPORT
==================================================

Create only:

backend/data/CLIENT_CORRELATION_CLEAN_RESET_REPORT.md

It must show:

PRESERVED
REMOVED
MOVED TO LEGACY
AUTHORITATIVE DATA FOUND
DATABASES FOUND
ACTIVE FRONTEND FILES
ACTIVE BACKEND MODULES
REUSABLE PROVIDERS
UNRESOLVED ITEMS

==================================================
FINAL RESPONSE
==================================================

CLIENT CORRELATION CLEAN RESET: PASS / FAIL

AUTHORITATIVE MASTER SOURCE PRESERVED:
YES / NO

APPROXIMATE MASTER SOURCE ROWS:
<actual if already safely determinable, otherwise NOT YET PROFILED>

OLD UI REMOVED FROM ACTIVE BUILD:
YES / NO

OLD CCR WORKFLOW REMOVED FROM ACTIVE PRODUCT:
YES / NO

SEC PROVIDER CODE PRESERVED:
YES / NO

GLEIF PROVIDER CODE PRESERVED:
YES / NO

WEB PROVIDER CODE PRESERVED:
YES / NO / NOT PRESENT

MASTER DATA MODIFIED:
NO / FAIL

SOURCE DATA DELETED:
0 / FAIL

ACTIVE FRONTEND:
<short description>

ACTIVE BACKEND:
<short description>

LEGACY LOCATION:
<path>

REPORT:
backend/data/CLIENT_CORRELATION_CLEAN_RESET_REPORT.md

STOP.

DO NOT START THE NEW BUILD.
