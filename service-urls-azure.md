# Azure - Service URL Patterns for Pentesting

These are **Azure service URL formats** commonly encountered during enumeration, misconfiguration testing, or passive recon.

Azure Service URLs frequently used during attacks

Attackers often interact with legitimate Azure service endpoints during reconnaissance, credential theft, privilege escalation, data exfiltration, command-and-control operations, and persistence activities. Monitoring access to these URLs and DNS suffixes can help identify suspicious behavior.

## Use Cases

- **Recon**: Identify public services by fuzzing known patterns (blob.core.windows.net, etc.).
- **SSRF**: Leverage endpoint metadata services (`http://169.254.169.254/metadata/`) or storage.
- **Privilege Escalation**: Target misconfigured function URLs or key vaults with public access.
- **Exfiltration**: Abuse blob storage for staging or exfil via signed URLs (SAS).

These tools and techniques help in testing for:

- **Unsecured APIs and web interfaces** hosted on Azure services.
- **Misconfigured subdomains or storage endpoints**.
- **Lack of proper access controls or endpoint restrictions**, leading to potential data exposure or further pivoting opportunities.

## All

- Azure Container Instances (ACI): `https://\<container\>.region.azurecontainer.io`
- Azure Kubernetes Service (AKS): (Typically internal unless public IP assigned; inspect Ingress or LoadBalancer IP)
- CDN: `https://\<cdnendpoint\>.azureedge.net/`
- API Management Gateway: `https://\<apiname\>.azure-api.net/\<api\>`
- Event Hubs / Service Bus / IoT Hub:
  - `sb://\<namespace\>.servicebus.windows.net/`
  - `mqtt://\<hubname\>.azure-devices.net:8883`
  - `https://\<hubname\>.azure-devices.net`
- SignalR: `https://\<resource\>.service.signalr.net`
- Azure Cognitive Search:`https://\<searchservice\>.search.windows.net`
- Media Services: `https://\<account\>.restv2.\<region\>.media.azure.net`
- Azure Monitor Logs / Application Insights (API): `https://api.applicationinsights.io/v1/apps/\<app_id\>`
- Azure DevOps (Repos, Pipelines, Artifacts): `https://dev.azure.com/\<org\>/`
- ARM Endpoint (for Azure Resource Manager API calls): `https://management.azure.com/`

## Microsoft Entra ID

Common URLs

- `https://login.microsoftonline.com/tenant_id/oauth2/token`
- `https://graph.windows.net/<tenant_id>` (legacy Azure AD Graph)
- `https://graph.microsoft.com/v1.0/`
- `https://management.core.windows.net`

Attack Usage

- Credential phishing targeting Microsoft 365 and Azure users.
- Password spraying and brute-force authentication attempts.
- OAuth consent grant abuse.
- Enumeration of users, groups, applications, and service principals.
- Access token theft and token replay attacks.
- Privilege escalation through compromised administrative accounts.

## Azure Resource Manager (ARM)

- `https://management.azure.com`
- `https://portal.azure.com`

Attack Usage

- Enumeration of Azure subscriptions and resources.
- Creation of malicious resources for persistence.
- Modification of network security groups and firewall rules.
- Deployment of attacker-controlled virtual machines.
- Discovery of storage accounts, Key Vaults, and managed identities.

## Azure Cloud Shell

- `https://shell.azure.com/`

## Storage Accounts

Common Endpoints

- `https://<storage_account>.blob.core.windows.net/container/file`
- `https://<storage_account>.file.core.windows.net/share`
- `https://<storage_account>.queue.core.windows.net`
- `https://<storage_account>.table.core.windows.net`

Attack Usages

- Discovery of publicly accessible containers.
- Data exfiltration using compromised credentials or SAS tokens.
- Malware hosting within storage containers.
- Uploading malicious payloads for later execution.
- Abuse of overly permissive access keys.

High-Risk Indicators

- Anonymous blob access.
- Long-lived SAS tokens.
- Access from unusual geographic locations.
- Large-volume downloads.

## Azure SQL Database

Common Endpoint

- `https://<server>.database.windows.net`
- `tcp:<servername>.database.windows.net,1433`

Attack Usage

- Credential stuffing against exposed databases.
- Exploitation of weak firewall configurations.
- Data theft from misconfigured databases.
- Unauthorized administrative access.

