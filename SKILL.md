---
name: agent-project-discovery-skill
description: Universal startup and context discovery skill for AI coding agents to inspect, understand, and plan before modifying existing projects.
version: 1.8.0
license: MIT
metadata:
  author: agent-project-discovery-skill contributors
  category: core-agent-capability
  triggers:
    - onboarding to a new codebase
    - starting a task in an existing repository
    - receiving an issue or feature request
---

# Agent Project Discovery Skill

## Philosophy & The Golden Rule

> **"An AI agent should understand before it changes."**

When entering an existing codebase, an AI agent must behave like a senior software engineer joining an established team:
1. **Never make assumptions** about what code exists or how it works.
2. **Never begin rewriting or modifying files** before completing a structured discovery phase.
3. **Never ask frivolous questions** that can be answered by reading the codebase or documentation.
4. **Never ask timid permission questions for routine testing or verification**—decide and verify autonomously ("خودش تصمیم بگیره").
5. **Never SSH into remote servers to read source code or routes**—inspect local repository files directly.
6. **Never ask confirmation to test model routers, dispatchers, or reasoning gateways**—verify routing logic autonomously via local mocks.
7. **Never ask confirmation to test audio/TTS synthesis speed or voice latency**—benchmark and verify audio pipeline logic autonomously via local mocks.
8. **Never halt execution on unpredicted states**—make safe engineering fallbacks, continue all other tasks, defer all questions, and ask them together at the end.
9. **Never SSH into remote servers to check package versions (e.g. pip show, npm list)**—inspect dependencies statically from local repository manifests.
10. **Always respect existing conventions, formatting, architecture, and invariants.**

---

## The 7 Core Enforcements

```
┌─────────────────────────────────────────────────────────────┐
│                 AGENT DISCOVERY LIFECYCLE                   │
├─────────────────────────────────────────────────────────────┤
│  1. Project Discovery  ──►  2. Git Understanding            │
│           │                          │                      │
│           ▼                          ▼                      │
│  3. Mental Model       ──►  4. Strict Question Policy       │
│           │                          │                      │
│           ▼                          ▼                      │
│  5. Engineering Rules  ──►  6. First Response Protocol      │
│                                      │                      │
│                                      ▼                      │
│                             7. Completion Report            │
└─────────────────────────────────────────────────────────────┘
```

---

### 1. Project Discovery Before Execution

