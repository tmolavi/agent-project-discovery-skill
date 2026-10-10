# AGENTS.md — AI Agent Guidance & Project Discovery Policy

Welcome, AI Agent. Treat this repository as a production environment maintained by senior engineers.
Before proposing changes, executing commands, or asking questions, you **MUST** follow the Discovery Protocol defined below.

---

## 1. Prime Directive

> **"Understand before you change. Inspect before you ask."**
> Act like a senior engineer newly onboarded to this codebase. Do not make assumptions, do not rewrite functional patterns, and do not make changes without establishing your mental model first.

---

## 2. Onboarding & Discovery Checklist

Before generating code or editing any file:
1. **Inspect Repository Layout**: Check directory hierarchy, package definitions, and workspace roots.
2. **Review Documentation**: Read `README.md`, `docs/`, API specifications, and architecture decisions (`ADR`s).
3. **Verify Git State**: Run `git status`, check current branch, inspect `git log -n 5`, and note uncommitted diffs.
4. **Identify Dependencies & Runtimes**: Check lockfiles (`pnpm-lock.yaml`, `package-lock.json`, `poetry.lock`, `Cargo.lock`, `go.sum`).
5. **Inspect Environment & Config**: Check `.env.example`, docker-compose files, CI/CD pipelines (`.github/workflows/`).
6. **Locate Test Suites**: Identify test commands, coverage requirements, and how to verify locally without destructive side effects.

---

## 3. Strict Question Policy

