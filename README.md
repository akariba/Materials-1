Do not redesign the UI yet.

Perform a focused relationship-data reconciliation for the existing Lending Relationship Intelligence application.

I need to establish whether the relationship data currently shown across Overview, Clients, Network, Relationship Explorer, AI Create Relationship, External Research, and Review Queue is internally consistent.

Inspect the actual backend data and APIs and reconcile:

1. Total source relationship records.
2. Total normalized relationship records.
3. Unique subject/related-entity pairs.
4. Relationship counts by relationship family/type.
5. Counts by origin/source lane:
   - CAM / internal
   - AI-defined
   - external research
   - external overlay
6. Current vs historical/unknown relationship states.
7. Canonical vs review-required vs published supplemental records.
8. Evidence records and independent source counts.
9. Number of portfolio clients with at least one relationship.
10. Number of portfolio clients with zero relationships.
11. Relationship records whose subject or related entity cannot be mapped to the portfolio/entity master.
12. Relationship types that cannot be mapped to the governed taxonomy.
13. Duplicate relationship instances or duplicate entity pairs.
14. AI definition instances by definition/version.
15. Review Queue counts and how they reconcile to relationship records.

Specifically investigate why the Clients screen shows many rows as “No relationships / 0 records” while the Network and relationship surfaces contain relationship records.

Determine whether this is:
- correct,
- filtering/source-lane behavior,
- entity-ID mismatch,
- API mismatch,
- incomplete population,
- or a UI counting problem.

Do not modify data.
Do not change CAM.
Do not redesign the UI.
Do not invent mappings.

Return a concise reconciliation report with:

RELATIONSHIP DATA FLOW
SOURCE COUNTS
NORMALIZED COUNTS
COUNTS BY FAMILY
COUNTS BY ORIGIN
CLIENT COVERAGE
UNMAPPED ENTITIES
UNMAPPED RELATIONSHIP TYPES
DUPLICATES
REVIEW RECONCILIATION
AI-DEFINITION RECONCILIATION
INCONSISTENCIES FOUND
ROOT CAUSES
RECOMMENDED FIX ORDER

Also propose one canonical relationship record/API contract that all frontend screens should use.

Stop after the report. Do not implement fixes yet.
