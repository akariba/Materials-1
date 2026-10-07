Once the current ADK grounded-search issue is fixed and the bounded smoke test passes, make the approved web/ADK capability a permanent, self-contained part of the CCR Correlation project.

IMPORTANT:
RPR may be used only as a reference implementation.
CCR must NOT require:
- the RPR repository
- the RPR virtual environment
- RPR source files
- RPR launch scripts
- RPR PYTHONPATH entries
- RPR-specific environment assumptions
- an already-running RPR service

The goal is that a completely new session can clone/open CCR Correlation, follow the CCR project setup, and successfully run the ADK grounded-web smoke test without knowing that RPR exists.

==================================================
1. PROVE CURRENT CCR VS RPR DEPENDENCIES
==================================================

Trace the complete CCR ADK/web path.

For every imported module, configuration file, environment variable, launch script and runtime dependency used by CCR web search, identify whether it comes from:

- CCR repository
- CCR .venv
- shared approved enterprise dependency
- RPR repository
- RPR .venv
- global Python
- user-machine PATH/PYTHONPATH
- another external location

Explicitly report any hidden RPR dependency.

Do not assume copying the implementation yesterday made CCR independent. Prove it.

==================================================
2. REMOVE RUNTIME DEPENDENCY ON RPR
==================================================

If CCR currently imports or reaches into RPR at runtime, migrate the required approved implementation into CCR using the smallest maintainable change.

CCR must own its own equivalents of the required:
- ADK agent construction
- approved web-search adapter
- grounding/citation extraction
- evidence-quality validation
- provider configuration
- launch integration
- tests

Do not create duplicate dead implementations.

Do not modify RPR.

Do not use absolute paths to RPR.

After migration, temporarily make RPR unavailable to the smoke test if practical and prove CCR still works.

==================================================
3. PIN THE REQUIRED DEPENDENCIES IN CCR
==================================================

The working environment must not depend on someone having manually installed packages in a previous terminal.

Inspect the repository's dependency-management mechanism:
- requirements*.txt
- pyproject.toml
- uv/poetry configuration
- lock file
- environment bootstrap scripts

Add the actual approved ADK dependencies used by CCR there.

Pin versions appropriately so a recreated CCR environment gets a compatible ADK stack.

Do not simply rely on:
`pip install google-adk`
having been run manually.

If exact pinning is required for the known-good implementation, record it explicitly.

If a compatible version range is safer, justify it and ensure the adapter is version-tolerant.

==================================================
4. MAKE THE CCR VENV AUTHORITATIVE
==================================================

Ensure CCR has one documented and deterministic Python runtime.

Verify:
- intended Python version
- `.venv` creation command
- dependency installation command
- VS Code interpreter setting if repository policy allows it
- launch scripts use the CCR interpreter
- tests use the CCR interpreter

Do not allow the application silently to fall back to global Citi Python if `.venv` exists.

Add an early diagnostic or startup guard if appropriate so the application fails clearly with something like:

WRONG_CCR_RUNTIME

rather than later claiming:

WEB_PROVIDER_UNAVAILABLE

when the wrong interpreter is being used.

==================================================
5. REMOVE OR NEUTRALIZE STALE ADK PATHS
==================================================

Search CCR for obsolete or conflicting web-provider implementations, including:
- old ADK adapters
- legacy imports
- unused provider switches
- stale configuration
- old model/provider names
- fallback code that silently bypasses grounded search
- hard-coded RPR paths
- global-Python assumptions

Do NOT delete code blindly.

For each conflicting path:
- prove whether it is used
- remove it if genuinely obsolete and safe to remove
- otherwise consolidate it into the canonical CCR ADK path

There must be one clearly identifiable production ADK/web path.

==================================================
6. MAKE CONFIGURATION REPRODUCIBLE
==================================================

Ensure all non-secret configuration required for ADK is represented inside CCR.

