# Azure PenTest

Penetration testing on Cloud environments

- Scope & Access will be more limited.
- Spell out enforced limitations in your reporting
- Cloud providers typically require an approval process be followed

Attacking Azure, AWS, or Google Cloud Deployments

- Requires preapproval by account owner (Azure and AWS)
- Standard Rules of Engagement stuff
- Limited to customer owned resources
- No DoS
- Can include attempts to break isolation (Azure)

Where is the data?

- Cloud services rely on data storage for nearly everything
- How is data stored in the cloud?
- Do I need to attack the service or is the data my real goal?

Pathfinding, recon, and targeting in multiple dimension

**How do I figure out what I even need to look at the cloud?**

## Path finding

Identifying Cloud Deployments
In the public cloud, DNS is your best friend

<img src="media/image1.png" style="width:4.3782in;height:2.35915in" />

**Cloud Recon: DNS MX Records**

- **Microsoft Office 365**: DOMAIN-COM.mail.protection.outlook.com

## Azure service URLs

<table>
<colgroup>
<col style="width: 24%" />
<col style="width: 51%" />
<col style="width: 23%" />
</colgroup>
<thead>
<tr>
<th>Azure Service</th>
<th>URL/DNS Suffix/Endpoint</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr>
<td>Azure Active Directory (AAD)</td>
<td><p>Service Endpoint Resource ID: <a
href="https://management.core.windows.net/">https://management.core.windows.net/</a></p>
<p>Authority: <a
href="https://login.microsoftonline.com/">https://login.microsoftonline.com/</a></p>
<p>Graph URL: <a
href="https://graph.windows.net/">https://graph.windows.net/</a></p></td>
<td>Authentication and directory services.</td>
</tr>
<tr>
<td>Azure Management</td>
<td><p>Management Portal URL: <a
href="https://portal.azure.com">https://portal.azure.com</a></p>
<p>Service Management URL: <a
href="https://management.core.windows.net/">https://management.core.windows.net/</a></p>
<p>Resource Manager URL: https://management.azure.com/</p></td>
<td>Core Azure management interfaces.</td>
</tr>
<tr>
<td>Azure Storage</td>
<td><p>Blob Storage: https://&lt;account&gt;.blob.core.windows.net</p>
<p>Queue Storage: https://&lt;account&gt;.queue.core.windows.net</p>
<p>Table Storage: https://&lt;account&gt;.table.core.windows.net</p>
<p>File Storage: https://&lt;account&gt;.file.core.windows.net</p></td>
<td>Storage services for various data types.</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>DNS Suffix: .database.windows.net</td>
<td>Relational database service.</td>
</tr>
<tr>
<td>Azure Key Vault</td>
<td><p>DNS Suffix: vault.azure.net&lt;br&gt;</p>
<p>Service Endpoint Resource ID: https://vault.azure.net</p></td>
<td>Secret and key management.</td>
</tr>
<tr>
<td>Azure CDN</td>
<td>Refer to documentation.</td>
<td>Content delivery network.</td>
</tr>
<tr>
<td>Azure IoT Hub</td>
<td>DNS Suffix: .azure-devices.net</td>
<td>Internet of Things hub.</td>
</tr>
<tr>
<td>Azure API Management</td>
<td>DNS Suffix: .azure-api.net</td>
<td>API management platform.</td>
</tr>
<tr>
<td>Azure Automation</td>
<td>DNS Suffix: .azure-automation.net</td>
<td>Automation and orchestration.</td>
</tr>
<tr>
<td>Azure Event Hubs</td>
<td>DNS Suffix: .servicebus.windows.net</td>
<td>Real-time event ingestion.</td>
</tr>
<tr>
<td>Azure Machine Learning</td>
<td><p>Studio: https://studio.azureml.net&lt;br&gt;</p>
<p>Gallery: https://gallery.cortanaintelligence.com/</p>
<p>Web Service Management: https://services.azureml.net</p></td>
<td>Machine learning services.</td>
</tr>
<tr>
<td>Azure Batch</td>
<td>Endpoint: https://&lt;region&gt;.batch.azure.com</td>
<td>Cloud-scale job scheduling.</td>
</tr>
<tr>
<td>Azure Service Bus</td>
<td>DNS Suffix: .servicebus.windows.net</td>
<td>Messaging service.</td>
</tr>
<tr>
<td>Azure Traffic Manager</td>
<td>DNS Suffix: trafficmanager.net</td>
<td>DNS-based traffic routing.</td>
</tr>
<tr>
<td>Azure Data Lake</td>
<td><p>Store File System Endpoint Suffix: azuredatalakestore.net</p>
<p>Analytics Catalog and Job Endpoint Suffix:
azuredatalakeanalytics.net</p></td>
<td>Big data storage and analytics.</td>
</tr>
<tr>
<td>Azure Redis Cache</td>
<td>DNS Suffix: .redis.cache.windows.net</td>
<td>In-memory data store.</td>
</tr>
<tr>
<td>Azure App Service</td>
<td>DNS Suffix: .azurewebsites.net</td>
<td>Web application hosting.</td>
</tr>
<tr>
<td>Azure Document DB (Azure Cosmos DB)</td>
<td>Endpoint: https://&lt;account&gt;.documents.azure.com</td>
<td>NoSQL database service.</td>
</tr>
</tbody>
</table>

