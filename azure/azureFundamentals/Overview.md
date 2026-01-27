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
