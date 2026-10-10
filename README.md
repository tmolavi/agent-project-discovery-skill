# agent-project-discovery-skill 🧭

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.5.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)
[![Supported Agents](https://img.shields.io/badge/Agents-Codex%20%7C%20Claude%20Code%20%7C%20Cursor%20%7C%20Antigravity%20%7C%20Copilot-blueviolet.svg)](#supported-ai-agents)

> **"An AI agent should understand before it changes."**

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
| **Clobbering Diffs**: Overwrites uncommitted work or ignores ongoing work in the working tree. | **Git Awareness**: Inspects `git status`, current branch, recent commits, and protects existing user modifications. |
| **Architectural Churn**: Rewrites working patterns, duplicates existing utilities, or installs redundant libraries. | **Pattern Adherence**: Matches existing conventions, preserves backward compatibility, and produces minimal diffs. |
| **No Accountability**: Leaves ambiguous completion messages without test results. | **Deterministic Protocols**: Mandates structured First Response (`Understanding`, `Current State`, `Plan`, `Blocking Questions`) and Completion Reports (`STATUS`, `CHANGES`, `VALIDATION`, `DEPLOYMENT`, `REMAINING`). |
| **Middle-of-the-Night Halts**: Executes unprompted out-of-sandbox commands (`ssh`, public `curl`, obscure git diagnostics) that trigger confirmation modals and freeze the agent while you sleep. | **The "Sleep-Well" Protocol**: Enforces 100% in-sandbox deterministic local builds, canonical commands, and single-script automation so agents work completely unattended until morning. |

---

## 🌙 The "Sleep-Well" Principle: True Overnight Autonomy

The ultimate design goal of this skill is simple:
> **"Assign a task, close your laptop, go to sleep, and review clean completed code in the morning without waking up to stalled confirmation prompts."**

### Why Do AI Agents Prompt for Approvals?
Modern AI coding assistants (Google Antigravity, Claude Code, Cursor) enforce a **Sandbox Security Boundary**:
1. **Standard Sandboxed Commands**: Local file edits, git status/diff, local test runners (`pytest`, `vitest`), and builds execute silently with zero approval prompts.
2. **Approval Prompts Triggered When**:
   - The agent requests **Unsandboxed Execution** (`BypassSandbox: true`) to gain raw network or full filesystem access without pre-configured permission grants.
   - The agent prompts to ask **routine verification permission** (`Allow testing /api/models/generate? ssh root@server "docker exec ..."`).
   - The agent prompts to ask **route inspection permission** (`Allow checking model router endpoints? ssh ...`).
   - The agent prompts to ask **central model dispatch testing permission** (`Allow testing central model dispatch? ssh ...`).
   - The agent probes **live public URLs** or external domains (`curl -s https://example.com/...`).
   - The agent runs **unsolicited remote server commands** (`ssh server "docker images"` or `ssh server "ssh -T git@github.com"`).
   - The agent executes **obscure Git plumbing** (`git count-objects`, `git fsck`).
   - The agent attempts to **tamper with system or IDE config files** (`config.json`, global settings outside workspace).
   - The agent runs **long chained shell pipelines** (`cmd1 && cmd2 | grep ... | awk ...`) that break prefix-based auto-approval rules.
   - The agent runs **fragmented, iterative AppleScript/OS one-liners** (`osascript -e '...'`) to inspect browser sessions.

### How This Skill Fixes It:
- **Autonomous Decision Mandate ("Decide By Itself")**: The agent never asks *"Allow testing <endpoint>?"*, *"Allow checking model router endpoints?"*, or *"Allow testing central model dispatch?"*. It autonomously inspects local repository files and chooses local mocks, fixtures, and local test runners without human intervention.
- **Enforces Canonical Local Verification**: All code changes are verified through local builds (`npm run build`, `cargo check`, `go test`) and unit tests instead of hitting live production domains or remote servers.
- **Zero Remote Code Probing**: Discovers endpoints, routers, decorators, and schemas from local workspace files directly without SSH.
- **Autonomous Router & Dispatch Mocking**: Validates reasoning routers and model tier payloads using mocked transports locally.
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