Do **NOT** ask questions such as:
- ❌ *"What should I do next?"*
- ❌ *"Can you provide more files or show me where X is located?"*
- ❌ *"How does the auth system work?"*
- ❌ *"Allow testing <endpoint>?"* (e.g., `Allow testing /api/models/generate?` or asking permission to run SSH/docker test snippets).
- ❌ *"Allow checking model router endpoints?"* (e.g., asking permission to SSH and parse router decorators or code files).
- ❌ *"Allow testing central model dispatch?"* (e.g., asking permission to test reasoning routers or gateways via SSH).
- ❌ *"Allow testing TTS synthesis speed?"* or *"Allow testing updated Edge-TTS?"* (e.g., asking permission to benchmark speech synthesis latency, test updated Edge-TTS, or run remote `TTSService.synthesize_chunk` scripts).
- ❌ *"Allow testing STT pipeline?"* (e.g., asking permission to test speech-to-text transcription, decode audio, or run remote `STTService.transcribe_audio_bytes` scripts).
- ❌ *"Allow checking edge-tts version?"* (or asking permission to run `pip show`, `pip list`, `pip freeze` via SSH).
- ❌ *"Allow upgrading edge-tts?"* (or asking permission to run `pip install -U`, `npm update`, `pip install --upgrade` via SSH).
- ❌ *"Allow checking container contents?"* (or asking permission to run `docker exec ... ls`, `find`, `cat` via SSH).
- ❌ *"Allow checking server container and git status?"* (e.g., asking permission to run `ssh ... "docker ps ... && git status -s"`).
- ❌ *"Allow checking server git branch and log?"* (e.g., asking permission to run `ssh ... "git branch --show-current && git log ..."`).
- ❌ *"Allow listing git branches on server?"* (e.g., asking permission to run `ssh ... "git branch -a"`).
- ❌ *"Allow viewing server docker-compose.yml?"* (or asking permission to run `cat`, `head`, `less` on remote deployment files via SSH).
- ❌ *"Allow checking server MobileMenu.tsx?"* (or asking permission to run `cat`, `head`, `less` on remote frontend components or source files via SSH).
- ❌ *"Allow checking STT providers?"* (e.g., asking permission to inspect provider keys or query `/models` via SSH).
- ❌ *"Allow testing Groq Whisper STT?"* (e.g., asking permission to test transcription endpoints via SSH).
- ❌ *"Allow deploying updated app files to production?"* or *"Allow deploying hermes_router and restarting container?"* (e.g., asking permission to run `scp ...` or `docker restart` via SSH).
- ❌ *"Allow restarting hamzad-ara container?"* (or asking permission to restart containers via SSH).
- ❌ *"Allow checking ARA health endpoint?"* (e.g., asking permission to curl internal health endpoints via SSH).
- ❌ *"Allow running 20-utterance Persian evaluation suite?"* or *"Allow running full 20-utterance benchmark?"* (e.g., asking permission to upload and run remote benchmark suites via SSH).
- ❌ *"Allow checking molavi-pro container on server?"* (e.g., asking permission to run `docker ps --format ...` via SSH).
- ❌ *"Allow checking hamzad-ara container logs?"* (e.g., asking permission to run `docker logs` via SSH).
- ❌ *"Allow checking server command history?"* (e.g., asking permission to run `history | tail` via SSH).
- ❌ *"Allow checking .next on server host?"* (e.g., asking permission to inspect host build folders via SSH).
- ❌ *"Allow retrying SSH connection?"* (e.g., asking permission to retry failed SSH connections or run `uptime` via SSH).
- ❌ *"Allow testing SSH to hamzad_server?"* or *"Allow testing SSH connection?"* (e.g., asking permission to run `echo 'connection test ok'` via SSH).
- ❌ *"Allow checking server molavi-pro container and git?"* (e.g., asking permission to run compound `docker ps && git status` via SSH).
- ❌ *"Allow listing Hermes skills?"* or *"Allow listing <service> skills?"* (e.g., asking permission to query skill endpoints via remote `docker exec`).
- ❌ *"Allow inspecting container .next directory?"* (e.g., asking permission to run `docker exec ... ls -la /app/.next` via SSH).
- ❌ *"Allow copying components to server?"* (e.g., asking permission to copy components via `scp`).
- ❌ *"Allow copying page.tsx and robots.ts to server?"* or *"Allow copying robots.ts to server?"* (e.g., asking permission to copy pages or files via `scp`).
- ❌ *"Allow checking node on server host?"* or *"Allow checking <runtime / binary> on server host?"* (e.g., asking permission to run `ssh ... "node -v || true"` or check host runtimes).
- ❌ *"Allow checking docker images on server?"* or *"Allow checking <docker images / tags> on server?"* (e.g., asking permission to run `ssh ... "docker images | grep ..."`).
- ❌ *"Allow listing containers on hamzad_server?"* or *"Allow listing containers on <server>?"* (e.g., asking permission to run `ssh ... "docker ps --format ..."`).
- ❌ *"Allow uploading build assets archive?"* or *"Allow uploading <archive / build assets> to server?"* (e.g., asking permission to run `scp ... /tmp/...tar.gz ...`).
- ❌ *"Allow inspecting Hermes skills from hamzad-ara?"* or *"Allow inspecting <service> skills from <container>?"* (e.g., asking permission to run `ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`).
- ❌ *"Allow deploying assets to container and restarting?"* or *"Allow deploying <assets> to container and restarting?"* (e.g., asking permission to run `ssh ... "tar -xzf ... && docker cp ... && docker restart ... && curl ..."`).
- ❌ *"Allow listing all Hermes skills?"* or *"Allow listing all <service> skills?"* (e.g., asking permission to run `ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`).
- ❌ *"Should I run this test on the remote server?"*

