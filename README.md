TASK: Build a Complete, Accuracy-First Entity Enrichment Engine for CCR Relationship Intelligence

ROLE

Act as a Principal Software Engineer, Senior Credit Risk Data Architect, and AI/LLM Engineering Specialist.

Your assignment is to upgrade the existing CCR Relationship Intelligence platform into a comprehensive entity and relationship enrichment system.

This is an implementation task, not a research proposal.

Primary objective: Enrich every eligible entity in the available client universe with the maximum amount of accurate, verifiable information obtainable from approved data sources.

Do not restrict enrichment to the five-company demonstration cohort or the small subset currently represented in the relationship graph.

1. Critical problem to solve

The current system contains a large universe of companies, counterparties, lenders, investors, subsidiaries, SPVs, and other relationship participants.

However, only a small fraction have meaningful enriched information.

Many entities currently lack:

* Verified legal identity
* Parent and subsidiary information
* Entity classifications
* External credit ratings
* Financial information
* Industry and geographic classifications
* Ownership information
* Credit and lending relationships
* Direct and indirect relationship evidence
* Market indicators
* Connection to other entities
* Evidence provenance and confidence assessments

The application must evolve from a primarily name-and-relationship display into an entity intelligence platform.

2. Enrich the complete universe

Identify the actual source of the selectable PHR client universe and other active entity registries.

Determine which records represent:

1. Actual Citi clients or counterparties.
2. Legal entities belonging to a parent group.
3. Banks, lenders, agents, and syndicate members.
4. Investors and shareholders.
5. Subsidiaries, SPVs, and joint ventures.
6. Customers, vendors, and other commercial counterparties.
7. Named entities without confirmed legal identity.
8. Generic or anonymized descriptors that cannot be uniquely resolved.

Implement a deterministic, deduplicated master entity registry.

Each source record must remain traceable to its origin.

Do not merge two legal entities merely because their names are similar.

Distinguish parent companies, branches, subsidiaries, and individual obligors.

Every eligible entity must enter the enrichment workflow, not just entities that already have network connections.

Unresolvable or anonymized records must remain visible with an explicit status rather than being assigned fabricated identities.

3. Canonical entity resolution

Implement robust identity resolution using available identifiers:

* CAGID
* GFCID
* TFA identifiers
* LEI
* CIK
* ISIN, where applicable
* Ticker and exchange
* Official legal name
* Registered jurisdiction
* Company registration number, where supported

Apply deterministic identifier matching before fuzzy matching.

Use candidate generation and evidence-based disambiguation for ambiguous names.

For example, distinguish:

* Digital Realty Trust from its individual subsidiary entities.
* JPMorgan Chase & Co. from JPMorgan Chase Bank, N.A.
* Citi legal entities from Citi business divisions.
* Investment funds from their asset managers.
* SPVs from their sponsors and parent groups.

Use the LLM only to assist with ambiguous candidate resolution, never to invent identifiers.

Maintain verified, probable, ambiguous, and unresolved identity states.

4. Data source hierarchy

Use all existing approved data integrations and reusable functionality.

Tier 1 — Internal authoritative information

Prioritize:

* CAM documents and extracted fields
* Existing canonical client records
* TFA mappings
* Citi exposure information, when available and authorized
* Existing verified relationship artifacts
* Existing client reference data
* Available Oracle data
* Previously validated analyst overrides

These sources should establish internal identity and internal relationships.

Tier 2 — Authoritative external sources

Where accessible through approved connectors, retrieve:

* SEC EDGAR disclosures
* Relevant national corporate registries
* Company annual reports
* Audited financial statements
* Official investor relations documents
* External rating agency publications
* Official ownership disclosures
* Official debt and financing disclosures

Use jurisdiction-appropriate sources. Do not assume every entity is an SEC filer.

Tier 3 — Supplementary information

Use approved market and external research sources to discover:

* Recent financing arrangements
* Major business relationships
* Ownership changes
* Joint ventures
* Strategic partnerships
* Material acquisitions
* Customer and supplier dependencies
* Potential indirect exposure pathways

Use these sources to generate candidates that require verification.

Preserve source authority, date, URL or internal document reference, and extraction details.

Never represent unverified news or AI inference as authoritative fact.

5. Build the enrichment pipeline

Implement the following workflow:

COMPLETE ENTITY UNIVERSE
          |
          v
CANONICAL IDENTITY RESOLUTION
          |
          v
INTERNAL CAM / TFA / REFERENCE DATA
          |
          v
APPROVED EXTERNAL DATA RETRIEVAL
          |
          v
