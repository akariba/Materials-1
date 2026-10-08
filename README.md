TASK: Senior Software Engineer — Complete CCR Correlation Repository Cleanup and Restructuring

Role

Act as a Principal Software Engineer and Software Architect with extensive experience in enterprise Python applications, FastAPI, React, financial risk analytics, data engineering, and AI/LLM platforms.

Your assignment is to perform a comprehensive repository audit, structural cleanup, and professional reorganization of the existing CCR CORRELATION / CCR Relationship Intelligence project.

This is an implementation task, not merely a recommendation or documentation exercise.

The desired outcome is a clean, maintainable, professional repository suitable for continued enterprise development and eventual controlled deployment.

1. Primary objectives

1. Inspect the complete repository recursively.
2. Understand the actual system architecture, dependencies, entry points, and execution paths.
3. Identify redundant, obsolete, generated, temporary, duplicated, and unused files.
4. Remove unnecessary files and directories safely.
5. Consolidate duplicated implementations and documentation.
6. Organize the remaining source code into a consistent, professional structure.
7. Preserve all essential business logic, data pipelines, and working integrations.
8. Ensure backend, frontend, APIs, tests, and data ingestion continue functioning.
9. Reduce unnecessary repository complexity and improve developer navigation.
10. Produce a clear final report describing every significant change.

Do not simply move everything into new folders. The objective is to genuinely eliminate unnecessary complexity and clutter.

2. Mandatory discovery phase

Before modifying anything, investigate the repository thoroughly.

Inspect:

* Python source files and their imports
* FastAPI routes and application initialization
* React/TypeScript frontend and build configuration
* CAM extraction and normalization pipelines
* Entity resolution and identifier mapping
* Direct and indirect relationship discovery
* Oracle CAM integration and database interfaces
* R2D2/LLM integration and model routing
* AI refinement, validation, and evidence provenance
* Correlation and portfolio analytics
* Reports, scripts, tests, documentation, and configuration
* Runtime artifacts, caches, experiment folders, logs, and generated files
* Git status, ignored files, and uncommitted changes

Build an internal dependency map and determine which files are actively used.

Do not assume a file is unnecessary simply because its name looks old or unfamiliar.

3. Target repository architecture

Aim for a clean structure similar to:

CCR-Correlation/
│
├── backend/
│   ├── api/
│   ├── core/
│   ├── services/
│   ├── models/
│   ├── repositories/
│   └── integrations/
│       ├── cam/
│       ├── oracle/
│       └── r2d2/
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── pipelines/
│   ├── ingestion/
│   ├── normalization/
│   ├── enrichment/
│   ├── entity_resolution/
│   └── relationship_analysis/
│
├── analytics/
│   ├── correlation/
│   ├── network/
│   ├── portfolio/
│   └── stress/
│
├── config/
│
├── scripts/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── regression/
│
├── docs/
│   ├── architecture.md
│   ├── data_flow.md
│   └── setup.md
│
├── data/
│   ├── reference/
│   └── samples/
│
├── output/
│
├── .gitignore
├── .env.example
├── pyproject.toml
├── requirements.txt
└── README.md

This is a reference architecture, not a mandatory migration.

Adapt it to the actual application. Do not introduce layers, abstraction, or directories without genuine functional justification.

Avoid unnecessary refactoring of stable business logic.

4. File and folder cleanup

Classify every relevant directory and file into one of four categories.

A. KEEP

Preserve all actively used application components, configuration, reference data, required documentation, and operational dependencies.

B. CONSOLIDATE

Identify duplicated functionality, redundant helper modules, outdated parallel implementations, and repetitive documentation.

Consolidate only when equivalent behavior has been demonstrated.

C. DELETE

Remove genuinely unnecessary items, including:

* Python __pycache__ directories
* .pytest_cache and .ruff_cache
* Temporary files
* Obsolete debug logs
* Unused browser-testing profiles
* Disposable browser screenshots and recordings
* Regenerable frontend build artifacts where appropriate
* Abandoned experimental scripts
* Duplicate temporary exports
* Unused test fixtures and redundant test files
* Stale local benchmark outputs
* Redundant intermediate JSON/CSV artifacts
* Empty directories
* Obsolete backups whose content is safely preserved elsewhere

D. PRESERVE FOR REVIEW

Retain files with uncertain ownership, unknown dependencies, unique business data, or potentially useful historical experiment results.

Generate a deletion manifest containing the file path, reason, dependency verification, and disposition.

Critical deletion rules

* Do not blindly delete the entire test suite.
* Preserve meaningful unit, integration, regression, and API contract tests.
* Remove obsolete tests only when demonstrably superseded or irrelevant.
* Do not delete CAM source artifacts or unique historical evidence.
* Do not delete live database files, reference datasets, or required enrichment outputs.
* Do not delete manually reviewed AI decisions or analyst overrides.
* Preserve experiment results needed to compare relationship-discovery quality.
* Do not discard uncommitted user changes.
* Never delete credentials, environment configurations, or operational data without first assessing dependencies and recovery requirements.
* Never modify or delete files outside the repository.

Create a recoverable baseline before cleanup. Do not put sensitive data, credentials, or large proprietary datasets into a Git commit or unsecured backup.

For safe, verified disposable files, perform deletion. For uncertain or potentially valuable files, preserve them and report them separately.

5. Specific attention: output directory

The current project contains extensive historical output, including generated relationship graphs, enrichment files, experiment artifacts, JSON reports, temporary browser outputs, and logs.

