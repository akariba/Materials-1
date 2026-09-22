You are responsible for moving the existing Lending Relationship Intelligence application from the current Windows development environment to the Market Dev Unix server and getting the EXISTING application running end to end there.

This is a deployment/migration task.

Do NOT redesign the UI.
Do NOT add new product features.
Do NOT refactor working business logic unless required for Unix compatibility.
Do NOT remove existing functionality.
Do NOT mutate CAM/source artifacts.

The goal is:

CURRENT WINDOWS APPLICATION
        ↓
validate current build
        ↓
create clean deployment copy
        ↓
transfer to Market Dev
        ↓
build dependencies natively on Unix
        ↓
configure runtime
        ↓
start backend/frontend
        ↓
validate application
        ↓
validate AI / relationship / research tools
        ↓
make service reachable from browser through Market Dev
        ↓
report final URL and remaining infrastructure requirements

==================================================
KNOWN MARKET DEV CONNECTION
==================================================

Remote host:

sd-f34e-972f.nam.nsroot.net

User:

ak54743

SSH port:

22

Remote platform:

Linux / Unix

The working OpenSSH client on Windows is currently:

C:\Users\ak54743\AppData\Local\CitiSoftware\CTC1829056_GITFORWINDOWSPORTABLE_2.45.0\usr\bin\ssh.exe

Before relying on this path, verify it still exists.

Do not expose passwords, tokens, JWTs, bearer credentials, cookies, or other secrets in output or logs.

==================================================
OPERATING RULES
==================================================

Work sequentially.

Do not jump ahead.

At the end of each phase:

1. validate what was done
2. report the result briefly
3. continue automatically if safe
4. STOP if a blocker requires:
   - user authentication
   - elevated privileges
   - firewall changes
   - corporate network approval
   - reverse-proxy/DNS registration
   - certificates
   - unknown production credentials
   - destructive replacement of existing Market Dev files

Do not guess around corporate infrastructure blockers.

Preserve any existing application already on Market Dev.

Do not overwrite an existing directory until you inspect it.

==================================================
PHASE 1 — INSPECT CURRENT WINDOWS APPLICATION
==================================================

First determine the exact local project directory.

Inspect:

backend/
frontend/
data/
scripts/
requirements files
package.json
package-lock.json
environment/configuration files
SQLite databases
JSON persistence
reference/source files

Identify:

- repository root
- backend entry point
- frontend entry point
- current development ports
- current build commands
- database/data locations
- required environment variables
- AI relationship persistence
- External Research persistence
- map/static assets
- Helix integration
- Stylus/Runner integration

Do NOT modify anything yet.

==================================================
PHASE 2 — VALIDATE THE WINDOWS SOURCE BEFORE TRANSFER
==================================================

Before copying the application, prove that the source is in a valid state.

Run the existing quality checks.

At minimum:

BACKEND
- run all backend tests
- run focused AI relationship tests if separate
- record failures

FRONTEND
- TypeScript validation
- production build
- any configured frontend tests

Also verify that these important application areas still compile/load:

Overview
Clients
Network
Relationship Explorer
Relationship Definitions
AI Create Relationship
External Research
Review Queue

If the CURRENT source does not build locally:

STOP migration work.

Fix only build-breaking issues first.

Do not transfer a knowingly broken source tree.

==================================================
PHASE 3 — CREATE A CLEAN DEPLOYMENT COPY
==================================================

Do not transfer the Windows runtime environment verbatim.

Create a clean deployment directory/archive.

INCLUDE:

backend source
frontend source
package.json
package-lock.json
Python requirements / dependency definition
required scripts
required static assets
required reference/source data
configuration templates
required database/schema code
required application state that we explicitly want to preserve
relationship definitions and versions where appropriate
required evidence/reference metadata where appropriate

EXCLUDE:

node_modules/
.venv/
venv/
__pycache__/
.pytest_cache/
Vite cache
temporary logs
PID files
Windows temporary files
IDE metadata unless necessary
raw tokens
credential caches
passwords
browser session data
Windows-only credential files

Do not accidentally package secrets from .env files.

Inspect .env/configuration before packaging.

If configuration contains secrets:

create a sanitized Unix environment template instead.

