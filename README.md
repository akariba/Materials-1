THE CLIENT DEMO IS FINISHED.

We are now returning to the real CCR Relationship Intelligence implementation.

IMPORTANT:
Do NOT redesign the application.
Do NOT build another five-company demo.
Do NOT create a new relationship model from scratch.

We previously built a more complete CCRIG POC with:
- candidate-first relationship discovery
- multi-factor relationship scoring
- pairwise calibration
- AI event / relationship extraction
- typed second-order paths
- exposure mapping
- Fact / Derived / Exposure separation
- approximately 56 passing tests

First find and reuse that implementation.

==================================================
0. PRESERVE CURRENT WORKING VERSION
==================================================

Before changing anything:

1. Commit the current five-company working version.
2. Tag or clearly identify it as the client-demo baseline.
3. Do not destroy or rewrite it.
4. Continue development from the current CCR Relationship Intelligence project.

There must be NO RPR dependency.

==================================================
1. RECOVER EXISTING CCRIG IMPLEMENTATION
==================================================

Search the current repository, git history, branches and archived modules for the previous CCRIG implementation.

Search specifically for concepts / symbols related to:

- candidate-first scoring
- pairwise calibration
- relationship score
- CounterpartyRelevance
- EventRelevance
- typed second-order paths
- exposure mapping
- Fact / Derived / Exposure
- relationship candidates
- relationship resolver
- CCRIG
- R2D2 adapter
- CAM parser
- graph/path calculations
- existing CCRIG tests

Do not reimplement these components until you have established whether the old implementation already exists.

Report what is reusable.

==================================================
2. TARGET ARCHITECTURE
==================================================

The real pipeline should be:

CAM
    ↓
deterministic CAM extraction
    ↓
canonical entity resolution
    ↓
existing relationship candidates
    ↓
R2D2 retrieval / evidence enrichment
    ↓
Claude Opus refinement
    ↓
deterministic evidence validation
    ↓
relationship graph
    ↓
direct / indirect / hidden analysis
    ↓
CCR portfolio / stress analytics


==================================================
3. CAM IS THE INTERNAL SOURCE OF TRUTH
==================================================

The current UI is incorrectly showing many fields as:

Not available
—
Unknown

although the CAM contains substantially more information.

Inspect the actual CAM schema/files.

Extract all available internal fields deterministically.

In particular find and populate:

- Citi EXP / Citi exposure
- TFA
- facility amounts
- lending exposure
- internal ratings
- RLR
- FORR
- country of risk
- industry / sector
- parent / hierarchy
- guarantor
- collateral
- facilities
- maturity
- liquidity where present
- customer / supplier relationships
- ownership / investment
- strategic relationships
- contractual relationships
- leases / offtake
- other disclosed relationship facts

DO NOT ask Opus to invent or estimate Citi EXP or TFA.

If CAM contains a numerical value, the UI must display the exact CAM-derived value with provenance.

Retain the raw CAM source reference for every extracted field.

==================================================
4. FACT / DERIVED / AI CANDIDATE SEPARATION
==================================================

Restore the previous separation:

FACT
DERIVED
EXPOSURE

Extend it where necessary with:

AI_CANDIDATE

Definitions:

FACT
= explicitly supported by CAM or validated external evidence.

DERIVED
= deterministically calculated from verified facts.

EXPOSURE
= Citi internal exposure information such as Citi EXP / TFA.

AI_CANDIDATE
= relationship proposed by the AI which still requires evidence/review.

Never mix these categories.

==================================================
5. DIRECT RELATIONSHIPS
==================================================

DIRECT means there is explicit evidence of an A ↔ B relationship.

Examples:

supplier/customer
investor/investee
parent/subsidiary
guarantor/borrower
lender/borrower
strategic_partner
lessor/lessee
offtaker/provider
JV
ownership
funding
collateral dependency
commercial dependency

Every direct relationship must preserve:

