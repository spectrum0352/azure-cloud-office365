To secure cloud environments, consider these key categories and tools:

- Digital Workspace Security:

  - Secure collaboration platforms (Microsoft 365, Google Suite, Teams,
    Zoom) using native controls and potentially CASB solutions.

- Cloud Access Security Broker (CASB):

  - Gain visibility and control over SaaS applications (sanctioned and
    unsanctioned).

  - Tools: Skyhigh Security, Microsoft Defender for Cloud Apps.

- Cloud Workload Protection Platform (CWPP):

  - Secure cloud data centers and workloads without hindering agility.

  - Tools: Microsoft Defender for Cloud, Prisma Cloud, Aqua Security,
    CrowdStrike Falcon.

- Cloud Security Posture Management (CSPM):

  - Assess and improve the overall security posture of cloud
    environments.

  - Tools: CloudGuard (Check Point), Azure Security Center, AWS Security
    Hub, Google Cloud Security Command Center, Lacework.

- Cloud Data Security:

  - Control data access, location, and encryption keys.

  - Tools: Azure Key Vault, AWS KMS, Entrust, Thales.

- Cloud Identity and Access Management (IAM) and Identity Entitlement
  Management (IEM):

  - Manage user access and permissions.

  - Tools: Microsoft Entra, Saviynt, CyberArk, SailPoint, Orca.

- Cloud Application Security:

  - Secure the DevOps pipeline.

  - tools: Azure Devops, Github, Atlassian.

- Monitoring and Threat Detection:

  - End to end visibility of infrastructure and applications, and threat
    detection.

  - Tools: Dynatrace, Datadog, New Relic.

<!-- -->

- Cloud Access Security Broker (CASB)

- Cloud Identity and Entitlement Management (CIEM)

- Cloud Native Application Protection Platform (CNAPP)

- Cloud Security Posture Management (CSPM)

- Cloud Workload Protect Platform (CWPP)

- SaaS Security Posture Management (SSPM)

- Secure Web Gateway (SWG)

- Security Service Edge (SSE)

- Zero Trust Network Access (ZTNA)

**Security in the Cloud**

- **Focus:** Primarily concerned with safeguarding data and applications
  within the cloud environment.

- **Responsibilities:** Shared between the cloud provider and the
  organization using the cloud.

- **Examples of measures:**

  - Encryption of data at rest and in transit

  - Strong authentication and access controls

  - Vulnerability management and patching

  - Network security measures

## CSPM

- Security posture is a reference to the cybersecurity strength of an
  organization, which includes an assessment of its ability to detect
  and respond to security threats. Security posture encompasses
  readiness for both external and internal threats, as well as response
  and remediation capabilities.

- **Cloud Governance & Compliance**

  - Framework and regulatory compliance packs

  - Automatic and scheduled reporting

- **Asset Discovery & Identification**

  - Asset discovery

  - Risk assessment, prioritization, and remediation support

  - Automatic remediation

- **Cloud Threat Protection**

  - Applying a single, unified policy across all public clouds

  - Continuous behaviour monitoring

  - Implementing guardrails while maintaining speed and flexibility of
    Cloud

- **Cloud Data Protection**

  - Security & Privacy by Design

  - Cloud encryption

  - DLP

- **DevSecOps**

  - Support for CI/CD integration by shifting security left

  - API enablement

  - Ensuring that IaC templates are not vulnerable

<img src="media/image1.png" style="width:5.78814in;height:3.89167in" />

## CWPP

CWPP stands for Cloud Workload Protect Platform

- Cloud Workload Protection Platform (CWPP) is a workload-centric
  security product that protect server workloads in hybrid, multi-cloud,
  and data center environments.

- Provide consistent visibility and control for physical machines,
  virtual machines (VMs), containers and serverless workloads,
  regardless of location.

- Protect workloads using a combination of system integrity protection,
  application control, behavioural monitoring, intrusion prevention and
  optional anti-malware protection at runtime.

- CWPP offerings should also include scanning for workload risk
  proactively in the development pipeline.

<img src="media/image2.png" style="width:9.70906in;height:1.475in" />

<img src="media/image3.png" style="width:6.71698in;height:2.96667in" />

CWPP Risk Based Hierarchy

<img src="media/image4.png" style="width:8.68954in;height:4.09167in" />

## CIEM

- Cloud Infrastructure Entitlement Management (CIEM) is a cloud security
  solution used to manage identities and cloud permissions through the
  principle of least privilege (POLP).

- CIEM uses machine learning and analytics to detect anomalies in
  account permissions within multi-cloud environments. This visibility
  enables organizations to apply consistent identity access management
  (IAM) across their cloud services to mitigate cyber threats, such as
  data breaches and data exfiltration