==================================================
PHASE 4 — INSPECT MARKET DEV BEFORE TRANSFER
==================================================

Use SSH to connect to:

ak54743@sd-f34e-972f.nam.nsroot.net

Verify:

whoami
hostname -f
pwd
uname -a

Then inspect the user's home directory.

Do NOT overwrite existing folders blindly.

Specifically inspect currently visible directories such as:

Application
helix-cli
other existing application folders

Determine a clean target directory.

Preferred concept:

~/lending-relationship-intelligence

or another non-conflicting directory.

If the target already exists:

report it and inspect it before replacing anything.

==================================================
PHASE 5 — CHECK UNIX RUNTIME PREREQUISITES
==================================================

On Market Dev determine:

Python availability:
python3 --version
which python3

Node:
node --version
which node

npm:
npm --version
which npm

Also check:

git
curl
tar
unzip

Do not install system packages automatically if sudo/root is required.

If an adequate Python or Node runtime is missing:

STOP and report the exact required version/tool.

If multiple Python versions exist, choose one compatible with the application dependencies.

Do not rely on the rh-python warning messages from login without checking the actual installed Python.

==================================================
PHASE 6 — TRANSFER THE CLEAN APPLICATION
==================================================

Choose a reliable transfer method available in the environment.

Preferred possibilities:

1. scp/sftp
2. tar archive + scp
3. existing Tectia Secure File Transfer
4. approved internal Git repository if already configured

Do not require Git repository setup if transfer through SSH is simpler.

Transfer the CLEAN deployment package, not node_modules/.venv.

After transfer:

verify file count
verify archive integrity if archived
extract into the selected remote directory
confirm expected backend/frontend structure exists

Do not delete the local copy.

==================================================
PHASE 7 — CREATE UNIX PYTHON ENVIRONMENT
==================================================

Inside the Market Dev application directory:

create a fresh Unix virtual environment.

Example concept:

python3 -m venv .venv

Activate it.

Install backend dependencies using the repository's actual dependency file.

Do not blindly change dependency versions unless installation proves incompatible.

If a dependency fails because of:

- unavailable corporate registry
- incompatible Python version
- missing compiler/system library
- proxy/authentication requirement

STOP and report the exact package and error.

Do not substitute random versions just to get installation to complete.

==================================================
PHASE 8 — BUILD FRONTEND NATIVELY ON UNIX
==================================================

Inside frontend:

use:

npm ci

not copied Windows node_modules.

Then:

npm run build

Confirm the production build succeeds.

Verify expected dist/build output exists.

Do not run npm dev as the final deployment architecture.

Development mode may be used temporarily for diagnosis only.

==================================================
PHASE 9 — NORMALIZE RUNTIME PATHS
==================================================

Now inspect actual Unix startup failures.

Fix ONLY concrete portability problems.

Examples:

C:\ paths
Windows backslashes
PowerShell-only runtime commands
relative paths depending on Windows working directory
hardcoded 127.0.0.1 where server binding requires another address
Windows temporary directories
Windows executable paths

Use portable path handling such as pathlib where appropriate.

Do not broadly refactor working code.

All durable locations should resolve correctly from the Unix project root or environment configuration.

==================================================
PHASE 10 — DATA / DATABASE VALIDATION
==================================================

Identify which data stores are:

IMMUTABLE INPUTS
and which are
MUTABLE OPERATIONAL STATE

Preserve immutable source/reference artifacts as read-only where practical.

Ensure mutable stores are writable by the current Unix user.

Validate existing SQLite/JSON stores for:

relationship definitions
definition versions
published AI relationship instances
audit events
review decisions
external-research state
evidence metadata

Do not migrate temporary test data unintentionally.

Do not rebuild CAM/source truth.

CAM remains authoritative and immutable.

==================================================
PHASE 11 — PRODUCTION FRONTEND SERVING MODEL
==================================================

Prefer the simplest same-origin model supported by the existing code.

Target concept:

Browser
      ↓
Market Dev host:PORT
      ↓
application
      ├── frontend production assets
      └── /api backend

If FastAPI already supports serving frontend/dist safely:

use that.

Otherwise use the smallest existing production-capable serving approach.

