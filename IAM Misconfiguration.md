# IAM Misconfigurations in Azure

Insecure identity and access management (IAM) in Azure exposes environments to significant risks. Attackers frequently target weak access controls, overprivileged roles, improperly managed credentials, and poorly maintained keys to escalate privileges and persist in a cloud
environment.

**Common Misconfigurations**

| **Category** | **Misconfiguration** | **Impact** |
|----|----|----|
| **Identity** | Excessive role assignments (e.g., Owner, Contributor to regular users or apps) | Privilege escalation, lateral movement |
| **Credentials** | Hardcoded secrets in scripts, function apps, or VM extensions | Credential theft, persistence |
| **Access Control** | Lack of role-based scoping and Just-in-Time (JIT) access | Long-term exposure to sensitive resources |
| **Privileged Accounts** | Inactive or unmonitored Global Admins or Key Vault Admins | High risk of post-exploitation |
| **Key Management** | Unrotated or mismanaged secrets in Azure Key Vault | Unauthorized data access |

## Offensive Opportunities in Pentest:

- Enumerate and exploit over-permissioned roles using:
  - az role assignment list
  - AzureHound / BloodHound for Azure
- Extract secrets from:
  - Key Vaults with list, get, or purge permissions
  - VM extensions (e.g., CustomScriptExtension)
- Target stale or shadow admin accounts that are still assigned high privileges
- Pivot through managed identities attached to services (e.g., App Services, VMs) with excessive RBAC or Microsoft Entra App roles.

## Key Principles for Azure IAM Security

| **Principle** | **PenTest Focus** |
|----|----|
| Least Privilege | Validate and exploit role sprawl in IAM -\> Role Assignments |
| Separation of Duties | Check for privilege aggregation across accounts |
| Zero Trust | Test for implicit trust relationships, unmanaged access paths |
| Risk-Based Scoring | Identify high-risk users with frequent sensitive access patterns |

## Real-World Examples

1. **CapitalOne (2019)**: AWS-based breach using EC2 instance with an
    overprivileged IAM role. Azure analog: VMs with Managed Identity and
    high-privilege access (e.g., Contributor to Subscription).

2. **SEGA Europe (2021)**: Cloud credentials exposed via public
    buckets and hardcoded values. In Azure, this is analogous to
    Function App config leaks or Storage Account exposure.

3. **Twitch, Twilio, and others (2021)**: Insider abuse of privileged
    access. In Azure, inactive or orphaned admin accounts often go
    unnoticed and can be used for post-exploitation access.

## Best Practices (Blue Team Focus)

- Enforce **JIT access** with Azure Privileged Identity Management (PIM)
- Regularly **review role assignments** and remove stale or unused accounts
- Use **Azure Key Vault with RBAC + auditing**
- Monitor high-impact permissions such as
  `(Microsoft.Authorization/roleAssignments/\*`, `Microsoft.KeyVault/\*/secrets/\*)`
- Implement **CIEM (Cloud Infrastructure Entitlement Management)** tooling for continuous access evaluation

## ⚠️ Business Impact of Poor IAM Hygiene

- Data loss or ransomware due to unauthorized access
- Cloud service disruption from insider or lateral attacks
- Legal/regulatory impact (e.g., GDPR, HIPAA violations)
- Incident response and forensic costs
- Reputation damage from breach disclosure

## Azure Identity & Secrets (PenTest-Oriented)

Unlike AWS, Azure does not use prefix-based identifiers for identities. Instead, identities and secrets are associated with structured objects in Microsoft Entra, Azure Resource Manager (ARM), and Key Vault.

## Common Azure Identity Types & What to Look For

