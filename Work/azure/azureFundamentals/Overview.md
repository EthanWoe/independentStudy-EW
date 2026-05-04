# Azure Fundamentals (AZ-900)

### Course Description
* The purpose of this Certification is to learn and demonstrate fundamental knowledge of cloud concepts in Microsoft Azure. At the end of this course, I should be able to describe
  common phrases such as PaaS, IaaS, and SaaS. I should also be able to discuss Azure architectural components and Azure services, such as Compute, Networking, and Storage
---
## 1.1 Cloud Computing
**Cloud computing** is the delivery of computing services (servers, storage, networking, databases, software, AI, and analytics) over the internet. These resources can be rapidly provisioned and released with minimal management effort.

---

## Shared Responsibility Model
The **shared responsibility model** defines which security and operational tasks are handled by Microsoft Azure and which are handled by the customer.

- **On-Premises:** Customer is responsible for everything.
- **IaaS:** Azure manages hardware; customer manages OS, apps, and data.
- **PaaS:** Azure manages OS and runtime; customer manages apps and data.
- **SaaS:** Azure manages almost everything; customer manages data and access.

---

## Cloud Deployment Models

### 1.3.1 Public Cloud
The **public cloud** runs entirely on the cloud provider’s infrastructure.
- Highly scalable
- Pay-as-you-go pricing
- No hardware maintenance
- Common for startups and modern applications

---

### Private Cloud
A **private cloud** runs in an organization’s own data center.
- Full control over infrastructure
- Supports legacy systems
- Higher cost and maintenance responsibility

---

###  Hybrid Cloud
A **hybrid cloud** combines public and private clouds.
- Keeps sensitive or legacy workloads on-premises
- Uses public cloud for scalability and innovation
- Common in large enterprises

---

## Economic Concepts in the Cloud

###  Economies of Scale
**Economies of scale** allow cloud providers to offer lower costs because they purchase hardware and operate infrastructure at massive scale.

---

### Capital Expenditure (CapEx)
**CapEx** is upfront spending on physical infrastructure such as servers and data centers.
- Common in on-premises environments

---

### Operational Expenditure (OpEx)
**OpEx** is ongoing spending based on usage.
- Pay-as-you-go
- Common in cloud environments

---

### 1 Consumption-Based Pricing
You pay only for what you use.
- Billed per minute, per GB, or per execution
- Example: Virtual Machines, Storage, Azure Functions

---

### Fixed Pricing Model
Resources are provisioned at a fixed cost.
- Predictable monthly pricing
- Example: Reserved instances or AI commitment tiers

---

## Serverless Computing
**Serverless computing** is a cloud execution model where the cloud provider automatically manages infrastructure.
- Stateless
- Event-driven
- Scales automatically
- Pay-per-execution

---

##  Platform as a Service (PaaS)
**PaaS** provides a managed platform for building and deploying applications.
- No server management
- More control than serverless
- Requires configuration for scaling

---

##  Serverless vs PaaS

| Feature | Serverless | PaaS |
|------|----------|------|
| Scaling | Automatic | Configured |
| Execution | Event-driven | Always running |
| Billing | Per execution | Per instance |
| Control | Less | More |

---

## Azure Serverless Services

### 1.9.1 Azure Logic Apps
**Azure Logic Apps** automate workflows using pre-built connectors.
- No-code / low-code
- Integrates with Microsoft and third-party services

---

###  Azure Functions
**Azure Functions** run code in response to events.
- Event-triggered
- Supports multiple programming languages
- Billed per execution

---

###  Azure Event Grid
**Azure Event Grid** routes events using a publish-subscribe model.
- Push-based event delivery
- Commonly used with Functions and Logic Apps

---

##  Availability and Reliability Concepts

###  Availability
* **Availability** measures how accessible a service is over time.
*  Expressed in “nines” (99.9%, 99.99%)



###  Scalability
* **Scalability** is the ability to handle increased workloads by adding resources.


### Elasticity
* **Elasticity** is the ability to automatically scale resources up and down based on demand.


### Agility
* **Agility** is the speed at which resources can be provisioned and deprovisioned.



###  Fault Tolerance
* **Fault tolerance** allows systems to continue operating when individual components fail.



###  High Availability
* **High availability** ensures services remain operational for long periods of time.



### 1.10.7 Disaster Recovery
**Disaster recovery** focuses on restoring services after a major outage.

## Domain 2: Azure Architecture and Services

### 2.1 Core Architectural Components
* **Geography:** Market typically containing 2+ regions
* **Region:** Set of datacenters connected by a low-latency network such as US EAST
* **Region Pairs:** Two regions within the same geography usually >300 miles apart) paired for disaster recovery updates, such as US East and US West
* **Availability Zones (AZs):** Unique physical locations within a region with independent power, cooling, and networking. Protects against datacenter failures.

* **Resource Hierarchy:**
    1.  **Management Groups:** Governance across multiple subscriptions.
    2.  **Subscriptions:** Billing/Management boundary.
    3.  **Resource Groups:** A logical container for resources sharing a lifecycle.
    4.  **Resources:** Instances of services (VMs, Storage Accounts, etc.).

### 2.2 Compute and Networking Services
* **Compute Options:**
    * **Azure Virtual Machines (VMs):** IaaS. Control over OS.
    * **VM Scale Sets:** A group of identical load-balanced VMs that auto-scale.
    * **Availability Sets:** Protects against hardware failures.
    * **Azure Virtual Desktop (AVD):** Cloud VDI, windows 10 and 11.
    * **Containers:**
        * **Azure Container Instances (ACI):** Container on demand.
        * **Azure Kubernetes Service (AKS):** Orchestrated container management, for example, having prod and a testing branch.
    * **Azure App Service:** PaaS for hosting web apps/APIs.