**Instead — Decide Autonomously ("خودش تصمیم بگیره"):**
- Search the codebase using grep, symbol search, or directory listing.
- Inspect local route definitions, controllers, schemas, and models in the workspace directly instead of attempting remote SSH inspection.
- Infer conventions from existing implementations and commit history.
- Read existing unit/integration tests for usage patterns.
- Autonomously verify model routers, dispatch logic, and payload generation using local mocks (`httpx.MockTransport`, `respx`, `unittest.mock`) without asking for human permission.
- Autonomously verify speech synthesis, audio streaming, updated Edge-TTS libraries, and TTS services (`TTSService`) using local async mocks (`unittest.mock.AsyncMock`) and dummy audio chunk bytes without asking permission or triggering remote SSH benchmarks.
- Autonomously verify speech-to-text transcription, audio chunk decoding, and STT services (`STTService`) using local async mocks (`unittest.mock.AsyncMock`) and dummy audio bytes without asking permission or triggering remote SSH transcription benchmarks.
- Autonomously inspect installed package versions, CLI tools, and library requirements from local manifests (`requirements.txt`, `poetry.lock`, `pyproject.toml`, `package.json`, `Dockerfile`) without firing remote `pip show` commands or asking permission.
- Autonomously manage dependency upgrades by updating local manifests (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) and testing compatibility locally without firing remote SSH `pip install -U` commands or asking permission.
- Autonomously discover container configurations, service definitions, and deployment port bindings from local files (`docker-compose.yml`, `Dockerfile`), and inspect git branch (`git branch --show-current`), branch listings (`git branch`, `git branch -a`), commit history, and working tree status locally (`git status -s`, `git log`) without SSH probing or asking permission.
- Autonomously discover container filesystem layouts and directory structures by inspecting local repository files, `Dockerfile` (WORKDIR, COPY directives), and `docker-compose.yml` (volume mounts) without executing remote container directory probing (`docker exec ... ls`) or asking permission.
- Autonomously discover deployment configurations, service definitions, and compose files (`docker-compose.yml`, `Dockerfile`, `nginx.conf`) from local workspace files directly without executing remote `cat` commands or asking permission.
- Autonomously discover frontend components, UI templates, and application code (`components/MobileMenu.tsx`, `.tsx`, `.jsx`, `.vue`) from local workspace files directly without executing remote `cat` commands or asking permission.
- Autonomously discover STT provider configurations, endpoints, and credentials from local settings (`app/config.py`, `.env.example`) and test integrations locally via mocked HTTP clients without firing remote SSH probes or asking permission.
- Autonomously manage code commits and deployment preparation in the local workspace repository without firing ad-hoc `scp` uploads or container restarts mid-task.
- Autonomously execute benchmark and evaluation suites locally using local fixtures and test doubles without uploading or running evaluation scripts on remote containers.
- Autonomously verify health endpoints, error logs, command history, and build outputs (`.next`) locally within the workspace environment without SSH probing or asking permission.
- Autonomously handle SSH connection drops and latency fallbacks: never ask permission to retry SSH or test reachability via uptime/echo probes; fall back to local offline test runners and mocks.
- Autonomously inspect container architectures and git status from local manifests and local git status without running compound SSH checks.
- Autonomously discover skills and internal microservice APIs from local registry manifests (`hermes-skill-discovery-registry-v1.json`, `isolated_hermes/`) and mock endpoints locally without remote container execution.
- Autonomously verify container build outputs locally using `npm run build` without inspecting container `.next` directories over SSH.
- Autonomously manage components, pages, and SEO files through local version control (`git commit`, `git push`), avoiding ad-hoc SCP commands to server directories.
- Autonomously discover runtime requirements (Node.js versions, Python runtimes) from local repository manifests (`package.json` engines, `.nvmrc`, `Dockerfile`) without firing remote SSH `node -v` probes or asking permission.
- Autonomously inspect Docker images, container image tags, and base images from local repository manifests (`docker-compose.yml`, `Dockerfile`, CI pipelines) without firing remote SSH `docker images` or `grep` commands or asking permission.
- Autonomously discover container services, container names, and port allocations from local repository manifests (`docker-compose.yml`, `Dockerfile`) without firing remote SSH `docker ps` commands or asking permission.
- Autonomously verify build assets locally and restrict server artifact deployments to planned release workflows without firing ad-hoc `scp ... /tmp/*.tar.gz` archive uploads or asking permission.
- Autonomously discover cross-container microservice capabilities and skill endpoints from local manifests without firing remote SSH cross-container inspection commands or asking permission.
- Autonomously manage container releases through planned deployment scripts (`deploy.sh`) without firing ad-hoc chained container hot-patching commands (`tar -xzf ... && docker cp ... && docker restart ...`) or asking permission.
- Autonomously discover complete skill catalogs, tool definitions, and microservice capabilities from local registry manifests (`hermes-skill-discovery-registry-v1.json`, `isolated_hermes/`) without firing remote SSH skill enumeration scripts or asking permission.

