The ADK web-search setup worked yesterday.

We configured it using the existing **RPR project as the reference implementation**, and the ADK agent/web-search path was working successfully.

Today it is reporting that the ADK/web provider is unavailable.

Please investigate what changed.

Compare the current implementation and runtime directly against:
1. the APR project configuration we used as the reference, and
2. yesterday’s known-working setup.

Check the ADK integration, dependencies, imports, environment, configuration, launch path, and provider setup.

Do not redesign the solution and do not introduce another web-search approach.

The objective is simply to determine why the same ADK setup that worked yesterday is failing today, restore the known-working configuration, and run a small smoke test to confirm ADK web search works again.

Report:
- what changed
- root cause
- exact fix
- smoke-test result

Do not continue with the full NVIDIA enrichment until the ADK smoke test passes.
