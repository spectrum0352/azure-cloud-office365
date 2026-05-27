Azure-pentest-initial-attack-vectors

# Initial Access attack vector in Azure

In the context of **Azure cloud environments**, attackers may employ a
blend of traditional phishing and cloud-specific misconfigurations to
achieve **initial access**. Based on the content from your uploaded
document and Azure-specific risks, here’s a summarized and
contextualized list:

## Common Initial Access Techniques in Azure

### 1. Phishing via Third-Party Channels

- **Pretext**: Fake job offers, investor inquiries, marketing outreach.

- **Payloads**:

  - **HTML Smuggling** – Embeds malicious JS that reconstructs
    executables client-side.

  - **Office Docs** (e.g. .docm, .xll, .xsl) with **VBA macros**,
    **DotNetToJS**, or **DLL droppers**.

- **Delivery**: Avoid corporate email detection by using LinkedIn, web
  contact forms, or partner channels.

✅ **Azure Context**: Targets employees with access to Azure resources
like the Azure Portal, privileged VMs, or key vaults.

### 2. Exploitation of Azure Web Apps and Public Services

- Vulnerable **Azure App Service** (e.g., via deserialization, SSRF).

- Misconfigured **Function Apps**, especially when exposing environment
  variables or managed identity tokens.

- **Containerized malware** in **AKS** (Azure Kubernetes Service) or
  uploaded to **Azure Container Registry**.

### 3. Compromised Azure Credentials

- **Leaked API Keys**, SAS tokens, or Storage account credentials from:

  - Public GitHub/GitLab repos

  - Misconfigured Azure DevOps pipelines

- **Stolen access tokens** via MITM or phishing.

✅ **Impact**: Immediate access to services like Azure Blob Storage,
Cosmos DB, Key Vault, or VM RunCommand.

### 4. Abusing Azure AD OAuth Applications

- Malicious Azure AD OAuth applications consented via phishing.

- Abusing **multi-tenant apps** with overly broad Graph API permissions.

- Stealing **refresh tokens** or **primary refresh tokens (PRTs)** for
  long-term persistence.

✅ Seen in real-world phishing campaigns with **HTML Smuggling** + OAuth
token theft.

### 5. Initial Access via Misconfigured Services

- **Publicly exposed VMs**, Jumpboxes, or Bastion Hosts.

- **NSG misconfigurations** allowing RDP/SSH from Internet.

- **Azure Firewall** permitting egress to attacker infrastructure.

### 6. Containerized Malware in Azure Environments

- Weaponized files inside ISO/IMG/ZIP uploaded to storage accounts or
  shared via Teams/OneDrive.

- Bypasses **Mark-of-the-Web** and avoids sandboxing.

### 7. Insider or Third-Party Breaches

- Azure partners, vendors, or SaaS integrations mismanaging access
  rights.

- Overprivileged **Azure AD Guest Users**.

# Azure Initial Access Attack Vectors

In **Azure penetration testing**, gaining **initial access** typically
mirrors traditional cloud or enterprise entry points, but it's adapted
to **Azure-specific services, identity models, and configurations**.
Below is a comprehensive list of **initial access attack vectors** used
in Azure, along with how each is exploited during a PenTest.

## 1. Phishing for Azure AD Credentials

- **Technique**: Credential harvesting via fake Microsoft login pages
  (e.g., login.microsoftonline.com clone).

- **Use in Pentest**:

  - Capture Azure AD credentials.

  - Replay credentials for access to Azure Portal, Outlook, Teams, or
    Graph API.

  - MFA fatigue attacks are increasingly used with push notifications.

## 2. Leaked Credentials / Secrets

- **Sources**:

  - GitHub (e.g., leaked AZURE_CLIENT_SECRET, AZURE_STORAGE_KEY).

  - Pastebin, public S3/Git repos, old scripts.

- **Use in Pentest**:

  - Use az login --service-principal to authenticate using:

  - az login --service-principal -u APP_ID -p CLIENT_SECRET --tenant
    TENANT_ID

  - Exploit access via Azure CLI, PowerShell, or REST API.

## 3. Compromised Azure AD Tenant (Misconfigured App Registrations)

- **Technique**: Abusing over-permissive Azure AD App Registrations or
  Service Principals.

- **Use in Pentest**:

  - Impersonate applications with Application.ReadWrite.All,
    User.Read.All, etc.

  - Pivot into Graph API for lateral movement.

## 4. Misconfigured Azure Services (Public Exposure)

- **Examples**:

  - **Public Blob Containers**: Anonymous access to .core.windows.net.

  - **Function Apps / Logic Apps**: With HTTP trigger + no auth
    (anonymous or function level).

  - **App Services**: Leaked environment variables, credentials in
    web.config.

- **Use in Pentest**:

  - Enumerate with tools like AzScanner, Burp, or custom fuzzers.

  - Exploit SSRF, RCE, or code download.

## 5. Password Spraying / Brute Forcing Azure AD

- **Technique**: Spray login.microsoftonline.com with known users.

- **Use in Pentest**:

  - Tools: [MicroBurst](https://github.com/NetSPI/MicroBurst),
    [MSOLSpray](https://github.com/dafthack/MSOLSpray),
    [o365creeper](https://github.com/LMGsecurity/o365creeper).

  - Bypass conditional access if targeting non-MFA legacy auth
    (IMAP/SMTP).

## 6. OAuth Token Abuse / Malicious App Consent

- **Technique**: Trick user into consenting to a malicious Azure app
  with broad API scopes.

- **Use in Pentest**:

  - Attackers use crafted OAuth URLs:

  - https://login.microsoftonline.com/common/oauth2/v2.0/authorize?

  - client_id=\<malicious_app\>&response_type=code&redirect_uri=...&scope=...&prompt=consent

  - Gain persistent access via refresh tokens.

## 7. SSRF to Metadata Service

- **Target**: http://169.254.169.254/metadata/identity/oauth2/token

- **Use in Pentest**:

  - From SSRF-vulnerable Azure Function/App, steal Managed Identity
    tokens.

  - Impersonate services to access Key Vault or Storage.

## 8. Azure DevOps Token / PAT Theft

- **Technique**: Leaked Personal Access Tokens (PATs) or OAuth tokens
  for Azure DevOps.

- **Use in Pentest**:

  - Access repos, pipelines, agent secrets, or downstream Azure
    deployments.

## 9. Insider Access / Shared Tenant

- **Technique**: An insider or vendor has delegated access to the Azure
  AD tenant.

- **Use in Pentest**:

  - Abuse RBAC roles (e.g., Contributor) to create backdoors, dump Key
    Vault, or escalate to Owner.

## 10. Abusing External Identities (B2B / Guest Accounts)

- **Technique**: Exploit mismanaged B2B guest accounts.

- **Use in Pentest**:

  - Check if guest has too much privilege.

  - Lateral move from guest to tenant-wide data if RBAC is weak.

## 11. Malicious Extensions in Azure VMs

- **Technique**: If you can access ARM or Contributor role, inject VM
  extensions like CustomScriptExtension.

- **Use in Pentest**:

  - Execute PowerShell or shell commands as SYSTEM/root on a target VM.

## Tools Commonly Used

- **MicroBurst** – Azure enumeration & exploitation

- **ROADtools** – Token exploration & exploitation

- **TokenTactics** – OAuth abuse & Azure token operations

- **Aztuna / AzADEnum** – Azure AD user & role enumeration

- **Stormspotter / Azucar** – Attack path mapping