STRUCTURED FACT EXTRACTION
          |
          v
ENTITY & RELATIONSHIP MATCHING
          |
          v
R2D2 / APPROVED LLM REFINEMENT
          |
          v
DETERMINISTIC EVIDENCE VALIDATION
          |
          v
ENRICHED ENTITY REGISTRY
          |
          v
VERIFIED RELATIONSHIP GRAPH
          |
          v
CREDIT RISK INTELLIGENCE UI

Every stage should produce a structured output with a clear status and provenance.

Preserve the existing code and reuse working components instead of creating duplicate pipelines.

6. LLM-assisted enrichment using R2D2 and Opus

Investigate the existing R2D2 integration and approved model routing.

Use the currently available models according to their strengths.

Evidence extraction

Use an approved efficient model to process retrieved evidence and extract structured facts.

Relationship refinement

Use Claude Opus through the approved R2D2 route, where available, to assess:

* Whether two entities have a genuine relationship.
* Whether a relationship is direct or indirect.
* The type and direction of the relationship.
* Whether the relationship involves ownership, financing, lending, guarantees, or commercial dependence.
* Whether the relationship is current or historical.
* Whether evidence supports the specific legal entities involved.
* Whether the relationship should be accepted or flagged for review.

The LLM must return structured results linked to the evidence.

Do not ask models to generate unsupported relationships from general knowledge.

Do not transmit confidential internal identifiers, exposure amounts, or CAM content to unapproved external services.

All processing must comply with existing enterprise-approved data handling and AI access restrictions.

7. Relationship intelligence

For each entity, discover and validate relevant relationships.

Prioritize:

* Parent/subsidiary
* Ownership and control
* Borrower/lender
* Loan syndication
* Guarantor/guaranteed entity
* Sponsor/SPV
* Joint venture
* Investor/investee
* Customer/supplier
* Strategic partnership
* Other supported financial dependencies

Classify each as:

DIRECT: Verified direct connection supported by appropriate evidence.

INDIRECT: A traceable multi-hop connection composed of valid underlying relationships.

HIDDEN CANDIDATE: A potentially material connection discovered through analysis but requiring further evidence or human review.

Do not classify speculative relationships as confirmed.

Preserve multiple independent relationships between the same two entities.

For every relationship, store:

* Source entity ID
* Target entity ID
* Relationship type
* Direction
* Evidence references
* Source date and effective date, if available
* Confidence and verification status
* LLM refinement outcome
* Human review status

Avoid confusing a facility participant, arranger, agent, or lender with a direct creditor to every named participant.

8. Credit risk enrichment

Populate the existing Credit Risk Intelligence panel from verified data.

Identity

Legal name, canonical identifiers, jurisdiction, group, parent, and entity classification.

External ratings

Agency, rating, outlook, rating date, rated legal entity, and source.

Do not substitute parent ratings for subsidiary ratings.

Do not confuse Citi internal ORR with external agency ratings.

Financials

Retrieve available financial statements and key financial indicators:

* Revenue
* EBITDA
* Total assets
* Total debt
* Net debt
* Equity
* Operating cash flow
* Liquidity metrics
* Leverage ratios
* Interest coverage

Each numeric observation must preserve its reporting period, currency, units, consolidation basis, and source.

Do not invent financials for private entities or SPVs.

Market data

Where verified data exists, provide:

* Equity information
* CDS information
* Bond or credit-spread indicators
* Relevant market movements

Private entities without listed securities should have an appropriate unavailable or not-applicable status.

Relationships

Display direct, indirect, and review-required connections with evidence and relationship type.

Risk indicators

Calculate supported risk indicators using explicit, documented methodologies.

Do not fabricate default probabilities, credit correlations, or exposure amounts.

9. Coverage and completeness tracking

Implement a coverage registry for the entire entity universe.

Each entity should have an enrichment status:

* Pending
* In progress
* Enriched
* Partially enriched
* Unresolved
* Failed
* Review required

Track field-level coverage separately from entity-level completion.

A completed attempt does not mean all requested data exists.

Add backend metrics for:

* Total eligible entities
* Attempted entities
* Successfully resolved identities
* Partially enriched entities
* Verified financial records
* Verified external ratings
* Verified relationships
* Indirect paths discovered
* Review-required relationships
* Failed requests
* Unresolvable records

Keep entity universe counts separate from graph node counts, client counts, and relationship counts.

All displayed counts must be sourced from real backend records.

10. Efficient, resumable processing

The universe must be processed without requiring one enormous synchronous request.