Which one of these URL mostly used by attackers for data breach?

Attackers exploit *misconfigurations* and *vulnerabilities* related to
these URLs, not the URLs themselves. However, here are the URL patterns
most frequently associated with the vulnerabilities I described:

- **Azure Storage (Blob Storage):**

  - https://\*\<account\>\*.blob.core.windows.net/\<container\>/

  - (Especially when \<container\> is public or SAS tokens are misused)

- **Azure SQL Database:**

  - https://\*\<your-database-server\>\*.database.windows.net

  - (Direct exposure without proper firewall rules)

- **Azure Active Directory (AAD):**

  - https://login.microsoftonline.com/ (Phishing target)

- **Azure App Service:**

  - https://\*\<your-app-name\>\*.azurewebsites.net (Vulnerable web
    applications)

Important Considerations:

- **Phishing:** Attackers often create very similar-looking URLs to
  these, so users enter their credentials into fake login pages.

- **Misconfigurations are Key:** The risk is not in the URL itself, but
  in how it is secured. For example, a properly secured Blob storage URL
  is safe. A publicly accessible one is not.

- **SAS Tokens:** Shared Access Signature tokens can be appended to
  storage URLs. If these tokens are overly permissive or leaked, they
  provide unauthorized access.

- **Connection Strings:** Database connection strings that are hard
  coded into applications, or stored in insecure locations, present a
  large risk.

Therefore, while these URLs are associated with services that *can* be
vulnerable, the real focus should be on secure configurations and
practices.

When considering which Azure URLs are most frequently associated with
data breaches, it's crucial to understand that attackers primarily
exploit vulnerabilities in the *implementation* and *configuration* of
these services, rather than the URLs themselves. However, based on
available information, here are the key areas:

- **https://\<account\>\*.blob.core.windows.net (Azure Blob Storage):**

  - This is consistently highlighted as a major risk area.
    Misconfigurations, such as publicly accessible containers or leaked
    Shared Access Signature (SAS) tokens, allow attackers to easily
    access and exfiltrate sensitive data.

- **https://login.microsoftonline.com/ (Azure Active Directory):**

  - This is a prime target for phishing attacks. Attackers create fake
    login pages that mimic this URL to steal user credentials, granting
    them access to a wide range of Azure resources.

  - Also, the enumeration of information from the tenants using this URL
    structure, can give attackers valuable information for further
    attacks.

- **\*.azurewebsites.net (Azure App Service):**

  - Web applications hosted on Azure App Service are vulnerable to
    traditional web exploits like SQL injection and cross-site scripting
    (XSS).<sup>4</sup> If these applications are not properly secured,
    attackers can gain access to underlying data.

Key takeaways from my findings:

- **Misconfigurations are the primary risk:** Regardless of the URL,
  improper security settings are the root cause of most breaches.

- **Phishing is a major threat:** Attackers heavily rely on social
  engineering to obtain credentials.

- **Storage and identity are high-value targets:** Attackers prioritize
  access to data storage and user accounts.

It's important to emphasize that staying up-to-date with Azure security
best practices, implementing strong authentication, and regularly
auditing configurations are essential for mitigating these risks.

## Reconnaissance

