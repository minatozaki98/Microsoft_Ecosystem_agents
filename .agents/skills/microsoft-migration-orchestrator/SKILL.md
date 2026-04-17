---
name: microsoft-migration-orchestrator
description: Use when converting a project from non-Microsoft tools, apps, SDKs, auth, hosting, data, AI, CI/CD, observability, or features to Microsoft and Azure equivalents with analysis, planning, implementation, and review.
---

# Microsoft Migration Orchestrator

## Overview

Coordinate a Microsoft migration from inventory to review. Use Microsoft Learn as the source of truth, map existing non-Microsoft choices to Microsoft equivalents, and dispatch the project-local Codex role prompts for application, architecture, implementation, and testing work.

## Source Of Truth

- Read `references/microsoft-mcp-reference-sources.md` when the task touches Azure resources, Microsoft Graph, Entra ID, Azure DevOps, Microsoft Foundry, MCP servers, or official Microsoft architecture guidance.
- Use Microsoft Learn MCP tools for current guidance before recommending or implementing replacements:
  - `microsoft_docs_search` for discovery and decision support.
  - `microsoft_docs_fetch` for high-value pages that drive architecture or implementation.
  - `microsoft_code_sample_search` for Microsoft SDK examples.
- Use connected Microsoft MCP servers when available:
  - Azure MCP Server for Azure resource inventory, management, diagnostics, Bicep schema, deployments, Azure CLI generation, and Azure best practices.
  - Microsoft MCP Server for Enterprise for Microsoft Graph and Microsoft Entra tenant context.
  - Azure DevOps MCP Server for boards, repos, PRs, builds, pipelines, test plans, search, and wiki context.
  - Microsoft Foundry MCP tooling for hosted Foundry agents that use MCP servers as tools.
  - Azure-hosted custom MCP servers on App Service or Container Apps for project-specific APIs or internal tools.
- If Learn MCP is unavailable, use the CLI fallback from the installed `microsoft-skill-creator` skill:
  - `npx @microsoft/learn-cli search "..."`
  - `npx @microsoft/learn-cli fetch "..."`
  - `npx @microsoft/learn-cli code-search "..." --language ...`
- Use the installed `microsoft-agent-framework` skill when replacing Semantic Kernel, AutoGen, LangChain-style agents, CrewAI, LlamaIndex agent flows, or custom agent orchestration.
- For Azure migration structure, align planning language with the Microsoft Cloud Adoption Framework: discover inventory, select a migration strategy, assess workloads, execute migration, optimize, and decommission only after approval.
- For architecture review, use Azure Well-Architected pillars: Reliability, Security, Cost Optimization, Operational Excellence, and Performance Efficiency.

## Role Dispatch

Codex does not have a stable named-agent registry. Treat the files in `../../agents/` as role prompts and run them with `spawn_agent(agent_type="worker")` when multi-agent support is available.

Use this dispatch framing:

```text
Your task is to perform the following. Follow the instructions below exactly.

<agent-instructions>
[contents of the selected .agents/agents/*.md file]
</agent-instructions>

Project/request context:
[focused task context, relevant files, constraints, and expected output]

Execute this now. Output only the structured response requested by the role prompt.
```

If subagents are unavailable, read each role prompt and perform the same pass sequentially in the main Codex thread.

| Phase | Role prompt | Purpose |
| --- | --- | --- |
| Inventory and impact | `../../agents/microsoft-application-manager.md` | Identify app features, stakeholders, risks, value, and migration readiness. |
| Architecture mapping | `../../agents/microsoft-senior-engineer.md` | Choose Microsoft equivalents and design the target architecture. |
| Azure provisioning | `../../agents/microsoft-azure-provisioning-engineer.md` | Create, preview, update, and verify Azure resources with az CLI and Bicep guardrails. |
| Implementation | `../../agents/microsoft-senior-developer.md` | Replace tools with scoped code/config/docs changes. |
| Verification | `../../agents/microsoft-migration-tester.md` | Test behavior, validate migration risks, and report gaps. |

## Migration Workflow

1. Inventory the current project:
   - Search manifests, lockfiles, configs, CI files, infrastructure files, env examples, docs, imports, SDK usage, and deployment settings.
   - Capture tools by category: hosting, runtime, UI, APIs, auth, data, storage, messaging, AI/agents, search, CI/CD, observability, payments, docs, and local developer tooling.
   - Separate first-party app behavior from replaceable vendor integration.

2. Map Microsoft equivalents:
   - Read `references/microsoft-equivalents.md` before creating the first mapping.
   - Read `references/microsoft-mcp-reference-sources.md` when choosing Microsoft MCP, Azure, Graph, DevOps, Foundry, or custom MCP sources.
   - Use Learn MCP to verify current names, migration guidance, SDKs, and known limitations for each replacement.
   - Produce a table with: current tool, purpose, Microsoft equivalent, migration strategy, confidence, behavior gaps, docs consulted, and owner role.

3. Create the migration plan:
   - Preserve behavior first, then adopt Microsoft-native patterns.
   - Prefer incremental slices with rollback paths over broad rewrites.
   - Call out secrets, identity, data migration, network, cost, licensing, compliance, and downtime assumptions.
   - Ask before destructive changes, data deletion, credential changes, source workload decommissioning, or irreversible migrations.

4. Provision Azure resources when required:
   - Dispatch `../../agents/microsoft-azure-provisioning-engineer.md` before live Azure resource creation or infrastructure-as-code changes.
   - Confirm Azure CLI authentication, subscription, tenant, region, resource group, SKU, tags, network posture, and cost assumptions.
   - Prefer Bicep or Azure Developer CLI files for repeatable infrastructure.
   - Use Azure CLI `what-if` or `--confirm-with-what-if` for Bicep/ARM deployments when possible.
   - Do not run paid, destructive, credential, RBAC, or public exposure changes without explicit user approval.

5. Execute the plan:
   - Keep edits scoped to the approved slice.
   - Use Microsoft SDKs and identity patterns appropriate to the project language.
   - Prefer `DefaultAzureCredential` or equivalent Azure identity chains for server-side Azure auth.
   - Never commit real secrets. Update env examples and setup docs with placeholder variables.
   - Keep non-Microsoft tools only when no equivalent exists, feature parity is not acceptable, or the user approves retaining them.

6. Review and test:
   - Run the most specific verification first, then broader checks when available.
   - Review against the mapping table and Well-Architected pillars.
   - Report remaining non-Microsoft dependencies, behavior gaps, test gaps, and follow-up migration waves.

## Output Contract

For analysis-only requests, return:

- Current inventory.
- Microsoft equivalent mapping.
- Recommended migration plan.
- Risks, unknowns, and Microsoft MCP/reference sources consulted.

For implementation requests, return:

- Files changed.
- Replacements made.
- Azure resources provisioned or intentionally not provisioned.
- Verification commands and results.
- Remaining migration work.

## Common Mistakes

- Treating "Microsoft equivalent" as a one-for-one package rename. Always validate behavior, identity model, data shape, and operational model.
- Replacing auth without planning tenants, redirect URIs, token validation, session behavior, and user migration.
- Migrating data or storage without backup, rollback, and validation steps.
- Choosing Azure services from memory when Microsoft Learn can verify current product names and SDK patterns.
- Letting implementation run ahead of inventory and stakeholder impact.
