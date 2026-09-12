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

**Instead:**
- Search the codebase using grep, symbol search, or directory listing.
- Infer conventions from existing implementations and commit history.
- Read existing unit/integration tests for usage patterns.

**Only ask questions when:**
1. A genuine blocker exists where information cannot be found in the repository.
2. The user requested an ambiguous destructive operation (e.g., database wipe, deprecating public APIs).
3. An architectural decision has multiple valid, non-obvious trade-offs requiring human business judgment.

---

## 4. Engineering Standards & Behavioral Rules

- **Minimal Diffs**: Make targeted, atomic modifications. Never refactor surrounding untouched code unless explicitly asked.
- **Pattern Matching**: Match the existing paradigm (error handling, logging, naming, formatting, type definitions).
- **Backward Compatibility**: Preserve existing public interfaces, APIs, schemas, and runtime contracts.
- **Zero Hallucinated Dependencies**: Do not introduce new third-party dependencies without verifying existing alternatives in the lockfile.
- **Zero Unsolicited Remote/SSH Probing**: NEVER run `ssh`, `scp`, `rsync`, or remote `docker` commands (`docker ps`, `docker images`, `docker inspect`) on external servers during discovery or development. Understand deployment statically by reading `Dockerfile`, `compose.yaml`, and CI configs.
- **Zero Remote Port Probing**: NEVER run port checks or endpoint pings via SSH (e.g. `ssh server "curl ..."`). Determine port mappings statically from `docker-compose.yml`, `Dockerfile`, and service configs.
- **Zero Remote Git SSH Probing**: NEVER run unsolicited remote Git/SSH authentication probes (e.g. `ssh server "ssh -T git@github.com"`).
- **Zero Live Route Probing**: NEVER run live route crawlers or active HTTP endpoint scanners against public domains (e.g. `curl https://...`). Verify code deterministically via local builds (`npm run build`, `cargo test`, `pytest`) or local loopback servers (`http://127.0.0.1:<port>`).
- **Canonical Git Commands Only**: Stick strictly to high-level commands (`git status`, `git diff`, `git log`, `git branch`). NEVER run obscure repository plumbing (`git count-objects`, `git fsck`).
- **Zero Global Config Tampering**: NEVER attempt to modify global IDE configs, agent permission files (e.g., `config.json`), or files outside the workspace root. All project work must remain strictly self-contained within the repository.
- **Sandbox Discipline**: Run all commands inside the default sandbox without triggering permission confirmation modals unless the user explicitly requested remote operations.
- **Batch Remote Operations**: If the user explicitly asks for remote work, combine operations into a unified script instead of firing dozens of individual SSH commands that trigger confirmation prompts.
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