- **Get-AzContext, Get-AzSubscription, Get-AzResourceGroup,
  Get-AzResource:**

  - These are foundational for understanding the target's Azure
    environment. They allow you to map out subscriptions, resource
    groups, and individual resources.

  - During a penetration test, this helps identify potential targets and
    understand the overall architecture.

- **Get-AzStorageAccount, Get-AzWebApp, Get-AzSQLServer,
  Get-AzSqlDatabase, Get-AzSqlServerFirewallRule,
  Get-AzSqlServerActiveDirectoryAdministrator:**

  - These commands are crucial for identifying specific services like
    storage accounts, web applications, and SQL databases.

  - They also help reveal potential vulnerabilities, such as open
    firewall rules or misconfigured access controls.

- **Get-AzAutomationAccount, Get-AzAutomationRunbook:**

  - Azure Automation Runbooks can contain sensitive information or be used for malicious purposes. Enumerating them is essential.

  - Export-AzAutomationRunbook can extract the code of the runbook for
    offline analysis.

- **Get-AzVM, Get-AzVirtualNetwork, Get-AzPublicIpAddress,
  Get-AzExpressRouteCircuit, Get-AzVpnConnection:**

  - Networking commands allow you to map the target's network
    infrastructure, including virtual machines, virtual networks, public
    IPs, and VPN connections.

  - This helps identify potential entry points and understand network
    segmentation.

- **Get-MSolCompanyInformation, Get-MSolUser, Get-MSolGroup:**

  - These MSOnline commands are used to gather information about the
    O365 tenant, including company details, user accounts, and groups.
    This is critical for understanding the target's user base and
    potential attack vectors.

**2. Authentication and Authorization:**

- **Connect-AzAccount, Connect-MsolService:**

  - These commands are used to authenticate to Azure and O365.

  - The alternative methods using Get-Credential are important for
    bypassing MFA in certain scenarios (though ethical considerations
    apply).

  - Import-AzContext and Save-AzContext are very useful for utilizing
    stolen tokens, and persisting access.

- **Get-AzRoleAssignment:**

  - This command reveals the current user's role assignments, which is
    crucial for understanding their privileges.

  - During a penetration test, it helps identify potential privilege
    escalation opportunities.

- **Select-AzSubscription:**

  - If a user has access to multiple subscriptions this allows for easy
    switching between them.

**3. Exploitation and post-exploitation:**

- **Invoke-AzVMRunCommand:**

  - This command allows you to execute commands on Azure VMs, which can be used for various purposes, including privilege escalation, data exfiltration, and installing backdoors.
  - Using PowerShell scripts with this command provides a powerful way to automate malicious actions.

- **Creating Service Principals as Backdoors:**

  - The commands provided for creating a service principal with the "Owner" role are a classic example of creating a persistent backdoor.
  - This allows an attacker to maintain access to the Azure environment even if the initial compromised account is remediated.
  - The MSOL portion of the service principal creation allows for increased permissions within the O365 environment.

- **SQL Server Manipulation:**

  - Modifying SQL server firewall rules, or adding rogue AD admins can
    provide long term access, or allow for data exfiltration.

**Ethical Considerations:**

- It is crucial to emphasize that these commands should only be used in authorized penetration testing engagements.
- Unauthorized use of these commands is illegal and unethical.
- When performing penetration testing, it is essential to have a clear scope of work and obtain explicit permission from the target organization.

- When bypassing MFA, or utilizing stolen credentials, extra care must be taken to ensure that the testing is being performed within the agreed upon scope.

**Key Takeaways for Penetration Testing:**

- **Automation:** PowerShell scripts can be used to automate many of these commands, making reconnaissance and exploitation more efficient.
- **Privilege Escalation:** Pay close attention to role assignments and identify opportunities to escalate privileges.
- **Persistence:** Focus on establishing persistent access, such as by creating service principals or modifying SQL Server configurations.
- **Data Exfiltration:** Look for ways to exfiltrate sensitive data, such as through storage accounts or SQL databases.
- **Defense Evasion:** Be aware of Azure and O365 security controls and develop techniques to bypass them.

By understanding how to use these commands, penetration testers can effectively assess the security of Azure and O365 environments.

## Cloud PenTest Tools

Catalogs: Nessus, Metasploit
Pinpoint: nmap, ettercap, hping3, curl, tcpreplay