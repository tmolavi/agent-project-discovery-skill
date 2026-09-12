---
name: agent-project-discovery-skill
description: Universal startup and context discovery skill for AI coding agents to inspect, understand, and plan before modifying existing projects.
version: 1.0.0
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
4. **Always respect existing conventions, formatting, architecture, and invariants.**

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
> **Static Local Discovery & Silent Autonomy (Zero Sandbox Escapes):**
> The #1 killer of overnight autonomous execution is issuing unprompted out-of-sandbox commands (`BypassSandbox: true` / SSH / network probes), which triggers human confirmation modals and freezes the agent until morning.
> - **Stay 100% inside the workspace sandbox**: Local file operations (`read`, `write`, `edit`, `git status`, local tests) execute completely silently without bothering the user.
> - **NEVER** SSH into remote servers (`ssh ...`) to inspect containers, images, processes, or ports (e.g., `ssh server "docker images | grep ..."`, `ssh server "docker ps"`, `ssh server "docker inspect ..."`).
> - **NEVER** run network/port probes (`curl`, `wget`, `nc`, `telnet`) against remote hosts or localhost endpoints over SSH tunnels.
> - **NEVER** run unsolicited remote Git/SSH authentication probes (e.g., `ssh server "ssh -T git@github.com"`).
> - **NEVER** run live route crawlers or active HTTP endpoint scanners. Discover routes statically from source router definitions (`app/`, `pages/`, `routes/`) and OpenAPI specs.
> - **Determine images, ports, remotes, routes, and containers statically**: Read local `.git/config`, router files, `docker-compose.yml` (`image:`, `ports:`, `labels:`), `Dockerfile` (`FROM`, `EXPOSE`), reverse proxy configs (`nginx.conf`), and CI build workflows.
> - **Batch Remote Operations**: If the user explicitly commands remote server work, combine all operations into a single script or unified execution rather than firing dozens of fragmented SSH commands that re-prompt the user.

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

AI agents lose user trust when they ask trivial or helpless questions.

#### Prohibited Questions (Never Ask These Immediately):
- ❌ *"What should I do?"*
- ❌ *"Can you give me the files related to this?"*
- ❌ *"Where is the database configuration located?"*
- ❌ *"How should I run the project?"*
- ❌ *"What does function XYZ do?"*

#### The Autonomous Resolution Process:
1. **Search First**: Use grep, file name matchers, AST symbol lookup, or ripgrep.
2. **Inspect Existing Code**: Look for precedent patterns elsewhere in the repository.
3. **Read Documentation**: Check docs, schemas, comments, and README.
4. **Infer from Context**: If a pattern is repeated in 5 places, follow that pattern in the 6th place.

#### Permitted Questions (ONLY Under These Conditions):
You may **ONLY** prompt the user with a question if:
1. **Information genuinely does not exist in the codebase**: E.g., access to external third-party sandbox credentials not listed in `.env.example`.
2. **Destructive Choices**: The requested action would permanently delete data, drop tables, remove public APIs, or reset git state.
3. **Architecture Fork**: Multiple mutually exclusive design options exist that carry significant architectural trade-offs requiring product or business approval.

---

### 5. Engineering Behavior

The agent must act as a custodian of the existing codebase:

#### Strong Preferences:
- **Minimal Changes**: Only touch lines and files strictly necessary for the objective. Do not reformat untouched code.
- **Existing Patterns**: Match existing error handling, logging, naming, indentation, and typing styles even if you personally prefer a different style.
- **Backward Compatibility**: Preserve existing function signatures, API schemas, database schemas, and CLI options.
- **Test Before Deployment**: Verify existing tests pass before modifying code, and add new tests covering your changes.
- **Reversible Changes**: Keep edits modular and easy to roll back cleanly via git.

#### Strict Anti-Patterns (Avoid):
- 🚫 **Unsolicited Remote/SSH Probing**: NEVER run `ssh`, `scp`, `rsync`, remote `docker images`, `docker ps`, `docker inspect`, or remote `kubectl` commands during discovery. Understand deployment statically by reading `docker-compose.yml`, `Dockerfile`, and CI workflows.
- 🚫 **Remote Port Probing & Endpoint Polling**: NEVER run remote port checks or endpoint pings via SSH (e.g., `ssh ... "curl -s -I http://127.0.0.1:..."`). Determine ports and URLs statically from configs.
- 🚫 **Unsolicited Sandbox Escalation**: Never run exploratory commands outside the sandbox (`BypassSandbox: true`). Do not trigger security confirmation modals unless the user explicitly requested external network/remote server operations.
- 🚫 **Unnecessary Rewrites**: Do not replace an entire file or subsystem when a 5-line diff solves the problem.
- 🚫 **Duplicate Systems**: Do not write a new HTTP client or utility when the repository already has an internal helper for it.
- 🚫 **Architectural Churn**: Do not change libraries (e.g. replacing Axios with Fetch or Jest with Vitest) unless explicitly instructed.
- 🚫 **Tampering with Global IDE / System Configurations**: NEVER attempt to modify global IDE configs, agent permission files (e.g., `config.json`), shell profiles (`~/.zshrc`, `~/.bashrc`), or files outside the workspace root. All project configurations, scripts, and dependencies must remain strictly self-contained within the repository.
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