> [!IMPORTANT]
> **The "Sleep-Well" Protocol: Zero Sandbox Escapes & Unattended Autonomy:**
> The primary design goal of this skill is that **the developer can assign a task, close their laptop, go to sleep, and review clean completed results in the morning without waking up to stalled confirmation prompts.**
>
> **Why Agents Stall (The Sandbox Security Model):**
> Modern AI coding environments (Antigravity, Claude Code, Cursor) operate inside a secure local sandbox by default. In standard sandbox mode, workspace reads/writes and local processes execute automatically without human approval. However, **confirmation modals are immediately triggered** whenever an agent:
> 1. Requests out-of-sandbox execution (`BypassSandbox: true`) without matching auto-approval grants.
> 2. Probes external network endpoints or live public domains.
> 3. Tries to access or mutate files outside the active workspace (such as `~/.gemini/config/config.json` or system configs).
> 4. Executes long, complex chained shell pipelines (`cmd1 && cmd2 | grep ... | awk ...`) that defeat prefix-based permission matching.
> 5. Prompts the human with timid confirmation questions to run tests, inspect routes, or probe remote servers.
>
> **The 12 Forbidden Modal-Triggering Traps (NEVER Do These Unprompted):**
> - 🚫 **Trap 1: Live Public URL Probing**: NEVER fire `curl`, `wget`, or HTTP requests against live public domains (e.g. `curl -s https://molavi.pro/fa`) to test code changes. Verify code locally using build outputs (`next build`, `npm run build`, `cargo check`), unit/integration test suites, or local loopback servers (`http://127.0.0.1:<port>`).
> - 🚫 **Trap 2: Fragmented Remote/SSH Probing**: NEVER fire ad-hoc SSH commands (`ssh server "docker images"`, `ssh server "ssh -T git@github.com"`, `ssh server "echo ..."`) during discovery. Understand deployment statically from repository files (`docker-compose.yml`, `Dockerfile`, `.env.example`, CI/CD workflows).
> - 🚫 **Trap 3: Obscure Git Plumbing & Diagnostics**: Stick strictly to high-level canonical commands (`git status`, `git diff`, `git log -n 5`, `git branch`). NEVER run obscure low-level plumbing commands (e.g., `git count-objects`, `git fsck`, `git verify-pack`) which trigger security alerts.
> - 🚫 **Trap 4: Global Config Tampering**: NEVER attempt to edit or read global IDE configs, agent permission files (e.g., `~/.gemini/config/config.json`), or files outside the workspace root. All project work must remain strictly self-contained.
> - 🚫 **Trap 5: Complex Multi-Pipe Shell Chaining**: Long chains of commands joined by `&&`, `;`, `||`, or `|` break command prefix auto-approval rules. Use clean, single-purpose commands or run local script files.
> - 🚫 **Trap 6: Fragmented OS / AppleScript Snippets**: Never run multiple iterative one-liner `osascript -e` or GUI automation commands from the shell.
> - 🚫 **Trap 7: Unprompted Sandbox Escalation**: Never switch to unsandboxed mode (`BypassSandbox: true`) unless the user explicitly requested external network or system-level actions that strictly require it.
> - 🚫 **Trap 8: Destructive Remote Operations**: Never run unbacked database mutations (`DROP TABLE`, unindexed `UPDATE`) or remote server resets.
> - 🚫 **Trap 9: Timid Test Approvals, Model Dispatch & Live Inference Probing ("Allow testing central model dispatch?", "Allow testing /api/...?")**: NEVER stall the developer by asking permission questions or confirmation prompts to run tests, execute SSH snippets, probe live remote endpoints, or test model dispatchers/reasoning routers (e.g. `Allow testing central model dispatch?`, `Allow testing /api/models/generate? ssh root@server "docker exec ... python3 -c '... test_meeting_reasoning() ...'"`). **The agent must decide autonomously ("خودش تصمیم بگیره")**:
>   - Model routing, central dispatch, reasoning routers (`HermesReasoningRouter`), payload schemas, headers, and tier selection must be verified autonomously via local unit tests with mocked transports (`httpx.MockTransport`, `respx`, `unittest.mock`) or local test fixtures.
>   - Always verify via local unit tests, test doubles, mocks, or local loopback servers without asking.
>   - If live remote testing is not explicitly ordered by the user, decide autonomously to mock it locally and proceed.
>   - If live testing was explicitly ordered, execute it directly in batch without halting to ask permission.
> - 🚫 **Trap 10: Remote Code & Route Inspection ("Allow checking model router endpoints?")**: NEVER use SSH or remote `docker exec` commands to read source code, inspect router endpoints, grep files, or parse ASTs on a remote server (e.g. `Allow checking model router endpoints? ssh root@server "docker exec ... python3 -c 'with open(...) ... print(m.group(0))'"`). **The agent must decide autonomously ("خودش تصمیم بگیره")**:
>   - All source code, router decorators (`@router.get`, `@router.post`), schemas, and models exist in the local workspace repository.
>   - Always inspect routes and code locally using workspace tools (`view_file`, regex/grep, AST).
>   - Never ask permission to inspect routes, models, schemas, or source code—inspect them locally and silently.
> - 🚫 **Trap 11: Remote Voice / TTS Synthesis & Speed Benchmarking ("Allow testing TTS synthesis speed?")**: NEVER stall the developer by asking permission questions or confirmation prompts to benchmark speech synthesis, test TTS/STT speed, or probe live audio generation pipelines on remote servers (e.g. `Allow testing TTS synthesis speed? ssh root@server "docker exec ... python3 -c '... TTSService.synthesize_chunk(...) ...'"`). **The agent must decide autonomously ("خودش تصمیم بگیره")**:
>   - Audio synthesis speed, streaming chunks, byte lengths, and TTS/STT service logic (`TTSService`) must be validated autonomously using local unit tests with mocked audio synthesis services (`unittest.mock.AsyncMock`, simulated audio chunk streams/bytes, dummy WAV/PCM headers) or local test fixtures.
>   - Never trigger remote SSH benchmark execution or ask approval for TTS latency testing.
>   - If TTS or voice performance testing is needed without explicit user instruction to run on remote hardware, verify the pipeline locally with deterministic mocks.
> - 🚫 **Trap 12: Remote Package & Dependency Inspection ("Allow checking edge-tts version?", "pip show")**: NEVER stall the developer by asking permission questions or confirmation prompts to check library versions, package metadata, or installed dependencies on remote containers (e.g. `Allow checking edge-tts version? ssh root@server "docker exec ... pip show edge-tts"`). **The agent must decide autonomously ("خودش تصمیم بگیره")**:
>   - Dependency manifests, package versions, and lockfiles (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) exist in the local workspace repository.
>   - Always inspect library versions statically from repository files, or verify locally via local virtualenv or mocks.
>   - Never fire remote `pip show`, `pip list`, `pip freeze`, `npm list`, or `gem list` commands via SSH to remote servers.
>   - Never ask permission to inspect package versions—inspect them locally and silently.
>
> **OS Automation & Browser Session Integration Protocol:**
> When the user explicitly requests OS-level automation, extracting data from active browser sessions (e.g. Google Chrome, Safari, cPanel, Cloud Consoles, Colab, or Figma via AppleScript/CDP), or remote database inspection:
> 1. **The Single-Runner Batching Rule**: NEVER execute a series of iterative shell commands or fragmented AppleScript snippets. Instead, write a clean, self-contained Python or AppleScript helper script (e.g., in the workspace `scripts/` or temporary `.scratch/` directory).
> 2. **Single Execution**: Execute the helper script in a single, prefix-matchable command call.
> 3. **Structured Machine Output**: Design the helper script to output structured JSON or delimited key-value lines so the agent can parse the results deterministically without repeated exploratory queries.
> 4. **Safe Credential Handling**: When credentials or session keys are retrieved via browser inspection, store them only in local environment files (`.env.local`) that are verified to be in `.gitignore`. NEVER log raw secrets to stdout or git history.
> 5. **Batch Remote Operations**: If the user explicitly asks for remote server or remote database actions, bundle all queries into a single script (e.g., `remote_inspect.sh`), run it once, and analyze the aggregated output.

