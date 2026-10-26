Act as a principal data architect and senior Python data engineer specializing in financial risk data, entity resolution, and graph relationships.

Project: CCR Correlation.

All source data is now located under data/raw/:
- data/raw/cams/: CAM documents from multiple sources
- data/raw/master/: Parquet, CSV and Excel master/client/identifier datasets
- data/raw/narratives/: CAGID-related JSON narratives

Your task is to PLAN a rigorous data discovery, profiling and architecture assessment before implementing anything.

1. Inspect the current repository structure and existing pipeline. Identify all source datasets, file formats, sizes, schemas and current output dependencies. Avoid loading entire large files into memory.
2. Develop a read-only profiling approach for Parquet, CSV, JSON, Excel and CAM documents. Determine row counts, distinct values, null distributions, duplicates and potential primary keys.
3. Discover and assess identifier fields such as CAGID, LEI, CIK, ISIN and CUSIP wherever present. Evaluate join coverage, cardinality, ambiguous matches and mismatches, without assuming these identifiers refer to the same entity level.
4. Examine the CAM structure and propose a method for extracting entities and evidence-backed lending or credit relationships. Differentiate observed relationships from speculative inferences and statistical correlations.
5. Inspect existing DuckDB schemas and the current correlation pipeline. Propose a source-to-staging-to-curated architecture, including tables for entities, identifiers, relationships, source evidence, run history and batch outputs. Explain why DuckDB/Parquet or another storage solution is appropriate for the actual workload.
6. Design a performance benchmarking plan using the existing new pipeline for 10,000 and 100,000 clients, with a cautiously justified extrapolation to 1,000,000. Include execution time, throughput, peak memory, number of valid relationships, errors, and cold/warm cache distinctions.
7. Propose a recurring batch architecture to precompute and persist relationships so interactive client queries only read indexed or materialized results.
8. Produce a phased implementation plan, measurable acceptance criteria, and prioritized risks.

Constraints:
- Windows environment, single machine, no cluster.
- Never modify, move, overwrite, or delete raw inputs, current working code, databases, or existing outputs.
- Read-only assessment only. No implementation, migrations, AI extraction batches, or benchmark execution yet.
- Do not upload confidential data to external services.
- Do not invent schemas, entity mappings, relationships, data quality statistics or performance results. Clearly distinguish observations from hypotheses.

First explain what actually exists and what needs verification, then present the architecture alternatives and detailed proposed execution plan. Wait for approval before implementation.
