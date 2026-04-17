# Microsoft MCP And Reference Sources

Use these sources in addition to Microsoft Learn MCP. Prefer connected MCP tools when available, then official Microsoft docs, SDK samples, and CLI tools as fallback.

## Priority Order

1. Microsoft Learn MCP: documentation discovery, full docs pages, and code samples.
2. Azure MCP Server: Azure resource discovery, management, diagnostics, deployment help, CLI command generation, Bicep schema, and Azure best practices.
3. Azure DevOps MCP Server: work items, PRs, repos, builds, pipelines, test plans, search, and wiki context.
4. Microsoft MCP Server for Enterprise: Microsoft Graph and Microsoft Entra tenant context.
5. Microsoft Foundry Agent MCP tooling: hosted Foundry agents that connect to MCP servers as tools.
6. Azure-hosted custom MCP servers: App Service or Container Apps hosting for project-specific APIs, databases, or internal tools.
7. Official Microsoft docs and repos: Azure Architecture Center, Well-Architected Framework, Cloud Adoption Framework, Graph docs, Azure SDK docs, Azure Samples, and Azure Verified Modules.
8. Local Microsoft CLIs: `az`, `azd`, `func`, Bicep, Microsoft Graph PowerShell, and Azure DevOps CLI.

## Source Selection

| Need | Prefer | Fallback |
| --- | --- | --- |
| Current docs or samples | Microsoft Learn MCP | `npx @microsoft/learn-cli` |
| Azure resource inventory or provisioning | Azure MCP Server | `az`, Bicep, Azure Portal docs |
| Azure CLI command discovery | Azure MCP Server Azure CLI tools | `az --help`, CLI reference docs |
| Bicep schema or deployment preview | Azure MCP Server Bicep/deploy tools | `az deployment ... what-if` |
| Azure best practices or compliance scan | Azure MCP best practices / Azure Quick Review | Well-Architected Framework, `azqr` |
| Entra users, groups, apps, policies, roles | Microsoft MCP Server for Enterprise | Microsoft Graph docs, Graph PowerShell |
| Azure DevOps project state | Azure DevOps MCP Server | `az repos`, `az boards`, Azure DevOps REST docs |
| Hosted AI agent with MCP tools | Microsoft Foundry MCP tooling | Microsoft Agent Framework docs and SDK samples |
| Project-specific tools exposed to agents | Custom MCP on App Service or Container Apps | Direct REST API integration |

## Azure MCP Server

Use for Azure services and Azure operations. It can help with subscriptions, resource groups, App Service, Azure CLI command generation, Azure Developer CLI install guidance, Bicep schema, Azure deployments, Azure Monitor, RBAC, App Configuration, Application Insights, Azure AI Search, Foundry, Event Hubs, Service Bus, Event Grid, Cosmos DB, Azure SQL, PostgreSQL, Azure Functions, and more.

Guardrails:

- Treat connected Azure MCP tools as live Azure access governed by the signed-in user and Azure RBAC.
- Prefer read-only discovery first, then previewable changes.
- Use the Azure provisioning role for live create/update/delete work.
- Do not create paid resources, assign broad RBAC, expose private services publicly, or delete resources without explicit approval.

Official docs:

- `https://learn.microsoft.com/azure/developer/azure-mcp-server/overview`
- `https://learn.microsoft.com/azure/developer/azure-mcp-server/tools/`

## Microsoft MCP Server For Enterprise

Use for Microsoft Graph and Microsoft Entra tenant context. It is useful for users, groups, applications, audit logs, policies, directory roles, licenses, access reviews, lifecycle workflows, provisioning logs, and identity risk data.

Guardrails:

- It uses delegated `MCP.*` scopes and user privileges.
- Use least privilege scopes and admin consent only when required.
- Do not change tenant settings, app registrations, Conditional Access, role assignments, or user lifecycle state without explicit approval.
- Avoid printing personally identifiable information unless the user asked for it and access is appropriate.

Official docs:

- `https://learn.microsoft.com/graph/mcp-server/overview`
- `https://learn.microsoft.com/graph/mcp-server/get-started`

## Azure DevOps MCP Server

Use for Azure DevOps work items, pull requests, builds, repos, search, wiki, test plans, sprint status, and project health. Prefer the local server when broad client compatibility or local data control matters.

Guardrails:

- Read project context first before editing work items or test plans.
- Do not create or update work items, PRs, test plans, or pipeline settings without explicit approval.
- For remote Azure DevOps MCP, verify client support because preview support varies by environment.

Official docs:

- `https://learn.microsoft.com/azure/devops/mcp-server/mcp-server-overview`
- `https://learn.microsoft.com/azure/devops/mcp-server/remote-mcp-server`

## Microsoft Foundry Agent MCP Tooling

Use when designing hosted agents in Microsoft Foundry that connect to MCP servers as tools. This is for production agent architecture, not local repo migration by itself.

Guardrails:

- Configure allowed tools narrowly.
- Keep approval required for sensitive tools unless the user explicitly approves otherwise.
- Store MCP server authentication in Foundry project connections or secure app settings, not in source files.

Official docs:

- `https://learn.microsoft.com/azure/foundry/agents/how-to/tools/model-context-protocol`

## Azure-Hosted Custom MCP Servers

Use when the project should expose its own APIs, databases, workflows, or internal tools to AI agents. App Service works well for existing web apps and APIs; Container Apps works well for containerized MCP servers, scalable HTTP ingress, and dynamic sessions.

Guardrails:

- Protect endpoints with Entra ID, managed identity, API Management, or another approved auth layer.
- Expose only the minimum tool surface.
- Add logging, health checks, and rate limits before production use.
- Treat tool calls as actions that need authorization and auditability.

Official docs:

- `https://learn.microsoft.com/azure/app-service/scenario-ai-model-context-protocol-server`
- `https://learn.microsoft.com/azure/container-apps/mcp-overview`

## Official Non-MCP References

Use these when MCP tools are unavailable or when architecture guidance is needed:

- Azure Architecture Center: `https://learn.microsoft.com/azure/architecture/`
- Azure Well-Architected Framework: `https://learn.microsoft.com/azure/well-architected/`
- Microsoft Cloud Adoption Framework: `https://learn.microsoft.com/azure/cloud-adoption-framework/`
- Microsoft Graph docs: `https://learn.microsoft.com/graph/`
- Azure SDK docs: `https://learn.microsoft.com/azure/developer/`
- Azure Samples: `https://github.com/Azure-Samples`
- Azure Verified Modules: `https://azure.github.io/Azure-Verified-Modules/`
- Azure CLI reference: `https://learn.microsoft.com/cli/azure/`