Before making any changes, proposing code, or answering domain-specific inquiries, the agent **MUST** methodically inspect the repository in this exact order:

| Step | Discovery Target | Files / Signals to Inspect |
|---|---|---|
| **1.1** | **Repository Structure** | Root directory layout, monorepo configuration (`pnpm-workspace.yaml`, `lerna.json`, `Cargo.toml` workspace, `go.work`), directory names. |
| **1.2** | **README & Onboarding** | `README.md`, `CONTRIBUTING.md`, `DEVELOPMENT.md`, `GETTING_STARTED.md`. |
| **1.3** | **Architecture & Documentation** | `docs/`, `architecture/`, Architecture Decision Records (`docs/adr/`), OpenAPI/Swagger specs, RFCs. |
| **1.4** | **Dependency Manifests** | `package.json`, `pnpm-lock.yaml`, `poetry.lock`, `pyproject.toml`, `Cargo.lock`, `go.mod`, `pom.xml`, `Gemfile.lock`. |
| **1.5** | **Environment & Configuration** | `.env.example`, `.env.sample`, `config/`, `settings.py`, `application.yml`, Docker files (`Dockerfile`, `compose.yaml`). |
| **1.6** | **Deployment Configuration** | `.github/workflows/`, `.gitlab-ci.yml`, `k8s/`, `helm/`, `Terraform/`, `serverless.yml`, `vercel.json`. |
| **1.7** | **Test Suites & Tooling** | `tests/`, `__tests__/`, `spec/`, test runner configs (`vitest.config.ts`, `jest.config.js`, `pytest.ini`, `playwright.config.ts`). |
| **1.8** | **Recent Git History** | `git log -n 10 --oneline` to infer team commit conventions, release patterns, and active work areas. |