High-Risk Indicators

- Databases exposed to the Internet.
- Excessive failed login attempts.
- Unexpected outbound data transfers.

## Key Vault

Common Endpoint

- `https://<vault-name>.vault.azure.net`

Attack Usage

- Theft of secrets, certificates, and encryption keys.
- Credential harvesting for lateral movement.
- Extraction of application secrets and API keys.
- Abuse of excessive permissions granted to service principals.

High-Risk Indicators

- Secret enumeration activity.
- Bulk secret retrieval operations.
- Access from unfamiliar IP addresses.

---

## Azure App Service

Common Endpoint

- `https://<appname>.azurewebsites.net`

Attack Usage

- Exploitation of vulnerable web applications.
- Web shell deployment.
- Remote code execution attacks.
- Credential theft through compromised applications.

High-Risk Indicators

- Suspicious file uploads.
- Unexpected deployment activities.
- Outbound connections to unknown domains.

## Function apps

Common Endpoints

- `https://<functionname>.azurewebsites.net/api/<function>`

## Azure Cosmos DB

Common Endpoint

- `https://<account>.documents.azure.com`
- `https://\<account\>.documents.azure.com:443/`

## MySQL/PostgreSQL/Flexible Server

- `mysql:<servername>.mysql.database.azure.com`
- `postgres:<servername>.postgres.database.azure.com`

## Azure Redis Database

Common Endpoints

- `https://<name>.redis.cache.windows.net:6380`

Attack Usage

- Data theft through exposed keys.
- Exploitation of misconfigured access controls.
- Unauthorized database enumeration.

## Service Bus and Event Hubs

Common Endpoint

- `*.servicebus.windows.net`

Attack Usage

- Interception or abuse of messaging infrastructure.
- Data exfiltration through message queues.
- Persistence through compromised applications.

## Azure Automation

Common Endpoint

- `*.azure-automation.net`

Attack Usage

- Creation of malicious runbooks.
- Scheduled execution of attacker-controlled scripts.
- Persistence through automation tasks.

## Azure API Management

Common Endpoint

- `*.azure-api.net`

Attack Usage

- Discovery of exposed APIs.
- Abuse of weak authentication controls.
- API key theft.
- Data extraction through compromised APIs.

## Azure IoT Hub

Common Endpoint

- `*.azure-devices.net`

Attack Usage

- Compromise of IoT devices.
- Device impersonation.
- Command injection against connected devices.

---

## Azure Data Lake

Common Endpoints

- `*.azuredatalakestore.net`
- `*.azuredatalakeanalytics.net`

Attack Usage

- Unauthorized access to large datasets.
- Data exfiltration.
- Reconnaissance of sensitive information repositories.

## Azure Redis Cache

Common Endpoint

- `*.redis.cache.windows.net`

Attack Usage

- Access to cached credentials and session data.
- Information disclosure through misconfigured caches.
- Application compromise through stolen session tokens.

## Azure Batch

Common Endpoint

- `https://<region>.batch.azure.com`

Attack Usage

- Abuse of compute resources for cryptocurrency mining.
- Execution of malicious workloads.
- Large-scale automated attacks.

## Virtual machine

- **VM DNS (Public IP):** vmname.region.cloudapp.azure.com

## Threat Hunting Recommendations

Monitor connections, authentication attempts, and API activity involving:

- `login.microsoftonline.com`
- `management.azure.com`
- `graph.microsoft.com`
- `*.blob.core.windows.net`
- `*.vault.azure.net`
- `*.database.windows.net`
- `*.azurewebsites.net`
- `*.servicebus.windows.net`
- `*.documents.azure.com`

Particular attention should be paid to:

- Unusual authentication patterns.
- Access from unfamiliar countries or IP addresses.
- Excessive use of SAS tokens.
- Secret retrieval from Key Vault.
- Large data transfers from Storage Accounts or Cosmos DB.
- Creation of new resources through Azure Resource Manager APIs.
- OAuth application consent grants.
- Service principal creation and privilege assignments.

These URLs themselves are legitimate Microsoft Azure services; the security concern arises when attackers abuse compromised credentials, misconfigurations, exposed secrets, or vulnerable applications to access them.
