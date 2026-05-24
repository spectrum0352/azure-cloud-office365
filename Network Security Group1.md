# Network Security Groups

Azure NSGs are used to filter network traffic to and from resources in
an Azure virtual network

Subnet level network and application access control

## NSG Limits

limits are applied per region per subscription:

- 5000 NSGs per subscription

- 1000 Rules per NSG

- 4000 IP’s or ranges specified per NSG

>  

## NSG Rules Components

- Name: name with purpose of NSG rule

- Priority rang is 100-4096. Low number processed before higher

- Source: Any IP address or CIDR or Service tag or Application security
  group

- Destination: Any or IP address or CIDR or Service tag or Application
  security group

- Protocol: TCP, UDP, ICMP, SMTP, SSH, RDP, FTP, or any

- Direction: Inbound or Outbound

- Port Range: Individual or range of ports, 22, 3389, 100-110

- Action: Allow or Deny

 

<table style="width:75%;">
<colgroup>
<col style="width: 7%" />
<col style="width: 6%" />
<col style="width: 12%" />
<col style="width: 7%" />
<col style="width: 12%" />
<col style="width: 11%" />
<col style="width: 5%" />
<col style="width: 4%" />
<col style="width: 6%" />
</colgroup>
<thead>
<tr>
<th>Rule Name</th>
<th>Priority</th>
<th>Source</th>
<th>Source Port</th>
<th>Destination</th>
<th>Destination Port</th>
<th>Protocol</th>
<th>Access</th>
<th>Direction</th>
</tr>
</thead>
<tbody>
<tr>
<td>Name</td>
<td>100-4096</td>
<td><p>Any,</p>
<p>IP/CIDR,</p>
<p>Service Tag,</p>
<p>App security group</p></td>
<td>0-65535</td>
<td><p>Any,</p>
<p>IP/CIDR,</p>
<p>Service Tag,</p>
<p>App security group</p></td>
<td>0-65535</td>
<td><p>Any,</p>
<p>TCP,</p>
<p>UDP,</p>
<p>ICMP</p></td>
<td><p>Allow,</p>
<p>Deny</p></td>
<td><p>Inbound,</p>
<p>Outbound</p></td>
</tr>
</tbody>
</table>

## NSG Workflow

> <img src="media/image1.png" style="width:6.13957in;height:2.89583in" />
>
>  
>
>  

## Default NSG Rules

Inbound Rules:

| Rule Name | Priority | Source | Source Port | Destination | Destination Port | Protocol | Access |
|----|----|----|----|----|----|----|----|
| AllowVNetInBound | 65000 | VirtualNetwork | 0-65535 | VirtualNetwork | 0-65535 | Any | Allow |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | 0-65535 | 0.0.0.0/0 | 0-65535 | Any | Allow |
| DenyAllInbound | 65500 | 0.0.0.0/0 | 0-65535 | 0.0.0.0/0 | 0-65535 | Any | Deny |

Outbound Rules

| Rule Name | Priority | Source | Source Port | Destination | Destination Port | Protocol | Access |
|----|----|----|----|----|----|----|----|
| AllowVNetOutBound | 65000 | VirtualNetwork | 0-65535 | VirtualNetwork | 0-65535 | Any | Allow |
| AllowInternetOutBound | 65001 | 0.0.0.0/0 | 0-65535 | Internet | 0-65535 | Any | Allow |
| DenyAllOutbound | 65500 | 0.0.0.0/0 | 0-65535 | 0.0.0.0/0 | 0-65535 | Any | Deny |

>  

## Sample NSG Rules 

Network rule collection group

- Priority: 100

- Rule collection action: Allow

<table style="width:76%;">
<colgroup>
<col style="width: 4%" />
<col style="width: 11%" />
<col style="width: 16%" />
<col style="width: 14%" />
<col style="width: 7%" />
<col style="width: 11%" />
<col style="width: 9%" />
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Source type</th>
<th>Source</th>
<th>Protocol</th>
<th>Ports</th>
<th>Destination type</th>
<th>Destination</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rule-1</td>
<td>IP/CIDT/IP group</td>
<td><p>*, 10.0.0.0,</p>
<p>172.16.0.0</p></td>
<td>TCP, UDP, ICMP, Any</td>
<td>80, 150-155</td>
<td><p>IP/CIDR/IP group</p>
<p>Service tag/FQDN</p></td>
<td><p>*, 10.0.0.0,</p>
<p>172.16.0.0/24</p></td>
</tr>
<tr>
<td>Test-1</td>
<td>IP_Address</td>
<td>10.0.0.0</td>
<td>TCP</td>
<td>80</td>
<td>IP address</td>
<td></td>
</tr>
<tr>
<td>Test-2</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td>TCP</td>
<td>443</td>
<td>Service tag</td>
<td></td>
</tr>
<tr>
<td>Test-3</td>
<td>IP_Address</td>
<td>10.0.0.0</td>
<td>UDP</td>
<td>150</td>
<td>IP Group</td>
<td></td>
</tr>
<tr>
<td>Test-4</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td>UDP</td>
<td>135</td>
<td>FQDN</td>
<td></td>
</tr>
</tbody>
</table>

