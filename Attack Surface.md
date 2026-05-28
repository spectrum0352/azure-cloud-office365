# Azure - Service URL Patterns for Pentesting

These are **Azure service URL formats** commonly encountered during
enumeration, misconfiguration testing, or passive recon.

## Storage & Content Delivery

- **Blob Storage -**
  https://\<account\>.blob.core.windows.net/\<container\>/\<file\>

- **File Storage -** \\\<account\>.file.core.windows.net\\share\> (SMB)

- **Queue Storage -** https://\<account\>.queue.core.windows.net/

- **Table Storage -** https://\<account\>.table.core.windows.net/

- **CDN -** https://\<cdnendpoint\>.azureedge.net/

## Compute & Networking

- **VM DNS (Public IP):** vmname.region.cloudapp.azure.com

- **App Service (Web Apps / Functions):**
  https://\<appname\>.azurewebsites.net/

- **Function App (API endpoint):**
  https://\<functionname\>.azurewebsites.net/api/\<function\>

- **Azure Container Instances (ACI):**
  https://\<container\>.region.azurecontainer.io

- **Azure Kubernetes Service (AKS):** (Typically internal unless public
  IP assigned; inspect Ingress or LoadBalancer IP)

## Database Services

- **Azure SQL Database:** tcp:\<servername\>.database.windows.net,1433

- **CosmosDB:** https://\<account\>.documents.azure.com:443/

- **MySQL/PostgreSQL/Flexible Server:**

  - mysql:\<servername\>.mysql.database.azure.com

  - postgres:\<servername\>.postgres.database.azure.com

- **Redis:** \<name\>.redis.cache.windows.net:6380

## API, Messaging, IoT

- **API Management Gateway:** https://\<apiname\>.azure-api.net/\<api\>

- **Event Hubs / Service Bus / IoT Hub**

  - sb://\<namespace\>.servicebus.windows.net/

  - mqtt://\<hubname\>.azure-devices.net:8883

  - https://\<hubname\>.azure-devices.net

- **SignalR**: https://\<resource\>.service.signalr.net

## Search, Media, Analytics

- **Azure Cognitive Search:**
  https://\<searchservice\>.search.windows.net

- **Media Services:**
  https://\<account\>.restv2.\<region\>.media.azure.net

- **Azure Monitor Logs / Application Insights (API):**
  https://api.applicationinsights.io/v1/apps/\<app_id\>

## Identity & Access

- **Azure AD Login:**
  https://login.microsoftonline.com/\<tenant_id\>/oauth2/token

- **Microsoft Graph API:** https://graph.microsoft.com/v1.0/

- **Azure AD Graph (legacy):** https://graph.windows.net/\<tenant_id\>/

## Developer Tools & Admin

- **Azure DevOps (Repos, Pipelines, Artifacts):**
  https://dev.azure.com/\<org\>/

- **Cloud Shell (browser interface):** https://shell.azure.com/

- **ARM Endpoint (for Azure Resource Manager API calls):**
  https://management.azure.com/

##  Use Cases in Pentesting:

- **Recon**: Identify public services by fuzzing known patterns
  (blob.core.windows.net, etc.).

- **SSRF**: Leverage endpoint metadata services
  (http://169.254.169.254/metadata/) or storage.

- **Privilege Escalation**: Target misconfigured function URLs or key
  vaults with public access.

- **Exfiltration**: Abuse blob storage for staging or exfil via signed
  URLs (SAS).

# Insecure Interfaces and APIs

**Summary**

These tools and techniques help in testing for:

- **Unsecured APIs and web interfaces** hosted on Azure services.

- **Misconfigured subdomains or storage endpoints**.

- **Lack of proper access controls or endpoint restrictions**, leading
  to potential data exposure or further pivoting opportunities.

Would you like me to provide automated script templates for each of
these steps?

Great — below are **automated script templates** for each of the Azure
PenTest tasks related to **Insecure Interfaces and APIs**. These can be
integrated into your playbook or automation workflows.

**🔧 1. Scan for Open Ports on Azure-Hosted Services (using
cloudhunter.py)**

**File: azure_port_scan.sh**

\#!/bin/bash

TARGET=\$1

if \[ -z "\$TARGET" \]; then

echo "Usage: \$0 http://target-url"

exit 1

fi

python3 cloudhunter.py --write-test --open-only "\$TARGET"

**Usage**: ./azure_port_scan.sh http://myapp.azurewebsites.net

**🔧 2. Azure Subdomain & Endpoint Enumeration (using cf enum)**

**File: azure_cf_enum.sh**

\#!/bin/bash

DOMAIN=\$1

if \[ -z "\$DOMAIN" \]; then

echo "Usage: \$0 \<domain\>"

exit 1

fi

cf enum "\$DOMAIN" \> "\${DOMAIN}\_cf_enum.txt"

echo "\[+\] Results saved to \${DOMAIN}\_cf_enum.txt"

**Usage**: ./azure_cf_enum.sh contoso.com

**🔧 3. Fuzz Azure API Endpoints (using ffuf)**

**File: azure_api_fuzzer.sh**

\#!/bin/bash

TARGET=\$1

WORDLIST="/usr/share/seclists/Discovery/Web-Content/api.txt"

if \[ -z "\$TARGET" \]; then

echo "Usage: \$0 https://target-url"

exit 1

fi

ffuf -w "\$WORDLIST" -u "\$TARGET/FUZZ" -mc all -o ffuf_api_results.json

echo "\[+\] Fuzzing complete. Output saved to ffuf_api_results.json"

**Usage**: ./azure_api_fuzzer.sh https://api.contoso.com

**🔧 4. Brute-Force Azure Blob Containers (Modified AWS S3 Script)**

**File: azure_blob_enum.py**

\#!/usr/bin/env python3

import requests

account_name = "contoso" \# Customize this

wordlist = "containers.txt" \# Each line: e.g., public, backup, logs

with open(wordlist) as f:

for container in f:

container = container.strip()

url =
f"https://{account_name}.blob.core.windows.net/{container}?restype=container&comp=list"

r = requests.get(url)

if "PublicAccess" in r.text or r.status_code == 200:

print(f"\[+\] Found public container: {container}")

**Usage**: python3 azure_blob_enum.py (requires a containers.txt
wordlist)

Would you like me to bundle these into a ready-to-clone GitHub repo
layout?
