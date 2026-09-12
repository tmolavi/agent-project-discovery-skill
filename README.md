# agent-project-discovery-skill 🧭

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.1.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
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
| **Clobbering Diffs**: Overwrites uncommitted work or ignores ongoing work in the working tree. | **Git Awareness**: Inspects `git status`, current branch, recent commits, and protects existing user modifications. |
| **Architectural Churn**: Rewrites working patterns, duplicates existing utilities, or installs redundant libraries. | **Pattern Adherence**: Matches existing conventions, preserves backward compatibility, and produces minimal diffs. |
| **No Accountability**: Leaves ambiguous completion messages without test results. | **Deterministic Protocols**: Mandates structured First Response (`Understanding`, `Current State`, `Plan`, `Blocking Questions`) and Completion Reports (`STATUS`, `CHANGES`, `VALIDATION`, `DEPLOYMENT`, `REMAINING`). |

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

## 📄 License

Distributed under the [MIT License](LICENSE). Open-source and free for personal, commercial, and enterprise use.