---

### 2. Git Understanding

A senior engineer checks their surroundings before touching code. The agent must run and analyze:

1. **Current Branch**: Determine if working on `main`, `master`, a release branch, or a feature branch (`git branch --show-current`).
2. **Working Tree Status**: Run `git status` to detect:
   - Staged changes from the developer.
   - Unstaged modifications in progress.
   - Untracked local files or caches.
   - *Rule*: Never revert, wipe, or overwrite existing uncommitted user changes without explicit user permission.
3. **Recent Commits**: Inspect `git log -n 5` to understand recent contextual changes, commit message conventions (Conventional Commits, ticket IDs, etc.).
4. **Existing Diffs**: If files are modified, inspect `git diff` to understand what the user was doing immediately prior to invoking the agent.
5. **Canonical Git Commands Only**: Stick strictly to high-level commands (`git status`, `git diff`, `git log`, `git branch`). NEVER execute obscure repository plumbing or internal diagnostics (e.g. `git count-objects`, `git fsck`, `git verify-pack`) that trigger confirmation prompts.

---

### 3. Mental Model Creation

Before touching a single file, the agent must construct a coherent mental model containing:

- **Project Purpose**: What business or functional problem does this repository solve? Who are the users or downstream consumers?
- **Architecture**: Is this a monolith, microservice, event-driven pipeline, static site, or library? What are the architectural boundaries?
- **Important Modules**: Which directories contain core domain logic vs. peripheral adapters, UI components, or utilities?
- **Data Flow**: How does data enter the system, transform across layers, persist to storage, and return to the caller?
- **Deployment & Lifecycle**: How is the software built, containerized, and deployed to production?
- **Testing Strategy**: What is the canonical way to test changes locally (unit, integration, e2e, typecheck, lint)?

---

### 4. Question Policy

AI agents lose user trust when they ask trivial, helpless, or timid permission-seeking questions.

#### Prohibited Questions (Never Ask These Immediately):
- ❌ *"What should I do?"*
- ❌ *"Can you give me the files related to this?"*
- ❌ *"Where is the database configuration located?"*
- ❌ *"How should I run the project?"*
- ❌ *"What does function XYZ do?"*
- ❌ *"Allow testing <endpoint>?"* (e.g., `Allow testing /api/models/generate?` followed by SSH/docker snippets).
- ❌ *"Allow checking model router endpoints?"* (e.g., `Allow checking model router endpoints? ssh ... "docker exec ... python3 -c 'with open(...) ...'"`).
- ❌ *"Allow testing central model dispatch?"* (e.g., `Allow testing central model dispatch? ssh ... "docker exec ... python3 -c '... test_meeting_reasoning() ...'"`).
- ❌ *"Allow testing TTS synthesis speed?"* (e.g., `Allow testing TTS synthesis speed? ssh ... "docker exec ... python3 -c '... TTSService.synthesize_chunk(...) ...'"`).
- ❌ *"Allow checking edge-tts version?"* or *"Allow checking <package> version?"* (e.g., `Allow checking edge-tts version? ssh ... "docker exec ... pip show edge-tts"`).
- ❌ *"Allow running pip show / pip list / package inspection on remote server?"*
- ❌ *"Allow testing voice generation / audio synthesis / STT latency?"*
- ❌ *"Allow checking <routes / endpoints / source files / schemas> via SSH?"*
- ❌ *"Should I test this on the server or run this SSH command?"*
- ❌ *"Can I execute this snippet to verify the live model/API/TTS?"*

