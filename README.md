Continue from the current CCR ADK self-containment task.

Current state:

- CCR ADK implementation changes are in place.
- search_si_svy03.py now separates:
  - simple diagnostic answer
  - strict grounded-evidence provider result
- no_grounded_citations / grounding_unavailable correctly fail closed.
- focused regression: 31 passed.
- prior clean-candidate regression: 456 passed, 1 skipped.
- wrong/inherited runtime correctly fails closed with exit code 78.
- editor diagnostics are clean.
- no commit has yet been made.

The only current infrastructure blocker is:

setup.ps1 cannot recreate the actual CCR project environment because processes:

PID 33460
PID 4128

are still using the environment and appear to be PDF-repair workers.

This is now a targeted completion task.

DO NOT redesign ADK.
DO NOT rerun CAM extraction.
DO NOT rerun NVIDIA enrichment.
DO NOT change relationship logic.
DO NOT use RPR at runtime.

==================================================
1. VERIFY THE TWO BLOCKING PROCESSES
==================================================

Inspect PID 33460 and PID 4128.

For each report:

- executable
- command line
- parent process
- working directory if available
- start time
- whether it belongs to CCR
- whether it is specifically a PDF-repair worker
- whether it is still doing useful work or is stale

Do not terminate anything until ownership is proven.

If either process is unrelated to CCR, STOP and report the blocker.

==================================================
2. SAFELY STOP ONLY THE CONFIRMED CCR PDF WORKERS
==================================================

If both PIDs are confirmed to be old/stale CCR PDF-repair workers:

stop them gracefully first.

If graceful shutdown is not possible, terminate only those confirmed worker processes.

Do NOT terminate:
- VS Code
- current shell
- unrelated Python processes
- RPR
- user applications

Report exactly what was stopped.

==================================================
3. RECREATE THE CCR ENVIRONMENT FROM PROJECT CONFIG
==================================================

Run the existing CCR setup/bootstrap path.

The environment must be recreated using only CCR-owned project configuration.

It must NOT depend on:

- RPR repository
- RPR .venv
- global Python packages
- manual package installs from a previous session
- RPR PYTHONPATH
- absolute RPR paths

Use the committed/intended CCR dependency definitions.

Report:

- Python version
- new CCR interpreter path
- google-adk version
- google-genai version
- all relevant provider dependencies
- dependency source file(s)

==================================================
4. PROVE RPR IS NOT REQUIRED
==================================================

Search CCR runtime paths for any remaining RPR dependency.

Check:

- imports
- sys.path manipulation
- PYTHONPATH
- absolute paths
- launch scripts
- configuration
- subprocess calls
- test fixtures
- provider adapters

RPR may remain referenced in documentation or comments as historical/reference material, but it must not be required at runtime.

Return:

RPR_RUNTIME_DEPENDENCIES = 0

or STOP with the exact remaining dependency.

==================================================
5. RUN THE FRESH-ENVIRONMENT ADK SMOKE TEST
==================================================

From a brand-new process using the recreated CCR .venv, run the bounded grounded-search smoke test.

The test must prove the entire production path:

CCR .venv
→ ADK import
→ approved search tool attached
→ search executes
→ grounding metadata returned
→ external source extracted
→ URL extracted
→ source/publisher extracted
→ grounded excerpt/snippet extracted
→ date retained where genuinely available
→ strict CCR evidence contract evaluates result

Report separately:

simple_answer_status
strict_evidence_status

The simple answer succeeding is NOT enough.

The strict evidence path must succeed.

Expected successful outcome:

strict_evidence_status = ACCEPTED

with at least one valid grounded external evidence record.

If it returns:

no_grounded_citations
grounding_unavailable
BLOCKED_BY_GROUNDING

STOP.

Do not commit an ungrounded configuration as complete.

==================================================
6. RESTART / NEW-SESSION REPRODUCIBILITY TEST
==================================================

After the first successful smoke test:

close that test process.

Start another fresh process from the CCR root.

Do not reuse imported Python state.

Run the same smoke test again.

This proves the setup survives a new session.

Both runs must succeed using the CCR environment alone.

==================================================
7. CHECK PROJECT BOOTSTRAP
==================================================

Verify that a future user/session can reproduce the environment using documented CCR commands.

Confirm that:

- required dependencies are declared
- setup.ps1 or equivalent creates/repairs the environment
- VS Code selects the CCR interpreter where appropriate
- wrong interpreter produces a clear failure
- no manual pip command from this session is required

Update README/setup documentation only where necessary.

Do not expose secrets.

==================================================
8. RUN TESTS
==================================================

Run:

- focused ADK tests
- grounding/citation tests
- environment/runtime guard tests
- relevant regression suite

Report:

passed
failed
skipped
warnings

Do not fix unrelated pre-existing failures.

==================================================
9. COMMIT ONLY AFTER THE CLEAN SMOKE PASSES
==================================================

If and only if:

- the CCR environment was recreated successfully,
- ADK is installed from CCR project configuration,
- RPR_RUNTIME_DEPENDENCIES = 0,
- fresh-process grounded search succeeds,
- strict evidence contract passes,
- relevant tests pass,

then prepare and commit the CCR changes.

Before committing:

inspect git status.

Exclude:

- secrets
- credentials
- local .env files
- temporary logs
- generated enrichment output
- cache files
- virtual environment files
- unrelated changes

Commit message:

fix(web): make CCR ADK grounded search self-contained and reproducible

Report:

- commit hash
- committed files
- deliberately excluded files
- google-adk version
- google-genai version
- Python version

==================================================
10. FINAL PROOF
==================================================

Answer explicitly:

CCR environment recreated from project config: YES/NO
CCR uses its own .venv: YES/NO
google-adk installed from CCR dependency config: YES/NO
RPR repository required at runtime: YES/NO
RPR virtual environment required: YES/NO
Global Python required: YES/NO
Fresh-process ADK search works: YES/NO
Grounding metadata returned: YES/NO
Strict evidence contract passes: YES/NO
New-session rerun passes: YES/NO
Changes committed: YES/NO

Required successful answers:

YES
YES
YES
NO
NO
NO
YES
YES
YES
YES
YES

==================================================
FINAL STATUS
==================================================

Return exactly one:

CCR_ADK_SELF_CONTAINED_AND_COMMITTED
CCR_ADK_SELF_CONTAINED_COMMIT_READY
BLOCKED_BY_ACTIVE_PROCESS
BLOCKED_BY_CCR_ENV_RECREATION
BLOCKED_BY_RPR_RUNTIME_DEPENDENCY
BLOCKED_BY_GROUNDING
BLOCKED_BY_TEST_FAILURE
BLOCKED_BY_REPOSITORY_POLICY
BLOCKED_BY_PIPELINE_ERROR

STOP after this.

Do NOT resume NVIDIA external enrichment automatically.