| **Type** | **Azure Term** | **ID Format / Example** | **Use / Pentest Relevance** |
|----|----|----|----|
| **User** | Azure AD User | [<u>GUID / UPN (user@domain.com)</u>](mailto:user@domain.com) | Lateral movement, role assignments |
| **Group** | Azure AD Group | GUID | Privilege enumeration, nested group abuse |
| **Application** | App Registration / Enterprise App | App ID (Client ID) = GUID | Service principals, OAuth token abuse |
| **Service Principal** | Identity backing an app | Object ID / App ID | Target for password/symmetric key abuse |
| **Managed Identity** | System/ User-assigned Managed Identity | Object ID / Resource ID | Used by Azure resources to access other services securely |
| **Role Assignment** | Role Definition + Principal + Scope | JSON Structure | Enumerate to discover overprivileged identities |
| **Tenant** | Azure AD Tenant | GUID | Required for many MS Graph & Azure API calls |
| **Subscription** | Azure Subscription | GUID | Scope identifier; used in API calls |
| **Access Key (Storage)** | Shared Access Keys (base64) | 88-char Base64 strings | Storage exploitation, lateral movement |
| **Shared Access Signature (SAS)** | Temporary token for storage access | URL Token (signed with access key) | Exfiltration, misconfig abuse |
| **Client Secret** | App Secret (like password for apps) | GUID or base64 string | Post-exploitation: access APIs or impersonate apps |
| **Certificate** | Used by app registration / key credentials | PEM / PFX | App authentication via cert-based login |

## High-Value Tokens / Secrets to Identify in PenTest

| **Item** | **How It’s Found** | **Use Case** |
|----|----|----|
| **AZURE_CLIENT_ID** | Env var / code / web.config | OAuth flows, app impersonation |
| **AZURE_CLIENT_SECRET** | Config files / repos / Key Vault dumps | Access token generation |
| **AZURE_TENANT_ID** | Public / MS Graph / response headers | Required for token requests |
| **AZURE_SUBSCRIPTION_ID** | Code / CLI / environment | Scope operations |
| **Azure Key Vault Secrets** | Retrieved via API, CLI, or SSRF | Stealing DB creds, API keys, secrets |
| **Storage Account Keys** | Via RBAC, KeyVault, or leaked configs | Full access to blob, file, table, and queue |
| **SAS Tokens** | Captured from URLs or logs | Temporary read/write access to storage |

## Example Post-Exploitation Use

- **Enumerate app identities**:
  - az ad app list --query "\[\].{appId:appId, displayName:displayName}" --all
- **Extract secrets from Key Vault**:
  - az keyvault secret list --vault-name \<name\>
  - az keyvault secret show --vault-name \<name\> --name \<secret\>

## Azure API Calls / Operations That May Expose Credentials or Tokens 

These Azure operations can return **sensitive credentials**, **secrets**, or **access tokens** if misconfigured or abused during post-exploitation:

- **Managed Identity Token Retrieval**: Abuse of [Azure Instance Metadata Service (IMDS)](http://169.254.169.254/metadata/identity/oauth2/token) to extract access tokens for Managed Identities via SSRF, RCE, or open proxy.
- **Microsoft Entra OAuth2 Token Leaks**: APIs using oauth2/token endpoints can return access_token when scoped with correct resource (e.g., https://management.azure.com/).
- **Service Principal Credential Dumping**: If compromised or misconfigured, secrets for SPNs can be pulled from Key Vaults or environment variables.
- **Microsoft Entra SSO Token Extraction**: If browser sessions or token caches (e.g., MSAL/ADAL) are accessible via local compromise.
- **Privileged Role Assignment via Microsoft Graph API**: Abuse of RoleAssignmentScheduleRequests to assign roles and generate access.
- **Microsoft Entra Token Replay via sts/tokenorassertion injection**: Leverage access_token, id_token, or refresh_token leaks for session hijack.
- **Azure Key Vault (GetSecret / ListSecrets)**: Leaks API keys, passwords, or connection strings This requires Secret Reader role or misconfigured access policies.
- **Azure Automation Account Credential Access**: Dump credentials stored in Automation Runbooks or Variables.
- **Azure App Service AppSettings Dump**: Environment variables may contain connection strings and  credentials.
- **Azure Container Instances / AKS Env Leak**: Environment variables may hold credentials (e.g., AZURE_CLIENT_SECRET).
- **Function Apps / Logic Apps**: May expose credentials or hardcoded secrets in source or via /admin/token.
- **Azure DevOps PAT Leakage**: Abuse pipeline variables or endpoints to dump Personal Access     Tokens.
- **Storage Account Shared Access Signature (SAS) Tokens**: Misconfigured SAS URLs can expose sensitive blobs or file shares.
- **Azure SQL or Cosmos DB with leaked connection strings**: Abuse cleartext creds in config or key vault.