Yes. Give Luna the control of the PowerShell flow, but you should type the two SEC values directly into the terminal when prompted. Luna should never receive them in chat or write them to disk.
Paste this to Luna:
Execute the SEC configuration and Stage 7 resume yourself using a fresh VS Code integrated PowerShell terminal.
1. Open a new PowerShell terminal in VS Code.
2. cd to the repository root:
   C:\Users\ak54743\Downloads\ccrig-master (3)\ccrig-master
3. In that terminal, run an interactive PowerShell block that:
   - prompts me for SEC_USER_AGENT using Read-Host -AsSecureString;
   - prompts me for SEC_CONTACT_EMAIL using Read-Host -AsSecureString;
   - converts each securely only long enough to assign:
     - Env: Sec User Agent
     - Env: Sec Contact Email
   - never prints either value;
   - never writes either value to .env, config files, source files, logs, reports, shell history, or Git;
   - only prints:
     - SEC_USER_AGENT configured: True/False
     - SEC_CONTACT_EMAIL configured: True/False
4. Pause at the first masked prompt and wait for me to type the value directly into the terminal.
5. After I enter both values and both configuration checks return True, keep using that exact same PowerShell process.
6. Inspect the existing Stage 7 runner and determine the exact previously designed controlled partial-resume command. Do not invent a new Stage 7 workflow.
7. Resume the same frozen Stage 7 pilot selection manifest. Do not change:
   - the eight-entity pilot population;
   - ontology;
   - acceptance gates;
   - correlation definitions;
   - graph depth;
   - identity rules;
   - evidence rules.
8. The resume must now execute the previously blocked SEC portion while preserving all prior GLEIF work and run lineage.
9. Do not start Stage 8.
10. Do not modify the frontend.
11. Do not create synthetic relationships or loosen any gate to obtain a correlation.
12. At completion, regenerate/update the Stage 7 controlled-enrichment report and explicitly report:
    - SEC calls attempted/succeeded/failed;
    - documents retrieved;
    - passages retained;
    - atomic claims created;
    - accepted/candidate/rejected/context-only outcomes;
    - new VERIFIED+EXACT identities, if any;
    - new accepted relationships and versions;
    - coverage by pilot entity/family;
    - correlation results before/after;
    - whether any non-zero correlation arose naturally;
    - replay/idempotence result;
    - database/source-master integrity.
13. Stop after Stage 7 completion for senior review.
Important interaction rule: create the terminal and present the masked prompt. Do not ask me to paste SEC_USER_AGENT or SEC_CONTACT_EMAIL into chat. I will type them directly into the PowerShell terminal when it is waiting.
