LENDING RELATIONSHIP INTELLIGENCE — ENGINEERING OPERATING CONTRACT

Work ONLY in the current Lending repository.

This is Lending, NOT CCR. Do not modify CCR code, CCR databases, CCR migrations, CCR routes, or CCR artifacts.

Before changing anything:
1. Inspect the current implementation.
2. Reuse existing tables, modules, APIs, utilities, models, and frontend components where they already provide the required capability.
3. Do NOT create parallel duplicate stores or another relationship universe.
4. Identify current callers before changing an interface.
5. Preserve backward compatibility unless this task explicitly authorizes a controlled migration.
6. Use migrations for persistent schema changes.
7. Never rewrite source CAM files.
8. Never modify Customer_latest.parquet or thousandClients.csv.
9. Never silently promote external research into CAM truth.
10. Never silently convert review-required/rejected data into canonical data.
11. Never hide loss of information through aggregation.
12. Preserve raw evidence and lineage.
13. A relationship type substitution must be explicit and traceable.
14. Entity identity resolution and relationship classification are separate decisions.
15. Do not use display names as permanent entity IDs.
16. Do not claim external research succeeded if a provider failed.
17. Fail closed when evidence, identity, or provider state is uncertain.
18. Every persisted AI-created object must retain provenance and lifecycle metadata.
19. All new behavior requires tests.
20. Do not change production/deployment until explicitly requested.

CURRENT GOVERNANCE THAT MUST BE PRESERVED DURING MIGRATION

- CAM/V3 is authoritative for the CAM relationship lane.
- External intelligence is supplemental unless explicitly reviewed/published under its own governed lane.
- AI-published relationships are a governed AI projection, not CAM rows.
- The normalized workbench is currently a separate governed projection.
- Existing V2 fallback behavior must not silently become the new global truth.
- Current source lanes may disagree. Preserve those disagreements and explain them.
- The target architecture may provide a unified READ MODEL, but this must not erase source authority or provenance.

KNOWN CURRENT PROBLEMS

The current application has multiple relationship populations/stores:
- Portfolio CAM/V3.
- Conditional V2 fallback.
- Normalized workbench.
- Legacy external research.
- V3-aware external overlay.
- Published AI relationships.
- Independent analytical/control populations.

The redesign must converge these through canonical identity, evidence, relationship, lineage, and projection contracts rather than by blindly merging rows.

BENCHMARK

There is an existing manually adjudicated benchmark of 37 source-supported relationships across nine source document families, including cases involving:
- Project Indigo / CoreWeave / NVIDIA / Meta.
- N01.
- Hut 8 / NVIDIA / Anthropic / Fluidstack.
- Lambda / NVIDIA / Microsoft / Anthropic.
- Applied Digital / CoreWeave / Oracle / Meta.
- Serverfarm / Amdocs / Oracle / Meta / Manulife.
- OpenAI and counterparties.
- Cavalry / CyrusOne.
- BO Westover / Blue Owl.

Preserve this benchmark and use it for regression testing.

OUTPUT REQUIREMENT FOR EVERY TASK

At completion report:
- What was inspected.
- What was reused.
- What was created.
- Exact files changed.
- Exact schema changes.
- Migration/rollback approach.
- Tests added.
- Tests executed and results.
- Data counts before/after where relevant.
- Known limitations.
- Remaining risks.
- Recommended next task.

Do not proceed into the next phase automatically.
STOP after completing the requested task.
