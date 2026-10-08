Proceed with the complete CCR Relationship Intelligence architecture and implementation specification. Cover all 15 work items, organized by technical dependencies.

Do not stop at a generic improvement plan. Produce a detailed, implementation-ready blueprint for a new self-contained project that Luna can build directly in VS Code.

Include:

1. Complete repository folder and file structure, explaining the responsibility of every important file.
2. Exact Python backend architecture using FastAPI, DuckDB and Parquet.
3. Automatic CAM ingestion from the input folder, including PDF, DOCX, TXT and spreadsheet parsing.
4. Indexed passage retrieval combined with an evidence-grounded LLM MapReduce pipeline: MAP extraction, independent semantic checker, deterministic validation, REDUCE aggregation and canonical entity resolution.
5. Typed database schemas for documents, passages, canonical entities, relationships, evidence, exposures, financials, review decisions and processing jobs.
6. Separate verified direct relationships, review candidates, graph-derived indirect relationships and possible hidden-risk indicators.
7. SEC and approved enterprise web enrichment, with strict citation validation and no fabricated evidence.
8. Credit-risk analytics, graph metrics, portfolio concentration, TFA and Citi exposure calculations, with missing data handled explicitly.
9. Full frontend architecture covering Correlation, Credit Risk Intelligence, Portfolio Analytics, Stress Analytics and Risk Heatmap.
10. All backend API contracts, configuration files, agent instructions, development skills, startup scripts, dependencies and automated tests.
11. A simple operating workflow: copy CAM documents into input/, configure approved enterprise credentials, run the startup command, and automatically obtain an indexed database, verified relationships, analytics and an interactive frontend.
12. Concrete implementation order, acceptance criteria and complete code-level instructions for Luna.

Use all accessible documents from the CCR Improvement Project library. If document retrieval fails, identify the missing evidence rather than inventing details.

Provide the deliverables in logically ordered implementation batches so a code-capable agent can implement them without another architectural redesign.

Do not ask further scoping questions. Do not claim any application, tests or deployment has been executed unless that actually happened.