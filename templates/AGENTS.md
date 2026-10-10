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
- ❌ *"Allow checking edge-tts version?"* (or asking permission to run `pip show`, `pip list`, `pip freeze` via SSH).
- ❌ *"Allow upgrading edge-tts?"* (or asking permission to run `pip install -U`, `npm update`, `pip install --upgrade` via SSH).
- ❌ *"Allow checking container contents?"* (or asking permission to run `docker exec ... ls`, `find`, `cat` via SSH).
- ❌ *"Allow checking server container and git status?"* (e.g., asking permission to run `ssh ... "docker ps ... && git status -s"`).
- ❌ *"Allow checking server git branch and log?"* (e.g., asking permission to run `ssh ... "git branch --show-current && git log ..."`).
- ❌ *"Allow listing git branches on server?"* (e.g., asking permission to run `ssh ... "git branch -a"`).
- ❌ *"Should I run this test on the remote server?"*

**Instead — Decide Autonomously ("خودش تصمیم بگیره"):**
- Search the codebase using grep, symbol search, or directory listing.
- Inspect local route definitions, controllers, schemas, and models in the workspace directly instead of attempting remote SSH inspection.
- Infer conventions from existing implementations and commit history.
- Read existing unit/integration tests for usage patterns.
- Autonomously verify model routers, dispatch logic, and payload generation using local mocks (`httpx.MockTransport`, `respx`, `unittest.mock`) without asking for human permission.
- Autonomously verify speech synthesis, audio streaming, updated Edge-TTS libraries, and TTS services (`TTSService`) using local async mocks (`unittest.mock.AsyncMock`) and dummy audio chunk bytes without asking permission or triggering remote SSH benchmarks.
- Autonomously inspect installed package versions, CLI tools, and library requirements from local manifests (`requirements.txt`, `poetry.lock`, `pyproject.toml`, `package.json`, `Dockerfile`) without firing remote `pip show` commands or asking permission.
- Autonomously manage dependency upgrades by updating local manifests (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) and testing compatibility locally without firing remote SSH `pip install -U` commands or asking permission.
- Autonomously discover container configurations, service definitions, and deployment port bindings from local files (`docker-compose.yml`, `Dockerfile`), and inspect git branch (`git branch --show-current`), branch listings (`git branch`, `git branch -a`), commit history, and working tree status locally (`git status -s`, `git log`) without SSH probing or asking permission.
- Autonomously discover container filesystem layouts and directory structures by inspecting local repository files, `Dockerfile` (WORKDIR, COPY directives), and `docker-compose.yml` (volume mounts) without executing remote container directory probing (`docker exec ... ls`) or asking permission.

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
- **Zero Timid Test Prompts ("Decide By Yourself")**: NEVER prompt the user with interactive confirmation questions to test an endpoint, inspect router decorators, test central model dispatch, test TTS synthesis speed, test updated Edge-TTS, check package versions, upgrade packages, check container contents, check server container, git branch, or git log, or list remote branches (e.g. `Allow testing /api/models/generate?`, `Allow checking edge-tts version?`, `Allow upgrading edge-tts?`, `Allow testing updated Edge-TTS?`, `Allow checking container contents?`, `Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`). Decide autonomously to inspect and test locally with mocks or test suites.
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