Do NOT create a complex reverse proxy unless required.

React client routes must survive browser refresh.

Validate at least:

/
or /lending

/lending/clients
/lending/network
/lending/relationships or existing Relationship Explorer route
/lending/external-research
/lending/review

==================================================
PHASE 12 — SERVER BINDING
==================================================

The Windows development server may currently use:

127.0.0.1

For Market Dev, the application must be able to listen on an appropriate server interface.

Prefer configuration such as:

HOST=0.0.0.0
PORT=<approved available port>

Do not hardcode the port until checking availability.

Use:

ss -ltn
or equivalent

to identify conflicts.

Choose an appropriate non-conflicting port.

Do not stop unrelated processes.

==================================================
PHASE 13 — FIRST UNIX START
==================================================

Start the application manually in the foreground first.

Do not immediately daemonize it.

Verify:

backend starts
database initializes
frontend assets load
API responds
no fatal path errors
no Windows-only command invocation
no missing required source files

Add or use a health endpoint if one already exists.

Otherwise perform simple API checks.

==================================================
PHASE 14 — LOCAL MARKET DEV VALIDATION
==================================================

From Market Dev itself, test with curl.

Example concept:

curl http://127.0.0.1:<PORT>/

curl http://127.0.0.1:<PORT>/api/health

or equivalent existing endpoints.

Confirm:

HTTP response
frontend page returns
API responds

Do not yet assume external accessibility.

==================================================
PHASE 15 — VALIDATE APPLICATION FUNCTIONS ON UNIX
==================================================

Validate the major existing tools.

OVERVIEW
- loads portfolio data
- exposure and sector analytics work
- geography/map assets work

CLIENTS
- population loads
- client filters work

NETWORK
- relationship data loads
- map/network components render from existing APIs

RELATIONSHIP EXPLORER
- existing records load

RELATIONSHIP DEFINITIONS
- definitions persist
- drafts/versions load

AI CREATE RELATIONSHIP
- existing backend workflow is reachable

REVIEW QUEUE
- existing review data loads

EXTERNAL RESEARCH
- page loads
- do not claim live external access until provider validation is complete

==================================================
PHASE 16 — HELIX VALIDATION
==================================================

Market Dev already appears to contain a helix-cli directory.

Inspect it.

Do not copy Windows Helix tokens.

Determine whether the Unix environment has:

helix executable
required PATH/configuration
corporate authentication state
required CA certificates
network access

Use the actual existing application Helix integration.

Test readiness without logging tokens.

If authentication requires an interactive user step:

STOP and clearly tell the user what command/action is required.

Do not expose the token value.

==================================================
PHASE 17 — STYLUS / RUNNER VALIDATION
==================================================

Stylus is separate from Helix.

Do not treat them as one credential.

Inspect existing configuration for:

Runner Service URL
Stylus preset
CA bundle
SOEID/user identity
token acquisition
token expiry logic

Test readiness safely.

Do not log JWT/token values.

If current Unix environment cannot acquire a usable Stylus credential automatically:

STOP that integration validation and report exactly what external authentication step/configuration is missing.

Do not invent a refresh-token mechanism.

The rest of the application should continue working even if Stylus is unavailable.

==================================================
PHASE 18 — AUTO-PREFLIGHT VALIDATION
==================================================

Where existing code supports it, validate:

AI/R2D2 action
    ↓
Helix readiness check
    ↓
continue or clear authentication error

External Research
    ↓
Stylus readiness check
    ↓
continue or clear authentication error

Provider failures must not crash the whole application.

==================================================
PHASE 19 — TEST RELATIONSHIP WORKFLOW ON UNIX
==================================================

Execute a non-destructive relationship workflow.

Prefer Common Guarantor.

Validate:

create/open draft
preview
candidate generation
Why Detected/provenance
save/version behavior

Do NOT publish test data into live-like stores unless explicitly safe.

If publication must be validated, use isolated test storage or clean up afterward.

Confirm CAM remains unchanged.

==================================================
PHASE 20 — BROWSER ACCESS FROM WINDOWS
==================================================

Once Market Dev local curl works, determine whether the Market Dev server/port is reachable from the Windows desktop.

First identify:

