The ruling resolves the last ambiguity. The next step is implementation with Luna; no further Claude review is needed before proceeding.
Implement with Luna
Paste this exactly:
Senior ruling received. Implement this narrow Stage 7 correction only. Stage 8 remains blocked.
1. Correct the meaning of GLEIF COMPLETE
The prior implementation incorrectly treated COMPLETE as requiring a usable relationship pair.
Replace that rule.
For each frozen:
entity × family × required GLEIF query
where the family is only OWNERSHIP or CONTROL:
Query status = COMPLETE
when:
- the governed query was actually issued;
- it targeted the correct verified LEI and correct governed endpoint;
- a definitive terminal GLEIF response was retained;
- that response is either:
  - a relationship record, or
  - GLEIF's legitimate documented absence/no-relationship response.
COMPLETE means the governed query reached its defined boundary.
It does not mean that a relationship was found.
Preserve separately:
- FOUND
- NONE_FOUND
as the result of a COMPLETE query.
2. Query status = UNAVAILABLE
Use UNAVAILABLE only where the retained response demonstrates a technical/execution failure rather than a legitimate registry answer, for example:
- wrong endpoint
- wrong LEI/target
- malformed request
- authentication failure
- rate limiting that prevented completion
- server/network failure
- other execution defect
Do not classify a valid registry absence response as UNAVAILABLE.
3. Query status = NOT_ATTEMPTED
Use NOT_ATTEMPTED only when the required governed query was never issued.
4. Inspect retained artifacts FIRST — no provider calls
Before making any GLEIF request, inspect the retained Stage 7 artifacts already available.
For each required OWNERSHIP / CONTROL GLEIF query determine from:
- request URL
- target LEI
- endpoint class
- HTTP status
- retained response body
- request/retrieval metadata
- content hash/provenance
whether the previous request was:
1. correctly targeted + definitive positive response → COMPLETE / FOUND
2. correctly targeted + definitive registry absence response → COMPLETE / NONE_FOUND
3. technically invalid/incorrect request → UNAVAILABLE
4. never issued → NOT_ATTEMPTED
This is a reclassification of retained research, not a new research run.
Do not infer status from HTTP code alone.
In particular, inspect every retained 404 response body and request URL.
A 404 that is GLEIF's legitimate response for absence of the requested relationship resource at the correct LEI/endpoint is:
COMPLETE / NONE_FOUND
A 404 caused by an incorrect URL, malformed endpoint, or wrong target is:
UNAVAILABLE
5. Aggregate the GLEIF source-class cell mechanically
For each:
entity × OWNERSHIP
and
entity × CONTROL
determine the exact required GLEIF query set from the existing governed configuration.
Then:
- every required query COMPLETE + at least one valid finding → GLEIF source cell COMPLETE / FOUND
- every required query COMPLETE + no findings → GLEIF source cell COMPLETE / NONE_FOUND
- any required query UNAVAILABLE or NOT_ATTEMPTED → GLEIF source cell remains incomplete/partial
Do not require a relationship pair to exist for source coverage to be complete.
6. Identity and GLEIF coverage remain separate axes
A correctly completed GLEIF query remains COMPLETE even when downstream identity is:
- AMBIGUOUS
- NOT_FOUND
Identity state may block relationship acceptance but must not demote GLEIF research coverage.
Example:
GLEIF coverage = COMPLETE
identity = AMBIGUOUS
relationship acceptance = BLOCKED
is valid and expected.
Never create a VERIFIED+EXACT link from an ambiguous result.
7. Narrow corrective GLEIF calls are authorized
After the retained-artifact pass, provider calls are authorized only for a required query where the retained evidence proves that the original query did not actually reach its governed boundary because of an invalid target/request.
For each such query:
- make exactly one corrective re-query
- use the existing audited CCR backend GLEIF provider
- target the correct existing frozen entity/LEI
- use the exact missing governed endpoint/query
- retain full normal provenance
Do not:
- perform exploratory discovery
- broaden entities
- broaden relationship families
- rerun correctly completed queries
- retry merely because the result was negative
- change the frozen population
No broad GLEIF rerun is authorized.
8. Preserve multi-source coverage computation
Keep the already approved source-class vector:
- COMPLETE
- NOT_ATTEMPTED
- UNAVAILABLE
Top-level entity×family outcome remains exactly:
- NOT_ELIGIBLE
- NOT_RESEARCHED
- RESEARCHED_FOUND
- RESEARCHED_NONE_FOUND
- PARTIAL
- UNAVAILABLE
IDENTITY_UNRESOLVED remains a reason code only.
Overall RESEARCHED_NONE_FOUND is allowed only when every required source class for that entity/family is COMPLETE and none produced an accepted result.
A negative GLEIF result is not itself a partial result if its governed query completed correctly.
9. Do NOT hold SEC/Web work
GLEIF and Stylus SEC/Web execution are independent source-class tracks.
Preserve the previously derived frozen matrix:
- 30 SEC_FILING cells
- 42 R2D2_WEB cells
- 72 currently outstanding SEC/Web cells total
Do not change that matrix unless inspection of the authoritative frozen request JSON itself shows an error.
Stylus remains:
Lending Relationship Research - Web + SEC
with only:
- SEC_FILING
- R2D2_WEB
Never add GLEIF as a Stylus channel.
EPA remains NOT_ELIGIBLE and is not sent to Stylus.
10. Tests
Add/update tests proving:
1. correct GLEIF query + relationship record → COMPLETE / FOUND
2. correct GLEIF query + legitimate no-relationship response → COMPLETE / NONE_FOUND
3. legitimate negative result does not become UNAVAILABLE
4. wrong/malformed endpoint → UNAVAILABLE
5. query never issued → NOT_ATTEMPTED
6. valid expected GLEIF 404 absence response can become COMPLETE / NONE_FOUND
7. invalid-target 404 cannot become COMPLETE
8. ambiguous downstream identity does not demote a COMPLETE GLEIF source cell
9. ambiguous identity still cannot produce VERIFIED+EXACT
10. source cell is complete only when every required query in its governed query set is complete
11. no completed retained GLEIF query is reissued
12. corrective provider call is limited to exactly the deficient query
13. frozen Stage 7 manifest/fingerprint is unchanged
14. six correlation definitions remain unchanged
11. Required report before proceeding
After the retained-artifact reclassification and any strictly authorized corrective queries, report a table for every frozen applicable entity:
Entity | Family | Required query | Target LEI | Endpoint | Retained HTTP/result | Classification | FOUND/NONE_FOUND | Corrective call made? | Reason
Then summarize:
- number of GLEIF query components COMPLETE
- number UNAVAILABLE
- number NOT_ATTEMPTED
- resulting GLEIF source cells COMPLETE / FOUND
- resulting GLEIF source cells COMPLETE / NONE_FOUND
- source cells still partial
- exact corrective provider calls made, if any
Confirm explicitly that no correctly completed negative GLEIF query was rerun.
12. Then provide the first Stylus job again
Do not execute Stylus yourself.
After the GLEIF reclassification report, reproduce the first outstanding SEC/Web job only, with:
- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- ResearchInstruction
- AsOfDate
- expected raw JSON filename
The first job may proceed even if some narrowly corrective GLEIF work remains, because the provider tracks are independent.
Do not attempt token extraction.
Do not automate browser authentication.
Use supported interactive Stylus login only.
Frozen throughout
Do not change:
- 8-entity Stage 7 population
- selection fingerprint
- manifest
- relationship ontology
- VERIFIED+EXACT identity gate
- evidence acceptance gates
- evidence-basis model
- six correlation definitions
- two-hop correlation limit
- frontend
Do not start Stage 8.