Application rule collection group

- Priority: 101

- Action: Allow

<table style="width:83%;">
<colgroup>
<col style="width: 4%" />
<col style="width: 11%" />
<col style="width: 16%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 14%" />
<col style="width: 17%" />
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Source type</th>
<th>Source</th>
<th>Protocol</th>
<th>TLS Inspection</th>
<th>Destination type</th>
<th>Destination</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rule-1</td>
<td>IP/CIDR/IP group</td>
<td>*, 10.0.0.0, 172.16.0.0</td>
<td><p>HTTP/HTTPS,</p>
<p>FTP/FTPS</p>
<p>RDP/SSH</p></td>
<td>80, 150-155</td>
<td><p>FQDN/FQDN tag</p>
<p>Web URL/Categories</p></td>
<td>*, 10.0.0.0, 172.16.0.0/24</td>
</tr>
<tr>
<td>Test-1</td>
<td>IP_Address</td>
<td>10.0.0.0</td>
<td></td>
<td>80</td>
<td>FQDN</td>
<td>*.microsoft.com</td>
</tr>
<tr>
<td>Test-2</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td></td>
<td>443</td>
<td>FQDN tag</td>
<td></td>
</tr>
<tr>
<td>Test-3</td>
<td>IP_Address</td>
<td>10.0.0.0</td>
<td></td>
<td>150</td>
<td>URL</td>
<td><a href="http://www.microsoft.com/">www.microsoft.com</a></td>
</tr>
<tr>
<td>Test-4</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td></td>
<td>135</td>
<td>Web Categories</td>
<td></td>
</tr>
</tbody>
</table>

DNAT rule collection group

DNAT stands for Destination Network Address Translation.

- Priority:

- Action: Allow

<table>
<colgroup>
<col style="width: 3%" />
<col style="width: 9%" />
<col style="width: 14%" />
<col style="width: 4%" />
<col style="width: 9%" />
<col style="width: 9%" />
<col style="width: 15%" />
<col style="width: 8%" />
<col style="width: 16%" />
<col style="width: 8%" />
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Source type</th>
<th>Source</th>
<th>Protocol</th>
<th>Destination port</th>
<th>Destination type</th>
<th>Destination</th>
<th>Translated type</th>
<th>Translated address or FQDN</th>
<th>Translated port</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>IP/CIDR/ IP group</td>
<td><p>*, 10.0.0.0,</p>
<p>172.16.0.0</p></td>
<td><p>HTTP</p>
<p>RDP</p>
<p>FTP</p>
<p>SMTP</p></td>
<td>80, 150-155</td>
<td>IP address, FQDN</td>
<td><p>*, 10.0.0.0,</p>
<p>172.16.0.0/24</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>1</td>
<td>IP Address</td>
<td>10.0.0.0</td>
<td></td>
<td>80</td>
<td>IP address</td>
<td>172.16.0.0</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>2</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td></td>
<td>443</td>
<td>IP address</td>
<td>172.16.0.0</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>3</td>
<td>IP Address</td>
<td>10.0.0.0</td>
<td></td>
<td>150</td>
<td>FQDN</td>
<td>*.microsoft.com</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td>4</td>
<td>IP Group</td>
<td>ipgroup-oracleappserver</td>
<td></td>
<td>135</td>
<td>FQDN</td>
<td>*.microsoft.com</td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Logging and Monitoring

## Design and Implementation

How to design and implement NSG and ASG?

## Application Security Group

What is ASG and how to design and implement ASG?

## Azure Policy

- Adaptive network hardening recommendations should be applied on
  internet facing virtual machines

- All Internet traffic should be routed via your deployed Azure Firewall

- All network ports should be restricted on network security groups
  associated to your virtual machine

- Azure Firewall Led the security assessment of azure security services
  such as Azure Firewall

<!-- -->

- Configure diagnostic settings for Azure Network Security Groups to Log
  Analytics workspace

- Configure network security groups to enable traffic analytics

- Configure network security groups to use specific workspace for
  traffic analytics

- Deploy a flow log resource with target network security group

<!-- -->

- Finding the most efficient way to implement firewall policies across
  Contoso's multiple Azure regions.

<!-- -->

- Flow logs should be enabled for every network security group

- Gateway subnets should not be configured with a network security group

<!-- -->

- Internet-facing virtual machines should be protected with Network
  Security Groups

- IP Forwarding on your virtual machine should be disabled

- Management ports of virtual machines should be protected with
  just-in-time network access control

- Management ports should be closed on your virtual machines

<!-- -->

- Network Watcher flow logs should have traffic analytics enabled

<!-- -->

- Non-internet-facing virtual machines should be protected with network
  security groups

- NSG Led the security assessment of azure security services such as
  network security groups,

- Secured Virtual Hubs and Hub Virtual Networks.

- Subnets should be associated with a Network Security Group

- Virtual network design considerations and configuration options for
  Azure Active Directory Domain Services

Understand Azure Private Link:
<https://docs.microsoft.com/azure/private-link/private-link-overview>

Security architecture:
<https://docs.microsoft.com/azure/cloud-adoption-framework/organize/cloud-security-architecture>

## Best practices