- CIEM solutions are delivered through a software-as-a-service (SaaS)
  model, alongside other cloud security solutions, such as Cloud
  Security Posture Management (CSPM) and Cloud Access Service Brokers
  (CASBs).

**CIEM Benefits**

- Granular Cross Cloud Visibility of cloud entitlements from a Single
  Dashboard

- Stronger Overall Security Posture

- Enforce principle of least privilege

- Uncover the unused permission risk

- Monitor, detect & remediate anomalies

- Empower your DevOps team with the needed speed & agility

<img src="media/image5.png" style="width:9.69306in;height:2.11597in" />

**CIEM Lifecycle**

- **Discovery**: Provide granular visibility of cloud identities and
  their entitlements, in line with cloud-based activity on a continuous
  basis:

  - Non-Human /workloads Identity (services, compute instances, data
    stores, secrets)

  - Cloud policies (IAM policies, resource policies, permissions
    boundaries, ACLs)

  - Native and federated identities (On-Prem AD, Okta, Ping)

- **Correlation**: As cloud providers uses different mechanisms and
  terminology to address permissions, CIEM should have ability to
  correlate entitlements across CSPs

- **Visualization**: Provide ability to visualize and understand the
  access available to a given identity in tabular or visual format, to
  filter and search, and to view metrics and scores that help quantify
  the risk

  - visualize all identities that have access to a confidential
    resource/data

  - all permissions assigned to a given role

- **Entitlement Optimization:** Provide ability to continuously remove
  excessive permissions and reduce the attack surface of cloud
  environment.

  - Enforces strict access control via principle of least privileges.

  - Uses advanced analytics to understand which permissions are being
    used, and to assess the risk level of unused permissions and ensures
    identities have just enough entitlements to do their job and nothing
    more

- **Protection**: Detect when privileges are changed and alert the
  changes

  - Changes to entitlement/privilege could indicate a threat (e.g.
    privilege escalation).

  - Provide configurable rulesets that enable you to define the
    entitlement guardrails to be enforced.

  - Ensures IAM compliance with CIS, GDPR, SOC2, NIST, PCI DSS, ISO

- **Detection**: Provide continuous monitoring of resources and policies
  to detect suspicious activity

  - Indicates an external threat or an internal human error.

  - Configure rules to stream data to a SIEM or UEBA platform as per
    organization policy

- **Remediation**: CIEM solutions support multiple means of remediation.
  Organizations have different processes for managing entitlements

  - A new remediation policy can be sent directly to the cloud provider
    via API, or to a ticketing system or IGA system for fulfilment.

<!-- -->

- For DevOps teams, remediation can be handled as part of the pipeline
  using IaC platforms.

## CNAPP

CNAPP stands for Cloud Native Application Protection Platform

**Hybrid/Multi-Cloud Security Challenges**

- **Decentralized Administration & Lack of Visibility:**

  - No CMDB, real-time asset inventory or network topology diagrams
    exist for public cloud

  - Large number of privileged users with little governance

  - Traditional security is focused on Infrastructure built in house

  <!-- -->

  - **Complexity of Compliance Management in the Cloud:**

    - Hundreds of unique cloud services, with more added daily

    - Proving compliance to auditors challenging in dynamic environments

    - People and companies move to a greater and greater use of Cloud
      they need to be more fluid and rapid to reduce risk

  - **Inability to Rapidly Detect & Respond to Threats**

    - Data that is created natively in the cloud is invisible to
      traditional security measures

    - Traditional SIEMs do not have cloud context, and are unable to
      adapt to large data volumes and speed of change in cloud

    - Network security fails to protect data in the cloud and mobile era

-  

  - Are my Apps & Data Secure?

  - Am I compliant?

  - What do I have in the cloud?

  - What was historical behaviour seen?

  - Are my hosts & containers secure?

  - What is happening?

  - Who is making changes & why?

  - Are my apps & data secure?

## CASB

**CASB stands for Cloud Access Security Broker**

CASB is an on-premises, or cloud-based security policy enforcement
points, placed between cloud service consumers and cloud service
providers to combine and interject enterprise security policies as the
cloud-based resources are accessed. CASBs consolidate multiple types of
security policy enforcement.

CASB Security Policies include:

- Authentication

- Single sign-on

- Authorization

- Credential mapping

- Device profiling

- Encryption

- Tokenization

- Logging & alerting

- Malware detection/prevention

- Primarily aimed at protecting Software as a Service (SaaS) application
  in the cloud

- Have limited capability to support PaaS & IaaS

CASB Features

- **Visibility:**

  - Shadow IT detection

  - SaaS Usage Tracking

  - Risk Visibility

