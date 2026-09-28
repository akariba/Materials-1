Internal bank data discovery only — do not modify any data or configuration.
I want to know whether the bank already holds GLEIF / LEI / Legal Entity relationship data anywhere internally, so that we can reuse governed internal data instead of repeatedly calling the external GLEIF API.
Search across every internal database, data lake, warehouse, catalog, governed dataset, reference-data source, client-master source, entity-master source, regulatory dataset, counterparty dataset, KYC dataset, risk dataset, and other data source that you are authorized to inspect.
Look for both explicit GLEIF references and equivalent fields.
Search for terms/fields such as:
- GLEIF
- LEI
- legal_entity_identifier
- legal_entity_id
- lei_legal_name
- LEI status
- entity status
- direct parent
- ultimate parent
- direct_parent_lei
- ultimate_parent_lei
- relationship record
- relationship status
- relationship period
- relationship qualifier
- Level 1
- Level 2
- RR-CDF
- LEI-CDF
- GLEIF Golden Copy
- GLEIF Concatenated Files
- GLEIF delta
- legal entity hierarchy / ownership hierarchy / parent hierarchy
Also search for datasets that may contain GLEIF-derived information without using the word GLEIF.
For every relevant dataset found, report:
1. System / database / platform name
2. Schema / dataset / table name
3. Business owner or data domain, if visible
4. Relevant fields
5. Whether it contains:
   - LEI
   - legal name
   - entity status
   - jurisdiction
   - direct parent
   - ultimate parent
   - ownership/control relationship
   - relationship status
   - effective dates / validity dates
6. Source/provenance if known:
   - direct GLEIF feed
   - copied from GLEIF
   - internal mastered data
   - vendor data
   - unknown
7. Refresh frequency / latest available date
8. Approximate record count / coverage, if available
9. Whether the data is historical/versioned or current-state only
10. Whether there is a reliable key to map it to our client universe, especially:
    - GFCID
    - LEI
    - legal_entity_id
    - CAGID
    - another mastered entity ID
Then answer these specific questions:
A. Do we already have an internal authoritative or near-authoritative LEI/GLEIF dataset?
B. Do we already have GLEIF Level-2-style direct-parent / ultimate-parent relationship data internally?
C. Is there an internal mastered Legal Entity hierarchy that may be more appropriate than calling GLEIF externally?
D. Can any discovered dataset be joined reliably to Customer_latest.parquet / the Client Universe using LEI, legal_entity_id, GFCID, or another identifier?
E. Which internal source would be the strongest candidate for CCR identity verification and ownership/control enrichment?
Do not rank sources merely by convenience. Explain differences in:
- provenance
- freshness
- completeness
- identifier quality
- relationship coverage
- historical depth
If multiple copies of the same GLEIF data exist, identify which appears to be the mastered/governed version and which appear to be downstream copies.
If access permissions prevent inspection of a promising dataset, list it separately as:
POTENTIAL SOURCE — ACCESS NOT AVAILABLE
Do not create tables, run updates, alter schemas, request new access, or change configurations.
Finish with:
INTERNAL GLEIF/LEI DATA FOUND: YES / NO
INTERNAL PARENT/HIERARCHY DATA FOUND: YES / NO
BEST CANDIDATE DATASET(S): <names>
EXTERNAL GLEIF API STILL NECESSARY: YES / NO / ONLY FOR GAPS
