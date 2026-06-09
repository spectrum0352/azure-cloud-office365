# Contents

[Introduction [1](#introduction)](#introduction)

[Shared responsibility model
[1](#shared-responsibility-model)](#shared-responsibility-model)

[Security of the Cloud
[4](#security-of-the-cloud)](#security-of-the-cloud)

[Physical Security [4](#physical-security)](#physical-security)

[Virtualization Security
[5](#virtualization-security)](#virtualization-security)

[Business Continuity [6](#business-continuity)](#business-continuity)

[Disaster Recovery [6](#disaster-recovery)](#disaster-recovery)

[Core Connectivity Security
[7](#core-connectivity-security)](#core-connectivity-security)

[API/Management Plane Security
[7](#apimanagement-plane-security)](#apimanagement-plane-security)

[Security in the Cloud
[8](#security-in-the-cloud)](#security-in-the-cloud)

[Cloud Identity [8](#cloud-identity)](#cloud-identity)

[Cloud Security Products
[9](#cloud-security-products)](#cloud-security-products)

[QnA [9](#qna)](#qna)

# Introduction

## Shared responsibility model

**Cloud vs. On-Premises Security**

While both cloud and on-premises environments require robust security
measures, there are distinct differences in how security controls are
implemented and managed.

**Shared Responsibility Model**

- **Cloud:** Security is a shared responsibility between the cloud
  provider and the customer. The provider is responsible for securing
  the underlying infrastructure, while the customer is responsible for
  securing their applications and data.  

- **On-premises:** The organization is solely responsible for all
  aspects of security, including hardware, software, network, and data.

**Dynamic Infrastructure**

- **Cloud:** Infrastructure can be rapidly scaled up or down, requiring
  dynamic security controls.

- **On-premises:** Infrastructure changes are typically slower, allowing
  for more static security configurations.

**Security as a Service**

- **Cloud:** Many security services (e.g., WAF, SIEM, IAM) are offered
  as managed services, reducing the operational burden.

- **On-premises:** Organizations must manage and maintain these services
  in-house.

**Compliance and Regulations**

- **Cloud:** Cloud providers often offer compliance certifications
  (e.g., SOC 2, HIPAA, GDPR) to simplify customer compliance efforts.

- **On-premises:** Organizations must ensure compliance with regulations
  independently.

**Attack Surface**

- **Cloud:** The distributed nature of cloud environments can increase
  the attack surface, requiring more comprehensive security measures.

- **On-premises:** Security controls can be more focused on the physical
  perimeter and internal network.

**Specific Control Differences**

| **Security Control** | **Cloud** | **On-premises** |
|----|----|----|
| Network Segmentation | Virtual Networks (VNETs), subnets, NSGs | Physical network segmentation, firewalls |
| IAM | Cloud-based identity providers, role-based access control | On-premises identity stores, access controls |
| Data Protection | Encryption, key management, data loss prevention | Encryption, backup, access controls |
| Threat Detection and Response | Cloud-native SIEM, threat intelligence | Traditional SIEM, intrusion detection systems |

In summary, while the fundamental principles of security remain
consistent, the cloud introduces unique challenges and opportunities. By
understanding these differences, organizations can effectively protect
their assets in both environments.

How to conduct azure cloud security risk assessment?

Can you give me a brief overview of you cloud security solution**?**
Explaining your solution to non-tech peoples.

Can you name a few recent security breaches**?** Name a few types of
security breaches.

Shared Responsibility Model:

The shared responsibility model in cloud computing defines the security
responsibilities between the cloud provider and the customer.
Essentially, the provider is responsible for securing the
*infrastructure* (the "cloud itself"), while the customer is responsible
for securing *what they put in the cloud* (data, applications, operating
systems, network configurations). The specific division of
responsibility varies depending on the service model (IaaS, PaaS, SaaS).

- **IaaS (Infrastructure as a Service):** The provider manages the
  physical infrastructure (servers, networking, storage). The customer
  is responsible for securing everything else, including operating
  systems, applications, and data.

- **PaaS (Platform as a Service):** The provider manages the underlying
  infrastructure and the platform (operating systems, middleware). The
  customer is responsible for securing their applications and data.

- **SaaS (Software as a Service):** The provider manages everything,
  including the application, infrastructure, and data. The customer's
  responsibility is limited to managing user accounts and data within
  the application.

Public vs. Private Cloud Considerations

When choosing between public and private cloud, key considerations
include:

- **Cost:** Public cloud often has lower upfront costs and operates on a
  pay-as-you-go model. Private cloud requires significant capital
  expenditure for hardware and infrastructure.

- **Scalability:** Public cloud offers greater scalability and
  elasticity, allowing resources to be easily scaled up or down as
  needed. Private cloud scalability can be more limited and require
  planning.

- **Security:** While public cloud providers invest heavily in security,
  the shared responsibility model means you're still responsible for
  securing your own data and applications. Private cloud offers more
  control over security, but it's your responsibility entirely.

- **Control:** Private cloud provides greater control over
  infrastructure and customization. Public cloud offers less control but
  simplifies management.

- **Compliance:** Certain industries with strict regulatory requirements
  may lean towards private cloud for greater control over data
  governance. Public cloud providers offer various compliance
  certifications, but you must still ensure your usage meets those
  standards.

- **Management:** Public cloud often simplifies management with
  provider-managed services. Private cloud requires dedicated IT staff
  for maintenance and administration.

- **Availability/Reliability:** Both public and private cloud can offer
  high availability, but public cloud providers often have more robust
  infrastructure.

Cloud Environment Security Monitoring Tools:

- Examples: Microsoft Defender for Cloud, Azure Security Center, AWS
  CloudTrail, Google Cloud Security Command Center. (These are examples;
  there are many others.)

Advantages of Cloud-Based Databases:

- Scalability: Easily adjust storage and compute resources.

- Cost-effectiveness: Pay-as-you-go pricing, reducing upfront
  infrastructure costs.

- High Availability and Disaster Recovery: Built-in redundancy and
  failover capabilities.

- Accessibility: Access data from anywhere with an internet connection.

- Security: Cloud providers invest heavily in security measures.

- Automation: Streamlined maintenance and updates.

# Security of the Cloud 

- Physical Security (Facility/Datacentres)

- Hardware Security

- Abstraction/Virtualization Security

- API/Management Plane Security

- Core Connectivity Security

- Business Continuity

- Disaster Recovery

**Differentiating Security in the Cloud vs. Security of the Cloud**

While the terms "security in the cloud" and "security of the cloud" may
seem interchangeable, they represent distinct concepts.

**In essence, "security in the cloud" is about protecting your data and
applications within the cloud environment, while "security of the cloud"
is about ensuring the underlying cloud infrastructure is secure.**

**Key differences and considerations:**

- **Shared responsibility model:** In most cloud environments, there is
  a shared responsibility between the cloud provider and the
  organization using the cloud. The cloud provider is responsible for
  the security of the cloud infrastructure, while the organization is
  responsible for the security of their data and applications within the
  cloud.

- **Compliance:** Cloud providers often need to comply with various
  security standards and regulations. Organizations using the cloud
  should ensure that the cloud provider meets their specific compliance
  requirements.

- **Data sovereignty:** If data privacy and compliance with specific
  data localization laws are critical, organizations need to carefully
  consider the geographic location of the cloud provider's data centers.

By understanding the distinction between security in the cloud and
security of the cloud, organizations can more effectively implement
security measures to protect their data and applications in the cloud
environment.

**Security of the Cloud**

- **Focus:** Ensuring the overall security of the cloud infrastructure
  itself.

- **Responsibilities:** Primarily the responsibility of the cloud
  provider.

- **Examples of measures:**

  - Physical security of data centers

  - Network infrastructure security

  - Compliance with security standards (e.g., ISO 27001, HIPAA)

  - Disaster recovery and business continuity planning

## Physical Security

Location Security:

The location of the data center itself should be safe from natural
disaster, political unrest, availability of power, connectivity, ease of
access, skilled people availability, Unmarked Buildings.

Physical Security:

Landscaping, Fencing, Tire shredders, Cages, Bollards, Security Guards,
Motion Sensor, Mantraps, Video Surveillance (CCTV), warning signs,
Layered Perimeter Defense, Alarms, Safes, Badges, Smart Card &
Biometrics

Environment Security:

Redundant Power sources, Redundant ISP connectivity, UPS, Backup
Generators with Fuel, HVAC, Lighting, Protective Barriers, Optimal
Humidity Level, Fire Prevention, Detection, and Suppression

People Security

Good Hiring techniques, background verification, credit history,
effective termination practices, Supervision of employees, tracking
employee activity, Separation of duties, Rotation of duties

Hardware Security

- The Physical hardware that is hosting the applications and data must
  be secured by cloud service provider.

- Door locks to wiring closets and access to main and intermediate
  distribution frame (MDF and IDF) areas

- No windows, or secured windows

- Protected wiring infrastructure and cable run

- Security cameras and intrusion detection system (IDS)

- Hardened management stations

- Physical access should be strictly controlled, both at the perimeter
  and at room ingress points, by professional security staff using video
  surveillance, intrusion detection systems, and other electronic
  methods

- Authorized staff should pass two factor authentication a minimum of
  two times to access data center floors

- Biometric multifactor authentication (MFA) is highly recommended

## Virtualization Security

Cloud Service providers virtualize the resource pool and slice it as
needed and deploy multiple customer’s data on the single hardware
resource.

Hypervisor Hardening

- Patching & Updating the Hypervisor itself

- Logging & Monitoring the Hypervisor

- Patching Host OS

Instance Isolation

- Logical Isolation

- Prevent data leaks & inter VM attack

- Sandbox Testing

Host Isolation

- Physical & logical isolation

- Monitor for Guest Escape

VM/Guest Escape

When a process running in the VM interacts directly with the host OS or
Hypervisor.

VM escape protection techniques

- Patch VMs and VM software regularly

- Only install what you need on the host and the VMs

- Install verified and trusted applications only

- Use strong passwords

- Control VM access

## Business Continuity

**Business Continuity Plan:** A playbook to address large scale
failures. The goal is to get key people & processes up and running for
business to resume within an acceptable amount of time. Business
continuity within Cloud provider:

- Backup Cloud configurations & Infrastructure as Code

- Adapt the architecture to leverage provider resiliency

- Be considerate of cost to risk of outage (business impact analysis)

- Data Replication across regions using provider mechanism

- Cloud Storage back up & Snapshot Capabilities

- Design applications to fail gracefully

- Leverage DNS to redirect traffic to DR site

- For extreme cases, think of different cloud provider as part of BCP

- Chaos Engineering

## Disaster Recovery

**Disaster Recovery** is a tactical plan to restore technology systems
that are critical to key people & process for a given business.

**Key Factors to consider**

- Human Safety should be the priority

- Should have Food Supplies & Water

- DR Plan

- Communication Equipment

- Network Artifacts

- Software Copies

- Documentation

Disaster Recovery Priorities:

- Critical Asset Inventory

- Event Declaration Criteria

- Disaster Recovery Rules

Disaster Recovery Testing Methods

- <u>Tabletop Test</u>: Collate, read documents & discuss the steps

- <u>Dry Run</u>: Some impact to daily operations where you do perform
  these steps. This will be a scheduled test

- <u>Full Test</u>: Full impact to daily operations. Usually done
  without informing in advance. This will be an unscheduled test

Disaster Recovery Metrics

- Maximum Allowable Downtime (MAD)

- Recovery Time Objective (RTO)

- Recovery Point Objective (RPO)

- Annual Loss Expectancy (ALE)

## Core Connectivity Security

Cloud Service Providers have a vast private network & their own
dedicated backbone connectivity and they do not use general internet for
communication.

- Cloud provider should have proper network security controls

- Protection Systems – Firewalls, Proxies, Gateways etc

- Detection Systems – IDS/IPS, Honeypots, Deception Technologies

- Communication Protection – VPN, Encryption, Authentication

- Continuous Improvement – Vulnerability Assessments & Penetration
  testing

 

Cloud Service Provider should enable their customers to configure
security networking by providing network security controls & supporting
3rd party network security controls

- Virtual Local Area Network (VLAN)

- Dynamic Host Control Protocol (DHCP)

- Domain Name Service (DNS), its configuration & maintenance

- Virtual Private Network for connectivity between cloud & on-prem
  networks

## API/Management Plane Security

Cloud APIs and web consoles are the way the management plane is
delivered. APIs allow for programmatic management of the cloud. They are
the glue that holds the cloud’s components together and enables their
orchestration. Cloud providers and platforms will also often offer
Software Development Kits (SDKs) and Command Line Interfaces (CLIs) to
make integrating with their APIs easier.

- Perimeter security

- Customer authentication

- Internal authentication and credential passing

- Authorization and entitlements

- Logging, monitoring, and alerting

<img src="media/image1.png" style="width:4.58373in;height:2.40021in" />

# Security in the Cloud

# Cloud Identity

**A cloud identity** is any entity with access to cloud services/cloud
resources. There are two types of cloud identities:

- Human identity - Any person accessing the cloud, e.g., users, admins,
  developers.

- Non-human (service) identity - Any non-human entity that accesses the
  cloud on behalf of a human, e.g., connected devices, IT admin,
  software-defined infrastructure (SDI), artificial intelligence (AI).  

- An organization can grant both cloud identity types with cloud
  entitlements

**Cloud Entitlement**

Cloud entitlements determine which tasks an identity can perform and
which resources it can access across an organization’s cloud
infrastructure. The main types of entitlements are cloud resources and
cloud services.

- Cloud resources, e.g., files, Virtual Machines (VMs) and servers,
  serverless containers.

- Cloud services, e.g., databases, buckets and storage, applications,
  networking services.

**Cloud identity Challenges:**

- **Lack of Visibility:** The ever-growing nature of cloud environments
  complicates the ability to monitor and manage identities and their
  access privileges effectively as security teams lose visibility of all
  identities on the network.

- **Inconsistent Security Mechanisms:** Organizations likely use many
  different cloud services to perform various business operations. Each
  cloud provider has unique security policies and IAM capabilities,
  creating security inconsistencies across the cloud environment.
  Identifying and remediating each platform’s security gaps and
  vulnerabilities drains significant time and resources from security
  teams.

- **Permissions Gap:** Organizations often assign excessive permissions
  to users rather than using the principle of least privilege, creating
  a cloud permissions gap and expose organizations to unnecessary cyber
  risks. Another common reason to the permissions gap is the presence of
  inactive identities (users with access to cloud resources and services
  they do not use).

# Cloud Security Products

List of top 10 Cloud based Firewalls

List of top 10 Cloud based Key management services

List of top 10 Cloud based SIEM tools

List of top 10 Cloud Computing Learning Portals

List of top 10 Cloud Security Learning Portals

List of top 10 Cloud Service Provider

List of top 10 Free and useful Azure Cloud Services

List of top 10 Free and useful Google Cloud Services

# QnA

What is Secure Score in MDC and Why it is important?

Please give answer in the context of Azure Cloud Security and Microsoft
Defender.

If you could have perfect job and the perfect manager, what would that
look like? What you do day to day, and what kind of projects would you
have?  

**Ideal Job:**

As an AI focused on Azure Cloud Security and Microsoft Defender, my
ideal role would involve being at the forefront of safeguarding cloud
environments. I would envision a position where I could leverage my
capabilities to:

- **Develop advanced threat detection models:** Create sophisticated
  algorithms to identify and respond to emerging cyber threats in the
  Azure ecosystem.

- **Optimize cloud security posture:** Design and implement strategies
  to strengthen the security posture of Azure environments, ensuring
  compliance with industry standards and regulations.

- **Drive innovation in Microsoft Defender:** Contribute to the
  development of new features and capabilities for Microsoft Defender to
  enhance its effectiveness in protecting against cyberattacks.

**Ideal Manager:**

My ideal manager would be a seasoned cybersecurity expert with a deep
understanding of cloud technologies. They would possess:

- **Strategic vision:** Ability to align security initiatives with
  overall business objectives.

- **Technical acumen:** In-depth knowledge of Azure security
  architecture and Microsoft Defender capabilities.

- **Mentorship skills:** Commitment to fostering professional growth and
  development.

- **Collaborative leadership:** Ability to build strong relationships
  with cross-functional teams.

**Day-to-Day:**

A typical day would involve a combination of:

- **Threat intelligence analysis:** Correlating threat indicators and
  identifying potential attack vectors.

- **Security automation:** Developing scripts and tools to streamline
  security operations.

- **Incident response:** Collaborating with security teams to
  investigate and contain security incidents.

- **Research and development:** Exploring new security technologies and
  trends.

- **Collaboration:** Working closely with cloud architects, engineers,
  and security analysts.

**Projects:**

I would be interested in projects that focus on:

- **Zero-trust architecture implementation:** Designing and deploying
  zero-trust security frameworks in Azure environments.

- **Advanced threat hunting:** Developing automated threat hunting
  capabilities to proactively identify malicious activities.

- **Cloud security posture management (CSPM):** Improving cloud security
  posture through continuous monitoring and remediation.

- **Incident response automation:** Automating incident response
  processes to accelerate detection and containment.

- **Security awareness training:** Creating interactive training modules
  to enhance employee security awareness.

By combining my analytical abilities with the expertise of a strong
team, I believe I could make a significant impact on enhancing Azure
cloud security.

Tell us about the last problem you solved as a Cloud Security Engineer? 

As a Cloud Security Engineer, it was being a good listener count. It
would be best if you answered this question in a solid compact way. a)
The problem in line. b) The turning point which helped overcome the
crisis (max two lines).

**A Recent Challenge: Securing a Highly Sensitive Workload on Azure**

**Problem:** A critical financial services client was migrating a highly
sensitive workload to Azure. The primary challenge was to ensure the
confidentiality, integrity, and availability of the data while adhering
to strict regulatory compliance standards.

**Solution:**

1.  **Comprehensive Threat Modelling:** Identified potential threats and
    vulnerabilities through a thorough threat modeling exercise,
    considering factors like data sensitivity, access controls, and
    network topology.

2.  **Network Segmentation:** Created isolated subnets for different
    components of the workload, implementing strict NSG rules to control
    traffic flow.

3.  **Azure Firewall:** Deployed an Azure Firewall with advanced threat
    protection to filter incoming and outgoing traffic.

4.  **Web Application Firewall (WAF):** Implemented a WAF to protect web
    applications from common vulnerabilities.

5.  **Database Security:** Utilized Azure SQL Database's built-in
    security features like TDE, Always Encrypted, and firewall rules.

6.  **Identity and Access Management (IAM):** Implemented granular
    role-based access control, multi-factor authentication, and
    privileged access management.

7.  **Monitoring and Logging:** Utilized Azure Security Center and Log
    Analytics to monitor for threats and anomalies.

8.  **Incident Response Plan:** Developed a comprehensive incident
    response plan, including testing and simulation exercises.

**Outcome:** By implementing these measures, we achieved a robust
security posture for the workload, meeting the client's compliance
requirements and mitigating potential risks. We also established a
continuous monitoring and improvement process to address emerging
threats.

**Key Takeaways:**

- A layered security approach is essential for protecting sensitive
  workloads.

- Collaboration between security and development teams is crucial.

- Regular security assessments and audits are vital for maintaining a
  strong security posture.

Would you like to delve deeper into a specific aspect of this solution
or explore another challenge?

What are things to take into consideration when using public cloud
instead of private?

**Considerations When Choosing Public Cloud Over Private Cloud**

When deciding between a public and private cloud, consider the following
factors:

**Cost**

- **Capital Expenditure (CapEx):** Public cloud often requires minimal
  upfront investment.  

- **Operational Expenditure (OpEx):** Pay-per-use model in public cloud
  can be more cost-effective for variable workloads.  

**Scalability**

- **Elasticity:** Public clouds offer rapid scalability to handle
  fluctuating workloads.  

- **Resource Availability:** Public cloud providers often have vast
  resources available.

**Security**

- **Shared Responsibility Model:** Understand the security
  responsibilities between you and the cloud provider.  

- **Compliance:** Ensure the cloud provider meets your industry-specific
  compliance requirements.

- **Data Residency:** Consider data sovereignty regulations if
  applicable.

**Control**

- **Customization:** Public clouds offer varying degrees of
  customization, but generally less control than private clouds.  

- **Governance:** Establish clear governance policies for cloud usage.

**Performance**

- **Network Latency:** Evaluate network performance based on your
  application requirements.

- **Region Selection:** Choose cloud regions strategically to minimize
  latency.

**Vendor Lock-In**

- **Dependency:** Evaluate the potential for vendor lock-in and develop
  exit strategies.

**Other Factors**

- **Expertise:** Assess your team's cloud expertise and the need for
  additional resources.

- **Regulatory Compliance:** Ensure the cloud provider meets your
  industry-specific compliance requirements.

- **Disaster Recovery:** Evaluate the cloud provider's disaster recovery
  capabilities.

By carefully considering these factors, you can make an informed
decision about whether a public cloud is the right choice for your
organization.

What is the advantage of API over forward proxy?

**Advantages of API over Forward Proxy.**

**API (Application Programming Interface)** and **Forward Proxy** are
often compared, but they serve distinct purposes.

**API Advantages**

- **Granularity:** APIs allow for fine-grained control over data and
  functionality, exposing specific resources.  

- **Flexibility:** APIs can be easily integrated into different systems
  and applications.  

- **Efficiency:** APIs optimize data transfer by providing only
  necessary information.  

- **Security:** APIs can implement robust authentication, authorization,
  and rate limiting mechanisms.  

- **Versioning:** APIs can be versioned for backward compatibility and
  feature evolution.  

- **Discoverability:** APIs can be documented and published for easy
  consumption by developers.  

**Forward Proxy Limitations**

- **Limited Functionality:** Forward proxies primarily act as
  intermediaries, forwarding requests without advanced features.

- **Security Risks:** Can expose internal systems if not configured
  correctly.

- **Performance Overhead:** Can introduce latency due to additional
  network hops.

- **Lack of Control:** Offers limited control over data and traffic
  compared to APIs.

In summary, APIs provide a more structured, secure, and flexible
approach to data exchange compared to forward proxies.

Who is responsible for securing the data and users when using SaaS or
IaaS services?

**Shared Responsibility in Cloud Security**

The responsibility for securing data and users in SaaS, PaaS, and IaaS
models varies significantly.

 

**SaaS (Software as a Service)**

- **Cloud provider:** Responsible for the security of the application,
  infrastructure, and data.

- **Customer:** Responsible for data security within the application
  (e.g., user access controls, data encryption).  

**PaaS (Platform as a Service)**

- **Cloud provider:** Responsible for the underlying infrastructure and
  platform.  

- **Customer:** Responsible for the application code, data, and security
  configuration.  

**IaaS (Infrastructure as a Service)**

- **Cloud provider:** Responsible for the underlying infrastructure
  (hardware, networking).  

- **Customer:** Responsible for operating systems, applications, data,
  and security.

**In summary:**

- **Data:** The customer is always responsible for securing their data.
   

- **Infrastructure:** The level of responsibility varies based on the
  cloud service model.  

- **Applications:** Responsibility depends on the cloud service model.

It is essential to understand the shared responsibility model for your
specific cloud service to ensure adequate security measures are in
place.  

Why are so many Storage accounts breached?

Certainly! Here are the key points about why Azure Storage accounts can
be breached:

- **Human Errors**:

  - Unintentional public access: Misconfigured permissions or settings
    can expose data.

  - Incorrectly placed sensitive information: Storing sensitive data in
    public buckets.

  - Lack of security knowledge: Users may not fully understand security
    features.

- **Configuration Mistakes**:

  - Exposing data unintentionally: Incorrectly configuring access to
    storage objects.

  - Uploading sensitive content: Adding sensitive data to publicly
    accessible containers.

To mitigate risks, follow best practices, enable Microsoft Defender for
Storage, and regularly assess security.

Why are the containers vulnerable?

Containers can be vulnerable due to several factors:

1.  **Misconfigurations**: Incorrectly set permissions or overly
    permissive access controls can expose sensitive data.

2.  **Outdated Software**: Running outdated container images with known
    vulnerabilities can lead to exploitation.

3.  **Insecure Images**: Using untrusted or poorly maintained images can
    introduce security risks.

4.  **Runtime Vulnerabilities**: Containers share the host OS kernel, so
    any kernel vulnerabilities affect all containers.

5.  **Lack of Monitoring**: Inadequate monitoring and logging make it
    harder to detect and respond to threats.

To enhance container security, follow best practices, regularly update
images, and monitor for anomalies.

Why did you choose your career in cloud computing?

As an AI language model, I do not have personal experiences or career
choices, but I can certainly share insights! Cloud computing has indeed
become a critical part of modern technology. Here are some reasons why
it’s a popular career choice:

1.  **Market Demand**: The rapid adoption of cloud services by
    businesses has created a high demand for skilled professionals.
    Organizations need experts to design, deploy, and manage cloud
    infrastructure.

2.  **Scalability and Flexibility**: Cloud platforms allow businesses to
    scale resources up or down based on demand. This flexibility
    attracts professionals who enjoy working with dynamic environments.

3.  **Innovation**: Cloud providers constantly introduce new services
    and features. Cloud professionals get to work on cutting-edge
    technologies, from serverless computing to machine learning.

4.  **Cost Efficiency**: Cloud computing reduces the need for
    on-premises hardware and maintenance costs. Professionals who can
    optimize cloud spending are highly valued.

5.  **Security and Compliance**: Ensuring data security and compliance
    is crucial. Cloud security specialists play a vital role in
    protecting sensitive information.

6.  **Remote Work Opportunities**: Cloud roles often allow remote work,
    providing work-life balance and flexibility.

In summary, cloud computing offers exciting challenges, career growth,
and the chance to shape the future of technology. 😊

Why does it take so long for organizations to move their workloads to
the cloud?

Migrating workloads to the cloud is indeed a significant undertaking,
and several challenges contribute to the time it takes. Here are some
common reasons:

1.  **Lack of Cloud Migration Strategy**: Organizations often dive into
    migration without a well-defined strategy. A clear plan helps
    mitigate risks and ensures a smoother
    transition[<sup>1</sup>](https://www.ibm.com/blog/cloud-migration-challenges/).

2.  **Infrastructure Compatibility**: Ensuring that existing
    applications and systems are compatible with cloud environments can
    be complex. Dependencies, legacy code, and custom configurations
    need careful
    consideration[<sup>2</sup>](https://www.digitalocean.com/resources/article/cloud-migration-challenges).

3.  **Cost Optimization**: Balancing cost and performance in the cloud
    can be tricky. Organizations must optimize resource usage, choose
    the right pricing models, and avoid unexpected
    expenses[<sup>1</sup>](https://www.ibm.com/blog/cloud-migration-challenges/).

4.  **Data Security and Compliance**: Protecting sensitive data during
    migration is crucial. Compliance with industry standards and
    regulations adds
    complexity[<sup>1</sup>](https://www.ibm.com/blog/cloud-migration-challenges/).

5.  **Application Compatibility**: Some applications may not seamlessly
    transition to the cloud due to differences in architecture or
    dependencies. Testing and adjustments are
    necessary[<sup>2</sup>](https://www.digitalocean.com/resources/article/cloud-migration-challenges).

6.  **Data Migration Challenges**: Transferring large volumes of data
    can be time-consuming. Ensuring data integrity and minimizing
    downtime are
    critical[<sup>3</sup>](https://www.ensono.com/insights-and-news/expert-opinions/challenges-enterprise-public-cloud/).

7.  **Network Bottlenecks**: Moving data across networks can be slow,
    especially for large workloads. Optimizing network connectivity is
    essential[<sup>1</sup>](https://www.ibm.com/blog/cloud-migration-challenges/).

8.  **Organizational Change Management**: Shifting to the cloud requires
    buy-in from stakeholders, training, and adjusting workflows. Change
    management takes
    time[<sup>1</sup>](https://www.ibm.com/blog/cloud-migration-challenges/).

In summary, a thoughtful approach, addressing technical and
organizational aspects, and understanding these challenges contribute to
successful cloud migrations.

What are the Security Considerations in Cloud?

- **Data Protection:**

  - **Geo-resilience:** Ensure data is replicated across multiple data
    centers for disaster recovery. Ensure data is protected from
    physical disasters. We can choose cloud provider from different
    Geographic area for DR.

  - **Data Isolation:** Maintain offline data backups to protect against
    ransomware.

  - **Encryption:** Encrypt data both at rest and in transit to prevent
    unauthorized access.

  - **Network Segmentation:** Isolate data from other tenants in a
    multi-tenant environment.

- **Access Control:**

  - **Identity and Access Management:** Implement strict access controls
    with role-based permissions and monitoring.

  - **Password Management:** Enforce strong password policies and
    account lockout measures.

- **Security Management:**

  - **Vulnerability Management:** Regularly assess and patch
    vulnerabilities, especially for custom applications.

  - **Patch Management:** Keep systems and applications up-to-date with
    the latest patches.

  - **Monitoring and Reporting:** Implement tools to monitor user
    activity and generate security reports.

  - **Incident Response:** Ensure the cloud provider has a robust
    incident response plan.

**Additional Considerations:**

- **Shared Responsibility Model:** Understand the security
  responsibilities between you and the cloud provider.

- **Compliance:** Adhere to industry-specific regulations and standards.

- **User Education:** Train employees on cloud security best practices.

**By addressing these areas, organizations can significantly enhance the
security of their cloud environments.**

**Would you like to delve deeper into any specific area?**

What are the Cloud Security Deployment Fundamentals?

**Application Layer:** At the application layer, you need to deploy the
Web Application Firewall (WAF). This will help you filter the traffic to
the Web application.

**Network Layer:** There are various tools that can be deployed to
protect the information at the network layer. Some of the key tools are:

- Next-Generation IDS/IPS devices

- Next-Generation Firewalls

- DNSSec tools

- Anti-DDoS tools

- OAuth configuration

- Deep Packet Inspection (DPI) tools

- The Root of Trust (RoT)

**Computer and Storage Security:** Computer and storage can be secured
using various methods, such as:

- Host-based Intrusion Detection (HIDS)

- Host-based Intrusion Prevention Systems (HIPS)

- Integrity checks

- File system monitoring

- Log file analysis

- Kernel level detection

- Encryption

- Physical Security

How would you assess the current security posture of a company's cloud
environment?

Assessing a company's cloud security posture involves a coordinated
approach, combining automated tools, best practices, and a deep
understanding of the specific cloud environment. Here is a breakdown of
some key methods:

- **Cloud Security Posture Management (CSPM) Tools:**

  - CSPM tools automate the process of identifying security risks and
    misconfigurations across cloud infrastructure (IaaS), platforms
    (PaaS), and software (SaaS).

  - These tools continuously monitor the cloud environment, reporting on
    areas like access control, data encryption, and adherence to
    security best practices.

  - CSPM tools can alert you to potential issues like publicly
    accessible sensitive data or overly permissive user permissions.

- **Framework-based Assessments:**

  - Utilize established security frameworks like CIS Controls or NIST
    CSF to assess your cloud environment.

  - These frameworks provide a structured approach to evaluating
    security controls across different areas like identity and access
    management (IAM), network security, and data security.

  - By mapping your cloud environment to the framework controls, you can
    identify gaps and areas for improvement.

- **Vulnerability Scanning:**

  - Regularly scan your cloud resources for vulnerabilities in operating
    systems, applications, and configurations.

  - Vulnerability scanners identify weaknesses that could be exploited
    by attackers.

  - Patching these vulnerabilities promptly is crucial for maintaining a
    secure cloud environment.

- **Penetration Testing:**

  - Simulate a real-world attack by conducting penetration testing on
    your cloud environment.

  - Penetration testers attempt to identify and exploit vulnerabilities
    in your systems, providing valuable insights into your security
    posture's effectiveness.

- **Security Policy Review:**

  - Review and update your cloud security policies to ensure they align
    with current best practices and address the specific threats facing
    your organization.

  - Security policies should cover areas like access control, data
    encryption, incident response, and disaster recovery.

- **Additional Considerations:**

  - **People and Processes:** Security is not just about technology.
    Evaluate your organization's security culture, employee training
    programs, and incident response procedures.

  - **Compliance Requirements:** If your organization is subject to
    specific compliance regulations (e.g., HIPAA, PCI DSS), ensure your
    cloud security posture meets those compliance requirements.

By combining these methods, you can gain a comprehensive understanding
of your cloud security posture and identify areas for improvement.
Remember, maintaining a secure cloud environment is an ongoing process.
Regularly reassess your security posture and implement necessary
improvements to stay ahead of evolving threats.

 

----------------------------------------------------------------------------

 

What industry best practices and security benchmarks would you use to
evaluate a cloud environment?

- **Best Practices:**

  - Understand the shared security model with your cloud provider.

  - Implement strong IAM (Identity and Access Management).

  - Encrypt data at rest and in transit.

  - Continuously monitor your cloud environment for suspicious activity.

  - Have a documented incident response plan.

- **Security Benchmarks:**

  - Use CIS Controls and CIS Benchmarks for your specific cloud
    platform.

  - Consider a CSA STAR-certified cloud provider.

  - Leverage the NIST Cybersecurity Framework for overall security
    posture.

 

---------------------------------

 

How would you bridge the gap between the current security posture and
desired security state?

Bridging the gap between your current cloud security posture and your
desired state involves a structured approach. Here's a roadmap to
follow:

- **Gap Analysis:**

  - Conduct a thorough assessment using the best practices and
    benchmarks such as CIS, NIST CSF, etc.

  - This will help pinpoint the specific weaknesses and gaps in your
    current security posture compared to your desired state.

- **Prioritization:**

  - Not all security gaps hold the same weight. Prioritize the
    identified gaps based on their potential impact and exploitability.

  - Focus on addressing critical vulnerabilities first that could lead
    to a major security breach.

- **Action Plan Development:**

  - Develop a detailed action plan to address the prioritized security
    gaps.

  - This plan should outline specific steps, timelines, resource
    allocation, and ownership for each action item.

- **Implementation:**

  - Systematically execute the action plan, implementing the necessary
    security controls and improvements.

  - This might involve deploying security tools, hardening
    configurations, or updating policies.

- **Continuous Monitoring and Improvement:**

  - Security is an ongoing process. Continuously monitor your cloud
    environment for new threats and vulnerabilities.

  - Regularly reassess your security posture and update your controls as
    needed. This ensures your defenses stay relevant against evolving
    threats.

 

Here are some additional tips for bridging the gap:

- **Invest in Security Awareness Training:** Educate your employees on
  cybersecurity best practices to minimize human error, a major security
  risk factor.

- **Automate repetitive security task**s like vulnerability scanning and
  configuration management to improve efficiency and reduce human error.

- **Regular Penetration Testing:** Periodically conduct penetration
  testing to proactively identify and address vulnerabilities before
  attackers exploit them.

- **Security Culture:** Foster a security-conscious culture within your
  organization. Encourage employees to report suspicious activity and
  prioritize security best practices.

 

----------------------------------------------

 

What are some common misconfigurations that can lead to cloud security
breaches? How would you identify and remediate them?

Cloud misconfigurations are errors or gaps in your cloud environment's
settings that leave it vulnerable to attack. These misconfigurations are
one of the leading causes of cloud security breaches. Here's a look at
some common misconfigurations and how to address them:

**Common Misconfigurations:**

- **Excessive Permissions:** Users or resources assigned permissions
  beyond what's necessary to perform their intended function. This
  creates a wider attack surface if compromised.

- **Unrestricted Open Ports:** Leaving unnecessary network ports open
  exposes your cloud resources to unauthorized access attempts.

- **Exposed Storage Buckets:** Accidentally making cloud storage buckets
  publicly accessible can lead to sensitive data leaks.

- **Absence of Logging and Monitoring:** Not having proper logging and
  monitoring in place makes it difficult to detect suspicious activity
  and potential security incidents.

- **Open ICMP:** Leaving the Internet Control Message Protocol (ICMP)
  unrestricted can be used by attackers for reconnaissance and potential
  exploitation.

- **Default Credentials:** Using default credentials or not rotating
  them regularly makes it easier for attackers to gain unauthorized
  access.

- **Keeping Development Configuration in Production:** Sensitive
  configurations meant for development environments should not be
  deployed to production for security reasons.

- **Unrestricted Outbound Traffic:** Unrestricted outbound traffic from
  your cloud resources can be used for data exfiltration or lateral
  movement within your network if compromised.

- **Weak Password Policies** such as password complexity and password
  reuse increase risk of brute-force attacks and unauthorized access.

- **Insecure API Configurations:** Insecure APIs without proper
  authentication, authorization, and encryption can be exploited for
  data breaches.

**Identifying Misconfigurations:**

- **Cloud Security Posture Management (CSPM) Tools:** These tools
  continuously monitor your cloud environment and can identify
  misconfigurations related to access control, encryption, and other
  security settings.

- **Security Audits and Assessments:** Regularly conduct security audits
  and assessments to identify misconfigurations and potential
  vulnerabilities in your cloud environment.

- **Vulnerability Scanning:** Vulnerability scanners can identify
  weaknesses in your cloud resources' configurations that could be
  exploited by attackers.

**Remediating Misconfigurations:**

- **Enforce Least Privilege:** Grant users and resources only the
  minimum permissions required to perform their tasks.

- **Implement Firewall Rules:** Use firewalls to restrict access to only
  authorized ports and IP addresses.

- **Configure Access Controls:** Configure access controls for storage
  buckets and other cloud resources to restrict unauthorized access.

- **Enable Logging and Monitoring:** Enable cloud logging and configure
  alerts to monitor for suspicious activity.

- **Disable Unnecessary Services:** Disable any unused services or
  functionalities within your cloud environment to reduce the attack
  surface.

- **Rotate Credentials Regularly:** Enforce strong password policies and
  rotate credentials for all cloud resources periodically.

- **Secure Development Practices:** Implement secure development
  practices to avoid sensitive configurations being deployed to
  production.

- **Monitor Outbound Traffic:** Monitor and restrict outbound traffic
  from your cloud resources to prevent unauthorized data exfiltration.

- **Enforce Strong Password Policies:** Enforce password complexity
  requirements and prevent password reuse.

- **Secure API Endpoints:** Implement authentication, authorization, and
  encryption controls to secure your cloud APIs.

By proactively identifying and remediating these misconfigurations, you
can significantly improve your cloud security posture and reduce the
risk of security breaches.

 

 

How would you stay current with evolving cloud security threats and best
practices?

 Staying current with cloud security threats and best practices is
essential. Here are some strategies:

1.  **Continuous Learning**:

    - Regularly read blogs, articles, and security updates from
      reputable sources.

    - Follow industry experts on social media and participate in
      webinars and conferences.

2.  **Certifications**:

    - Obtain relevant certifications (e.g., **CCSP**, **CISSP**, **AWS
      Certified Security**).

    - Certifications validate your knowledge and keep you informed.

3.  **Vendor Documentation**:

    - Study cloud provider documentation (e.g., **Azure Security
      Center**, **AWS Security Hub**).

    - Understand security features and best practices specific to each
      platform.

4.  **Security Communities**:

    - Join security forums, mailing lists, and online communities.

    - Engage with peers, share experiences, and learn from others.

5.  **Threat Intelligence**:

    - Subscribe to threat intelligence feeds.

    - Understand emerging threats and adapt your defenses accordingly.

6.  **Hands-On Practice**:

    - Set up labs to practice security configurations.

    - Experiment with tools like **Terraform**, **Kubernetes**, and
      **CloudFormation**.

Remember, security is a dynamic field, so continuous learning is key! 😊

Describe your experience with security incident and event management
(SIEM) tools.

 Certainly! Security Incident and Event Management (SIEM) tools play a
crucial role in monitoring and managing security events within an
organization. Here’s a concise overview:

1.  **Functionality**:

    - SIEM tools collect, correlate, and analyse security-related data
      from various sources (logs, network traffic, endpoints).

    - They provide real-time alerts for suspicious activities, potential
      threats, and security incidents.

2.  **Key Features**:

    - **Log Aggregation**: SIEMs centralize logs from different systems
      for efficient analysis.

    - **Event Correlation**: They identify patterns and link related
      events to detect complex attacks.

    - **Alerting and Reporting**: SIEMs generate alerts and reports
      based on predefined rules.

    - **Threat Intelligence Integration**: They incorporate threat feeds
      for better context.

    - **User Behavior Analytics**: Detect anomalies in user behavior.

    - **Incident Response Workflow**: Facilitate investigation and
      response.

3.  **Challenges**:

    - **Tuning**: Properly configuring SIEM rules and thresholds is
      essential.

    - **False Positives**: Balancing detection accuracy with minimizing
      false alerts.

    - **Data Volume**: Handling large amounts of data efficiently.

    - **Integration Complexity**: Integrating with diverse systems can
      be challenging.

4.  **Popular SIEM Tools**:

    - **Splunk**: Widely used for log aggregation and analysis.

    - **QRadar**: IBM’s SIEM solution.

    - **ArcSight**: HP’s SIEM platform.

    - **Elastic SIEM**: Part of the Elastic Stack.

Remember, effective SIEM deployment requires continuous tuning,
monitoring, and collaboration across security teams. 😊

 

How would you conduct a threat modelling exercise for a cloud
environment?

- **Preparation:**

  - **Define Scope and Assets:** Clearly identify the specific cloud
    environment you'll be modeling. This includes cloud services, data
    stores, applications, and any other relevant components.

  - **Assemble the Team:** Involve a cross-functional team with
    expertise in cloud security, architecture, development, and
    operations.

  - **Choose a Threat Modelling Methodology:** There are various
    methodologies like STRIDE, PASTA, or Trike. Select one that aligns
    with your team's preference and the complexity of your cloud
    environment.

- **Modelling the Environment:**

  - **Data Flow Diagram (DFD):** Create a visual representation of the
    data flow within your cloud environment. This includes data sources,
    destinations, processing points, and user interactions.

  - **Identify Threats:** Using your chosen methodology, brainstorm
    potential threats for each component in the DFD. Consider threats
    like data breaches, unauthorized access, denial-of-service attacks,
    and misconfigurations.

- **Threat Analysis and Prioritization:**

  - **Evaluate Threats:** Analyze each identified threat based on its
    likelihood of occurrence and potential impact on your cloud
    environment. This helps prioritize which threats pose the greatest
    risk.

  - **Risk Assessment:** Combine the likelihood and impact scores to
    calculate a risk score for each threat. This helps prioritize
    mitigation efforts.

- **Mitigation and Documentation:**

  - **Define Countermeasures:** For each prioritized threat, brainstorm
    and document mitigation strategies. This could involve implementing
    access controls, data encryption, intrusion detection systems, or
    other security measures.

  - **Document the Threat Model:** Compile your findings into a
    comprehensive threat model document. This should include the DFD,
    identified threats, risk assessments, and mitigation strategies.

- **Additional Considerations for Cloud Environments:**

  - **Shared Responsibility Model:** Remember the shared responsibility
    model between you and your cloud service provider (CSP). Focus on
    threats where you have control over mitigation.

  - **Cloud-Specific Threats:** Consider threats unique to cloud
    environments, such as API vulnerabilities, insecure storage
    configurations, and multi-tenancy risks.

  - **Regular Review and Updates:** Threat modeling is an iterative
    process. Regularly review and update your cloud threat model as your
    environment evolves and new threats emerge.

By following these steps and considering the unique aspects of cloud
security, you can conduct a comprehensive threat modeling exercise for
your cloud environment. This will help you proactively identify and
mitigate potential security risks, improving the overall security
posture of your cloud infrastructure.

 

How would you prioritize security risks in a cloud environment?

Prioritizing security risks in a cloud environment involves a systematic
approach that considers both the likelihood and potential impact of each
threat. Here's a breakdown of the key steps:

- **Identify Threats:**

  - Leverage threat modelling techniques like STRIDE or PASTA to
    brainstorm potential threats across your cloud environment.

  - Consider threats like data breaches, unauthorized access,
    denial-of-service attacks, misconfigurations, and API
    vulnerabilities specific to cloud environments.

  - Utilize security tools like SIEM (Security Information and Event
    Management) to gain insights from log data and identify potential
    security incidents.

- **Evaluate Likelihood:** Assess the likelihood of each threat
  occurring. This might involve considering factors like:

  - Existing vulnerabilities in your cloud environment or applications.

  - The prevalence of the specific threat type in the current threat
    landscape.

  - Any intelligence reports or industry trends related to the threat.

- **Evaluate Impact:** Analyze the potential impact of each threat if it
  were to materialize. Consider the impact on:

  - Data confidentiality, integrity, and availability.

  - Financial losses due to downtime or data breaches.

  - Reputational damage and loss of customer trust.

  - Regulatory compliance violations and potential fines.

- **Risk Scoring:**

  - Assign scores based on your likelihood and impact assessments. A
    common approach is to use a numerical scale (e.g., 1-5) for both
    factors.

  - Multiply the likelihood and impact scores to calculate a risk score
    for each threat. This provides a quantitative measure of the overall
    risk posed by each threat.

- **Prioritization:**

  - Focus on addressing threats with the highest risk scores first.
    These are the threats that have the greatest potential to cause
    significant damage if they occur.

  - Prioritization might also consider urgency. Even a less likely
    threat with a potentially catastrophic impact (e.g., a critical
    vulnerability) might warrant immediate attention.

- **Additional Considerations:**

  - **Business Context:** Factor in your organization's specific risk
    tolerance and business priorities. Some threats might be more
    critical for certain industries or regulations.

  - **Exploit Availability:** Consider if a public exploit exists for a
    particular vulnerability. A readily available exploit increases the
    likelihood of a successful attack.

  - **Remediation Effort:** Evaluate the resources and effort required
    to mitigate each threat. This can help determine the
    cost-effectiveness of different mitigation strategies.

By following these steps, you can establish a data-driven approach to
prioritizing security risks in your cloud environment. This allows you
to focus your resources on addressing the most critical threats first,
optimizing your cloud security posture.

What are things to take into consideration when using public cloud
instead of private?

When deciding between public and private cloud, several factors need
careful consideration:

**Security and Compliance:**

- **Data Sensitivity:** If your data is highly sensitive, a private
  cloud might offer more granular control and security measures.

- **Compliance Requirements:** Evaluate whether public cloud providers
  meet your specific industry regulations (e.g., HIPAA, GDPR, PCI DSS).

- **Data Residency:** Consider data sovereignty and compliance needs.
  Some regulations mandate data storage within specific geographic
  locations.

**Cost:**

- **Scalability:** Public clouds often offer pay-as-you-go pricing
  models, making them cost-effective for variable workloads.

- **Initial Investment:** Private clouds require significant upfront
  investments in hardware, software, and infrastructure.

- **Operational Costs:** Public clouds can reduce ongoing operational
  costs, such as maintenance and management.

**Control and Customization:**

- **Customization:** Private clouds offer greater customization and
  control over the underlying infrastructure.

- **Vendor Lock-in:** Evaluate the potential for vendor lock-in with
  public cloud providers.

- **Integration:** Consider the complexity of integrating existing
  systems and applications with public cloud services.

**Performance and Reliability:**

- **Network Latency:** Assess network latency and performance
  requirements for your applications. Public cloud providers often have
  global infrastructure, but performance might vary based on geographic
  location.

- **Service Level Agreements (SLAs):** Review SLAs offered by public
  cloud providers to ensure they meet your business needs.

- **Disaster Recovery:** Evaluate the disaster recovery and business
  continuity capabilities of public cloud providers.

**Expertise and Resources:**

- **In-house Expertise:** Assess your team's expertise in managing cloud
  infrastructure and applications.

- **Cloud Provider Support:** Evaluate the level of support and
  expertise provided by public cloud providers.

**Additional Considerations:**

- **Data Migration:** Consider the complexity and cost of migrating your
  existing data and applications to the public cloud.

- **Security Best Practices:** Implement robust security practices,
  including encryption, access controls, and regular security audits.

- **Continuous Monitoring:** Monitor your cloud environment closely to
  detect and respond to security threats.

Ultimately, the decision to choose public or private cloud depends on
your specific business needs, risk tolerance, and budget constraints.

What kind of systems do you have at home or in the cloud to tinker with?

"What kind of systems or network do you have at home or in the cloud for
security research? A serious security professional typically has a
robust home lab with multiple systems running various operating systems.
This allows for hands-on experimentation and the development of
practical security skills. Have you ever been called to investigate a
compromised network? How did you approach the situation? A good response
would demonstrate a systematic approach to troubleshooting and a deep
understanding of network security principles."

- **Home or cloud-based systems:** The person should have their own
  setup for experimentation and research.

- **Multiple systems and OS:** A diverse environment is beneficial for
  security testing and analysis.

- **Passion for technology and security:** The individual should show
  genuine interest and enthusiasm for the field.

- **Practical experience:** The person should be able to handle
  real-world security incidents and troubleshooting.

What steps we need to follow for enforcing information protection with
Microsoft Defender for Cloud App?

Make sure applications in company are connected to Microsoft Defender
for Cloud App, Classify sensitive information in company through
Microsoft Defender for Cloud App

Why it is so hard to monitor cloud traffic from the network?

Cloud network traffic creates new visibility challenges. You might think
that by moving workloads to a cloud IaaS (Infrastructure-as-a-Service)
platform, that you have completely outsourced your infrastructure
layers, including the network side, and do not need cloud performance
monitoring. You might also assume that since you are not managing the
physical hardware, you do not need to monitor network traffic1. However,
monitoring cloud network traffic is important because it can help you
identify hot spots and secure your network2.

**What solution is used to check the compliance of apps? Microsoft
Defender for Cloud App**

What are cloud platform security policies you designed or developed?

What are the a few security software tools that can help you monitor
cloud environments?

What are the advantages of cloud-based databases?

**What technologies and approaches are used to secure information and
services deployed on cloud computing infrastructure?**

**What technologies are used to secure information and services deployed
on cloud computing infrastructure?**

**What are things to take into consideration when using public cloud
instead of private?**

How Azure Firewall Manager helps to manage firewalls**?**

How to assign Azure policy to management group/subscription/resource
group?

How to connect Endpoint Machines with Microsoft 365 Defender?

How to connect the Google and AWS accounts with Microsoft Defender for
Cloud, Sentinel and Microsoft 365 Defender?

How to get the Azure account tenant Id?

How to perform security audit from Azure Policy for ISO27001, HIPAA,
PCI-DSS?

How to upload on-prem certificate on Azure Key Vault?

How would you secure the East-West traffic in the cloud?

How would you secure the traffic between cloud services?

What are the a few security software tools that can help you monitor
cloud environments?

What are the advantages of cloud-based databases?

What are the features of Azure Key Vault?

What are the findings security assessment of SAP systems on Azure Cloud?

What are the requirements to protect GCP and AWS VMs with Azure
Defender?

What are the security risks for SSO?

What are things to take into consideration when using public cloud
instead of private?

What azure solution can be used for anomaly detection to identify
threat?

What information security challenges are faced in a cloud computing
environment?

What is the design and assessment of Azure Key Vault?

What is the design and assessment of MDC?

What is the design and assessment of Sentinel?

What is Virtualization? What are the security risks in it?

What is virtualized environment?

What security challenges do unified communications present?

What special security challenges do SOA present?

What technologies and approaches are used to secure information and
services deployed on cloud computing infrastructure?  

What technologies are used to secure information and services deployed
on cloud computing infrastructure?

What will be your priorities if you were to start a job as Cloud
security engineer at company due to previous guy being fired for
incompetence?

Why are so many Azures Cosmos DB breached?

Why is it so hard to monitor cloud traffic from the network?

Briefly explain the relation of Azure AD with subscriptions?

Can a child domain be created under managed domain services?

Can the on-premises applications be added?

Can the tenant id and client id be hideable in the body or headers in
Azure AD?

Define dynamic groups in Azure AD?