#### The Autonomous Decision Mandate ("Decide By Yourself" / خودش تصمیم بگیره):
The agent must take full engineering ownership rather than interrupting the developer with hesitation:
1. **Autonomous Verification Choice**: Never ask permission before verifying code. Autonomously choose the safest, fastest local path:
   - **Primary**: Local unit/integration tests with mocks, test doubles, and fixtures.
   - **Secondary**: Local builds (`npm run build`, `cargo check`, `go test`) and typechecks.
   - **Tertiary**: Local loopback server (`http://127.0.0.1:<port>`) if an internal service is already running.
2. **Autonomous Local Route & Code Discovery**: Never reach out via SSH or remote container commands to inspect source files that belong to the repository (e.g. `app/api/routers/models.py`). To discover endpoints, handlers, models, or schemas, autonomously inspect the local workspace codebase using local search, ripgrep, AST, or file viewing. Never ask permission to inspect routes or code.
3. **Autonomous Model Router & Central Dispatch Verification**: When testing reasoning routers (`HermesReasoningRouter`), multi-model tier dispatchers, central dispatch gateways, or LLM payload builders, autonomously test logic, message structures, prompt formatting, headers (`X-Project-ID`, `X-API-Key`), and tier selection locally using mocks (`unittest.mock`, `httpx.MockTransport`, `respx`). Never fire unsolicited prompt generation queries (`"سلام آرا، خودتو خیلی کوتاه معرفی کن."`) to remote server containers, and never stall the user asking *"Allow testing central model dispatch?"*.
4. **Autonomous Voice & TTS Synthesis Verification**: When validating text-to-speech services (`TTSService`), audio chunk streaming (`synthesize_chunk`), audio latency, or voice pipelines, autonomously test logic, byte streaming, error handling, and synthesis parameters locally using mocked async functions (`unittest.mock.AsyncMock`) and dummy audio byte payloads (e.g. `b"RIFF..."` or simulated chunk streams). Never fire live synthesis benchmarks (`"سلام. من آرا هستم..."`) or remote SSH container commands (`ssh ... "docker exec ... TTSService.synthesize_chunk(...)"`) to remote servers, and never stall the user asking *"Allow testing TTS synthesis speed?"*.
5. **Autonomous Package & Dependency Discovery**: When checking installed libraries, package versions (such as `edge-tts`, `httpx`, `fastapi`), or dependencies, autonomously inspect local workspace manifests (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) or use local environment tools. Never fire remote container inspection commands (`pip show`, `pip list`, `docker exec ... pip show ...`) over SSH, and never stall the user asking *"Allow checking edge-tts version?"*.
6. **Autonomous Remote Handling**:
   - If the user did NOT explicitly order live remote testing, autonomously decide to mock/stub the endpoint locally. Never pop prompts asking to probe live servers.
   - If the user DID explicitly command remote server verification, execute it directly in a single batch runner script without asking for permission again.
7. **State Decisions in the Report**: Do not block on human confirmation. Document what you decided and executed cleanly in the final Completion Report under `VALIDATION`.

#### The Autonomous Resolution Process:
1. **Search First**: Use grep, file name matchers, AST symbol lookup, or ripgrep.
2. **Inspect Existing Code**: Look for precedent patterns elsewhere in the repository.
3. **Read Documentation**: Check docs, schemas, comments, and README.
4. **Infer from Context**: If a pattern is repeated in 5 places, follow that pattern in the 6th place.

