# Microsoft Ecosystem Agents

Project-local Codex agent pack for migrating applications from non-Microsoft tools, services, SDKs, hosting, identity, data, AI, CI/CD, and observability choices to Microsoft and Azure equivalents.

The pack is designed to run a structured migration loop:

1. Analyze the current project.
2. Identify Microsoft equivalents.
3. Plan a safe replacement path.
4. Execute scoped migration work.
5. Review, test, and report remaining gaps.

## What Is Included

- `AGENTS.md` - root instructions for Codex in this workspace.
- `.agents/skills/microsoft-migration-orchestrator/` - the main migration orchestration skill.
- `.agents/skills/microsoft-agent-framework/` - installed Microsoft Agent Framework guidance.
- `.agents/skills/microsoft-skill-creator/` - installed Microsoft skill creation guidance.
- `.agents/agents/` - specialist role prompts used by the orchestrator.
- `docs/plans/` - design notes for the agent pack.
- `skills-lock.json` - installed skill source and hash lock data.

The `.agents/` directory is the source of truth. A local `.claude/` directory may exist as a compatibility link created by skill tooling, but it is intentionally ignored by Git to avoid committing duplicated junction contents on Windows.

## Specialist Agents

The orchestrator coordinates these role prompts:

| Agent | Role |
| --- | --- |
| Microsoft Application Manager | Inventories app capabilities, stakeholders, business impact, and migration readiness. |
| Microsoft Senior Engineer | Maps architecture to Microsoft and Azure equivalents using Well-Architected guidance. |
| Microsoft Azure Provisioning Engineer | Plans and performs Azure resource provisioning through Azure CLI, Bicep, and Azure MCP guardrails. |
| Microsoft Senior Developer | Implements scoped code, config, SDK, and documentation changes. |
| Microsoft Migration Tester | Reviews behavior, validates risks, runs tests, and reports migration gaps. |

Codex can use these prompts with `spawn_agent(agent_type="worker")` when subagent support is available. Otherwise, the same prompts can be followed sequentially in the main Codex thread.

## Microsoft Reference Sources

The pack uses Microsoft Learn MCP as the first source of truth for current Microsoft documentation and samples. It also references:

- Azure MCP Server for Azure resource discovery, management, diagnostics, Bicep, deployments, and best practices.
- Azure DevOps MCP Server for work items, PRs, builds, pipelines, test plans, search, and wiki context.
- Microsoft MCP Server for Enterprise for Microsoft Graph and Microsoft Entra tenant context.
- Microsoft Foundry MCP tooling for hosted agents that use MCP servers as tools.
- Azure-hosted custom MCP servers on App Service or Container Apps.
- Official Microsoft architecture, Azure SDK, Microsoft Graph, Azure CLI, Azure Samples, and Azure Verified Modules references.

See `.agents/skills/microsoft-migration-orchestrator/references/microsoft-mcp-reference-sources.md` for the full source policy.

## Migration Mapping

Starter mappings live in:

```text
.agents/skills/microsoft-migration-orchestrator/references/microsoft-equivalents.md
```

Examples include:

- Vercel, Netlify, Firebase Hosting, and Cloudflare Pages to Azure Static Web Apps or Azure App Service.
- Heroku, Render, Railway, Fly.io, and Elastic Beanstalk to Azure App Service, Azure Container Apps, or AKS.
- Auth0, Okta, Clerk, Cognito, Firebase Auth, and Keycloak to Microsoft Entra ID or Microsoft Entra External ID.
- AWS Lambda, Google Cloud Functions, and Cloudflare Workers to Azure Functions or Azure Container Apps jobs.
- S3, GCS, and R2 to Azure Blob Storage or Azure Data Lake Storage.
- Datadog, New Relic, and Sentry-only monitoring to Azure Monitor, Application Insights, and Log Analytics.
- LangChain-style agents, CrewAI, AutoGen, Semantic Kernel, or custom agent loops to Microsoft Agent Framework where appropriate.

Every mapping should still be verified with Microsoft Learn MCP before implementation.

## Azure Provisioning Safety

Use the Microsoft Azure Provisioning Engineer role before creating or updating Azure resources.

Minimum Azure CLI preflight:

```powershell
az version
az account show
az account list --output table
```

Before paid or live resource changes, confirm the subscription, tenant, region, resource group, SKU, tags, network posture, and expected cost. Prefer Bicep or Azure Developer CLI for repeatable infrastructure, and use `what-if` deployment previews where available.

Do not delete resources, purge Key Vaults, rotate credentials, assign broad RBAC, expose private services publicly, or decommission source systems without explicit user approval.

## How To Use

Ask Codex to use the Microsoft migration orchestrator for a target project. A good request includes the source project path and the migration goal:

```text
Use the Microsoft migration orchestrator to analyze this project and replace non-Microsoft hosting, auth, database, AI, and CI/CD choices with Microsoft equivalents. Start with inventory and a plan before making code changes.
```

For Azure resource creation, include the intended subscription, region, resource group, naming prefix, and whether live provisioning is approved.

## Repository Notes

This repository is intentionally lightweight. It stores agent prompts, skills, references, and planning notes rather than application runtime code.