* **Networking:**
    * **Virtual Network (VNet):** Logical representation of your network in cloud.
    * **Subnets:** Segmentation of VNet IP space.
    * **VNet Peering:** Connecting two Azure VNets.
    * **VPN Gateway:** Encrypted traffic over public internet (Site-to-Site).
    * **ExpressRoute:** Private connection to Azure
    * **Azure DNS:** Hosting service for DNS domains.

### 2.3 Storage Services
* **Storage Accounts Types:**
    * **Blob Storage:** Unstructured data such as Images, Video, and backups.
    * **Disk Storage:** Block storage for VMs.
    * **File Storage:** Managed file shares such as SMB/NFS.
    * **Table Storage:** NoSQL key-attribute store.
    * **Queue Storage:** Store large numbers of messages.
* **Access Tiers:**
    * **Hot:** Frequent access, highest storage cost, lowest access cost.
    * **Cool:** Infrequent access (30 days), lower storage cost.
    * **Cold:** Rarely accessed (90 days).
    * **Archive:** Rare access (180 days), lowest storage cost, highest hydration cost/time.
* **Redundancy:**
    * **LRS (Locally Redundant):** 3 copies in 1 datacenter.
    * **ZRS (Zone Redundant):** 3 copies across Availability Zones.
    * **GRS (Geo-Redundant):** Copy to secondary region RS in primary + LRS in secondary.
    * **GZRS (Geo-Zone Redundant):** ZRS in primary + LRS in secondary.
      
* **Migration Tools:**
    * **AzCopy:** CLI tool for data transfer.
    * **Azure Storage Explorer:** GUI for managing storage.
    * **Azure File Sync:** Sync on-prem file server with Azure Files.
    * **Azure Migrate:** Hub for migration assessment and execution.
    * **Azure Data Box:** Physical device to move TBs of data offline.

### 2.4 Identity, Access, and Security
* **Microsoft Entra ID (formerly Azure AD):** Cloud-based identity and access management service.
    * **Authentication (AuthN):** Verifying you are who you say you are.
    * **Authorization (AuthZ):** Verifying what you have permission to do.
* **Authentication Methods:**
    * **SSO (Single Sign-On):** Log in once, access many apps.
    * **MFA (Multi-Factor Authentication):** Something you know + have + are.
    * **Passwordless:** Windows Hello, Authenticator App, FIDO2 keys.
* **Access Control:**
    * **Conditional Access:** "If/Then" policies based on signals from User, Location, Device Risk.
    * **RBAC (Role-Based Access Control):** Fine-grained access management, such as Reader, Contributor, Owner.
* **Zero Trust Model:**
    1.  Verify Explicitly.
    2.  Use Least Privilege Access.
    3.  Assume Breach.
* **Security Tools:**
    * **Defender for Cloud:** CSPM (Cloud Security Posture Management) and workload protection.
    * **Network Security Groups (NSG):** Basic firewall (Allow/Deny rules) for subnets/NICs.
    * **Azure Firewall:** Managed, stateful firewall service.
    * **DDoS Protection:** Basic (Free/Default) vs. Standard (Paid/Enhanced features).

---

## Domain 3: Azure Management and Governance

### 3.1 Cost Management
* **Factors affecting cost:** Resource type, Service, Location, Ingress/Egress.
* **Reducing Costs:**
    * **Reserved Instances:** 1 or 3-year commitment for VMs up to 72% savings.
    * **Hybrid Use Benefit:** Bring on-prem Windows/SQL licenses to the cloud.
    * **Spot Pricing:** Use unused capacity for deep discounts.
* **Tools:**
    * **Pricing Calculator:** Estimate costs *before* deployment.
    * **TCO Calculator:** Estimate savings by moving from on-prem to Azure *before* deployment.
    * **Cost Management:** Monitor and optimize costs *after* deployment.
    * **Tags:** Metadata (Name:Value pairs) to organize resources like `Cost Center: IT`.

### 3.2 Governance and Compliance
* **Azure Policy:** Enforce rules/effects on resources like "Only allow VMs in East US".
* **Initiatives:** A collection of policies.
* **Resource Locks:** Prevent accidental deletion/modification. Can lock at the Subscription, Resource Group, or Resource level.
* **Service Trust Portal:** Access audit reports and compliance docs.
* **Microsoft Purview:** Unified data governance such as Data discovery and classification.
* **Azure Arc:** Extends Azure management to on-prem and other clouds, such as Multicloud management.

### 3.3 Management and Deployment Tools
* **Azure Portal:** Web-based UI.
* **Cloud Shell:** Browser-based CLI, for example, Bash or PowerShell.
* **Azure PowerShell / CLI:** Scripting and command-line management.
* **ARM Templates:** Infrastructure as Code, like json. Declarative and Idempotent.
* **Bicep:** Newer, simpler Infrastructure as Code language abstraction over ARM.

### 3.4 Monitoring Tools
* **Azure Advisor:** Personalized recommendations for HA, Security, Performance, and Cost.
* **Azure Service Health:** Status of Azure global services, such as outages and planned maintenance.
* **Azure Monitor:** Collects metrics and logs.
    * **Log Analytics:** Query logs using KQL (Kusto Query Language).
    * **Alerts:** Proactive notifications based on metrics/logs.
    * **Application Insights:** APM (Application Performance Monitoring) for developers that detects code-level issues.