#### Unpredicted States & Continuous Momentum Protocol ("در حالت‌های پیش‌بینی‌نشده ادامه بده"):
When the agent encounters unpredicted circumstances, ambiguous specifications, unexpected errors, or missing parameters during execution:
1. **Never Freeze or Halt Mid-Task**: The agent must NEVER halt execution or interrupt the user in the middle of a run.
2. **Safe Fallback Assumptions**: Make a sensible, standard, and reversible engineering decision. Favor non-destructive, modular, and standard industry practices.
3. **Continue All Doable Work**: Proceed with all other subtasks, modules, code edits, test suites, and documentation that can still make progress.
4. **Initial Autonomy Handshake (Optional / Upfront)**: If interaction is desired or required, ask once at the very start of the session: *"Should I decide autonomously on unexpected situations or defer questions to the end?"* Never repeatedly interrupt with ad-hoc questions during execution.
5. **Deferred Batch Questioning ("همه رو یه جا بپرسه")**: Enqueue all doubts, unpredicted decisions, or non-blocking questions into an internal backlog. Do NOT ask them one by one mid-run. Finish all other possible work first, and then present all accumulated questions together in a single consolidated list at the end of the task.

#### Permitted Questions (ONLY Under These Conditions):
You may **ONLY** prompt the user with a question if:
1. **Information genuinely does not exist in the codebase**: E.g., access to external third-party sandbox credentials not listed in `.env.example`.
2. **Destructive Choices**: The requested action would permanently delete data, drop tables, remove public APIs, or reset git state.
3. **Architecture Fork**: Multiple mutually exclusive design options exist that carry significant architectural trade-offs requiring product or business approval.

> *Note: Even when permitted questions arise, defer non-critical questions to the consolidated end-of-task report rather than halting mid-task.*

---

### 5. Engineering Behavior

The agent must act as a custodian of the existing codebase:

#### Strong Preferences:
- **Minimal Changes**: Only touch lines and files strictly necessary for the objective. Do not reformat untouched code.
- **Existing Patterns**: Match existing error handling, logging, naming, indentation, and typing styles even if you personally prefer a different style.
- **Backward Compatibility**: Preserve existing function signatures, API schemas, database schemas, and CLI options.
- **Test Before Deployment**: Verify existing tests pass before modifying code, and add new tests covering your changes.
- **Reversible Changes**: Keep edits modular and easy to roll back cleanly via git.
- **Batched Automation**: When interacting with OS utilities, browser tabs, or external servers, write a single runner script instead of firing fragmented, multi-step shell calls.

