# Active Directory Group Management in Multi-Domain Forest Scenarios
## Hands-On Lab Guide

### Lab Version
Windows Server Active Directory Domain Services (AD DS)

### Objectives

In this lab, you will learn how to:

- Manage Active Directory groups using administrative tools.
- Understand built-in administrative groups and their functions.
- Create Security Groups with appropriate scopes.
- Manage group membership using both User and Group objects.
- Implement group nesting strategies for efficient permission management.
- Use Universal Groups in multi-domain forests.
- Understand special security principals such as Authenticated Users and Interactive.
- Configure NTFS and Share permissions for network resource access.

---

# 1. Lab Setup and Management Tools

## Active Directory Management Tools

Active Directory groups can be managed using several administrative tools.

### Active Directory Users and Computers (ADUC)

1. Open **Server Manager**.
2. Select **Tools**.
3. Click **Active Directory Users and Computers**.

This is the most commonly used tool for managing:

- Users
- Groups
- Computers
- Organizational Units (OUs)

### Active Directory Administrative Center (ADAC)

ADAC provides a modern management interface with:

- Advanced filtering
- PowerShell integration
- Administrative history
- Recycle Bin management

Both ADUC and ADAC can be used to perform group management tasks.

---

## Group Creation Locations

Groups can be created in:

### Organizational Units (OUs)

Recommended for structured administration.

Example:

```text
Corp
├── Users
├── Groups
└── Computers
```

### Default Users Container

Groups may also be created in:

```text
Users
```

However, using dedicated OUs is considered a best practice.

---

# 2. Understanding Critical Default Groups

Several built-in groups provide administrative capabilities within Active Directory.

## Enterprise Admins

### Scope

Forest-wide administration.

### Capabilities

- Full administrative control across every domain in the forest.
- Create and remove domains.
- Manage trust relationships.
- Delegate permissions throughout the forest.
- Grant themselves Schema Admin privileges.

### Usage

Membership should be tightly controlled and used only when necessary.

---

## Domain Admins

### Scope

Single domain administration.

### Capabilities

- Full control within one domain.
- Create and manage users.
- Manage computers.
- Configure Group Policy.
- Manage domain resources.

### Example

```text
corp.contoso.com
```

A Domain Admin in:

```text
corp.contoso.com
```

does not automatically have administrative rights in:

```text
sales.contoso.com
```

---

## Schema Admins

### Scope

Forest-wide.

### Group Type

Universal Group.

### Capabilities

Allows modification of the Active Directory schema.

Examples:

- Adding attributes.
- Extending schema for applications.
- Updating directory structure.

### Important

By default, only the built-in Administrator account is a member.

Changes made by Schema Admins affect the entire forest.

---

## DNS Admins

### Purpose

Administration of DNS services.

### Responsibilities

- Managing zones.
- Configuring records.
- DNS server administration.
- DNS troubleshooting.

---

## Builtin Container Groups

The **Builtin** container contains Domain Local groups used for administrative delegation.

Examples include:

- Backup Operators
- Account Operators
- Print Operators
- Server Operators

These groups provide permissions specific to a domain or server.

---

# 3. Hands-On Lab: Creating and Configuring Groups

## Exercise 1: Create a Security Group

### Step 1: Open ADUC

Navigate to the desired OU.

Example:

```text
Groups
```

### Step 2: Create Group

Right-click the container.

```text
New
└── Group
```

### Step 3: Configure Group

Example:

```text
Group Name: Sales
Group Scope: Global
Group Type: Security
```

Click:

```text
OK
```

---

## Understanding Group Types

### Security Groups

Used for:

- Access control
- NTFS permissions
- Share permissions
- Delegation

### Distribution Groups

Used only for:

- Email distribution
- Exchange mailing lists

No security permissions are assigned.

---

## Understanding Group Scopes

### Global Group

Contains:

```text
Users
Computers
Other Global Groups
```

From the same domain.

Used primarily for:

```text
Department Membership
```

Examples:

```text
GG_Sales
GG_HR
GG_IT
```

---

### Domain Local Group

Used to assign permissions to resources.

Examples:

```text
DL_Modify_SalesDB
DL_Read_HRDocs
```

---

### Universal Group

Used in multi-domain forests.

Can contain:

```text
Global Groups from multiple domains
```

Used when access spans multiple domains.

---

## Exercise 2: Manage Group Membership

There are two common methods.

### Method 1: Member Of Tab

Open a user account.

Example:

```text
John Smith
```

Select:

```text
Member Of
```

Click:

```text
Add
```

Select desired group.

Example:

```text
GG_Sales
```

Apply changes.

---

### Method 2: Members Tab

Open a group.

Example:

```text
GG_Sales
```

Select:

```text
Members
```

Click:

```text
Add
```

Choose users to include.

Apply changes.

---

## Example Department Structure

Large departments should be subdivided.

### Sales Department

```text
GG_InsideSales
GG_OutsideSales
```

Benefits:

- Easier administration
- Better delegation
- Simplified reporting
- Flexible permission assignments

---

# 4. Advanced Strategy: Group Nesting and Permissions