hostname -f
hostname -I or equivalent

Then provide a candidate URL such as:

http://sd-f34e-972f.nam.nsroot.net:<PORT>/

Do not claim it is live until tested from the user's browser.

If browser access works:

report the working URL.

If browser access fails while local curl succeeds:

do NOT keep modifying application code.

This is probably infrastructure/network exposure.

Diagnose whether the issue is:

host firewall
corporate network ACL
reverse proxy requirement
approved ingress port requirement
DNS/proxy policy

STOP before making privileged network changes.

==================================================
PHASE 21 — USER-FRIENDLY LINK
==================================================

A raw host:port URL is acceptable for the first staging validation.

For the final internal link, determine whether Market Dev requires:

reverse proxy
corporate web gateway
registered internal DNS
HTTPS certificate
approved application route

If any of those require ServiceNow/infrastructure work:

report exactly what is required.

Do not fabricate an internal URL.

==================================================
PHASE 22 — KEEP APPLICATION RUNNING
==================================================

Only after manual foreground startup and browser validation pass:

determine the permitted process-management method.

Possible options:

systemd user service
systemd system service
approved corporate process manager
nohup as temporary staging only

Do not install a system-wide service without approval.

For a temporary staging run, a user-owned process is acceptable if policy permits.

Capture:

PID
port
log location
startup command
shutdown command

==================================================
PHASE 23 — FINAL REGRESSION TEST
==================================================

Run again:

backend tests
focused relationship tests
frontend TypeScript validation
frontend production build

Validate:

Overview
Clients
World/Geography map
Network
Relationship Explorer
Relationship Definitions
AI Create Relationship
External Research page
Review Queue

Where integrations are available also validate:

Helix
Stylus
AI analysis
external research

==================================================
PHASE 24 — SECURITY CHECK
==================================================

Search the Unix deployment for accidental secrets.

Confirm no:

raw Helix tokens
raw Stylus JWTs
Authorization headers
passwords
credential dumps
browser cookies
Windows credential files

exist in:

frontend source
frontend built assets
logs
URLs
audit records
deployment archive

Do not print discovered secret values in the report.

==================================================
PHASE 25 — FINAL REPORT
==================================================

Return a concise deployment report:

WINDOWS SOURCE VALIDATION
PASS / FAIL

TRANSFER
PASS / FAIL

REMOTE DIRECTORY
<path>

PYTHON
<version/status>

NODE / NPM
<versions/status>

BACKEND INSTALL
PASS / FAIL

FRONTEND BUILD
PASS / FAIL

DATA / SQLITE
PASS / FAIL

APPLICATION START
PASS / FAIL

LOCAL UNIX HTTP TEST
PASS / FAIL

WINDOWS BROWSER ACCESS
PASS / FAIL

WORKING URL
<URL if actually validated>

OVERVIEW
PASS / FAIL

CLIENTS
PASS / FAIL

NETWORK / MAP
PASS / FAIL

RELATIONSHIP EXPLORER
PASS / FAIL

RELATIONSHIP DEFINITIONS
PASS / FAIL

AI CREATE RELATIONSHIP
PASS / FAIL

REVIEW QUEUE
PASS / FAIL

HELIX
READY / AUTH REQUIRED / BLOCKED

STYLUS
READY / AUTH REQUIRED / BLOCKED

EXTERNAL RESEARCH
PASS / DEGRADED / BLOCKED

CAM IMMUTABILITY
PASS / FAIL

TEST RESULTS
<summary>

START COMMAND
<exact command>

STOP COMMAND
<exact command>

LOG LOCATION
<path>

REMAINING INFRASTRUCTURE ACTIONS
<only if required>

==================================================
IMPORTANT COMPLETION RULE
==================================================

Do not say the application is LIVE merely because:

- files were copied
- dependencies installed
- backend started
- curl worked locally

LIVE means:

1. application runs on Market Dev
2. frontend and backend communicate
3. required data is available
4. major application pages load
5. browser access from the user's Windows environment has been verified

If external AI providers are unavailable, clearly distinguish:

APPLICATION LIVE
from
OPTIONAL PROVIDER DEGRADED

Do not hide blockers.
Do not invent success.
