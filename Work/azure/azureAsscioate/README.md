# Administer Identity Module: Microsoft Entra ID Essentials

## PART 1: ENTRA


## Overview
Microsoft Entra ID is a cloud-based Identity and Access Management (IAM) service designed to help organizations secure and manage access to resources. This module covers the transition from on-premises Active Directory to the cloud, core Entra ID concepts, synchronization, licensing, and Self-Service Password Reset (SSPR).

---

## On-Premises Active Directory vs. Microsoft Entra ID
Transitioning from an on-premises environment (like Contoso's local setup) to the cloud changes how identities and infrastructure are managed.


* ENTRA: cloud-based service; no server deployment required,  OAuth, OpenID Connect, SAML, WS-Federation (HTTPS-based), Flat structure, managed via web portals, conditional access
*  ONPREM: Requires physical/virtual servers and OS setup (e.g., Windows Server),  NTLM, Kerberos, LDAP | OAuth, OpenID Connect, SAMv,  Hierarchical structure, Organizational Units (OUs), Group Policy Objects (GPOs)

---

## Core Cloud Concepts & Terminology

* **Identity:** An object that can authenticate.
* **Account:** The data associated with an identity.
* **Microsoft Entra Account:** An account created within Microsoft Entra ID or other Microsoft cloud services.
* **Tenant:** A dedicated instance representing your organization in the cloud. Creating a tenant automatically provisions the Entra ID back-end service.
* **Global Administrator:** The first user created during the setup process automatically receives this role, granting the highest level of access to manage Entra ID.

---

## Hybrid Environments & Entra ID Connect
Organizations do not need to recreate their existing on-premises users in the cloud. 

### Entra ID Connect
This service bridges the gap between on-premises Active Directory and Microsoft Entra ID.
* **Hybrid State:** Syncs on-premises users (e.g., "User 1") to the cloud, allowing them to authenticate seamlessly for cloud resources like `office.com`.
* **Writeback Options:** By default, syncing is typically one-way (on-prem to cloud). However, features like **Password Writeback** can be enabled. If a hybrid user changes their password in the cloud portal, this feature ensures the new password syncs back to their on-premises Active Directory, preventing the user from having to manage two separate passwords.

---

## Microsoft Entra ID Licensing Plans
Features vary depending on the organizational plan selected:

* **Free Plan:** Includes Single Sign-On (SSO), support for up to 500,000 objects, and basic Multi-Factor Authentication (MFA).
* **Premium P1 & P2:** Unlocks advanced features, conditional access, and broader self-service capabilities. 
* **Entra Suite:** Designed for organizations needing advanced Privileged Identity Management (PIM) and complex identity governance.

---

## Self-Service Password Reset (SSPR)
SSPR lessens the administrative burden by allowing users to reset their own passwords securely.

### SSPR Status Options
1.  **None:** Disabled for everyone.
2.  **All:** Enabled for the entire organization.
3.  **Selected:** Enabled for a specific group. *(Note: You can only target **one** group, though group nesting is permitted.)*

### Authentication Methods
To securely reset a password, users must register authentication methods (e.g., an Authenticator app or One-Time Passcodes). 
* **Secret Questions:** Administrators can configure security questions (e.g., picking 3 out of 5 registered questions). Because predefined questions can be vulnerable to social engineering, Microsoft allows the creation of **custom questions**.
* **Administrator Constraint:** Regardless of user settings, administrators are *always* required to register at least **two** different authentication methods for SSPR.

### SSPR Capabilities by License


*  **Free**  Cloud-only users. Can only change a password *if they know their existing password*. 
*  **Premium P1 & P2**  Hybrid and cloud users. Can reset passwords if forgotten, if the account is locked out, or if they just want to change it.

# Administering Identity — Microsoft Entra ID (Part 2)

## Managing Users in Entra ID

All users must have an account in Microsoft Entra ID.

There are two main account types:

* Member Account
  * Internal organizational users
  * Employees, administrators, staff

* Guest / External Account
  * External collaborators
  * Partners, contractors, vendors
  * Created through an invitation process

---

## 2. Creating a Member User Account

Steps:

1. Go to Entra Portal
2. Click Users
3. Select New User
4. Choose Create New User
5. Complete required fields

Required Fields:

* User Principal Name (UPN)
  * Unique login name
  * Must be unique in tenant

* Mail Nickname
  * Auto-derived from UPN
  * Can be manually edited

* Display Name
  * Name shown in Teams, Outlook, etc.

* Password
  * Auto-generated or manually created
  * User must reset at first login

* Account Enabled
  * Enabled = user can sign in
  * Disabled = user cannot sign in

---

## 3. Important User Properties

It is recommended to complete as many properties as possible.

Useful Properties:

* First Name
* Last Name
* Job Title
* Department
* Company
* Manager
* Hire Date
* City
* Usage Location

Usage Location is required before assigning licenses.

Different countries unlock different license features.
If Usage Location is missing, license assignment will fail.

---

## 4. Managing User Accounts

You can:

* Reset Password
* Disable Account
* Revoke Sign-in Sessions
* Delete Account

Deleted users remain recoverable for 30 days.
After 30 days, the account is permanently removed.

---

## 5. Assigning Licenses

Licenses are assigned through:

admin.microsoft.com (Microsoft 365 Admin Center)

Steps:

1. Go to Admin Center
2. Navigate to Licenses
3. Select license (e.g., E5, P2)
4. Assign to user or group
5. Optionally disable specific services (e.g., Clipchamp, Microsoft Loop)
6. Confirm assignment

Users must have a Usage Location before license assignment.

---

## 6. Managing Groups

Groups help organize users and control access.

Two Group Types:

* Security Group
  * Used for permissions, apps, roles
  * Can include users, devices, service principals, other groups
  * Supports group nesting

* Microsoft 365 Group
  * Used for collaboration
  * Mailbox, calendar, SharePoint, Teams
  * Only users can be members

---

## 7. Group Membership Types

* Assigned
  * Admin manually adds members

* Dynamic User
  * Members added automatically based on rules

* Dynamic Device
  * Devices added automatically (Security Groups only)

---

## 8. Dynamic Membership Rules

Rules are based on user properties.

Example Rule:

user.department -eq "IT"

This adds users whose department equals IT.

Example with AND:

user.department -eq "IT" -and user.companyName -ne "Fabricam"

User must:
* Be in IT
* Not belong to Fabricam

Example with OR:

(user.department -eq "IT" -and user.companyName -ne "Fabricam") -or user.city -eq "London"

This means:
* Either both IT and not Fabricam
* OR city equals London

AND = both conditions must be true  
OR = either condition can be true  

Dynamic groups do NOT allow manual member additions.

---

## 9. Group-Based License Assignment

Licenses can be assigned to groups.

Requirements:
* Must have enough available licenses
* Members automatically inherit the license

This simplifies large-scale user management.

---


# Azure Administrative Governance & Compliance

## Module Overview
This module covers how to manage and govern Azure environments.

Topics covered:
- Azure core architecture
- Azure regions
- Azure subscriptions
- Management groups
- Resource groups
- Tags
- Resource locks
- Cost management
- Azure Policy
- Policy Initiatives
- Role-Based Access Control (RBAC)

Goal: Understand how to effectively organize, secure, and manage Azure resources.

---

# Azure Core Architecture

Azure resources are organized in a hierarchical structure:

```
Management Groups
    ↓
Subscriptions
    ↓
Resource Groups
    ↓
Resources
```

### Resources
Resources are the actual services you create in Azure.

Examples:
- Virtual Machines (VMs)
- Virtual Networks (VNets)
- Load Balancers
- Storage Accounts
- Firewalls
- Web Apps

All resources must be placed inside a **Resource Group**.

---

# Azure Regions

Azure operates globally with many regions.

- 60+ regions worldwide
- Distributed across many countries
- Each region contains one or more data centers

### Availability Zones

Availability Zones provide:
- Fault isolation
- High availability
- Disaster protection

Regions may have:
- 1 zone
- Up to 3 zones

Example:

| Region | Availability Zones |
|------|------|
| UK West | 1 |
| UK South | 3 |

### Region Pairs

Each Azure region has a **paired region**.

Purpose:
- Disaster recovery
- Data redundancy

Characteristics:
- Usually **~300 miles apart**
- Protects against large regional outages.

### Choosing a Region

Reasons to select specific regions:

1. **Latency**
   - Place resources near users.

2. **Compliance**
   - Some regulations require data to remain in specific countries.

3. **Service availability**
   - Not all services are available in all regions.

---

# Azure Subscriptions

A **subscription** is required to create resources in Azure.

Purpose:
- Billing boundary
- Security boundary
- Resource organization

Without a subscription:
- Resources cannot be created.

### Multiple Subscriptions

Organizations often create multiple subscriptions.

Example:

```
Account
 ├ Dev Subscription
 ├ Test Subscription
 └ Production Subscription
```

Benefits:
- Separate billing
- Separate security controls
- Easier cost tracking

Each subscription:
- Has its own billing
- Can contain multiple users

### Subscription Security

Users inside a subscription **cannot access other subscriptions** unless permissions are granted.

---

# Types of Azure Subscriptions

### Free Trial
- $200 credit
- 30 days

### Pay-As-You-Go
- Pay for what you use

### Enterprise Agreement
- Large organizations
- Long-term contracts

### Cloud Solution Provider (CSP)
- Purchased through partners

### Student Subscription
- $100 credit
- 12 months

---

# Management Groups

Management groups allow administrators to manage **multiple subscriptions together**.

Example hierarchy:

```
Root Management Group
 ├ Human Resources
 │   └ HR Subscription
 ├ IT
 │   └ Production Subscription
 └ Marketing
```

### Benefits

Management groups allow:
- Policy enforcement
- Access control
- Governance across subscriptions

### Limits

- Maximum **6 hierarchy levels**
- Maximum **10,000 objects**

Root management group **does not count** toward the 6 levels.

---

# Resource Groups

Resource groups are **containers that hold Azure resources**.

Example:

```
Resource Group: WebProject

Contains:
- Virtual Machine
- Storage Account
- Database
```

### Key Characteristics

Resource groups:

- Cannot be renamed
- Cannot contain other resource groups
- Must belong to a subscription
- Can contain many resource types

### Best Practice

Group resources by **project or workload**.

Deleting a resource group **deletes all resources inside it**.

---

# Resource Group Regions

Resource groups are created in a region.

However, resources inside them **can be located in different regions**.

Example:

```
Resource Group Location: UK South

VM: East US
Storage: UK South
```

---

# Tags

Tags are labels applied to resources.

Tags are **key-value pairs**.

Example:

```
Department: IT
Owner: Admin
Environment: Production
```

Tags help with:
- Cost tracking
- Resource organization
- Filtering reports

---

# Resource Locks

Resource locks prevent accidental changes.

### Read-Only Lock
Prevents:
- Modifications
- Deletion

Users can only **view** the resource.

### Delete Lock

Prevents:
- Deleting the resource

But still allows:
- Modifications

Locks can be applied at:
- Subscription
- Resource group
- Individual resource

Locks **cannot be applied to management groups**.

---

# Azure Cost Considerations

Costs depend on:

- Resource type
- Resource size
- Region
- Data transfer

### Data Transfer

| Type | Cost |
|-----|-----|
| Ingress (incoming) | Usually free |
| Egress (outgoing) | Charged |

---

# Cost Optimization

### Reserved Instances
Reserve resources for:

- 1 year
- 3 years

Savings up to **72%**.

### Azure Hybrid Benefit
Use existing licenses for:
- Windows Server
- SQL Server

### Budgets
Budgets allow:
- Tracking spending
- Alert notifications

### Azure Advisor
Provides recommendations for:

- Cost optimization
- Performance improvements
- Security
- Reliability

---

# Azure Policy

Azure Policy allows administrators to **enforce rules and compliance** across resources.

Policies help control:

- Resource types
- Resource locations
- Allowed SKUs
- Required tags
- Security settings

### Why Use Policies

Organizations may need policies for:

- Compliance requirements
- Security standards
- Cost control
- Organizational governance

Example restrictions:

- Limit which regions resources can be deployed to
- Restrict expensive VM sizes
- Require tags for billing tracking
- Require backup settings

---

# Azure Policy Components

Three main components:

### 1. Policy Definition

Defines **what rule should be enforced**.

Examples:

- Allowed locations
- Allowed VM sizes
- Require tags

Azure includes many **built-in policy definitions**.

You can also create **custom policies**.

---

### 2. Policy Scope

Defines **where the policy applies**.

Policies can be applied to:

- Management Groups
- Subscriptions
- Resource Groups

Policies **cannot be applied directly to individual resources**.

---

### 3. Compliance Reports

Compliance reports show:

- Compliant resources
- Non-compliant resources

Non-compliant resources:

- Are **not automatically deleted**
- Continue to function
- Are flagged for administrators

---

# Policy Enforcement Timing

Policy enforcement typically takes:

**5 – 15 minutes**

After enforcement:

- New resources violating policy **cannot be created**
- Existing resources may appear **non-compliant**

---

# Remediation Tasks

Remediation tasks attempt to automatically fix policy violations.

Examples:

- Automatically add missing tags
- Apply configuration settings

Some tasks **cannot be automated**, such as moving a resource to another region.

---

# Policy Initiatives

Policy initiatives allow administrators to **group multiple policies together**.

Example:

Instead of assigning 100 policies individually:

```
Policy Initiative
 ├ Policy 1
 ├ Policy 2
 ├ Policy 3
 └ Policy 4
```

Benefits:

- Easier policy management
- Reduced administrative effort
- Reusable governance templates

Initiatives can be applied to:

- Management groups
- Subscriptions
- Resource groups

---

# Role-Based Access Control (RBAC)

RBAC controls **who can access Azure resources and what they can do**.

Also known as:

- IAM (Identity and Access Management)
- Access Control

RBAC can be applied at multiple levels:

- Management Group
- Subscription
- Resource Group
- Individual Resource

---

# RBAC Role Assignment

Roles determine **what actions users can perform**.

When a user creates a resource:

- They automatically become the **Owner**.

---

# Common RBAC Roles

### Owner

Highest level of access.

Permissions:
- Read
- Write
- Delete
- Assign permissions

Owner can **fully manage resources and access**.

---

### Contributor

Contributor can:

- Create resources
- Modify resources
- Delete resources

Contributor **cannot change permissions**.

---

### Reader

Reader can:

- View resources

Reader **cannot modify or delete resources**.

---

# User Access Administrator

Special role that allows:

- Managing user access
- Assigning roles
- Changing permissions

This role is often used by **administrators managing access control**.

---

# Principle of Least Privilege

Security best practice:

Users should receive **only the permissions they need**.

Example:

Instead of giving **Contributor on entire subscription**:

Assign:

```
Virtual Machine Contributor
```

This allows users to manage VMs but not other resources.

---

# Role Scope Strategy

RBAC can be applied at different scopes.

Example:

Assign at:

- Resource → limited access
- Resource group → access to all resources in group
- Subscription → access to everything

Best practice:

**Use the narrowest scope possible.**

---

# Built-in Roles

Azure includes **hundreds of predefined roles**.

Examples:

- Owner
- Contributor
- Reader
- Virtual Machine Contributor
- Storage Account Contributor
- Network Contributor

Roles define permissions using **JSON definitions**.

---

# Custom Roles

If built-in roles are insufficient:

Administrators can **create custom roles**.

Custom roles define:

- Allowed actions
- Denied actions
- Assignable scopes

Custom roles provide **fine-grained permission control**.

---

# Key Takeaways

Azure governance is built around several core mechanisms:

### Architecture

```
Management Groups
 → Subscriptions
 → Resource Groups
 → Resources
```

### Governance Tools

- Tags
- Resource Locks
- Azure Policy
- Policy Initiatives
- RBAC
- Budgets
- Azure Advisor

### Security Principles

- Least privilege access
- Controlled resource deployment
- Compliance monitoring

These tools allow organizations to **secure, manage, and scale Azure environments effectively**.


# Administer Virtual Networking (Azure) – Notes

## Overview
- Covers:
  - Virtual Networks (VNets)
  - Subnets
  - IP Addressing
  - Network Security Groups (NSGs)
  - Azure DNS (later)

---

## Virtual Network (VNet) Planning

### Why Planning Matters
- Creation is easy → planning is critical
- Key considerations:
  - **Region/location**
    - Resources must be in the same region as the VNet
  - **IP address scheme**
  - **Subnet sizing**
  - **Future connectivity needs**

### Important Rule
- ❗ No overlapping IP ranges between VNets if they will communicate

---

## IP Addressing Basics

### IPv4 vs IPv6
- Azure supports both
- Focus here: IPv4

### Private IP Ranges (RFC 1918)
Used for internal networks:

- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

### Public vs Private IPs
- **Private IPs**
  - Free
  - Used inside VNets
- **Public IPs**
  - Cost money
  - Used for internet access

---

## Subnets & Addressing

### Example
- VNet: `10.0.0.0/16`
- Subnet: `10.0.1.0/24`

### Address Count
- `/24` = 256 total addresses

### Azure Reserved IPs
Azure reserves **5 IP addresses per subnet**:
1. Network address (`.0`)
2. Gateway (`.1`)
3. DNS (`.2`)
4. DNS (`.3`)
5. Broadcast (`.255`)

**Usable IPs:**
- `256 - 5 = 251`

---

## Creating a Virtual Network

### Required Fields
- Subscription
- Resource Group
- Name
- Region

### Key Configurations
- Address space (CIDR)
- At least **one subnet required**

### Optional Features
- Encryption
- DDoS protection
- Firewall

### Notes
- You can add multiple address ranges to a VNet
- You cannot change address range after resources are deployed (without removing them)

---

## Subnets

- Required for placing resources
- Resources must live inside a subnet
- Can:
  - Adjust size (/24, /26, etc.)
  - Add more later

---

## Public IP Addresses

### Key Points
- Azure assigns IP automatically (cannot choose manually)
- Types:
  - IPv4 / IPv6
- SKU:
  - Standard only
- Allocation:
  - Static only (for Standard SKU)

### Routing Options
- Microsoft network (default)
- Internet routing

---

## Network Security Groups (NSGs)

### What is an NSG?
- Acts as a firewall for Azure resources
- Filters traffic using rules

### Uses 5-Tuple Filtering
- Source IP
- Destination IP
- Source Port
- Destination Port
- Protocol (TCP/UDP)

---

## NSG Placement

NSGs can be applied to:
- Subnet
- Network Interface Card (NIC)

### Important Rules
- One resource can only have **one NSG**
- One NSG can be applied to **multiple resources**

---

## NSG Traffic Flow

### If applied at both subnet and NIC:
Traffic must be allowed at **both levels**

Example:
- Port 80 allowed at subnet ✅
- Port 80 blocked at NIC ❌  
→ Traffic is blocked

---

## NSG Rules

### Default Rules (Cannot Change)

Inbound:
- Allow VNet traffic
- Allow Azure Load Balancer
- Deny all others

Outbound:
- Allow VNet traffic
- Allow Internet
- Deny all others

---

## Custom NSG Rules

### Rule Components
- Source (IP, service tag, etc.)
- Destination
- Port
- Protocol
- Action (Allow/Deny)
- Priority

### Priority
- Range: `100 – 4096`
- Lower number = higher priority
- Rules processed top-down

### Example
Allow HTTP:
- Port: 80
- Protocol: TCP
- Action: Allow

---

## Key NSG Notes
- Default "deny all" exists → no need to manually deny everything
- Max ~1000 rules per NSG
- Leave gaps in priority numbers for future rules

---