Audit this directory carefully.

Separate:

1. Outputs actively required by the application.
2. Source-of-truth and evidence artifacts.
3. Historical experiments that may be useful.
4. Reproducible intermediate artifacts.
5. Disposable outputs.

Eliminate repeated temporary outputs where safe.

Retain meaningful experiment comparisons and relationship evidence.

Ensure the application never depends accidentally on an obsolete generated artifact.

Avoid keeping hundreds of files in the main application directory when they belong in properly managed runtime output storage.

6. Tests and quality engineering

Review the entire testing strategy.

Identify tests that:

* Verify important business behavior
* Protect financial calculations
* Validate CAM extraction
* Validate entity matching
* Verify direct and indirect relationships
* Protect API contracts
* Validate model outputs and evidence provenance

Retain these.

Remove or consolidate tests that are obsolete, duplicated, or tied exclusively to discontinued implementations.

Organize the remaining test suite logically.

Do not remove tests merely to make the project appear smaller.

7. Preserve critical CCR functionality

The cleanup must not compromise:

* CAM document ingestion
* TFA and counterparty identifier mapping
* CAGID, GFCID, LEI, CIK, and other supported identifiers
* Direct relationship discovery
* Indirect and multi-hop relationship discovery
* Parent/subsidiary relationship mapping
* Ownership and financial relationship extraction
* Oracle database integration
* R2D2 integration
* Claude/Opus refinement where configured
* Evidence verification and confidence assessments
* Correlation analytics
* Network graphs
* Portfolio analytics
* Stress analytics
* Existing frontend UI and navigation

Preserve provenance, source references, confidence scores, and review-required classifications.

Do not replace actual data with mocked or fabricated data to make tests pass.

8. Current application behavior must be preserved

The application is accessible locally at:

http://127.0.0.1:8000/

Existing features and routes must remain compatible.

Verify that the cleanup does not introduce regressions in:

* /api/stats
* Live entity selection
* Relationship maps
* Database record statistics
* Exposure analytics
* Network graphs
* Available API endpoints and frontend screens

The application currently has incomplete or unavailable live-data displays. Record this as a baseline condition.

Do not interpret an existing data-loading problem as a cleanup regression, and do not claim the cleanup has fixed it without evidence.

Do not redesign the frontend or change its appearance.

9. Safe implementation strategy

Execute the work in controlled stages.

Stage 1 — Inventory

Map all source files, dependencies, execution entry points, and active runtime paths.

Stage 2 — Baseline

Record Git status, application startup behavior, relevant API responses, frontend build status, and test results.

Establish a recoverable baseline.

Stage 3 — Cleanup

Delete verified disposable files, remove obsolete clutter, consolidate safe duplicates, and update .gitignore.

Stage 4 — Structural organization

Move source files into logical directories where beneficial.

Update imports, paths, references, scripts, and configurations.

Prefer minimal, incremental changes over a large architectural rewrite.

Stage 5 — Verification

Run available checks appropriate to the repository:

* Python import verification
* Backend startup
* API smoke tests
* Frontend build
* Essential unit tests
* Integration tests where dependencies are available
* Entity resolution and CAM pipeline regression tests
* Relationship graph integrity checks
* Git diff and file-path consistency checks

Do not report checks as passed unless they actually execute successfully.

Stage 6 — Final cleanup

Remove residual temporary files generated by the cleanup itself.

Update documentation and verify that the resulting repository has a clear entry point.

10. Repository hygiene

Ensure:

* One clear backend startup procedure
* One clear frontend startup procedure
* Consistent configuration management
* Appropriate .gitignore rules
* No unnecessary generated files under source directories
* No accidental source-code duplication
* No hardcoded secrets
* No machine-specific absolute paths
* Clean import structure
* Reproducible Windows development setup
* Clear dependency specifications
* No unnecessary package installations

Keep the solution compatible with the existing Windows development environment.

Do not introduce Docker, a new framework, a database migration, or external services solely for repository cleanup.

11. Final deliverables

After implementation, provide:

A. Repository structure

Show the resulting simplified directory tree, excluding caches and generated artifacts.

B. Cleanup summary

Report the number of:

* Files removed
* Directories removed
* Files reorganized
* Duplicate implementations consolidated
* Files preserved for review

C. Deletion manifest

List removed files and the reason for deletion. Provide a separate list of files preserved because safe deletion could not be established.

D. Verification results

Show actual executed tests, build results, API checks, failures, and environmental limitations.

E. Remaining technical debt

Identify unresolved architectural problems separately from the repository cleanup.

12. Non-negotiable constraints

1. No frontend redesign.
2. No unnecessary business-logic rewriting.
3. No loss of CAM evidence or relationship data.
4. No loss of AI refinement functionality.
5. No destruction of important experiments.
6. No removal of essential regression tests.
7. No changes to external enterprise systems.
8. No broad destructive operations without verified scope and recoverability.
9. No unrelated feature development.
10. No declaring success without validation.

FINAL INSTRUCTION

Act like a senior engineer responsible for maintaining this codebase long-term.

Inspect first, establish a baseline, execute safe cleanup and restructuring, verify the results, and report exactly what changed.

The goal is a smaller, cleaner, easier-to-navigate CCR Correlation repository with no unnecessary clutter and no avoidable functional regressions.

Do not stop after producing a plan. Execute the verified cleanup, and clearly identify any deletions that require a separate decision.