Focused documentation check only.
We have a Client Universe built from Customer_latest.parquet. I want to know which existing customer/client columns can be used to join reliably to the internal AMC/GLEIF datasets, especially:
- AMCDATA.LEI_GENERAL_INFO
- AMCDATA.LEI_LEI_REL
Relevant Client Universe fields already present include:
- gfcid
- cagid
- cagid_name
- legal_entity_id
- lei_legal_name
- legal_name
- beneficial_owner_gfcid
- customer/account-type fields
- country fields
Please inspect the Citi/AMC documentation and determine, for each of these Client Universe fields:
1. What the field actually means.
2. Whether it is a stable entity identifier, group identifier, relationship identifier, or descriptive attribute.
3. Whether it maps directly to any field in AMCDATA.LEI_GENERAL_INFO.
4. Whether it maps directly to any field in AMCDATA.LEI_LEI_REL.
5. Whether the join is:
   - EXACT / AUTHORITATIVE
   - EXACT BUT NON-UNIQUE
   - DERIVED
   - UNSAFE
   - UNKNOWN
6. Expected cardinality:
   - 1:1
   - 1:many
   - many:1
   - many:many
7. Any documented transformation required before joining.
8. Any known nulls, duplicates, historical reuse, formatting issues, or semantic caveats.
Pay particular attention to:
GFCID
- Is gfcid the same GFCID used by the AMC GFCID Framework?
- Can Customer_latest.gfcid join directly to AMC tables?
- Which exact AMC columns contain GFCID?
LEGAL_ENTITY_ID
- What does legal_entity_id represent?
- Is it an LEI, internal mastered Legal Entity ID, vendor ID, or mixed identifier?
- Can it safely join to any AMC Legal Entity table?
LEI / LEI LEGAL NAME
- Does the customer source contain an actual LEI field under another name?
- Is lei_legal_name only a name, or is there a corresponding LEI identifier available elsewhere in the same customer/master model?
CAGID
- What is the authoritative meaning of cagid?
- Is it a legal-entity identifier, corporate group identifier, customer aggregation/group identifier, or something else?
- Should it ever be used for Legal Entity identity or ownership/control relationships?
BENEFICIAL_OWNER_GFCID
- What exactly does beneficial_owner_gfcid mean?
- Is it a governed ownership/control relationship?
- Is it suitable for CCR factual graph edges?
- Or should it remain only an internal source-link until its business semantics are confirmed?
Then give me a proposed join hierarchy for CCR, for example:
1. GFCID → ...
2. LEI → ...
3. internal Legal Entity ID → ...
4. legal name only as fallback / not authoritative
Do not invent mappings.
Mark every conclusion:
- DOCUMENTED
- NOT DOCUMENTED
- INFERRED
Finish with:
BEST JOIN KEY FROM CUSTOMER_LATEST TO AMC: <field>
SECONDARY JOIN KEY: <field>
FIELDS THAT MUST NOT BE USED AS IDENTITY KEYS: <list>
CAN CUSTOMER_LATEST BE JOINED DIRECTLY TO AMCDATA WITHOUT FUZZY MATCHING: YES / NO / PARTIALLY