**Handling Unpredicted States & Deferring Questions ("در حالت‌های پیش‌بینی‌نشده ادامه بده و همه رو آخرش یه جا بپرس"):**
- **Never Halt Mid-Run**: If an unexpected state, ambiguous parameter, or edge case arises, DO NOT freeze execution.
- **Proceed With All Doable Work**: Implement safe reversible fallbacks, and proceed with all independent subtasks, code changes, and tests.
- **Accumulate Questions**: Queue any non-critical doubts or unpredicted decisions into a pending batch.
- **Consolidated Batch at the End**: Ask all accumulated questions together in a single consolidated turn at the end of the run ("همه رو یه جا بپرسه").

**Only ask questions immediately when:**
1. A genuine destructive blocker exists where information cannot be found in the repository and execution cannot safely proceed.
2. The user requested an ambiguous destructive operation (e.g., database wipe, deprecating public APIs).
3. An architectural decision has multiple mutually exclusive trade-offs with no safe fallback.

---

## 4. Engineering Standards & Behavioral Rules

- **Minimal Diffs**: Make targeted, atomic modifications. Never refactor surrounding untouched code unless explicitly asked.
- **Pattern Matching**: Match the existing paradigm (error handling, logging, naming, formatting, type definitions).
- **Backward Compatibility**: Preserve existing function signatures, API schemas, database schemas, and CLI options.
- **Zero Hallucinated Dependencies**: Do not introduce new third-party dependencies without verifying existing alternatives in the lockfile.
- **Zero Timid Test Prompts ("Decide By Yourself")**: NEVER prompt the user with interactive confirmation questions to test an endpoint, inspect router decorators, test central model dispatch, test TTS synthesis speed, test updated Edge-TTS, test STT pipeline, check STT providers, test Groq Whisper, deploy files via SCP, copy components or pages via SCP, restart containers, check health endpoints, run evaluation suites, check package versions, upgrade packages, check container contents, view server docker-compose.yml, check server MobileMenu.tsx, check container logs, check bash history, check remote .next folder, retry SSH connections, test SSH liveness, check server container and git status compoundly, list Hermes skills, inspect container .next directories, copy components or pages via SCP, check Node or runtimes on server hosts, or check server container, git branch, or git log (e.g. `Allow testing /api/models/generate?`, `Allow checking edge-tts version?`, `Allow upgrading edge-tts?`, `Allow testing updated Edge-TTS?`, `Allow testing STT pipeline?`, `Allow checking STT providers?`, `Allow testing Groq Whisper STT?`, `Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`, `Allow checking ARA health endpoint?`, `Allow running 20-utterance Persian evaluation suite?`, `Allow checking container contents?`, `Allow viewing server docker-compose.yml?`, `Allow checking server MobileMenu.tsx?`, `Allow checking hamzad-ara container logs?`, `Allow checking server command history?`, `Allow checking .next on server host?`, `Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`, `Allow checking server molavi-pro container and git?`, `Allow listing Hermes skills?`, `Allow inspecting container .next directory?`, `Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`, `Allow checking node on server host?`, `Allow checking docker images on server?`, `Allow listing containers on hamzad_server?`, `Allow uploading build assets archive?`, `Allow inspecting Hermes skills from hamzad-ara?`, `Allow deploying assets to container and restarting?`, `Allow listing all Hermes skills?`, `Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`, `Allow checking molavi-pro container on server?`). Decide autonomously to inspect and test locally with mocks or test suites.
- **Zero Remote Host Runtime & Binary Probing via SSH**: NEVER run `ssh` commands (`ssh ... "node -v || true"`, `python3 --version`, `pnpm -v`) to probe host runtimes or installed binaries on remote servers. Determine runtime requirements statically from package manifests (`package.json`, `.nvmrc`, `Dockerfile`) and verify runtimes locally in the workspace.
- **Zero Remote Docker Image & Tag Probing via SSH**: NEVER run `ssh` commands (`ssh ... "docker images"`, `docker images | grep ...`, `docker image ls`) to inspect Docker images, tags, or cached layers on remote servers. Determine image configurations statically from repository manifests (`docker-compose.yml`, `Dockerfile`) and build or inspect images locally in the workspace if Docker is available.
- **Zero Remote Container Listing Probing via SSH**: NEVER run `ssh` commands (`ssh ... "docker ps --format ..."` or `docker ps`) to list running containers, inspect status tables, or query ports on remote servers. Determine container configurations and port mappings statically from repository manifests (`docker-compose.yml`, `Dockerfile`).
- **Zero Ad-hoc SCP Build Asset & Archive Uploading via SSH**: NEVER run exploratory `scp` commands to upload build asset archives, temporary tarballs, or asset bundles (`/tmp/*.tar.gz`) directly to production server hosts. Verify builds locally and use canonical deployment scripts (`deploy.sh`).
- **Zero Remote Cross-Container Service Probing via SSH**: NEVER run `ssh` commands (`docker exec <container> python3 -c '... urllib.request.urlopen("http://<service>:...") ...'`) to query internal APIs across containers. Discover service mesh configurations and skills statically from local manifests (`docker-compose.yml`, `hermes-skill-discovery-registry-v1.json`) and mock endpoints locally.
- **Zero Ad-hoc Container Hot-Patching & Deployment Mutation via SSH**: NEVER run compound `ssh` commands (`tar -xzf ... && docker cp ... && docker restart ... && curl ...`) to hot-swap files or restart containers mid-task. Use canonical release workflows (`deploy.sh`) and verify changes locally.
- **Zero Remote Exhaustive Skill Enumeration via SSH**: NEVER run `ssh` commands (`docker exec ... http://staging-hermes:8090/api/v1/skills ... names = [...]`) to parse or print skill catalogs on remote servers. Discover all skills statically from local manifests (`hermes-skill-discovery-registry-v1.json`).
- **Zero Remote SSH Connection Retries, Uptime & Echo Probing via SSH**: NEVER run `ssh` with retry/keepalive flags (`-o ConnectTimeout=15`, `-o ServerAliveInterval=5`) or run `uptime` and `echo 'connection test ok'` reachability probes. Fall back immediately to local workspace analysis and mocks.
- **Zero Remote Compound Container & Git Status Probing via SSH**: NEVER run compound `ssh` commands (`docker ps ... && cd ... && git status -s`) to inspect running container tables alongside remote git status. Inspect container configurations statically and git status locally in the workspace.
- **Zero Remote Internal Service & Skill Probing via SSH**: NEVER run `docker exec ... httpx.get('.../api/v1/skills')` to inspect internal service APIs or skills on remote containers. Inspect skills and registry files locally in the workspace.
- **Zero Remote Container Build Directory Probing via SSH**: NEVER run `ssh ... docker exec molavi-pro-web ls -la /app/.next` to check build folders inside remote containers. Verify Next.js build outputs locally with `npm run build`.
- **Zero Ad-hoc SCP Component & File Copying to Server**: NEVER run exploratory `scp` commands to copy individual components (`Header.tsx`, `MobileMenu.tsx`), pages (`page.tsx`), or SEO assets (`robots.ts`) directly to production server hosts. Commit code locally and use planned deployment workflows.
- **Zero Remote Source Code & UI Component Probing via SSH**: NEVER run `ssh` commands (`cat /opt/.../components/MobileMenu.tsx`, `head`, `tail`, `less`, `grep`) to read frontend components or source files on remote servers. Inspect all components and source code directly in the local workspace repository.
- **Zero Remote STT Provider & API Key Probing via SSH**: NEVER run `ssh` commands (`docker exec ... python3 -c '... test_stt_providers() ...'`, checking `GROQ_API_KEY`) to test third-party providers or live keys on remote servers. Test integrations locally using mocked HTTP transports (`httpx.MockTransport`).
- **Zero Unprompted SCP Deployments & Container Restarts via SSH**: NEVER run ad-hoc `scp` commands or remote container restarts (`docker restart`) mid-discovery or mid-task. Treat deployments as deliberate actions and verify all changes locally first.
- **Zero Remote Benchmark & Evaluation Execution via SSH**: NEVER upload test scripts via `scp` or execute multi-prompt/multi-utterance evaluation suites (`test_20_persian_utterances.py`) on remote containers unprompted. Run evaluation suites locally with mock models and audio doubles.
- **Zero Remote Health Endpoints, Container Logs & History Probing via SSH**: NEVER run `ssh` commands to curl internal health endpoints (`curl http://127.0.0.1:3050/api/health`), tail container logs (`docker logs --tail`), inspect shell history (`history | tail`), or list host build directories (`ls .next`). Diagnose issues and inspect builds locally within the workspace.
- **Zero Remote Speech-to-Text (STT) Probing via SSH**: NEVER run remote SSH or container commands to benchmark speech-to-text latency or execute live audio transcription (`STTService.transcribe_audio_bytes`) on remote servers unprompted. Validate all STT services locally with async mocks.
- **Zero Remote Deployment Manifest & Compose Probing via SSH**: NEVER run `ssh` commands (`cat /opt/.../docker-compose.yml`, `head`, `tail`, `less`, `grep`) to read deployment configurations or compose files on remote servers. Inspect all deployment manifests and compose files directly in the local workspace repository.
- **Zero Remote Container Filesystem Probing via SSH**: NEVER run `ssh` or remote container commands (`docker exec ... ls -la /app`, `find /app`, `cat /app/...`) to inspect container directory trees. Inspect repository files and folder hierarchies directly in the local workspace.
- **Zero Remote Package Upgrades via SSH**: NEVER run `ssh` or remote container commands (`pip install -U`, `pip install --upgrade`, `npm update`, `apt-get upgrade`) to mutate running packages on remote hosts. Update dependencies deterministically in local manifests and verify locally.
- **Zero Remote Container & Git Probing via SSH**: NEVER run compound `ssh` commands (`docker ps`, `git branch`, `git branch -a`, `git log`, `git status -s` on remote hosts) to check server status or remote checkouts. Understand deployment statically from local files and inspect git status, branches, and commit logs locally in the workspace.
- **Zero Remote Package & Dependency Probing**: NEVER run `ssh` or remote container commands (`pip show`, `pip list`, `pip freeze`, `npm list`) to inspect installed packages on external servers. Inspect all dependencies statically from local repository manifests.
- **Unpredicted States Momentum ("ادامه بده")**: Never freeze mid-task when encountering unexpected edge cases; use safe fallbacks, finish all other work, and batch any remaining questions for the end.
- **Zero Remote Source Code & Route Probing**: NEVER run `ssh` or remote `docker exec` commands to read codebase files or grep router decorators (e.g. `python3 -c "open('/workspace/...')"`). Inspect all routes and models locally from the repository workspace.
- **Zero Remote Voice / TTS Synthesis Benchmarking**: NEVER run remote SSH or container commands to benchmark audio/voice synthesis latency or execute live TTS synthesis (`TTSService.synthesize_chunk`, testing updated Edge-TTS) on remote servers unprompted.
- **Zero Unsolicited Live Model/API Probing**: NEVER run live inference queries (`/api/models/generate`) or execute ad-hoc remote container commands (`ssh ... "docker exec ... python3 -c '...' "`) unprompted.
- **Zero Unsolicited Remote/SSH Probing**: NEVER run `ssh`, `scp`, `rsync`, or remote `docker` commands (`docker ps`, `docker images`, `docker inspect`) on external servers during discovery or development. Understand deployment statically by reading `Dockerfile`, `compose.yaml`, and CI configs.
- **Zero Remote Port Probing**: NEVER run port checks or endpoint pings via SSH (e.g. `ssh server "curl ..."`). Determine port mappings statically from `docker-compose.yml`, `Dockerfile`, and service configs.
- **Zero Remote Git SSH Probing**: NEVER run unsolicited remote Git/SSH authentication probes (e.g. `ssh server "ssh -T git@github.com"`).
- **Zero Live Route Probing**: NEVER run live route crawlers or active HTTP endpoint scanners against public domains (e.g. `curl https://...`). Verify code deterministically via local builds (`npm run build`, `cargo test`, `pytest`) or local loopback servers (`http://127.0.0.1:<port>`).
- **Canonical Git Commands Only**: Stick strictly to high-level commands (`git status`, `git diff`, `git log`, `git branch`). NEVER run obscure repository plumbing (`git count-objects`, `git fsck`).
- **Zero Global Config Tampering**: NEVER attempt to modify global IDE configs, agent permission files (e.g., `config.json`), or files outside the workspace root. All project work must remain strictly self-contained within the repository.
- **Sandbox Discipline**: Run all commands inside the default sandbox without triggering permission confirmation modals unless the user explicitly requested remote operations.
- **Batched Browser & OS Automation**: When interacting with active browser sessions (Chrome, Safari, cPanel, cloud consoles via AppleScript/CDP), NEVER run multiple fragmented inline `osascript -e` or shell one-liners. Always write a self-contained helper script, run it once, and parse structured output cleanly.
- **Batch Remote Operations**: If the user explicitly asks for remote work or remote database queries, combine operations into a unified script instead of firing dozens of individual SSH commands that trigger confirmation prompts.
- **Verification First**: Always run existing lints, typechecks, and tests before and after making changes.

