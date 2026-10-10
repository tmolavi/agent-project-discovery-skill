# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.25.0] - 2026-10-10

### Added
- **The 34th Forbidden Trap (Remote Microservice Exhaustive Skill Enumeration)**: Strictly forbidden asking `Allow listing all Hermes skills?` or `Allow listing all <service> skills?` and firing remote SSH commands (`docker exec ... urllib.request.urlopen(...) ... names = [...]`) to parse or print skill catalogs on remote servers.
- **Autonomous Static Skill Catalog Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must discover complete skill catalogs, tool definitions, and microservice capabilities statically from local workspace manifests (`hermes-skill-discovery-registry-v1.json`, `isolated_hermes/`, `hermes_skills/`) without remote SSH skill enumeration scripts or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.25.0`.

## [1.24.0] - 2026-10-10

### Added
- **The 33rd Forbidden Trap (Ad-hoc Live Container Asset Deployment & In-Place Mutation)**: Strictly forbidden asking `Allow deploying assets to container and restarting?` or `Allow deploying <assets> to container and restarting?` and firing chained SSH commands (`tar -xzf ... && docker cp ... && docker restart ... && curl ...`) to hot-patch running containers or restart services mid-task.
- **Autonomous Atomic Deployment Mandate ("خودش تصمیم بگیره")**: Mandated that agents must restrict production releases strictly to canonical deployment scripts (`deploy.sh`) executed atomically without intermediate confirmation prompts for unpacking, copying files into containers, restarting, or curling health endpoints.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.24.0`.

## [1.23.0] - 2026-10-10

