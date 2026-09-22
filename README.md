You are working on the existing Lending Relationship Intelligence application in my local development environment.

OBJECTIVE
=========

I currently run the application locally on my Windows machine.

I want to test ways of allowing other users to access the COMPLETE application from their browsers while the application continues to run on my local machine.

I do NOT want a production deployment yet.

This is an accessibility/testing exercise for the existing local application.

The application appears to use a Vite/React frontend and may currently be running on port 5173, but DO NOT assume this without verifying it.

I want you to investigate, configure, test, and document these access methods:

1. Cloudflare Quick Tunnel — primary option
2. ngrok — secondary option
3. Local/LAN network access
4. VS Code port forwarding / Live Share if available and useful

The purpose is to determine which approach allows users to access the ENTIRE working application, including:

- frontend
- backend/API
- AI functions
- relationship intelligence
- maps
- network/graph views
- client pages
- event/news intelligence
- Helix integrations
- Stylus integrations
- authentication if currently implemented
- database-backed functions
- any workers/services required by the application

DO NOT simply expose a static frontend that cannot reach its backend.

IMPORTANT
=========

Do not redesign the application.
Do not rewrite working components.
Do not rename the application.
Do not introduce unnecessary infrastructure.
Do not migrate to cloud hosting.
Do not replace existing APIs.
Do not alter business functionality unless a very small configuration change is required to make remote access function correctly.

Preserve the current application behavior.

PHASE 1 — DISCOVER THE CURRENT LOCAL ARCHITECTURE
=================================================

Before making any changes, inspect the repository and determine exactly how the application currently runs.

Identify:

- project root
- frontend framework
- frontend entry point
- frontend dev server
- frontend port
- backend framework
- backend entry point
- backend port
- API base URLs
- WebSocket endpoints, if any
- AI endpoints
- Helix endpoints
- Stylus endpoints
- authentication endpoints
- database connections
- Redis/cache/queue usage
- background workers
- map services
- external APIs
- environment files
- Vite configuration
- package.json scripts
- Docker configuration if present
- proxy configuration
- CORS configuration
- CSP configuration
- any absolute localhost URLs
- any 127.0.0.1 URLs
- any hard-coded ports
- any frontend code that directly calls local backend ports

Search the repository for at least:

localhost
127.0.0.1
5173
3000
8000
5000
8080
VITE_
API_URL
BASE_URL
BACKEND
HELIX
STYLUS
WebSocket
ws://
wss://
http://
https://

Do not print secrets.

If .env files contain credentials, redact all secret values in your report.

Produce a concise architecture summary before proceeding.

Example:

Browser
   |
   v
Vite frontend :5173
   |
   +--> /api --> backend :8000
   |
   +--> /ai --> AI service
   |
   +--> Helix
   |
   +--> Stylus

But derive the real architecture from the repository.

PHASE 2 — VERIFY THE APPLICATION LOCALLY
========================================

Determine how the application is currently started.

Do not assume the command.

Inspect package.json, README, scripts, Docker files, etc.

Start all components required for the application.

Verify locally:

- frontend loads
- navigation works
- dashboard loads
- maps render
- relationship/network graph renders
- API calls succeed
- AI calls succeed if credentials/services are available
- Helix works if configured
- Stylus works if configured
- browser console does not show critical errors
- backend logs show successful requests

Record the actual local URLs.

For example only:

Frontend:
http://127.0.0.1:5173

Backend:
http://127.0.0.1:8000

But use the ports actually discovered.

Create a simple service matrix:

SERVICE | LOCAL URL | STATUS
Frontend | ... | UP/DOWN
Backend | ... | UP/DOWN
AI | ... | UP/DOWN
Helix | ... | UP/DOWN
Stylus | ... | UP/DOWN
Database | ... | UP/DOWN

If something is already broken locally, identify it BEFORE testing remote access.

Do not confuse an existing application problem with a tunnel problem.

PHASE 3 — CHECK REMOTE-ACCESS COMPATIBILITY
===========================================

This is critical.

Inspect how the browser accesses backend services.

If frontend code contains things like:

http://localhost:8000
http://127.0.0.1:8000

understand that this WILL NOT work correctly for an external user.

For an external user:

