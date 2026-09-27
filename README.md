top trying to create or control interactive terminals.
Create one local helper script:
backend/scripts/resume_stage7_sec.ps1
Requirements:
- it must prompt me interactively for SEC_USER_AGENT
- then prompt for SEC_CONTACT_EMAIL
- both inputs must be masked/not echoed
- keep both values process-local only
- do not write either value to disk, logs, reports, JSON, source code, shell history, or git
- set them only for the Stage 7 process
- run the existing Stage 7.1 controlled resume using the existing frozen selection manifest
- after execution, clear both environment variables in a finally block
- do not start Stage 8
- do not alter the frozen pilot population, ontology, acceptance gates, or correlation definitions
After creating and validating the script, give me ONLY the one short PowerShell command I need to run manually from:
C:\Users\ak54743\Downloads\ccrig-master (3)\ccrig-master
Do not try to open another terminal yourself
