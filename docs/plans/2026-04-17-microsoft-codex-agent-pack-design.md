# Microsoft Codex Agent Pack Design

## Goal

Create a project-local Codex agent pack that can analyze a project using non-Microsoft tools, find Microsoft equivalents, plan migration, execute approved replacements, and review the result.

## Approach

Use one orchestrator skill and role prompt files. Codex does not currently expose a stable project-local named-agent registry, so the orchestrator reads role prompts from `.agents/agents` and dispatches them with worker subagents when available. If subagents are unavailable, the same prompts work as sequential checklists.

## Components

- `microsoft-migration-orchestrator`: Coordinates inventory, mapping, planning, implementation, and review.
- `microsoft-application-manager`: Covers application purpose, business impact, stakeholder decisions, readiness, and migration waves.
- `microsoft-senior-engineer`: Covers Microsoft target architecture, identity, data, security, operations, and Azure Well-Architected review.
- `microsoft-azure-provisioning-engineer`: Covers Azure CLI connection, Bicep/ARM previews, resource creation, tags, identity, cost guardrails, and post-provision verification.
- `microsoft-senior-developer`: Covers scoped implementation changes using Microsoft SDKs and service patterns.
- `microsoft-migration-tester`: Covers verification, regression checks, configuration validation, and release risk.

## Microsoft Source Coverage

The pack uses Microsoft Learn MCP first, then `microsoft-mcp-reference-sources.md` to route work to Azure MCP Server, Microsoft MCP Server for Enterprise, Azure DevOps MCP Server, Microsoft Foundry MCP tooling, Azure-hosted custom MCP servers, official Microsoft architecture references, and local Microsoft CLIs.

## Data Flow

The orchestrator inventories the project, consults Microsoft Learn MCP, dispatches role prompts, merges findings into a migration plan, provisions Azure resources when approved, executes implementation slices, then runs tester and review passes.

## Safety

The pack requires explicit approval for destructive migrations, data deletion, credential changes, and source decommissioning. Microsoft equivalents must be verified with Microsoft Learn because product names and migration guidance change.