- entity_a
- entity_b
- relationship_type
- subtype
- direction
- source
- source URL/document
- source excerpt
- source date
- confidence
- evidence status
- provenance
- relationship strength if the existing CCRIG model provides one

Do not collapse multiple relationships between the same pair.

Example:

NVIDIA ↔ Intel strategic collaboration

and

NVIDIA → Intel equity investment

remain two separate edges.

==================================================
6. R2D2
==================================================

Use the existing approved R2D2 integration.

R2D2 should retrieve evidence / context around candidate relationships.

Do NOT ask one vague generic question.

Generate targeted retrieval tasks around:

- ownership
- investment
- supplier
- customer
- partnership
- guarantee
- financing
- collateral
- lease
- offtake
- data centre
- cloud
- common project
- SPV
- major commercial dependency
- common exposure
- parent / subsidiary
- material contract

R2D2 output is evidence/context.

It is not automatically a verified graph edge.

==================================================
7. OPUS REFINEMENT
==================================================

Use Claude Opus after CAM + R2D2 evidence has been gathered.

Opus receives:

1. canonical entities
2. CAM extracted facts
3. CAM relationship candidates
4. R2D2 evidence
5. existing direct-source evidence
6. current graph relationships

Opus responsibilities:

- entity reconciliation
- relationship classification
- directionality
- relationship normalization
- deduplication
- contradiction detection
- candidate relationship discovery
- evidence synthesis
- confidence assessment
- identification of possible hidden dependencies

Opus MUST return structured JSON.

Opus must NOT generate exposure amounts.

Opus must NOT convert unsupported candidates into verified facts.

==================================================
8. EXTERNAL EVIDENCE
==================================================

Reuse the already-working direct-source pipeline.

We already proved:

DIRECT_FETCH_WORKS

So do not return to the previous ADK grounding investigation.

Use:

real source URL
→ direct fetch
→ page text
→ title/publisher/date
→ exact excerpt
→ deterministic evidence validator

Priority:

1. SEC / EDGAR
2. official investor relations
3. official corporate disclosure/newsroom
4. annual reports
5. other approved direct publisher sources

R2D2/search may DISCOVER evidence.

The retrieved underlying source is the evidence.

==================================================
9. INDIRECT RELATIONSHIPS
==================================================

INDIRECT must primarily be GRAPH-DERIVED.

Do NOT ask Opus to simply hallucinate indirect relationships.

Example:

NVIDIA → Hut 8
Hut 8 → Company X

therefore:

NVIDIA → Hut 8 → Company X

is a two-hop relationship.

Store:

- origin
- destination
- path
- hop_count
- relationship types along path
- path strength
- evidence for every underlying edge

Use the previous typed second-order path implementation if it exists.

Restore it rather than creating a new one.

==================================================
10. HIDDEN RELATIONSHIPS
==================================================

Hidden relationships are different.

Opus/R2D2 may identify a previously unseen economic dependency such as:

- common supplier
- common customer
- shared project
- shared SPV
- common guarantor
- common collateral
- common financing source
- dependency through an intermediate company
- infrastructure dependency
- concentrated revenue dependency

But these initially become:

AI_CANDIDATE / REVIEW_REQUIRED

not VERIFIED.

Once independently supported by evidence they may be promoted.

==================================================
11. RELATIONSHIP SCORING
==================================================

Do NOT create a new arbitrary weighting scheme.

Find the previous CCRIG multi-factor / candidate-first scoring implementation and reuse it.

Likewise restore:

- pairwise calibration
- typed paths
- relationship strength
- existing distance calculations
- existing candidate ranking

If the prior score code exists, preserve its formulas and tests.

Do not substitute new weights merely because the current demo has Weighted Path/Jaccard fields.

==================================================
12. EXPOSURE + RELATIONSHIP ANALYTICS
==================================================

Restore the intended separation:

relationship relevance
+
Citi exposure
=
counterparty relevance

The previous intended concept was approximately:

CounterpartyRelevance
    = Σ Exposure × EventRelevance

Use the actual existing implementation if found.

Do not silently create a different formula.

This is where CAM Citi EXP / TFA becomes useful.

Relationship intelligence should eventually answer:

- Which Citi counterparties are directly affected?
- Which are indirectly connected?
- Through which entities?
- Which Citi exposures sit on those paths?
- How strong is the dependency?
- What evidence supports it?
- Is the relationship FACT, DERIVED or AI_CANDIDATE?

==================================================
13. FRONTEND
==================================================

Do not redesign CSS.

Keep the current shell:

Correlation
Stress Analytics
Portfolio Analytics
Risk Heatmap

The Correlation graph must stop being limited to five hardcoded nodes.

It should render the actual graph returned by the backend.

Filters:

ALL
DIRECT
INDIRECT
HIDDEN

must become real filters.

Right-hand dossier must populate from real backend data.

Citi EXP / TFA must come from CAM.

Distance tab must use real calculated graph values.

Evidence/provenance remains inspectable.

==================================================
14. FIRST END-TO-END TEST
==================================================

Do NOT immediately run hundreds of companies.

Start with NVIDIA.

Pipeline:

CAM NVIDIA
→ extract all CAM facts/exposures
→ canonicalize entities
→ recover all existing relationship candidates
→ R2D2 targeted enrichment
→ Opus refinement
→ direct-source validation
→ build direct graph
→ calculate second-order paths
→ generate hidden candidates
→ populate frontend

Then compare:

BEFORE:
5 nodes / 5 edges / almost no exposure data

AFTER:
real CAM entities
real Citi EXP/TFA
more direct relationships
derived indirect paths
review-required hidden candidates
full provenance

Do not force a particular number of relationships.

Quality and evidence matter more than count.

==================================================
15. ACCEPTANCE TEST
==================================================

For NVIDIA confirm:

[ ] CAM Citi EXP populated where CAM contains it
[ ] CAM TFA populated where CAM contains it
[ ] all available CAM relationship facts extracted
[ ] canonical identities resolved
[ ] R2D2 called successfully
[ ] Opus refinement successfully returns schema-valid JSON
[ ] direct relationships retain evidence
[ ] multiple edge types between same pair are preserved
[ ] indirect relationships are generated from verified paths
[ ] hidden/AI candidates remain REVIEW_REQUIRED
[ ] direct-source evidence pipeline still works
[ ] relationship scoring uses previous CCRIG implementation
[ ] graph frontend renders backend relationships
[ ] filters ALL/DIRECT/INDIRECT/HIDDEN work
[ ] evidence drill-down works
[ ] no RPR dependency
[ ] no fabricated numerical exposure data
[ ] tests pass

==================================================
16. DO NOT MODIFY FIRST
==================================================

Do not start by editing the frontend.

First recover the previous CCRIG backend implementation and tests.

Show me:

1. where the old CCRIG code exists
2. which modules are reusable
3. which tests exist
4. current CAM schema and where Citi EXP/TFA actually live
5. current R2D2 adapter
6. current Opus/model adapter
7. current direct-source evidence implementation
8. what is missing between these pieces

THEN implement the smallest integration required.

==================================================
17. COMMIT
==================================================

Once NVIDIA works end-to-end and tests pass:

commit the implementation.

Do not mix unrelated RPR files into the commit.

Report:

CCRIG RECOVERED MODULES:
...

CAM FIELDS FOUND:
...

R2D2:
WORKING / BLOCKED

OPUS:
WORKING / BLOCKED

DIRECT RELATIONSHIPS:
<count>

INDIRECT RELATIONSHIPS:
<count>

HIDDEN / REVIEW REQUIRED:
<count>

CITI EXP:
POPULATED / MISSING

TFA:
POPULATED / MISSING

TESTS:
<passed>/<total>

UI GRAPH:
WORKING / BLOCKED

COMMIT:
<hash>