---

## 5. Mandatory First Response Protocol

On your first turn interacting with a new task or upon onboarding to this project, format your response using this structure:

```markdown
## Understanding
[Summary of the repository purpose, architecture, runtime environment, and relevant domain patterns based on your discovery inspection.]

## Current State
[The current git branch, uncommitted working tree changes, active configuration, and relevant code modules related to the task.]

## Plan
[Step-by-step minimal implementation plan, including verification and testing strategy.]

## Blocking Questions
[None — or ONLY genuine blockers that cannot be resolved from codebase inspection.]
```

---

## 6. Completion Report Protocol

When completing a task, output a structured status summary:

```text
STATUS:
PASS | PARTIAL | BLOCKED

CHANGES:
- <file_path_1>: Brief explanation of modification
- <file_path_2>: Brief explanation of modification

VALIDATION:
- <command_or_test_executed>: Result (e.g., `pnpm test` passed with 42 tests)

DEPLOYMENT:
- Clean working tree / branch status / readiness for commit

REMAINING:
- Any known edge cases, technical debt, or optional follow-up items
```

---

## 7. Project Specific Overrides (Fill In For Your Project)

<!-- Customize the details below for your specific codebase -->

- **Primary Language & Runtime**: e.g., TypeScript Node 20 / Go 1.22 / Python 3.12
- **Package Manager**: e.g., `pnpm`, `uv`, `cargo`
- **Build Command**: e.g., `pnpm build`
- **Test Command**: e.g., `pnpm test`
- **Lint / Typecheck Command**: e.g., `pnpm lint && pnpm typecheck`
- **Critical Paths / Protected Areas**: e.g., `src/core/auth`, `migrations/`