Implement:

* Bounded enrichment jobs
* Configurable concurrency
* Rate limiting
* Retry with exponential backoff
* Timeouts
* Persistent checkpoints
* Resume after interruption
* Idempotent processing
* Deduplicated retrieval
* Model token and cost tracking
* Per-entity error isolation
* Incremental updates

Do not rerun successful enrichment unnecessarily.

Cache validated facts with timestamps and sensible refresh policies.

Do not automatically restart expensive AI jobs merely because the browser refreshes or the backend restarts.

Provide explicit user controls for starting, pausing, and resuming enrichment.

11. Quality validation

Accuracy takes priority over quantity.

Enforce:

1. Deterministic identity matching where possible.
2. Evidence-backed factual assertions.
3. Correct legal-entity attribution.
4. Relationship direction validation.
5. Separation of confirmed facts and hypotheses.
6. Detection of contradictory evidence.
7. Date and source freshness tracking.
8. Preservation of historical relationships.
9. Human review for ambiguous material relationships.
10. No fabricated identities, financials, or exposure amounts.

Create regression cases for similarly named companies, parent/subsidiary ambiguity, syndicated lending relationships, SPVs, and anonymous counterparties.

Use an independently reviewed reference set to measure identity matching precision and recall, relationship precision and recall, and false-positive rates.

Do not improve reported coverage by lowering evidence standards.

12. Frontend integration

Maintain the existing CCR Relationship Intelligence design.

Do not redesign or replace the UI.

Improve the existing components to support:

* Complete searchable entity registry
* Individual entity enrichment status
* Field-level source and freshness information
* Verified direct and indirect relationships
* Review-required candidates
* Available financial and rating information
* Enrichment progress and failure explanations

Make sure selecting any eligible entity loads that entity’s own enriched record.

Do not display the previous selected entity’s data or a generic fallback profile.

Avoid rendering hundreds of entities simultaneously in the network map.

Load entity-specific subgraphs on demand, with appropriate pagination and expansion.

13. Execution plan

Implement incrementally:

Phase 1 — Diagnose

Identify why the selectable universe is significantly larger than the enriched graph universe.

Audit the existing enrichment pipeline, identity mappings, source coverage, and database persistence.

Phase 2 — Master registry

Ensure all eligible entities are represented consistently with canonical identifiers and source lineage.

Phase 3 — Enrichment integration

Connect internal and authorized external retrieval to the canonical registry.

Phase 4 — AI refinement

Integrate structured, evidence-constrained R2D2/Opus refinement and deterministic validation.

Phase 5 — Persistent storage

Store enriched entity profiles, relationship evidence, enrichment states, and refresh timestamps.

Phase 6 — Full-universe execution

Run a representative pilot covering public companies, private companies, banks, subsidiaries, and SPVs.

Validate the pilot and correct systematic errors before scaling to the entire eligible universe.

Phase 7 — Frontend verification

Confirm enriched results appear in the existing application with correct attribution and confidence.

Preserve existing functionality throughout.

14. Final acceptance criteria

The task is complete only when:

* Every eligible entity is registered and has an enrichment status.
* Every eligible entity has been attempted or has a documented exclusion reason.
* Successfully retrieved facts are persisted and can be retrieved through the API.
* Entity identity is validated before relationships are published.
* Direct, indirect, and review-required relationships are clearly distinguished.
* External ratings and financials appear only when supported by evidence.
* No existing validated CAM relationships are lost.
* Failed entities can be retried independently.
* Enrichment can resume after interruption.
* The frontend displays the correct data for the selected legal entity.
* Tests demonstrate no material regression in existing functionality.

Provide final quantitative coverage metrics and a list of unresolved entities.

Do not claim that an entity is fully enriched when authoritative information is unavailable.

NON-NEGOTIABLE INSTRUCTIONS

* Preserve the existing frontend design.
* Preserve working backend functionality.
* Reuse existing R2D2 integrations.
* Use Opus for complex refinement only when justified.
* Do not create another disconnected enrichment pipeline.
* Do not use fabricated or demo data.
* Do not mix parent and subsidiary financials or ratings.
* Do not expose proprietary internal records to unapproved services.
* Do not undertake unrelated repository cleanup or major architectural redesign.
* Do not stop at analysis; implement and verify the solution.

FINAL OBJECTIVE

Transform CCR Relationship Intelligence from a limited relationship visualization into an evidence-backed entity intelligence platform capable of enriching the entire available client universe, identifying accurate direct and indirect relationships, and supporting credit risk analysis through reliable, traceable information.