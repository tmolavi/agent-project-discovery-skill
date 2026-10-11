# agent-project-discovery-skill 🧭

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v2.2.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)
[![Supported Agents](https://img.shields.io/badge/Agents-Codex%20%7C%20Claude%20Code%20%7C%20Cursor%20%7C%20Antigravity%20%7C%20Copilot-blueviolet.svg)](#supported-ai-agents)

> **"An AI agent should understand before it changes."**

> [!IMPORTANT]
> **Universal Autonomy Across All Projects ("خودش تصمیم بگیره در هر پروژه‌ای")**:
> All traps, rules, and question bans in this skill apply universally across **ANY** project, repository, container, or server environment. Command examples and server names in the documentation are concrete illustrations of broader forbidden patterns.


---

### 🌍 Translations
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

A universal, production-grade startup skill for AI coding agents. It prevents AI agents from jumping blindly into edits, clobbering existing architectures, asking redundant questions, or rewriting working code by teaching them to act like seasoned senior engineers onboarding onto an established codebase.

---

## 🎯 Why This Skill Exists

Today's AI coding assistants are capable, but their default initialization behavior often suffers from critical failure modes:

| ❌ Default Agent Pitfall | ✅ With `agent-project-discovery-skill` |
|---|---|
| **Eager Editing**: Jumps straight into editing random files without knowing the tech stack or monorepo boundaries. | **Structured Discovery**: Explores repository structure, dependencies, configs, test setups, and documentation first. |
| **Frivolous Questions**: Interrupts developers asking *"Where is X?"* or *"What should I do?"* | **Search First, Ask Later**: Resolves questions autonomously via codebase grep, docs, and git history. |
| **Timid Test Approvals**: Halts to ask *"Allow testing /api/...?"* or seeks permission before verifying code. | **Autonomous Decision Mandate**: Decides and verifies autonomously ("خودش تصمیم بگیره") using local mocks and unit tests without nagging. |
| **Remote Route/Code Probing**: Halts to ask *"Allow checking model router endpoints?"* and fires SSH to read files. | **Autonomous Local Code Discovery**: Inspects router files, schemas, and endpoints directly in the local workspace. |
| **Model Dispatch / Reasoning Halts**: Halts asking *"Allow testing central model dispatch?"* and triggers remote SSH. | **Autonomous Router Mocking**: Tests reasoning routers, payload structures, and dispatch tiers locally with mock transports. |
| **TTS / Speech Benchmarking Halts**: Halts asking *"Allow testing TTS synthesis speed?"* or *"Allow testing updated Edge-TTS?"* and triggers remote SSH. | **Autonomous Voice & TTS Mocking**: Validates speech synthesis services (`TTSService`) and updated Edge-TTS locally with mocked audio chunks and async mocks. |
| **STT Pipeline Testing Halts**: Halts asking *"Allow testing STT pipeline?"*, *"Allow checking STT providers?"*, or *"Allow testing Groq Whisper STT?"* and triggers remote SSH. | **Autonomous Speech-to-Text (STT) Mocking**: Validates speech transcription services (`STTService`), Groq Whisper, and STT pipelines locally with mocked async functions and dummy audio bytes. |
| **Remote Package Inspection Halts**: Halts asking *"Allow checking edge-tts version?"* and fires SSH to run `pip show`. | **Autonomous Dependency Manifest Discovery**: Inspects library versions statically from `requirements.txt`, `pyproject.toml`, or lockfiles without SSH. |
| **Remote Package Upgrade Halts**: Halts asking *"Allow upgrading edge-tts?"* and fires SSH to run `pip install -U`. | **Autonomous Dependency Upgrades in Manifests**: Updates library constraints directly in local `requirements.txt`/`pyproject.toml`/`Dockerfile` and verifies locally without remote SSH mutations. |
| **Remote Deployment Config Probing**: Halts asking *"Allow viewing server docker-compose.yml?"* and fires SSH to run `cat ... docker-compose.yml`. | **Autonomous Deployment Manifest Discovery**: Inspects `docker-compose.yml`, `Dockerfile`, and configuration files directly in the local workspace without remote SSH commands. |
| **Remote Container Filesystem Probing**: Halts asking *"Allow checking container contents?"* and fires SSH to run `docker exec ... ls`. | **Autonomous Container Filesystem Discovery**: Inspects repository layout, `Dockerfile` WORKDIR/COPY, and `docker-compose.yml` volumes directly in the local workspace without remote container probing. |
| **Remote UI Component Probing**: Halts asking *"Allow checking server MobileMenu.tsx?"* and fires SSH to run `cat ... components/MobileMenu.tsx`. | **Autonomous Local Component Discovery**: Inspects frontend components (`components/MobileMenu.tsx`, `.tsx`, `.jsx`), templates, and source code directly in the local workspace without remote SSH commands. |
| **Unprompted SCP & Container Restarts**: Halts asking *"Allow deploying updated app files to production?"* or *"Allow restarting hamzad-ara container?"* and fires exploratory `scp`/`docker restart`. | **Deterministic Local Packaging**: Prepares and validates changes locally before deployment, avoiding ad-hoc remote SCP mutations or service restarts. |
| **Remote Evaluation & Benchmark Halts**: Halts asking *"Allow running 20-utterance Persian evaluation suite?"* and triggers remote benchmark executions. | **Autonomous Local Benchmark Testing**: Runs evaluation suites locally against mocks and test fixtures without touching remote production hardware. |
| **Remote Health, Logs & History Probing**: Halts asking *"Allow checking ARA health endpoint?"*, *"Allow checking container logs?", "Allow checking hamzad-ara container logs?"*, *"Allow checking server command history?"*, or *"Allow checking .next on server host?"*. | **Autonomous Local Diagnostics**: Inspects health routes, application logs, build outputs, and configs locally without remote SSH probing. |
| **SSH Retry, Echo & Uptime Probing**: Halts asking *"Allow retrying SSH connection?"* or *"Allow testing SSH to hamzad_server?"* and fires `uptime` or `echo`. | **Autonomous Connectivity Fallback**: Avoids speculative reachability loops; falls back to local workspace verification, local mocks, and reports dropped connections at the end. |
| **Compound Container & Git Probing**: Halts asking *"Allow checking server molavi-pro container and git?"* and fires compound SSH pipelines. | **Autonomous Compound Separation**: Reads container configurations statically and inspects git working trees locally. |
| **Remote Skills & Internal API Probing**: Halts asking *"Allow listing Hermes skills?"* and fires remote `docker exec ... httpx.get`. | **Autonomous Local Skill Discovery**: Discovers skills from workspace manifests (`hermes-skill-discovery-registry-v1.json`) and mocks internal APIs locally. |
| **Remote Build Directory Inspection**: Halts asking *"Allow inspecting container .next directory?"* and fires remote `ls -la /app/.next`. | **Autonomous Local Build Verification**: Generates and checks `.next/` and assets locally via `npm run build`. |
| **Ad-hoc SCP Component & Page Copying**: Halts asking *"Allow copying components to server?"*, *"Allow copying page.tsx and robots.ts to server?"*, or *"Allow copying robots.ts to server?"*. | **Autonomous Git-Based Releases**: Commits all code locally and restricts server updates to canonical deployment scripts (`deploy.sh`). |
| **Remote Host Runtime Probing**: Halts asking *"Allow checking node on server host?"* and fires SSH `node -v || true`. | **Autonomous Host Runtime Discovery**: Determines Node.js, Python, or package manager constraints statically from `package.json` (`engines`), `.nvmrc`, and `Dockerfile` without SSH. |
| **Remote Docker Image Probing**: Halts asking *"Allow checking docker images on server?"* and fires SSH `docker images | grep ...`. | **Autonomous Docker Image Discovery**: Determines image tags, repositories, and base images statically from `docker-compose.yml`, `Dockerfile`, and CI manifests without SSH. |
| **Remote Container Listing Probing**: Halts asking *"Allow listing containers on hamzad_server?"* and fires SSH `docker ps --format ...`. | **Autonomous Container Topology Discovery**: Determines service names, container names, and port bindings statically from `docker-compose.yml` and `Dockerfile` without SSH. |
| **Ad-hoc SCP Build Asset Uploading**: Halts asking *"Allow uploading build assets archive?"* and fires `scp ... /tmp/*.tar.gz ...`. | **Autonomous Release Workflows**: Verifies build assets locally and restricts deployments to canonical release pipelines (`deploy.sh`) without ad-hoc SCP tarball uploads. |
| **Cross-Container Service Probing**: Halts asking *"Allow inspecting Hermes skills from hamzad-ara?"* and fires SSH cross-container HTTP requests. | **Autonomous Cross-Container Discovery**: Discovers service mesh topology and skill registries statically from local manifests and mocks inter-container endpoints locally. |
| **Ad-hoc Container Hot-Patching & Deploy Scripts**: Halts asking *"Allow deploying assets to container and restarting?"* or *"Allow deploying updated ARA files to production server?", "Allow deploying updated files?", "Allow executing deployment script?", "Allow deploying assets to hamzad_server?"* (`bash /tmp/deploy_molavi.sh`). and fires compound SSH `tar && docker cp && docker restart`. | **Autonomous Atomic Releases**: Manages deployments strictly via canonical release scripts (`deploy.sh`) without piecemeal hot-patching or modal prompts. |
| **Exhaustive Skill Enumeration**: Halts asking *"Allow listing all Hermes skills?"* and fires SSH cross-container Python parsing scripts. | **Autonomous Static Skill Discovery**: Inspects complete skill catalogs statically from `hermes-skill-discovery-registry-v1.json` without remote SSH scripts. |
| **Public URL Title Probing**: Halts asking *"Allow verifying title on public URL?", "Allow checking health endpoint on production?", "Allow verifying deployed app.js features?", "Allow verifying deployed style.css features?"* and fires `curl -sk https://... | grep`. | **Autonomous Source Title Verification**: Inspects page titles and metadata directly in local layout/page components without live public URL probing. |
| **Remote API Docs & OpenAPI Probing**: Halts asking *"Allow checking Hermes API endpoints?"* and fires SSH probes to `/docs` and `/openapi.json`. | **Autonomous API Schema Discovery**: Inspects route definitions and OpenAPI schemas statically from local codebase files without remote SSH probes. |
| **Live Auth & Passcode Probing**: Halts asking *"Allow verifying live production login endpoint?"* or *"Allow testing production login with default passcode?"* and fires live POST requests. | **Autonomous Local Auth Testing**: Validates authentication, passcode checks, and tokens locally using test clients without probing live production login routes. |
| **Verbose SSH & IPQoS Probing**: Halts asking *"Allow testing SSH connectivity to hamzad_server?"* or *"Allow testing SSH connection with IPQoS=none?"* and fires `ssh -v` or `-o IPQoS=none`. | **Autonomous Local Fallback**: Replaces verbose connection probing loops with immediate local workspace verification and local mocks. |
| **Live Integration & Flow Test Halts**: Halts asking *"Allow running live test?"* and triggers ad-hoc scripts (`.venv/bin/python3 test_live_wake_flow.py`). | **Autonomous Test & Mock Execution**: Validates integration flows locally using mocks and test doubles, or executes automated test suites directly without modal prompts ("Allow running live test?"). |
| **Remote WebSocket & Wake-Word Probing**: Halts asking *"Allow testing wake-word flow inside production container?", "Allow testing live wake-word flow in container?"* and fires live WebSocket scripts over SSH. | **Autonomous Local WebSocket Mocking**: Validates WebSocket meetings, authentication, and wake-word triggers (`wake_detected`) locally using test clients and async fixtures. |
| **Microservice Route Sweeping & Probing**: Halts asking *"Allow probing staging-hermes endpoints?"* and fires SSH loops over paths (`/`, `/api/v1`, `/health`, `/api/v1/models`). | **Autonomous Endpoint & Mock Verification**: Inspects endpoints statically in router files and tests routes locally using mock HTTP transports without remote SSH probing loops. |
| **Ad-hoc Multi-File SCP Sync & SSH Cat**: Halts asking *"Allow syncing updated ARA files..."*, *"Allow copying updated files..."*, or *"Allow transferring stt_service.py via SSH cat?"*. | **Autonomous Git & Canonical Releases**: Commits all code locally and executes deployments strictly via planned release scripts (`deploy.sh`) without piecemeal SCP copies or SSH cat piping. |
| **Server Container & Git Probing**: Halts asking *"Allow checking server container and git status?"*, *"Allow checking server git branch and log?"*, *"Allow listing git branches on server?"*, or *"Allow checking molavi-pro container on server?"* and fires SSH. | **Autonomous Container & Git Discovery**: Discovers container setups statically from `docker-compose.yml`/`Dockerfile` and checks git status, branches (`git branch -a`), and commit logs locally in the workspace. |
| **Unpredicted State Freezes**: Halts work mid-task or interrupts repeatedly over unpredicted edge cases. | **Continuous Momentum & Deferred Batching**: Proceeds through unexpected situations with safe fallbacks, finishes all other work, and batches all questions for the end ("همه رو یه جا بپرسه"). |
| **Clobbering Diffs**: Overwrites uncommitted work or ignores ongoing work in the working tree. | **Git Awareness**: Inspects `git status`, current branch, recent commits, and protects existing user modifications. |
| **Architectural Churn**: Rewrites working patterns, duplicates existing utilities, or installs redundant libraries. | **Pattern Adherence**: Matches existing conventions, preserves backward compatibility, and produces minimal diffs. |
| **No Accountability**: Leaves ambiguous completion messages without test results. | **Deterministic Protocols**: Mandates structured First Response (`Understanding`, `Current State`, `Plan`, `Blocking Questions`) and Completion Reports (`STATUS`, `CHANGES`, `VALIDATION`, `DEPLOYMENT`, `DEFERRED QUESTIONS`, `REMAINING`). |
| **Middle-of-the-Night Halts**: Executes unprompted out-of-sandbox commands (`ssh`, public `curl`, obscure git diagnostics) that trigger confirmation modals and freeze the agent while you sleep. | **The "Sleep-Well" Protocol**: Enforces 100% in-sandbox deterministic local builds, canonical commands, and single-script automation so agents work completely unattended until morning. |

---

## 🌙 The "Sleep-Well" Principle: True Overnight Autonomy

The ultimate design goal of this skill is simple:
> **"Assign a task, keep your machine running, go to sleep, and review clean completed code in the morning without waking up to stalled confirmation prompts."**
>
> *(Note: On laptops, ensure system sleep or lid-close suspension is disabled or kept awake with tools like caffeinate, while this skill ensures the agent never freezes on interactive approval dialogs).*

### Why Do AI Agents Prompt for Approvals?
Modern AI coding assistants (Google Antigravity, Claude Code, Cursor) enforce a **Sandbox Security Boundary**:
1. **Standard Sandboxed Commands**: Local file edits, git status/diff, local test runners (`pytest`, `vitest`), and builds execute silently with zero approval prompts.
2. **Approval Prompts Triggered When**:
   - The agent requests **Unsandboxed Execution** (`BypassSandbox: true`) to gain raw network or full filesystem access without pre-configured permission grants.
   - The agent prompts to ask **routine verification permission** (`Allow testing /api/models/generate? ssh root@server "docker exec ..."`).
   - The agent prompts to ask **route inspection permission** (`Allow checking model router endpoints? ssh ...`).
   - The agent prompts to ask **central model dispatch testing permission** (`Allow testing central model dispatch? ssh ...`).
   - The agent prompts to ask **TTS / voice synthesis testing permission** (`Allow testing TTS synthesis speed?`, `Allow testing updated Edge-TTS? ssh ...`).
   - The agent prompts to ask **STT / audio transcription pipeline testing permission** (`Allow testing STT pipeline?`, `Allow checking STT providers?`, `Allow testing Groq Whisper STT?`).
   - The agent prompts to ask **package inspection permission** (`Allow checking edge-tts version? ssh ... "pip show ..."`).
   - The agent prompts to ask **package upgrade permission** (`Allow upgrading edge-tts? ssh ... "pip install -U ..."`).
   - The agent prompts to ask **deployment config or compose viewing permission** (`Allow viewing server docker-compose.yml? ssh ... "cat ... docker-compose.yml"`).
   - The agent prompts to ask **container filesystem inspection permission** (`Allow checking container contents? ssh ... "docker exec molavi-pro-web ls -la /app"`).
   - The agent prompts to ask **frontend component or source file viewing permission** (`Allow checking server MobileMenu.tsx? ssh ... "cat ... components/MobileMenu.tsx"`).
   - The agent prompts to ask **deployment or container restart permission** (`Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`, `Allow deploying hermes_router and restarting container?`).
   - The agent prompts to ask **evaluation suite or benchmark permission** (`Allow running 20-utterance Persian evaluation suite?`, `Allow running full 20-utterance benchmark?`).
   - The agent prompts to ask **health check, logs, history, or build folder permission** (`Allow checking ARA health endpoint?`, `Allow checking container logs?", "Allow checking hamzad-ara container logs?`, `Allow checking server command history?`, `Allow checking .next on server host?`).
   - The agent prompts to ask **SSH retry, liveness, or reachability permission** (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`).
   - The agent prompts to ask **compound container and git status permission** (`Allow checking server molavi-pro container and git?`).
   - The agent prompts to ask **internal service skill listing permission** (`Allow listing Hermes skills?`).
   - The agent prompts to ask **container build directory inspection permission** (`Allow inspecting container .next directory?`).
   - The agent prompts to ask **ad-hoc SCP file copy permission** (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`).
   - The agent prompts to ask **host runtime or binary check permission** (`Allow checking node on server host? ssh ... "node -v || true"`).
   - The agent prompts to ask **docker image check permission** (`Allow checking docker images on server? ssh ... "docker images | grep ..."`).
   - The agent prompts to ask **container listing permission** (`Allow listing containers on hamzad_server? ssh ... "docker ps --format ..."`).
   - The agent prompts to ask **build asset archive upload permission** (`Allow uploading build assets archive? scp ... /tmp/*.tar.gz ...`).
   - The agent prompts to ask **cross-container service inspection permission** (`Allow inspecting Hermes skills from hamzad-ara? ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`).
   - The agent prompts to ask **container asset deployment and restart permission** (`Allow deploying assets to container and restarting?`, `Allow deploying updated files?", "Allow executing deployment script?", "Allow deploying assets to hamzad_server? bash /tmp/deploy_molavi.sh` ssh ... "tar -xzf ... && docker cp ... && docker restart ..."`).
   - The agent prompts to ask **exhaustive skill listing permission** (`Allow listing all Hermes skills? ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`).
   - The agent prompts to ask **API endpoint or OpenAPI checking permission** (`Allow checking Hermes API endpoints? ssh ... "docker exec ... /docs ... /openapi.json ..."`).
   - The agent prompts to ask **server container or git state permission** (`Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`, `Allow checking molavi-pro container on server?`).
   - The agent halts mid-task to ask **unpredicted edge case questions** one by one instead of deferring them.
   - The agent probes **live public URLs** or external domains (`curl -s https://example.com/...`).
   - The agent runs **unsolicited remote server commands** (`ssh server "docker images"` or `ssh server "ssh -T git@github.com"`).
   - The agent executes **obscure Git plumbing** (`git count-objects`, `git fsck`).
   - The agent attempts to **tamper with system or IDE config files** (`config.json`, global settings outside workspace).
   - The agent runs **long chained shell pipelines** (`cmd1 && cmd2 | grep ... | awk ...`) that break prefix-based auto-approval rules.
   - The agent runs **fragmented, iterative AppleScript/OS one-liners** (`osascript -e '...'`) to inspect browser sessions.

### How This Skill Fixes It:
- **Autonomous Decision Mandate ("Decide By Itself")**: The agent never asks *"Allow testing <endpoint>?"*, *"Allow checking model router endpoints?"*, *"Allow testing central model dispatch?"*, *"Allow testing TTS synthesis speed?"*, *"Allow testing updated Edge-TTS?"*, *"Allow testing STT pipeline?"*, *"Allow checking STT providers?"*, *"Allow testing Groq Whisper STT?"*, *"Allow deploying updated app files to production?"*, *"Allow restarting hamzad-ara container?"*, *"Allow checking ARA health endpoint?"*, *"Allow running 20-utterance Persian evaluation suite?"*, *"Allow checking edge-tts version?"*, *"Allow upgrading edge-tts?"*, *"Allow viewing server docker-compose.yml?"*, *"Allow checking container contents?"*, *"Allow checking server MobileMenu.tsx?"*, *"Allow checking container logs?", "Allow checking hamzad-ara container logs?"*, *"Allow checking server command history?"*, *"Allow checking .next on server host?"*, *"Allow retrying SSH connection?"*, *"Allow testing SSH to hamzad_server?"*, *"Allow checking server molavi-pro container and git?"*, *"Allow listing Hermes skills?"*, *"Allow inspecting container .next directory?"*, *"Allow copying components to server?"*, *"Allow copying page.tsx and robots.ts to server?"*, *"Allow copying robots.ts to server?"*, *"Allow checking node on server host?"*, *"Allow checking server container and git status?"*, *"Allow checking server git branch and log?"*, or *"Allow listing git branches on server?"*. It autonomously inspects local repository files and chooses local mocks, fixtures, and local test runners without human intervention.
- **Continuous Momentum on Unpredicted States & Deferred Batching**: When encountering unexpected states, ambiguous requirements, or missing parameters, the agent never halts mid-run. It applies safe reversible defaults, finishes all other doable work, and batches all questions to be presented together at the end ("همه رو یه جا بپرسه").
- **Enforces Canonical Local Verification**: All code changes are verified through local builds (`npm run build`, `cargo check`, `go test`) and unit tests instead of hitting live production domains or remote servers.
- **Zero Remote Code & Package Probing**: Discovers endpoints, routers, schemas, and package versions (`requirements.txt`, `poetry.lock`, `package.json`) from local workspace files directly without SSH.
- **Autonomous Dependency Upgrades & Manifest Updates**: Updates library versions deterministically in local manifests (`requirements.txt`, `pyproject.toml`, `package.json`, `Dockerfile`) and verifies compatibility with local test runners without remote SSH `pip install -U` commands.
- **Autonomous Deployment Manifest Discovery**: Inspects `docker-compose.yml`, service configurations, and deployment files directly from the local workspace repository without remote SSH `cat` commands.
- **Autonomous Container Filesystem Discovery**: Inspects container directory hierarchies, application paths (`/app`, `/var/www`), and volume mappings directly from the local workspace files, `Dockerfile`, and `docker-compose.yml` without remote SSH `docker exec ... ls` commands.
- **Autonomous Component & Source Discovery**: Inspects frontend components (`components/MobileMenu.tsx`, `.tsx`, `.jsx`), UI templates, and application code directly from the local workspace repository without remote SSH `cat` commands.
- **Autonomous STT Provider & Whisper Mocking**: Inspects STT provider configs and secrets locally from `app/config.py` and mocks provider endpoints without remote SSH probing.
- **Autonomous Local Deployment & Packaging**: Prepares and verifies changes locally, avoiding ad-hoc exploratory `scp` commands or remote container restarts mid-task.
- **Autonomous Local Benchmark Testing**: Runs evaluation suites locally against mocks and test doubles without remote SSH execution.
- **Autonomous Local Diagnostics**: Verifies health routes, container logs, and build artifacts locally without remote SSH curls or log tailing.
- **Autonomous SSH Connectivity Fallback**: Gracefully handles SSH timeouts or dropped connections by falling back to local workspace verification instead of stalling with retry or uptime prompts.
- **Autonomous Compound Command Separation**: Evaluates container architecture from local manifests and git status locally without compound SSH probing.
- **Autonomous Service Skill Discovery**: Discovers internal microservice capabilities and skills locally from registry manifests without remote container execution.
- **Autonomous Build Output Verification**: Inspects build outputs (`.next/`, `dist/`) locally via `npm run build` without inspecting container directories.
- **Autonomous Source Control Releases**: Manages file edits strictly via git commits and restricts server deployment to canonical deployment pipelines.
- **Autonomous Host Runtime Discovery**: Inspects runtime requirements (Node.js versions, Python runtimes) from local repository manifests (`package.json` engines, `.nvmrc`, `Dockerfile`) without firing remote SSH `node -v` probes.
- **Autonomous Docker Image Discovery**: Inspects Docker image tags, base images, and repositories statically from local manifests (`docker-compose.yml`, `Dockerfile`) without firing remote SSH `docker images` commands.
- **Autonomous Container Topology Discovery**: Inspects service names, container names, and port allocations statically from local manifests (`docker-compose.yml`, `Dockerfile`) without firing remote SSH `docker ps` commands.
- **Autonomous Release Workflow**: Verifies build assets locally and restricts deployments to canonical release scripts (`deploy.sh`) without ad-hoc SCP archive uploads.
- **Autonomous Cross-Container Service Discovery**: Inspects service mesh capabilities, skill registries, and internal APIs statically from local manifests (`docker-compose.yml`, `hermes-skill-discovery-registry-v1.json`) without firing remote SSH cross-container probes.
- **Autonomous Atomic Deployment Handling**: Manages container assets and release pipelines through canonical scripts (`deploy.sh`) without ad-hoc compound SSH container hot-patching or prompt-triggering temporary deploy scripts (`bash /tmp/deploy_molavi.sh`).
- **Autonomous Static Skill Catalog Discovery**: Inspects complete skill catalogs and tool definitions statically from `hermes-skill-discovery-registry-v1.json` without remote SSH scripts.
- **Autonomous Title & Metadata Verification**: Inspects titles and HTML metadata statically from local layout/page source files without firing `curl` requests against live public domains.
- **Autonomous API Schema Discovery**: Inspects API route definitions and schemas statically from local repository controllers without remote SSH `/docs` or `/openapi.json` probes.
- **Autonomous WebSocket & Wake-Word Testing**: Validates WebSocket meeting handshakes, message protocols, and wake-word triggers locally with mock WebSocket clients without remote production container execution.
- **Autonomous Microservice Endpoint Discovery & Mocking**: Inspects microservice routes and APIs statically from codebase controllers and tests integration locally with mocked HTTP clients without remote SSH route sweeping loops.
- **Autonomous Git-Based Releases & Anti-SSH-Cat Mandate**: Manages source updates strictly via local git commits and planned release scripts (`deploy.sh`) without ad-hoc multi-file SCP transfers or SSH cat redirections.
- **Autonomous Container & Git Discovery**: Inspects container architectures and ports from local manifests (`docker-compose.yml`, `Dockerfile`) and checks git status, branch listings (`git branch`, `git branch -a`), and commit history locally without remote SSH probing.
- **Autonomous Router & Dispatch Mocking**: Validates reasoning routers and model tier payloads using mocked transports locally.
- **Autonomous Voice & TTS Mocking**: Validates speech synthesis speed, streaming chunks, updated Edge-TTS libraries, and audio services (`TTSService`) locally with dummy audio bytes and async mocks instead of remote SSH benchmarks.
- **Autonomous Speech-to-Text (STT) Mocking**: Validates speech transcription services (`STTService`), audio decoding, and transcription pipelines locally with dummy audio bytes and async mocks instead of remote SSH benchmarks.
- **Batched Single-Runner Pattern for OS & Browser Automation**: If interacting with an active browser session (Chrome, Safari, cPanel, Colab, Figma via AppleScript/CDP) or remote database is required, the agent writes a single self-contained script (e.g. in workspace or scratch), runs it once, and parses structured JSON output.
- **Zero Global Config Tampering**: Agents never touch files outside the workspace root.

---

### 🛡️ Developer Guide: Granting Full Access Without Dialogs

If you prefer to give your agent full unattended power without confirmation prompts:

#### 1. Google Antigravity
Add prefix grants to your `~/.gemini/config/config.json` under `globalPermissionGrants.allow`:
```json
{
  "globalPermissionGrants": {
    "allow": [
      "command(git)",
      "command(pnpm)",
      "command(npm)",
      "command(python3)",
      "command(node)",
      "command(ssh)",
      "command(docker)",
      "command(curl)",
      "command(osascript)",
      "unsandboxed(python3)",
      "unsandboxed(bash)",
      "unsandboxed(osascript)",
      "unsandboxed(ssh)",
      "unsandboxed(docker)",
      "unsandboxed(curl)"
    ]
  }
}
```

#### 2. Claude Code
In your project or user configuration, enable auto-approved commands or run in non-interactive batch mode:
```json
{
  "allowedCommands": [
    "git *",
    "pnpm *",
    "npm *",
    "python3 *",
    "pytest *",
    "node *"
  ]
}
```

#### 3. Cursor
In `.cursorrules` or `.cursor/rules/discovery.mdc`, instruct the agent to run strictly within the workspace environment and follow the single-runner batch pattern.

---

## 🧠 The 7 Core Enforcements

1. **Project Discovery Before Execution**: Mandatory phased scan of directory layout, READMEs, architecture files, dependency lockfiles, environments, CI/CD, tests, and commit history.
2. **Git Understanding**: Inspection of branch, working tree diffs, unstaged changes, and recent team commit conventions.
3. **Mental Model Creation**: Full comprehension of project purpose, architecture, core modules, data flow, build/deployment pipelines, and test strategies before code editing.
4. **Strict Question Policy**: Ban on helpless questions. Exhaust codebase search first; only ask when information does not exist, an action is destructive, or an architectural fork needs human business judgment.
5. **Engineering Behavior**: Strict preference for minimal atomic diffs, existing idioms, backward compatibility, and reversible changes; active rejection of duplicate systems and unnecessary rewrites.
6. **First Response Protocol**: Uniform onboarding response on turn 1 (`Understanding`, `Current State`, `Plan`, `Blocking Questions`).
7. **Completion Report Protocol**: Uniform delivery summary (`STATUS`, `CHANGES`, `VALIDATION`, `DEPLOYMENT`, `REMAINING`).

---

## 🤖 Supported AI Agents & Integration Guides

This skill is runtime-agnostic and works with any modern LLM-driven coding agent.

### 1. Claude Code
Install globally or per repository:
```bash
# Repository-level setup
mkdir -p .claude/skills
cp SKILL.md .claude/skills/project-discovery.md
```
Or add the reference to your project's `CLAUDE.md`:
```markdown
# Instructions for Claude Code
Follow the discovery protocols outlined in templates/AGENTS.md before writing any code.
```

### 2. Google Antigravity
Copy into your Antigravity skills configuration directory:
```bash
mkdir -p ~/.gemini/config/skills/agent-project-discovery-skill
cp SKILL.md ~/.gemini/config/skills/agent-project-discovery-skill/SKILL.md
```

### 3. Cursor
Add to `.cursorrules` or create `.cursor/rules/discovery.mdc`:
```markdown
---
description: Universal project discovery protocol for AI agents
globs: *
alwaysApply: true
---

Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. OpenAI Codex & Custom LLM Orchestrators (LangChain, CrewAI, AutoGen)
Inject the contents of `SKILL.md` directly into the system prompt or agent tool persona:
```python
with open("SKILL.md", "r") as f:
    skill_prompt = f.read()

agent = Agent(
    role="Senior Staff Software Engineer",
    system_prompt=f"{base_system_prompt}\n\n{skill_prompt}",
    tools=[bash_tool, read_file_tool, search_tool, edit_tool]
)
```

### 5. GitHub Copilot & Copilot Workspace
Include in `.github/copilot-instructions.md`:
```markdown
# Copilot Workspace Instructions
Always execute the discovery phase detailed in `SKILL.md` prior to recommending file modifications or opening Pull Requests.
Format your plan using the Response Protocol (Understanding, Current State, Plan, Blocking Questions).
```

---

## 📂 Repository Structure

```
agent-project-discovery-skill/
├── README.md               # Repository documentation and integration guide
├── SKILL.md                # Core AI skill definition and instruction ruleset
├── LICENSE                 # MIT License
├── CHANGELOG.md            # Version history and release notes
├── examples/               # End-to-end real world walkthroughs
│   ├── software-project.md # Full-stack TypeScript + Go microservices walkthrough
│   ├── research-project.md # Python / PyTorch machine learning pipeline walkthrough
│   └── business-project.md # Enterprise billing / Stripe / automation workflow walkthrough
└── templates/
    └── AGENTS.md           # Turnkey template to drop into your repo root
```

---

## 📖 Real-World Examples

Check the [`examples/`](examples/) directory to see the discovery protocol in action:

- [**Full-Stack Software Project**](examples/software-project.md): How an agent detects Go microservices, existing Redis connection pools, monorepo structure, and preserves user uncommitted code while implementing rate limiting.
- [**Machine Learning & Research Project**](examples/research-project.md): How an agent inspects PyTorch configurations, preserves active GPU checkpoint weights, avoids breaking numerical stability, and verifies tensor dimensions.
- [**Business Automation Project**](examples/business-project.md): How an agent safely navigates Stripe webhooks, preserves idempotency invariants, enforces zero PII leakage, and runs local mock tests.

---

## 🚀 Quickstart: Bootstrap Your Own Repo in 30 Seconds

1. Copy [`templates/AGENTS.md`](templates/AGENTS.md) into the root of your project:
   ```bash
   curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
   ```
2. (Optional) Customize the bottom section in `AGENTS.md` with your repository's specific package manager, test command, and lint commands.
3. Your AI agent will automatically detect and respect this protocol upon entering your repository!

---

## 🤝 Contributing

Contributions are welcome from the open-source and AI engineering community!

1. Fork the repository.
2. Create a topic branch: `git checkout -b feature/new-agent-integration`.
3. Add or update improvements to `SKILL.md`, `templates/`, or `examples/`.
4. Commit your changes adhering to [Conventional Commits](https://www.conventionalcommits.org/).
5. Submit a Pull Request.

---

## 🔗 Related Projects

Part of the **Molavi AI Engineering Ecosystem**:

* [**mcp-agent-skills-hub**](https://github.com/tmolavi/mcp-agent-skills-hub): Curated production agent skills and MCP configurations.
* [**lean-agent-skills**](https://github.com/tmolavi/lean-agent-skills): Token-efficient, context-compressed skills for coding agents.
* [**n8n-agent-skills**](https://github.com/tmolavi/n8n-agent-skills): Production n8n agent workflow architecture.
* [**geo-scope**](https://github.com/tmolavi/geo-scope): Multi-model empirical AI visibility benchmark engine.
* [**Ecosystem Map**](https://github.com/tmolavi/geo-scope/blob/main/docs/GITHUB_ECOSYSTEM.md): Complete architecture and evidence flow.

---

## 👤 Author & License

Developed by **Taghi Molavi** — [molavi.pro](https://molavi.pro)  
Distributed under the [MIT License](LICENSE). Open-source and free for personal, commercial, and enterprise use.

