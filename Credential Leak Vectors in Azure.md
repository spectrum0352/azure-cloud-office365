# Azure Credential Leak Vectors

Pentest Reference Table

| **Attack Vector** | **API/Service or Method** | **Required Access / Misconfig** | **What You Can Extract** |
|----|----|----|----|
| **IMDS Token Abuse** | http://169.254.169.254/metadata/identity/oauth2/token | SSRF / RCE on VM / container | Managed Identity access tokens |
| **Key Vault Secrets Dump** | GET /secrets/{secret-name} via Azure Key Vault API | Key Vault Reader / misconfigured access | Credentials, API keys, secrets |
| **App Service AppSettings Dump** | Kudu / SCM or ARM API (/config/appsettings/list) | Contributor / Reader on App Service | Environment vars with credentials |
| **Automation Account Variable Dump** | ARM API / Runbook access (/variables, /credentials) | Contributor / Automation Operator | Stored credentials, passwords |
| **Azure Function Admin Token Dump** | https://\<func\>.azurewebsites.net/admin/token | Access to Function App | Admin bearer token (can invoke functions) |
| **Azure DevOps PAT Token Extraction** | Pipeline variable dump or REST API (/personalaccesstokens) | Pipeline access or contributor | PATs scoped to Azure DevOps resources |
| **Container Instance Env Leak** | docker inspect, /proc/self/environ, or API metadata | Access to container / API | Environment secrets, SPN secrets |
| **Logic App Credential Disclosure** | View Logic App JSON definition in portal or via ARM | Reader / Contributor | Embedded creds (SMTP, API keys, etc.) |
| **Azure SQL / Cosmos DB Connection Strings** | GET /config/connectionstrings or AppSettings | Contributor / Reader | Cleartext connection strings |
| **SAS Token Exposure** | URLs with ?sig= in Blob/File/Table/Queue storage | Public sharing or misconfig | Full/partial access to storage resources |
| **Service Principal Secrets from Config** | Hardcoded in code, AppSettings, or accessible logs | File access or source control | AZURE_CLIENT_ID, AZURE_CLIENT_SECRET |
| **AAD Token Replay / Session Hijack** | Access tokens found in logs, memory, or browser cache | Local compromise / token leak | Replay into Microsoft Graph or ARM API |
| **Role Elevation via Microsoft Graph API** | RoleAssignmentScheduleRequests, PrivilegedRoleAssignmentRequests | Privileged access | Assign self privileged roles (e.g., Global Admin) |
| **Azure AD OAuth2 Abuse** | POST /oauth2/token with client credentials | Known SPN creds or misconfigured apps | Access tokens for Azure services |