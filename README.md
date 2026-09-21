You are working on the existing CCRIG / Lending Relationship Intelligence repository.

The final target is Unix/Linux deployment. I want to be able to copy the CCRIG project to Unix, configure it, install dependencies, start it, and have the complete application work end to end.

DO NOT modify code yet.

First perform a deep repository audit.

Inspect the entire repository for:

- Windows-specific paths
- C:\ references
- Users\ / Downloads\ references
- PowerShell / pwsh
- cmd.exe
- .bat / .ps1 dependencies
- hardcoded localhost / 127.0.0.1
- hardcoded ports 5174 / 8001
- absolute filesystem paths
- database paths
- data paths
- log paths
- frontend build/start logic
- backend start logic
- SEC integration
- Helix
- Stylus
- bearer tokens
- refresh logic
- credential cache
- environment variables
- subprocess usage
- shell=True
- runtime-generated files
- relationship definition persistence
- relationship instance persistence
- external research persistence

Also inspect the current application architecture for:

Overview
Clients
Network
Relationship Explorer
External Research
Review Queue
AI Create Relationship / Relationship Definitions

I specifically need you to determine:

1. How the backend currently starts.
2. How the frontend currently starts.
3. Whether the frontend can be served as a production build.
4. Where application data is stored.
5. Where relationship definitions are stored.
6. Where relationship instances are stored.
7. How External Research works.
8. How SEC requests are executed.
9. Exactly how Helix credentials are obtained.
10. Exactly how Stylus credentials are obtained.
11. How token expiration is detected.
12. How tokens are refreshed today.
13. Whether anything depends on Windows-only authentication.
14. What will fail if the folder is copied directly to Unix today.
15. Which files need modification to make the application Unix-ready.

Return a structured report only.

Use sections:

CURRENT ARCHITECTURE
WINDOWS DEPENDENCIES
FRONTEND RUNTIME
BACKEND RUNTIME
PERSISTENCE
SEC / HELIX / STYLUS
RELATIONSHIP DEFINITIONS
UNIX BLOCKERS
FILES THAT NEED CHANGES
RECOMMENDED IMPLEMENTATION ORDER

Do not implement anything yet.
Do not rewrite existing working modules.
Do not invent Helix or Stylus authentication behavior.
Base the report only on what actually exists in the repository.
