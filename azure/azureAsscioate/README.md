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

## Key Takeaways

* Complete user properties fully
* Set Usage Location before assigning licenses
* Use Security Groups for permissions and role assignments
* Use Microsoft 365 Groups for collaboration
* Dynamic groups automate membership using rules
* Deleted users are recoverable for 30 days