localhost = THEIR computer

not my computer.

Determine whether the application already uses:

- relative API paths such as /api/...
- Vite proxy
- reverse proxy
- same-origin routing
- dynamically derived origin

If it already does, preserve it.

If not, recommend and implement the SMALLEST SAFE development-only change necessary so users access everything through a single public origin.

Preferred model:

External browser
       |
       | HTTPS
       v
Public tunnel URL
       |
       v
Frontend / local gateway
       |
       +---- /api/* ------> local backend
       |
       +---- /ai/* -------> local AI endpoints
       |
       +---- /auth/* -----> auth endpoint
       |
       +---- /ws/* -------> WebSocket endpoint if applicable

Prefer same-origin relative routes for browser-facing calls.

Do not expose database ports directly.

Do not expose Redis directly.

Do not expose internal service ports unless absolutely necessary.

PHASE 4 — CLOUDFLARE QUICK TUNNEL
=================================

This is the first method to test.

Check whether cloudflared is installed:

cloudflared --version

If it is not installed and winget is available, install it using:

winget install -e --id Cloudflare.cloudflared

If installation requires user approval or elevation, tell me exactly what action is required.

After installation, verify:

cloudflared --version

Then expose the correct HTTP entry point.

If the application entry point is port 5173, for example:

cloudflared tunnel --url http://localhost:5173

But DO NOT blindly use 5173.
Use the actual discovered application entry port.

Capture the generated:

https://xxxxxxxx.trycloudflare.com

URL.

Do NOT place this URL into source code.

TEST THE CLOUDFLARE URL
=======================

Test the public URL as though you were an external user.

Verify:

1. Home page opens.
2. Static assets load.
3. Client-side routing works.
4. Refreshing a nested URL works.
5. API calls work.
6. AI panel works.
7. Relationship map works.
8. World map loads.
9. Relationship/network visualization loads.
10. Client detail pages work.
11. Event/news intelligence works.
12. Helix-dependent functions work if available.
13. Stylus-dependent functions work if available.
14. WebSockets work if the app uses them.
15. Browser console has no blocking CORS errors.
16. Browser console has no mixed-content errors.
17. Network calls do not attempt to contact the remote user's localhost.
18. Authentication works if currently implemented.

If an external-access issue appears, diagnose it.

Common causes to check:

- CORS
- Host header validation
- Vite allowedHosts
- absolute localhost URLs
- WebSocket origin
- mixed HTTP/HTTPS
- CSP
- cookies
- SameSite
- secure cookie settings
- callback URLs
- OAuth redirect URIs
- API base URL
- HMR configuration

Make only minimal development configuration changes required.

Do NOT weaken production security globally.

If a change is needed solely for local tunnel testing, make it explicitly development-only.

PHASE 5 — CHECK VITE CONFIGURATION
==================================

If this is a Vite application, inspect vite.config.*.

Determine whether it should bind to:

0.0.0.0

for network access.

For LAN testing, something equivalent to:

server: {
  host: '0.0.0.0'
}

may be required.

Do NOT make this change unless appropriate.

Check Vite's host restrictions.

Do not use an unrestricted wildcard security setting unnecessarily.

If Cloudflare's generated hostname causes a host validation issue, use the narrowest reasonable development solution.

PHASE 6 — NGROK TEST
====================

After Cloudflare is working or its issue has been documented, test ngrok as the second method.

Check:

ngrok version

If ngrok is missing, determine the current supported Windows installation method.

Prefer:

winget install ngrok.ngrok

if that package is available.

Do NOT invent an authentication token.

If ngrok requires account authentication, stop at that stage and tell me:

- what command I need to run
- where I obtain the token
- what the token is used for

Never place ngrok auth tokens in source control.

After authentication, expose the same application entry point.

Example only:

ngrok http 5173

Use the real port.

Capture the public HTTPS URL.

Run the same functional tests used for Cloudflare.

Compare:

- setup complexity
- URL reliability
- browser compatibility
- API behavior
- WebSocket behavior
- performance
- authentication requirements
- free-tier limitations

PHASE 7 — LOCAL NETWORK ACCESS
==============================

Test access from other devices connected to the same local network.

Find the machine's IPv4 addresses using:

ipconfig

Identify the appropriate LAN interface.

Ignore irrelevant interfaces where possible, such as:

- disconnected adapters
- Docker virtual adapters
- Hyper-V adapters
- VPN adapters unless VPN access is the intention

Determine the correct LAN IPv4 address.

Example:

192.168.x.x
or
10.x.x.x

Ensure the frontend binds to:

0.0.0.0

if required.

Then verify access using:

http://<LAN-IP>:<PORT>

Example only:

http://192.168.1.25:5173

Do not expose additional backend ports unless necessary.

Prefer one browser-facing port with proxied internal services.

Check Windows Firewall behavior.

Do not disable Windows Firewall globally.

If a firewall rule is needed, create or recommend a narrow inbound rule for only the required development port.

Document exactly what was changed.

PHASE 8 — VS CODE PORT FORWARDING / LIVE SHARE
==============================================

Check whether this development environment supports:

- VS Code Ports panel / port forwarding
- VS Code Live Share

Do not install large extensions automatically unless necessary.

Explain whether either option provides value for this application.

If VS Code port forwarding can expose the running application safely and conveniently, test it if possible.

If Live Share is primarily useful for collaborative coding rather than normal end-user access, say so.

Do not recommend it as the main distribution mechanism if Cloudflare/ngrok is more appropriate.

PHASE 9 — BACKEND PROXYING
==========================

If remote access fails because the frontend uses hard-coded backend URLs, fix this in a clean development-compatible way.

Preferred approaches, in priority order:

1. Existing same-origin reverse proxy
2. Existing Vite proxy
3. Relative browser API URLs
4. Minimal local reverse proxy

Example architecture:

Browser
   |
   v
https://random.trycloudflare.com
   |
   v
Vite/local gateway :5173
   |
   +--> /api -> localhost:<backend-port>
   |
   +--> /ai -> localhost:<AI-port>
   |
   +--> /ws -> localhost:<ws-port>

Do not tunnel databases.

Do not tunnel internal credential/token services separately unless architecture genuinely requires it.

PHASE 10 — SECURITY REVIEW BEFORE SHARING
=========================================

Before declaring the URL safe to give to users, inspect whether the application exposes:

- customer data
- lending information
- internal counterparty information
- API keys
- access tokens
- environment variables
- debug endpoints
- Swagger/OpenAPI administration endpoints
- database admin interfaces
- developer dashboards
- stack traces
- source maps containing secrets
- internal URLs
- test credentials
- admin functions without authentication

Check frontend bundles for accidental exposure of server-side secrets.

Remember:

Anything prefixed with VITE_ may be delivered to the user's browser.

Therefore VITE_ variables must NEVER contain:

- client secrets
- private API credentials
- service account secrets
- Helix secrets
- Stylus secrets
- database credentials

If any such problem exists, STOP before sharing the tunnel URL and report it.

Do not print secret values.

PHASE 11 — HELIX / STYLUS
=========================

Inspect how Helix and Stylus are accessed.

Determine whether calls occur:

A. browser -> Helix/Stylus

or

B. browser -> local backend -> Helix/Stylus

Prefer server-side integration when credentials are involved.

Do not expose Helix or Stylus secrets to the frontend.

If tokens expire, inspect the existing token refresh mechanism.

Do not redesign it as part of this task unless it prevents the application from functioning.

If the system already has token refreshing, verify it works through the tunnel.

If tokens are currently hard-coded or manually renewed, report this separately.

PHASE 12 — CREATE SAFE STARTUP HELPERS
======================================

ONLY after the manual tests work, create simple Windows developer helper scripts if useful.

For example:

scripts/
    start-local.ps1
    start-cloudflare-tunnel.ps1
    start-lan.ps1
    check-local.ps1

Do NOT make these scripts embed:

- passwords
- access tokens
- API keys
- tunnel credentials

A possible Cloudflare helper may:

1. verify the application port responds
2. verify cloudflared exists
3. start the tunnel
4. display the public URL
5. explain that closing the process ends access

Do not over-engineer this.

PHASE 13 — HEALTH CHECK
=======================

Create or use an existing lightweight health check.

I want a result similar to:

LOCAL DEVELOPMENT STATUS

Frontend            UP
Backend API         UP
Database            UP
AI                   UP
Helix               UP / NOT CONFIGURED
Stylus              UP / NOT CONFIGURED
Map service         UP
Relationship engine UP

REMOTE ACCESS STATUS

Cloudflare Tunnel   WORKING
Public frontend     WORKING
Public API calls    WORKING
AI                  WORKING
Maps                WORKING
WebSockets          WORKING / NOT USED
Authentication      WORKING / NOT CONFIGURED

Do not mark something WORKING unless it was actually tested.

PHASE 14 — FINAL COMPARISON
===========================

At the end, provide a factual comparison:

METHOD:
Cloudflare Quick Tunnel

Status:
WORKING / PARTIAL / FAILED

External URL:
<URL if currently running>

Account required:
Yes/No

Changes required:
...

Limitations:
...

------------------------------------------------

METHOD:
ngrok

Status:
WORKING / BLOCKED BY AUTH / PARTIAL / FAILED

External URL:
...

Account required:
...

Changes required:
...

Limitations:
...

------------------------------------------------

METHOD:
LAN

Status:
...

LAN URL:
...

Scope:
Same network/VPN only

------------------------------------------------

METHOD:
VS Code

Status:
...

Use case:
...

PHASE 15 — RECOMMENDED TESTING MODE
===================================

Do not make a production architecture recommendation yet.

Instead identify which method is the most practical for THIS LOCAL TESTING scenario based on what actually worked.

The expected outcome is likely:

Cloudflare Quick Tunnel
        |
        v
One HTTPS URL
        |
        v
Local application gateway/frontend
        |
        +--> Backend
        +--> AI
        +--> Helix
        +--> Stylus
        +--> Maps
        +--> Relationship engine

But validate this rather than assuming it.

IMPORTANT EXECUTION RULES
=========================

1. Inspect before modifying.
2. Back up any configuration file before materially changing it.
3. Make minimal changes.
4. Do not redesign application architecture.
5. Do not delete working code.
6. Do not expose secrets.
7. Do not commit credentials.
8. Do not disable security controls globally.
9. Do not expose database or Redis ports publicly.
10. Do not assume port 5173.
11. Do not assume there is only one service.
12. Do not claim something works without testing it.
13. Keep a record of every file changed.
14. Clearly distinguish existing problems from tunnel-related problems.
15. If administrator approval or interactive login is required, stop at that action and tell me exactly what I need to do.
16. Do not silently install unrelated software.
17. Do not convert this into a production deployment exercise.

VERY IMPORTANT — DO NOT STOP AFTER SEEING THE UI
================================================

A tunnel is NOT considered successful merely because the login/home/dashboard page renders.

Success requires that an external browser can use the complete functional application.

Specifically inspect the browser Network panel or equivalent and confirm that calls such as:

/api/*
/ai/*
/relationships/*
/clients/*
/events/*
/news/*
/maps/*
/auth/*
WebSocket connections

reach the correct services.

No remote user's browser should be trying to contact:

localhost:<backend-port>

or:

127.0.0.1:<backend-port>

unless localhost is intentionally referring to something running on that user's own device, which is not expected here.

FIRST RESPONSE
==============

Before changing anything, report:

1. detected project root
2. detected frontend technology
3. detected frontend port
4. detected backend technology
5. detected backend port
6. how frontend currently reaches backend
7. all required supporting services
8. whether hard-coded localhost URLs exist
9. whether the application appears ready for tunneling as-is
10. the exact first test you intend to perform

Then proceed with the investigation and implementation.

FINAL DELIVERABLE
=================

When complete, give me:

A. Current architecture discovered

B. Files changed
For every changed file:
- path
- reason
- exact purpose of change

C. Commands used

D. Local URLs

E. Cloudflare public URL

F. ngrok public URL, if tested

G. LAN URL

H. Test matrix showing what actually works

I. Any remaining blockers

J. Security observations

K. How I start it next time

The final "How I start it next time" section should be extremely simple.

Ideally something like:

Terminal 1:
<command to start application>

Terminal 2:
<command to start Cloudflare tunnel>

Then:

Share:
https://xxxxx.trycloudflare.com

But derive the actual commands from this repository.

Start now with PHASE 1.
