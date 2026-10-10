# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
