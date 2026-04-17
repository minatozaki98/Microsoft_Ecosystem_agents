# Changelog

All notable changes to this repository are documented here.

## Unreleased

### Added

- Added this changelog to track repository changes.

## 2026-04-17 - Add Interactive Azure Requirements Flow

Commit: `0c25921`

### Added

- Added an interactive Azure requirements interview to the Microsoft Azure Provisioning Engineer role.
- Added a compact Azure requirements ledger format for incomplete provisioning requirements.
- Added one-question-at-a-time behavior before Azure preview or live provisioning commands.
- Added approval gates for paid resources, public exposure, RBAC changes, and secret changes.

### Changed

- Updated the Microsoft migration orchestrator to route incomplete Azure requirements through the provisioning interview.
- Updated `README.md` and `AGENTS.md` to document the interactive Azure provisioning requirements flow.

## 2026-04-17 - Initial Microsoft Ecosystem Agent Pack

Commit: `11e73da`

### Added

- Added the Microsoft migration orchestrator skill.
- Added Microsoft migration specialist role prompts:
  - Microsoft Application Manager.
  - Microsoft Senior Engineer.
  - Microsoft Azure Provisioning Engineer.
  - Microsoft Senior Developer.
  - Microsoft Migration Tester.
- Added Microsoft equivalents reference mappings for hosting, identity, data, storage, messaging, AI, observability, CI/CD, infrastructure, API management, email, and low-code tools.
- Added Microsoft MCP and official reference source guidance for Microsoft Learn MCP, Azure MCP Server, Azure DevOps MCP Server, Microsoft MCP Server for Enterprise, Microsoft Foundry MCP tooling, Azure-hosted custom MCP servers, and fallback Microsoft references.
- Added installed Microsoft Agent Framework and Microsoft Skill Creator skills.
- Added root Codex instructions in `AGENTS.md`.
- Added repository overview and usage guidance in `README.md`.
- Added `.gitignore` entry for `.claude/` compatibility links.
- Added the initial design note under `docs/plans/`.