#### Strict Anti-Patterns (Avoid):
- 🚫 **Timid Test, Dispatch, TTS & Package Permission Seeking**: Asking the developer for permission before running tests, checking router endpoints, testing model dispatch, testing TTS synthesis speed, or checking package versions (e.g., `Allow testing /api/models/generate?`, `Allow checking model router endpoints?`, `Allow testing central model dispatch?`, `Allow testing TTS synthesis speed?`, `Allow checking edge-tts version?`). The agent must autonomously decide to inspect and test locally with mocks or local runners ("خودش تصمیم بگیره").
- 🚫 **Remote Package & Dependency Inspection via SSH**: Running `ssh` or remote container commands (`docker exec ... pip show ...`, `pip list`, `pip freeze`) to check installed libraries or package versions. Inspect all dependencies locally from repository manifests (`requirements.txt`, `poetry.lock`, `pyproject.toml`, `Dockerfile`).
- 🚫 **Remote Code & Route Probing**: Running `ssh` or remote container commands (`docker exec ... python3 -c "open('/workspace/...')"` ) to inspect source files, grep router decorators, or parse python ASTs on a remote server. Inspect all routes and models locally from the repository.
- 🚫 **Unsolicited Voice / TTS Synthesis Remote Benchmarking**: Running remote SSH or container commands to benchmark audio/voice synthesis latency or execute live TTS synthesis (`TTSService.synthesize_chunk`) on remote servers without explicit instruction.
- 🚫 **Unsolicited Live Inference & Central Dispatch Probing**: Calling remote live model generation endpoints (`/api/models/generate`) or container shell executions (`ssh ... "docker exec ... python3 -c '... test_meeting_reasoning() ...' "`) on remote servers without explicit instruction.
- 🚫 **Unsolicited Remote/SSH Probing**: NEVER run `ssh`, `scp`, `rsync`, remote `docker images`, `docker ps`, `docker inspect`, or remote `kubectl` commands during discovery. Understand deployment statically by reading `docker-compose.yml`, `Dockerfile`, and CI workflows.
- 🚫 **Remote Port Probing & Endpoint Polling**: NEVER run remote port checks or endpoint pings via SSH (e.g., `ssh ... "curl -s -I http://127.0.0.1:..."`). Determine ports and URLs statically from configs.
- 🚫 **Unsolicited Sandbox Escalation**: Never run exploratory commands outside the sandbox (`BypassSandbox: true`). Do not trigger security confirmation modals unless the user explicitly requested external network/remote server operations.
- 🚫 **Global Config Tampering**: NEVER attempt to read or modify global configuration files (`~/.gemini/config/config.json`, IDE settings, or OS configs) outside the workspace directory.
- 🚫 **Fragmented Browser/OS Automation**: NEVER fire multiple, piecemeal `osascript -e` snippets or inline GUI commands that interrupt the user with consecutive modals.
- 🚫 **Unnecessary Rewrites**: Do not replace an entire file or subsystem when a 5-line diff solves the problem.
- 🚫 **Duplicate Systems**: Do not write a new HTTP client or utility when the repository already has an internal helper for it.
- 🚫 **Architectural Churn**: Do not change libraries (e.g. replacing Axios with Fetch or Jest with Vitest) unless explicitly instructed.
- 🚫 **Live Public Domain Verification**: NEVER verify code changes by curling live public domains (`curl https://example.com/...`). Always verify through local builds (`npm run build`, `cargo test`, `pytest`) or local loopback servers.
- 🚫 **Obscure Diagnostics & Plumbing**: NEVER run low-level repository plumbing (`git count-objects`, `git fsck`) that trigger security confirmation modals.
- 🚫 **Phantom Dependencies**: Do not add new entries to `package.json` or `requirements.txt` if an existing dependency can fulfill the need.

---

### 6. Response Protocol

When the agent starts a task or enters a project, its **first turn response** must follow this exact markdown structure:

```markdown
## Understanding
[Clear summary of what the project is, its architecture, and relevant domain patterns uncovered during discovery.]

## Current State
[The current git branch, uncommitted diffs, active configuration, and specific modules relevant to the user's prompt.]

## Plan
[Concise, step-by-step implementation plan highlighting minimal diffs, pattern adherence, and verification strategy.]

## Blocking Questions
[State "None" if work can proceed autonomously. Otherwise, list ONLY real, non-inferable blockers.]
```

---

### 7. Completion Report Protocol

Upon finishing an assigned task, the agent must output a structured completion report:

```text
STATUS:
PASS | PARTIAL | BLOCKED

CHANGES:
- <filepath>: Description of modification

VALIDATION:
- <command>: Result (e.g., test suite pass, lint pass, typecheck pass)

DEPLOYMENT:
- Working tree state and branch readiness

DEFERRED QUESTIONS & UNPREDICTED DECISIONS:
- [None — or consolidated list of all questions accumulated during execution to be answered at once]

REMAINING:
- Known limitations, follow-up items, or out-of-scope observations
```

---

## Agent Integration Quick Reference

| Agent Platform | Integration Method |
|---|---|
| **Claude Code** | Add to `~/.claude/commands/` or include in `.claude/skills/` |
| **Cursor** | Reference in `.cursorrules` or `.cursor/rules/discovery.mdc` |
| **Antigravity** | Place in `.gemini/config/skills/agent-project-discovery-skill/SKILL.md` |
| **GitHub Copilot** | Reference in `.github/copilot-instructions.md` |
| **OpenAI Codex / Custom Agents** | Inject into system prompt or runtime agent skill catalog |