## Why Group Nesting Matters

A common mistake is assigning permissions directly to many users or groups.

Example:

```text
Folder ACL
├── User1
├── User2
├── User3
├── User4
├── Group1
├── Group2
└── Group3
```

### Performance Impact

Every security principal has a Security Identifier (SID).

When permissions are evaluated:

- ACL entries must be processed.
- SIDs must be resolved.
- Token evaluation increases.

Large ACLs increase administrative complexity and can negatively impact performance.

---

## Recommended Model

### AGDLP Strategy

```text
Accounts
  ↓
Global Groups
  ↓
Domain Local Groups
  ↓
Permissions
```

### Example

#### Create Department Groups

```text
GG_InsideSales
GG_OutsideSales
```

Add users into the Global Groups.

#### Create Resource Access Group

```text
DL_Modify_SalesDB
```

Domain Local Group.

#### Nest Groups

```text
DL_Modify_SalesDB
├── GG_InsideSales
└── GG_OutsideSales
```

#### Assign Permissions

Open folder:

```text
SalesDB
```

Security Tab:

```text
Add:
DL_Modify_SalesDB
```

Grant:

```text
Modify
```

Result:

```text
Users
  ↓
Global Groups
  ↓
Domain Local Group
  ↓
Folder Permission
```

Much easier to manage and scale.

---

## Multi-Domain Forest Strategy

### AGUDLP Model

```text
Accounts
 ↓
Global Groups
 ↓
Universal Groups
 ↓
Domain Local Groups
 ↓
Permissions
```

### Example

#### Domain A

```text
GG_Sales_US
```

#### Domain B

```text
GG_Sales_Europe
```

#### Universal Group

```text
UG_GlobalSales
```

Contains:

```text
GG_Sales_US
GG_Sales_Europe
```

#### Resource Access Group

```text
DL_Modify_SalesDB
```

Contains:

```text
UG_GlobalSales
```

Assign:

```text
Modify Permission
```

to the Domain Local Group.

This design is ideal for multi-domain forests.

---

# 5. Special Groups and Network Access

Certain security principals are hidden and do not appear as traditional groups in ADUC.

They become visible when configuring permissions.

## Authenticated Users

### Represents

All users successfully authenticated by Active Directory.

Includes:

- Domain Users
- Service Accounts
- Computer Accounts

Excludes:

- Anonymous users

### Common Usage

Read access to:

```text
Shared Resources
```

and

```text
Group Policy
```

---

## Interactive

### Represents

Users logged on locally to a computer.

Examples:

```text
Keyboard Login
Console Session
Remote Console Session
```

### Typical Scenario

Grant access only to users physically or directly logged into a machine.

---

## Network

### Represents

Users accessing a resource across the network.

Examples:

```text
\\FILESERVER\Sales
```

or

```text
Mapped Drives
```

This differs from Interactive access.

---

## Everyone

### Represents

All users:

- Authenticated
- Anonymous

### Recommendation

Avoid assigning permissions to:

```text
Everyone
```

unless there is a specific business requirement.

Using:

```text
Authenticated Users
```

is generally safer.

---

# NTFS vs Share Permissions

When resources are accessed locally:

```text
NTFS Permissions
```

apply.

When resources are accessed over the network:

```text
NTFS Permissions
AND
Share Permissions
```

both apply.

The most restrictive permission wins.

## Share Permission Equivalents

| Share Permission | NTFS Equivalent |
|------------------|-----------------|
| Read | Read |
| Change | Modify |
| Full Control | Full Control |

Example:

```text
Share Permission:
Change

NTFS Permission:
Modify
```

These provide roughly equivalent functionality.

---

# Best Practices Summary

### Use Global Groups for Users

```text
GG_Sales
GG_HR
GG_IT
```

### Use Domain Local Groups for Resources

```text
DL_Modify_SalesDB
DL_Read_HRDocs
```

### Use Universal Groups in Multi-Domain Forests

```text
UG_GlobalSales
```

### Follow AGDLP or AGUDLP

Single Domain:

```text
A → G → DL → P
```

Multi-Domain Forest:

```text
A → G → U → DL → P
```

### Avoid Direct ACL Assignments

Do not assign permissions directly to individual users whenever possible.

### Prefer Authenticated Users over Everyone

Improves security by excluding anonymous access.

### Restrict Enterprise Admin and Schema Admin Membership

These groups have forest-wide impact and should be tightly controlled.

---

# Lab Completion Checklist

- [ ] Opened ADUC and ADAC
- [ ] Identified Enterprise Admins, Domain Admins, Schema Admins, and DNS Admins
- [ ] Created a Security Group
- [ ] Configured Global Group scope
- [ ] Added users using the Member Of tab
- [ ] Added users using the Members tab
- [ ] Created Domain Local resource groups
- [ ] Implemented AGDLP nesting
- [ ] Implemented AGUDLP nesting for multi-domain forests
- [ ] Configured NTFS permissions
- [ ] Configured Share permissions
- [ ] Reviewed Special Groups and Security Principals

**End of Lab**

---

![AD_Group_Management](./asset/image/AD_Group_Management.png)