- **Compliance**:

  - Regulatory requirements

  - Compliance & Risk Assessment

  - Reporting & Orchestration

- **Threat Protection:**

  - User & Entity Behaviour Analytics

  - Malware Detection

  - Activity Monitoring

  - Block unsanctioned cloud apps

  - Define adaptive access policies.

- **Data Security**

  - Encryption

  - Tokenization

  - Data Loss Prevention

  - Configuration Audit

  - Access Control

Shadow IT use cases:

- Discover cloud services in use Regular report such as TOP 10 risky
  services in use

- Assess cloud service risk Continuous tuning to mark reliable services

- Detect data exfiltration and proxy leakage Detection of malware
  operating on the enterprise network

- Applying Cloud governance policies Automatically block selected Shadow
  IT cloud based on agreed Criteria

Sanctioned cloud use cases:

- Forensic Investigation Capture an audit trail of user activity

- Detect threats Compromised accounts, insiders, and privileged users

- Enforce collaboration policies Data shared from cloud services

- Set up the same security policies Enforce on-premises DLP solution
  policies

- Prevent cloud data mis usage Detect and remediate malware

- Higher security for supported apps Encrypt data stored in the cloud

<img src="media/image6.png" style="width:6.89591in;height:4.48466in" />

## SSPM

SSPM (SaaS Security Posture Management)

Definition: SSPM is an automated, continuous process for monitoring
cloud-based SaaS applications. It aims to minimize security risks by
identifying and correcting misconfigurations, preventing configuration
drift, and ensuring compliance.

- Key Functions:

  - Visibility: Provides a centralized view of all SaaS applications
    used within an organization.

  - Policy Enforcement: Detects risky configurations by comparing them
    to security best practices and industry standards.

  - Alerting: Generates security alerts for misconfigurations and policy
    deviations.

  - Remediation: Offers automated workflows and recommendations to
    address security risks and misconfigurations.

- Benefits:

  - Simplifies compliance management.

  - Prevents cloud misconfigurations.

  - Detects and manages excessive permissions.

## SASE

SASE stands for Security Access Service Edge.

Secure Access Service Edge (SASE) consists of two distinct components
given below

Security Service Edge that provides network security as a service

WAN edge that provides network as a service

<img src="media/image7.png" style="width:5in;height:1.88333in" />

## Secure Web Gateway (SWG)

A secure web gateway (SWG) is a security solution that prevents
unsecured internet traffic from entering an organization’s internal
network. It is used by organizations globally to protect employees and
users from accessing or being infected by malicious websites. It also
helps to ensure regulatory compliance.

According to Gartner, a secure web gateway must, at a minimum, include
URL filtering, malicious code detection and filtering, and application
controls for popular cloud applications such as Microsoft 365. An SWG is
designed to block access to or from malicious websites and links. It
enforces granular use policies and stops threats from accessing web
applications by acting as a security gateway, and it does so by
filtering web and internet traffic at the application level.

<img src="media/image8.png" style="width:5.90347in;height:3.16356in" />

## SASE vs SWG vs Firewall vs WAF

| Feature | SASE | SWG | Firewall | WAF |
|----|----|----|----|----|
| Purpose | Combines network and security functions (SWG, FWaaS, CASB, ZTNA, SD-WAN) into a cloud-delivered service, providing secure access to applications and data from anywhere. | Filters unwanted software and internet traffic, enforcing corporate and regulatory policies for web traffic. | Monitors and controls network traffic based on security rules, acting as a barrier between trusted and untrusted networks. | Protects web applications by filtering and monitoring HTTP/HTTPS traffic, defending against application-layer attacks. |
| Scope | Broad: Encompasses network and security. | Web traffic. | Network traffic. | Web application traffic (HTTP/HTTPS). |
| Layer | Cloud-delivered; encompasses multiple layers. | Application layer (Layer 7). | Network layers (Layers 3, 4, and 7 in NGFWs). | Application layer (Layer 7). |
| Focus | Secure and optimized access to applications and data, regardless of location. | Web security, policy enforcement, and threat prevention. | Network perimeter security and traffic control. | Web application vulnerability protection. |
| Key Functions | Cloud-delivered security, SD-WAN integration, Zero Trust, global reach. | URL filtering, malware scanning, application control, DLP. | Network traffic filtering, access control, NAT. | Application-layer traffic filtering, protection against web application vulnerabilities. |
| Deployment | Cloud-based. | Cloud-based or on-premises. | On-premises, cloud-based, or hybrid. | Cloud-based, on-premises, or as a service. |
| Integration | Integrates many network security functions. | Often a part of a SASE architecture. | Can be a part of the SASE architecture via FWaaS. | Can work alongside SASE, and SWG solutions. |