### Added
- **The 32nd Forbidden Trap (Cross-Container Internal Service API & Skill Probing)**: Strictly forbidden asking `Allow inspecting Hermes skills from hamzad-ara?` or `Allow inspecting <service> skills from <container>?` and firing remote SSH commands (`docker exec <container> python3 -c '... urllib.request.urlopen("http://<service>:...") ...'`) to query internal microservice endpoints across containers.
- **Autonomous Cross-Container Discovery & Mocking Mandate ("خودش تصمیم بگیره")**: Mandated that agents must discover internal microservice network topology, skill registries, and APIs statically from local workspace manifests (`docker-compose.yml`, `hermes-skill-discovery-registry-v1.json`, `isolated_hermes/`) and mock inter-service endpoints locally without remote SSH cross-container inspection commands or modal confirmation prompts.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.23.0`.

## [1.22.0] - 2026-10-10

### Added
- **The 31st Forbidden Trap (Ad-hoc SCP Build Asset & Archive Uploading)**: Strictly forbidden asking `Allow uploading build assets archive?` or `Allow uploading <archive / build assets> to server?` and firing ad-hoc `scp` commands (`scp ... /tmp/*.tar.gz hamzad_server:/tmp/...`) to upload build tarballs or bundle archives to production server hosts.
- **Autonomous Release Workflow & Anti-SCP Archive Upload Mandate ("خودش تصمیم بگیره")**: Mandated that agents must verify build outputs locally (`npm run build`) and restrict artifact deployments strictly to canonical, planned release workflows (`deploy.sh`) without speculative ad-hoc SCP archive uploads or modal confirmation prompts.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.22.0`.

## [1.21.0] - 2026-10-10

### Added
- **The 30th Forbidden Trap (Remote Container Listing & Status Probing)**: Strictly forbidden asking `Allow listing containers on hamzad_server?` or `Allow listing containers on <server>?` and firing remote SSH commands (`ssh ... "docker ps --format 'table ...'"` or `docker ps`) to query active containers, status tables, or port mappings on remote server hosts.
- **Autonomous Local Container Topology Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must determine service definitions, container names, exposed ports, and network bindings statically from local repository manifests (`docker-compose.yml`, `compose.yaml`, `Dockerfile`), without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.21.0`.

## [1.20.0] - 2026-10-10

### Added
- **The 29th Forbidden Trap (Remote Docker Image & Tag Probing)**: Strictly forbidden asking `Allow checking docker images on server?` or `Allow checking <docker images / tags> on server?` and firing remote SSH commands (`ssh ... "docker images | grep -E '...'"` or `docker images`) to list, inspect, or filter images on remote server hosts.
- **Autonomous Local Docker Image & Tag Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must determine Docker image tags, repository names, base images (e.g. `node:18-alpine`, `python:3.11-slim`), and build contexts statically from local repository manifests (`docker-compose.yml`, `Dockerfile`, CI pipelines), or build/inspect images locally in the workspace without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.20.0`.

## [1.19.0] - 2026-10-10

### Added
- **The 28th Forbidden Trap (Remote Host Runtime & Binary Version Probing)**: Strictly forbidden asking `Allow checking node on server host?` or `Allow checking <runtime / binary> on server host?` and firing remote SSH commands (`ssh ... "node -v || true"`, `python3 -v`, `pnpm -v`) to check host binaries or environment versions.
- **Autonomous Local Host Runtime Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must determine Node.js, Python, or package manager constraints statically from local repository manifests (`package.json` `engines`, `.nvmrc`, `.node-version`, `Dockerfile`, `docker-compose.yml`) and verify runtimes locally within the workspace without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.19.0`.

## [1.18.0] - 2026-10-10

### Added
- **The 23rd Forbidden Trap (Remote SSH Connection Retries, Uptime & Echo Liveness Probing)**: Strictly forbidden asking `Allow retrying SSH connection?` or `Allow testing SSH to hamzad_server?` and firing `ssh -o ConnectTimeout=... hamzad_server "uptime"` or `echo 'connection test ok'`.
- **The 24th Forbidden Trap (Remote Server Container & Git Status Compound Probing)**: Strictly forbidden asking `Allow checking server molavi-pro container and git?` and firing chained SSH commands (`ssh ... "docker ps ... && cd /opt/projects/... && git status -s"`).
- **The 25th Forbidden Trap (Remote Service Internal API & Skill Probing)**: Strictly forbidden asking `Allow listing Hermes skills?` and firing remote SSH commands (`ssh ... "docker exec ... python3 -c '... httpx.get(\"http://127.0.0.1:8090/api/v1/skills\") ...'"`).
- **The 26th Forbidden Trap (Remote Container Build Output & .next Directory Probing)**: Strictly forbidden asking `Allow inspecting container .next directory?` and firing remote SSH commands (`ssh ... "docker exec molavi-pro-web ls -la /app/.next"`).
- **The 27th Forbidden Trap (Ad-hoc SCP Component & File Copying to Server)**: Strictly forbidden asking `Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, or `Allow copying robots.ts to server?` and firing ad-hoc `scp` uploads mid-task.
- **Autonomous Resolution Mandates ("خودش تصمیم بگیره")**: Mandated autonomous SSH connectivity fallbacks, static container and local git separation, local registry skill discovery, local `.next` build generation/verification, and strict git-commit/deploy script workflows.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.18.0`.

## [1.17.0] - 2026-10-10

### Added
- **The 18th Forbidden Trap (Remote Source Code & Frontend Component Probing)**: Strictly forbidden asking `Allow checking server MobileMenu.tsx?` or executing remote SSH commands (`ssh ... "cat ... components/MobileMenu.tsx"`) to view UI components or source code on remote servers.
- **The 19th Forbidden Trap (Remote STT Provider & API Key Probing)**: Strictly forbidden asking `Allow checking STT providers?` or `Allow testing Groq Whisper STT?` and executing remote SSH commands (`docker exec ... python3 -c '... test_stt_providers() ... GROQ_API_KEY ... WHISPER_URL ...'`) to probe provider configurations, API keys, or live STT APIs.
- **The 20th Forbidden Trap (Unprompted SCP Deployments & Remote Container Restarts)**: Strictly forbidden asking `Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`, or `Allow deploying hermes_router and restarting container?` and executing ad-hoc `scp` uploads or `ssh ... "docker restart ..."` mid-task without explicit user directive.
- **The 21st Forbidden Trap (Remote Benchmark Suite & Live Evaluation Execution)**: Strictly forbidden asking `Allow running 20-utterance Persian evaluation suite?` or `Allow running full 20-utterance benchmark?` and running remote SSH/SCP evaluation scripts (`scp ... test_20_persian_utterances.py ... && ssh ... "docker exec hamzad-ara python3 /app/test_20_persian_utterances.py"`).
- **The 22nd Forbidden Trap (Remote Health Endpoints, Container Logs, Shell History & Build Artifact Probing)**: Strictly forbidden asking `Allow checking ARA health endpoint?`, `Allow checking hamzad-ara container logs?`, `Allow checking server command history?`, `Allow checking .next on server host?`, or `Allow checking molavi-pro container on server?` and executing remote SSH `curl -s .../api/health`, `docker logs ... --tail`, `history | tail`, `ls -la .../.next`, or `docker ps --filter name=...`.
- **Autonomous Local Resolution Mandates ("خودش تصمیم بگیره")**: Mandated that agents must autonomously inspect local components, mock STT providers locally, prepare deployments without ad-hoc SCP/restarts, run benchmarks locally against test doubles, and diagnose health/logs/history from local code and logs without remote SSH probing or confirmation modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.17.0`.

## [1.16.0] - 2026-10-10

### Added
- **The 17th Forbidden Trap (Remote Speech-to-Text (STT) & Audio Transcription Pipeline Probing)**: Strictly forbidden asking `Allow testing STT pipeline?` or executing remote SSH commands (`docker exec ... python3 -c '... STTService.transcribe_audio_bytes(...) ...'`) to benchmark speech-to-text transcription, decode audio chunks, or probe live audio transcription pipelines on remote servers.
- **Autonomous Local Speech-to-Text (STT) Verification Mandate ("خودش تصمیم بگیره")**: Mandated that agents must autonomously validate speech-to-text services (`STTService`), transcription functions (`transcribe_audio_bytes`), audio chunk decoding, and transcript formatting locally using mocked async functions (`unittest.mock.AsyncMock`) and dummy audio byte payloads without remote SSH execution or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.16.0`.

## [1.15.0] - 2026-10-10

### Added
- **The 16th Forbidden Trap (Remote Deployment Manifest & Configuration Probing)**: Strictly forbidden asking `Allow viewing server docker-compose.yml?` or executing remote SSH commands (`ssh ... "cat /opt/.../docker-compose.yml"`, `head`, `less`, `more`) to read deployment configurations, compose definitions, Dockerfiles, or environment setups on remote servers.
- **Autonomous Local Deployment Manifest Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must inspect `docker-compose.yml`, service configurations, Dockerfiles, and environment files (`.env.example`) directly within the local workspace repository without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.15.0`.

## [1.14.0] - 2026-10-10

### Added
- **Expanded Forbidden Trap 11 (Remote Voice / TTS Synthesis & Testing Updated Edge-TTS)**: Strictly forbidden asking `Allow testing updated Edge-TTS?` or `Allow testing TTS synthesis speed?` and executing remote SSH commands (`docker exec ... python3 -c '... TTSService.synthesize_chunk(...) ...'`) to benchmark speech synthesis latency, test updated Edge-TTS library behaviors, or probe live audio pipelines on remote servers.
- **Autonomous Local Voice & TTS Verification Mandate ("خودش تصمیم بگیره")**: Mandated that agents must autonomously validate speech synthesis speed, streaming audio chunks, updated Edge-TTS libraries, and audio services (`TTSService`) locally using mocked async functions (`unittest.mock.AsyncMock`) and dummy audio chunk byte payloads without remote SSH execution or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.14.0`.

## [1.13.0] - 2026-10-10

### Added
- **Expanded Forbidden Trap 13 (Remote Server Git Branch Listing)**: Strictly forbidden asking `Allow listing git branches on server?` or executing compound remote SSH commands (e.g. `ssh ... "cd /opt/... && git branch -a"`, `git branch -r`) to list or probe git branches on remote deployment hosts.
- **Autonomous Local Git Branch Inspection Mandate ("خودش تصمیم بگیره")**: Mandated that agents must autonomously inspect git branches (`git branch`, `git branch -a`, `git branch -r`) directly within the local workspace repository without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.13.0`.

## [1.12.0] - 2026-10-10

### Added
- **The 15th Forbidden Trap (Remote Container Filesystem & Directory Probing)**: Strictly forbidden asking `Allow checking container contents?` or executing remote SSH commands (`docker exec ... ls`, `find /app`, `cat /app/...`) to inspect directory hierarchies, application files, or container filesystems.
- **Autonomous Local Container Filesystem & Directory Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must inspect repository folder structures, directory hierarchies, `Dockerfile` directives (WORKDIR, COPY), and `docker-compose.yml` volume mappings directly within the local workspace without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.12.0`.

## [1.11.0] - 2026-10-10

### Added
- **The 14th Forbidden Trap (Remote Package Upgrades & Container Mutation)**: Strictly forbidden asking `Allow upgrading edge-tts?` or executing remote SSH commands (`pip install -U ...`, `npm install -g ...`, `apt-get upgrade`) to mutate installed packages or upgrade libraries on remote servers or live containers.
- **Autonomous Local Dependency Upgrade Mandate ("خودش تصمیم بگیره")**: Mandated that agents must manage and upgrade packages deterministically by editing local workspace manifests (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) and testing compatibility with local test runners without remote SSH mutation or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.11.0`.

## [1.10.0] - 2026-10-10

### Added
- **Expanded Forbidden Trap 13 (Remote Server Git Branch and Log Probing)**: Strictly forbidden asking `Allow checking server git branch and log?` or executing compound remote SSH commands (e.g. `ssh ... "cd /opt/... && git branch --show-current && git log -n 3 --oneline"`) to inspect remote repository branches or commit history.
- **Autonomous Local Git Branch & Commit Log Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must autonomously inspect git branch (`git branch --show-current`), commit history (`git log -n 5`), and working tree status (`git status -s`) directly within the local workspace repository without remote SSH probing or user approval modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.10.0`.

## [1.9.0] - 2026-10-10

### Added
- **The 13th Forbidden Trap (Remote Server Container & Git Status Probing)**: Strictly forbidden asking `Allow checking server container and git status?` or executing compound remote SSH commands (e.g. `ssh ... "docker ps --filter name=... && cd /opt/... && git status -s"`) to inspect running container status or remote git checkouts.
- **Autonomous Local Container & Git Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must inspect container configurations and port mappings statically from local manifests (`docker-compose.yml`, `Dockerfile`, deploy scripts) and verify git status directly within the local workspace (`git status -s`, `git branch`, `git log`) without asking permission or triggering SSH confirmation modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.9.0`.

## [1.8.0] - 2026-10-10

### Added
- **The 12th Forbidden Trap (Remote Package & Dependency Inspection)**: Strictly forbidden asking `Allow checking edge-tts version?` or executing remote SSH commands (`pip show`, `pip list`, `pip freeze`) to inspect installed packages or library versions on remote environments.
- **Autonomous Local Manifest Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must inspect package versions, dependencies, and requirements statically from local repository manifests (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) without asking permission or triggering SSH confirmation modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) to version `v1.8.0`.

## [1.7.0] - 2026-10-10

### Added
- **Continuous Momentum on Unpredicted States ("در حالت‌های پیش‌بینی‌نشده ادامه بده")**: Mandated that agents must never freeze or halt execution mid-task when encountering unexpected circumstances, ambiguous options, or unpredicted errors. The agent must apply safe, reversible engineering defaults and continue progressing through all other doable tasks.
- **Deferred Batch Questioning Protocol ("همه رو آخرش یه جا بپرسه")**: Enforced that all accumulated non-critical questions, ambiguous trade-offs, and edge-case choices must be deferred to the end of the run and presented together in a single consolidated list rather than interrupting the user one-by-one mid-stream.
- **Initial Autonomy Handshake**: Allowed specifying autonomy upfront at the very start of a session instead of repeated mid-task questions.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`).

## [1.6.0] - 2026-10-10

### Added
- **The 11th Forbidden Trap (Remote Voice / TTS Synthesis & Speed Benchmarking)**: Strictly forbidden asking `Allow testing TTS synthesis speed?` or running ad-hoc remote SSH scripts testing speech synthesis latency, chunk streaming, or audio generation pipelines (e.g. `TTSService.synthesize_chunk`).
- **Autonomous Voice & TTS Mocking Mandate ("خودش تصمیم بگیره")**: Agents must autonomously decide verification approaches using local async mocking (`unittest.mock.AsyncMock`) and dummy audio byte payloads (e.g. `b"RIFF..."` or simulated chunk streams), rather than halting execution or triggering remote confirmation modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) with explicit TTS synthesis speed rules.

## [1.5.0] - 2026-10-10

### Added
- **Prohibition of Central Model Dispatch & Reasoning Router Approvals**: Strictly forbidden asking `Allow testing central model dispatch?` or running ad-hoc remote SSH scripts testing central dispatchers/reasoning routers (e.g. `HermesReasoningRouter`, gateway `/api/models/generate`).
- **Autonomous Router Mocking & Reasoning Validation Mandate ("خودش تصمیم بگیره")**: Agents must autonomously decide verification approaches using local mocking (`httpx.MockTransport`, `respx`, `unittest.mock`) and local unit tests, rather than halting execution or triggering remote confirmation modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) with explicit dispatch and reasoning router rules.

## [1.4.0] - 2026-10-10

### Added
- **The 10th Forbidden Trap (Remote Code & Route Inspection via SSH)**: Prohibited agents from prompting the user or firing SSH/docker commands to read codebase files, grep routers, or parse ASTs on remote servers (e.g. `Allow checking model router endpoints? ssh ... "docker exec ... python3 -c 'with open(...) ...'"`).
- **Autonomous Local Code Discovery Mandate ("خودش تصمیم بگیره")**: Mandated that agents must inspect router definitions (`@router.get`, `@router.post`), schemas, and models directly from the local repository workspace without asking permission or triggering SSH security modals.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all localized README files (`README.md`, `README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`) with the new rule.

## [1.3.0] - 2026-10-10

### Added
- **Autonomous Testing Decision Protocol ("Decide By Itself" / خودش تصمیم بگیره)**: Explicitly prohibited agents from popping timid interactive permission prompts to test APIs or endpoints (such as `Allow testing /api/models/generate? ssh root@... "docker exec ..."`).
- **The 9th Forbidden Trap (Timid Test Approvals & Live Endpoint Probing)**: Agents must autonomously decide verification strategy using local unit tests, mocks, test fixtures, or local loopbacks without stalling the user.
- **Strict Anti-Pattern for Live Inference Probing**: Prohibited unsolicited execution of live model generation calls and remote container execution scripts during discovery and verification.
- Updated `SKILL.md`, `templates/AGENTS.md`, and all primary documentation with the autonomous testing mandate.

## [1.2.0] - 2026-09-16

### Added
- **Full Access & Zero-Interruption Guide**: Comprehensive developer setup guide for Antigravity, Claude Code, and Cursor to enable 100% autonomous unattended execution.
- **The 8 Forbidden Modal-Triggering Traps**: Explicitly codified rules prohibiting live public domain curling, fragmented remote SSH calls, obscure Git plumbing diagnostics (`git count-objects`), global IDE config tampering, and chained multi-pipe shell commands.
- **OS Automation & Browser Session Integration**: Single-runner batching pattern for interacting with active browser tabs (cPanel, cloud consoles, Colab) via AppleScript/CDP without causing approval dialog fatigue.
- Updated all localized README files (`README.fa.md`, `README.tr.md`, `README.az.md`, `README.ar.md`, `README.md`) with complete explanations of the sandbox security model and full access permissions.

## [1.1.0] - 2026-09-13

### Added
- Multi-language documentation:
  - Persian (`README.fa.md`)
  - Istanbul Turkish (`README.tr.md`)
  - Azerbaijani Turkish (`README.az.md`)
  - Gulf Arabic (`README.ar.md`)
- Language navigation bar in main `README.md`.
- Strict prohibition of unsolicited remote SSH, port probing, and network health checks during project discovery.
- Autonomous unattended execution guidelines ensuring agents can run long-running tasks overnight without halting on confirmation prompts.

## [1.0.0] - 2026-09-12

### Added
- Initial public release of `agent-project-discovery-skill`.
- Universal `SKILL.md` defining discovery protocol, git comprehension, mental model creation, strict question policy, senior engineering heuristics, structured response format, and completion reports.
- `templates/AGENTS.md` project context template for repository root bootstrapping.
- `examples/software-project.md`: Full-stack TypeScript/Next.js and Go microservices discovery walkthrough.
- `examples/research-project.md`: Python ML / data science pipeline repository discovery walkthrough.
- `examples/business-project.md`: Enterprise workflow automation, CRM, and internal ops tool repository discovery walkthrough.
- Comprehensive `README.md` with multi-agent setup guides (Claude Code, Antigravity, Cursor, OpenAI Codex / Operator, GitHub Copilot Workspace).
