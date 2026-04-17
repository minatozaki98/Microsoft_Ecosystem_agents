# Microsoft Equivalents Reference

Use this as a starting map, then verify each candidate with Microsoft Learn MCP before planning or implementing. For Microsoft MCP servers and non-MCP official references, use `microsoft-mcp-reference-sources.md`.

## Common Mappings

| Category | Common non-Microsoft tools | Microsoft equivalent candidates |
| --- | --- | --- |
| Static web hosting | Netlify, Vercel, Firebase Hosting, Cloudflare Pages | Azure Static Web Apps, Azure App Service |
| Web/API hosting | Heroku, Render, Railway, Fly.io, AWS Elastic Beanstalk | Azure App Service, Azure Container Apps, Azure Kubernetes Service |
| Serverless functions | AWS Lambda, Google Cloud Functions, Cloudflare Workers | Azure Functions, Azure Container Apps jobs |
| Containers | ECS, EKS, Cloud Run, Kubernetes elsewhere | Azure Container Apps, Azure Kubernetes Service, Azure Container Registry |
| Identity for workforce apps | Auth0, Okta, custom OAuth, Keycloak | Microsoft Entra ID, Microsoft Graph |
| Customer identity | Auth0, Firebase Auth, Clerk, Cognito | Microsoft Entra External ID. Avoid new Azure AD B2C recommendations for new customers unless maintaining an existing tenant. |
| Secrets | AWS Secrets Manager, Doppler, Vault, dotenv-only secrets | Azure Key Vault, managed identities |
| Relational data | PostgreSQL/MySQL on other clouds, Supabase, PlanetScale | Azure Database for PostgreSQL, Azure Database for MySQL, Azure SQL Database |
| NoSQL data | MongoDB Atlas, DynamoDB, Firestore | Azure Cosmos DB, Azure Table Storage when appropriate |
| Object storage | S3, GCS, Cloudflare R2 | Azure Blob Storage, Azure Data Lake Storage |
| Queues and events | SQS, SNS, EventBridge, Kafka cloud services | Azure Service Bus, Azure Event Grid, Azure Event Hubs |
| Realtime/pubsub | Pusher, Ably, Socket.IO cloud services | Azure Web PubSub, Azure SignalR Service |
| Search | Algolia, Elasticsearch cloud, Meilisearch | Azure AI Search |
| AI models | OpenAI direct, Anthropic, Gemini, Cohere | Azure OpenAI, Azure AI Foundry, Microsoft Foundry models where available |
| Agent frameworks | LangChain agents, CrewAI, AutoGen, Semantic Kernel, custom tool loops | Microsoft Agent Framework. Use official migration guides for Semantic Kernel and AutoGen. |
| Observability | Datadog, New Relic, Sentry-only monitoring | Azure Monitor, Application Insights, Log Analytics |
| CI/CD | CircleCI, GitLab CI, Jenkins, Buildkite | GitHub Actions, Azure Pipelines |
| IaC | Terraform-only, Pulumi, CloudFormation | Bicep, Azure Verified Modules, Azure Developer CLI. Terraform can remain when approved. |
| API management | Kong, Apigee, custom gateway | Azure API Management |
| Email | SendGrid, Mailgun, Postmark | Azure Communication Services Email, Microsoft Graph mail for Microsoft 365 scenarios |
| Low-code apps | Retool, Appsmith, internal spreadsheet apps | Microsoft Power Platform, Power Apps, Power Automate |

## Azure Provisioning Guardrails

Use the `microsoft-azure-provisioning-engineer` role before creating Azure resources. It should connect through Azure CLI, verify the account context, and prefer previewable IaC.

Minimum Azure CLI preflight:

- `az version`
- `az account show`
- `az account list --output table`
- `az account set --subscription "<subscription-id-or-name>"` when the target subscription is known.

Resource group and region checks:

- `az group exists --name "<resource-group>"`
- `az group create --name "<resource-group>" --location "<location>" --tags project="<project>" owner="<owner>"`
- `az account list-locations --query "[].{Region:name}" --output table`

Bicep/ARM preview:

- Resource group: `az deployment group what-if --resource-group "<resource-group>" --template-file "<path-to-main.bicep>"`
- Subscription: `az deployment sub what-if --location "<location>" --template-file "<path-to-main.bicep>"`
- Confirmed create: `az deployment group create --confirm-with-what-if --resource-group "<resource-group>" --template-file "<path-to-main.bicep>"`

Do not delete resource groups, purge Key Vaults, delete databases or storage, rotate secrets, assign broad RBAC, or expose private services publicly without explicit user approval.

## Migration Strategy Labels

Use these Cloud Adoption Framework-aligned labels in plans:

- Retire: remove unused tool or feature.
- Retain: keep temporarily or permanently because replacement is not justified.
- Rehost: move hosting with minimal code changes.
- Replatform: move to a managed Microsoft service with small code/config changes.
- Refactor: change code structure to fit Microsoft SDKs or service models.
- Rearchitect: redesign major components for Azure-native architecture.
- Rebuild: recreate the feature on Microsoft services.
- Replace: swap a product with a Microsoft SaaS or managed equivalent.

## Verification Queries

Use these query patterns with Microsoft Learn MCP:

- `"{service} overview Microsoft Learn"`
- `"{service} quickstart {language} Microsoft Learn"`
- `"{source tool} migrate to {microsoft service} Microsoft Learn"`
- `"{microsoft service} best practices security Microsoft Learn"`
- `"{microsoft service} limits quotas pricing Microsoft Learn"`
- `"{microsoft service} Well-Architected Framework guidance"`
