# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
