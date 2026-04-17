# Codex Project Instructions

This workspace contains a project-local Microsoft migration agent pack.

Use `.agents/skills/microsoft-migration-orchestrator/SKILL.md` when the user asks to convert a project from non-Microsoft tools, apps, SDKs, hosting, auth, data, AI, CI/CD, observability, or features to Microsoft and Azure equivalents.

The orchestrator uses these Codex role prompts:

- `.agents/agents/microsoft-application-manager.md`
- `.agents/agents/microsoft-senior-engineer.md`
- `.agents/agents/microsoft-azure-provisioning-engineer.md`
- `.agents/agents/microsoft-senior-developer.md`
- `.agents/agents/microsoft-migration-tester.md`

Use Microsoft Learn MCP tools for current Microsoft guidance before recommending or implementing replacements. Also use `.agents/skills/microsoft-migration-orchestrator/references/microsoft-mcp-reference-sources.md` for Azure MCP Server, Microsoft MCP Server for Enterprise, Azure DevOps MCP Server, Microsoft Foundry MCP tooling, Azure-hosted custom MCP servers, and official Microsoft fallback references. Prefer project-local `.agents/skills` over `.claude` compatibility links when working in Codex.

Use the Azure provisioning role before creating Azure resources with `az`, Bicep, ARM, or Azure Developer CLI. Do not perform destructive migrations, create paid resources, delete data, rotate credentials, assign broad RBAC, expose private resources publicly, or decommission source systems without explicit user approval.