Examples:
- provider selection
- model configuration
- grounding/search-tool configuration
- API/version settings
- timeout/retry settings
- evidence-contract settings

Secrets/credentials must NOT be committed.

Instead:
- document required environment variable names
- provide an `.env.example` or repository-consistent equivalent if permitted
- validate required variables on startup
- never print secret values

==================================================
7. PRESERVE THE GROUNDING CONTRACT
==================================================

The permanent CCR implementation must preserve the current evidence requirements.

A successful ADK answer alone is NOT enough.

The canonical CCR path must retain:
- grounded source metadata
- external URL
- publisher/title
- publication date where genuinely supplied/verified
- exact grounded excerpt/snippet
- retrieval timestamp
- evidence status

Do not weaken the evidence contract to make installation easier.

==================================================
8. CREATE A REPRODUCIBILITY SMOKE TEST
==================================================

Add a small bounded test that can be run in any new CCR session.

It must prove:

CCR interpreter correct
→ ADK imports successfully
→ approved search tool is attached
→ grounded search executes
→ grounding metadata is received
→ at least one valid external source can be extracted
→ CCR evidence adapter accepts the record

The test must NOT:
- run full NVIDIA enrichment
- depend on RPR
- mutate production artifacts
- require CAM re-extraction

Provide one simple command to run it.

==================================================
9. TEST FROM A CLEAN CCR CONTEXT
==================================================

After implementing the permanent setup, test from a fresh process.

Preferably verify from:
- a newly opened terminal/process
- CCR project root
- CCR `.venv`
- no RPR process running
- no RPR path in PYTHONPATH

Where practical, also verify dependency installation from the committed dependency specification in a clean temporary environment.

The purpose is to prove this is reproducible and not merely working because of the current session state.

==================================================
10. COMMIT THE WORKING STATE
==================================================

Once all tests pass:

1. inspect `git status`
2. include only the CCR changes required for this ADK fix
3. do NOT commit:
   - secrets
   - tokens
   - `.env` containing credentials
   - temporary logs
   - generated NVIDIA enrichment outputs unless they already belong in source control
   - unrelated edits

Commit the working ADK configuration to the CCR repository.

Use a clear commit message such as:

`fix(web): make CCR ADK grounded search self-contained and reproducible`

Report:
- commit hash
- files committed
- files deliberately excluded
- dependency versions recorded

If repository policy prevents committing directly, prepare the exact changes and report:
COMMIT_READY_NOT_APPLIED

==================================================
11. FINAL INDEPENDENCE TEST
==================================================

After the commit, answer these explicitly:

Can CCR ADK run without the RPR repository? YES/NO
Can CCR ADK run without the RPR virtual environment? YES/NO
Can a new CCR session restore dependencies from committed project configuration? YES/NO
Does CCR force/use its intended interpreter? YES/NO
Does the grounded-search smoke test pass? YES/NO
Is the evidence/citation contract still enforced? YES/NO
Are any RPR runtime references left? YES/NO

If any answer except the last one is NO, do not declare this complete.

The final answer for:
"Are any RPR runtime references left?"
must be NO.

==================================================
12. DO NOT CONTINUE NVIDIA YET
==================================================

Even after the permanent ADK setup is committed, STOP.

Do NOT automatically rerun:
- NVIDIA web enrichment
- SEC
- CAM
- reconciliation
- graph construction

I want the infrastructure permanently fixed and committed first.

==================================================
FINAL STATUS
==================================================

Return exactly one:

CCR_ADK_SELF_CONTAINED_AND_COMMITTED
CCR_ADK_SELF_CONTAINED_COMMIT_READY
BLOCKED_BY_CCR_DEPENDENCY_SETUP
BLOCKED_BY_CONFIGURATION
BLOCKED_BY_GROUNDING
BLOCKED_BY_RPR_RUNTIME_DEPENDENCY
BLOCKED_BY_REPOSITORY_POLICY
BLOCKED_BY_PIPELINE_ERROR
