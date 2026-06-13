# Implement Group Policy in Active Directory Domain Services (AD DS) on Windows Server 2022

---

# Lab Info

| Item | Value |
|--------|--------|
| Domain Name | thantzinaung.com |
| Server OS | Windows Server 2022 |
| Feature | Group Policy Objects (GPOs) |
| Management Tool | Group Policy Management Console (GPMC) |
| Domain Controller | TZA-DC1 |
| Lab Type | Active Directory Domain Services |

---

# Lab Objectives

After completing this lab, you will be able to:

- Understand Group Policy architecture in Active Directory
- Create and manage Group Policy Objects (GPOs)
- Configure Computer and User policies
- Deploy software using Group Policy
- Configure startup, shutdown, logon, and logoff scripts
- Implement Security Filtering and WMI Filtering
- Configure Block Inheritance and Enforced policies
- Troubleshoot Group Policy processing
- Generate Group Policy reports

---

# Overview

## What is Group Policy?

Group Policy is a centralized management feature in Active Directory that allows administrators to configure and enforce settings across users and computers within a domain.

Using Group Policy, administrators can:

- Configure security settings
- Deploy software
- Restrict user actions
- Run scripts automatically
- Configure Windows features
- Standardize desktop environments

A single GPO can affect hundreds or thousands of domain-joined computers.

---

# Group Policy Infrastructure

## Group Policy Management Console (GPMC)

The primary tool used to manage Group Policies is:

```text
Group Policy Management Console (GPMC)
```

Launch it from:

```text
Server Manager
→ Tools
→ Group Policy Management
```

---

## GPO Storage Locations

### Active Directory Storage

GPO information is stored inside the Active Directory Domain Partition.

```text
thantzinaung.com
```

The GPO metadata replicates automatically between all Domain Controllers.

---

### SYSVOL Storage

The actual policy files are stored in:

```powershell
C:\Windows\SYSVOL\domain\Policies
```

Example:

```powershell
C:\Windows\SYSVOL\domain\Policies\{GUID}
```

Each folder represents a specific GPO.

---

## Backing Up GPOs

To protect Group Policy configurations:

### Manual Backup

Backup the following folder:

```powershell
C:\Windows\SYSVOL\domain\Policies
```

### GPMC Backup

```text
Group Policy Management
→ Group Policy Objects
→ Right Click GPO
→ Back Up
```

---

# Default Group Policies

Active Directory creates two GPOs automatically.

---

## Default Domain Policy

Applies to:

```text
Entire Domain
```

Common settings:

- Password Policy
- Account Lockout Policy
- Kerberos Policy

---

## Default Domain Controllers Policy

Applies to:

```text
Domain Controllers OU
```

Used for:

- DC Security Settings
- User Rights Assignment
- Audit Configuration

---

## Best Practice

Avoid making extensive modifications to:

- Default Domain Policy
- Default Domain Controllers Policy

Instead:

```text
Create new GPOs for specific tasks
```

This simplifies troubleshooting and future maintenance.

---

# Starter GPOs

## What are Starter GPOs?

Starter GPOs function as templates.

They allow administrators to pre-configure settings and reuse them when creating new GPOs.

Example:

```text
Disable Desktop Wallpaper
Disable Control Panel
Hide Network Settings
```

---

## Create a Starter GPO

```text
Group Policy Management
→ Starter GPOs
→ New
```

Example Name:

```text
Corporate Desktop Standard
```

---

# Understanding GPO Configuration Types

Every GPO contains two major sections.

---

## Computer Configuration

Applies to:

```text
Computers
```

Location:

```text
Computer Configuration
```

Can do:

- Windows Firewall
- Software Installation
- Security Policies
- Startup Scripts

---

## User Configuration

Applies to:

```text
Users
```

Location:

```text
User Configuration
```

Can do:

- Desktop Restrictions
- Control Panel Settings
- Logon Scripts
- Folder Redirection

---

## Conflict Resolution

If Computer Configuration and User Configuration conflict:

```text
Computer Configuration Wins
```

---

# Creating a New GPO

## Example: Disable Control Panel

### Step 1

Open:

```text
Group Policy Management

Rright-Click  > New > Starter Setting

Right-Clicck > Edit > User Configuration > Desktop > Desktop > Desktop WAllpaper > Disabled
```

---

### Step 2

Right-click:

```text
Group Policy Objects  > Right Click > New
Name: Sales Desktop Setting
Source Starter GPO: Starter Setting
```
Andalso add * Finance Desktop Setting and HR Desktop Setting * further more you need.


---

### Step 3

```text
Right Click > Sales Desktop Setting > 
Edit > User Configuration > Policies > Administrative 
Templates: > Desktop > Desktop > 
Disabled : Desktop Wallpaper
```

---

# Policies vs Preferences

Understanding the difference is critical.

---

## Policies

Policies force settings.

Characteristics:

- Cannot be modified by users
- Often gray out options
- Enforced by administrators

Example:

```text
Disable Task Manager
```

---

## Preferences

Preferences provide default settings.

Characteristics:

- User can change later
- Not enforced permanently

Example:

```text
Map Network Drive
Set Desktop Wallpaper
Create Registry Key
```

Location:

```text
User Configuration
→ Preferences
```

---

# Software Deployment using GPO

Group Policy can deploy MSI applications.

---

## Deployment Requirements

Application must be:

```text
MSI Package
```

Stored on:

```text
Shared Network Folder
```

Example:

```text
\\TZA-DC1\Software\7zip.msi
```

---

## Create Software Deployment GPO

Navigate:

```text
Computer Configuration
→ Policies
→ Software Settings
→ Software Installation
```

Right Click:

```text
New Package
```

Select:

```text
\\TZA-DC1\Software\7zip.msi
```

---

## Deployment Methods

### Assigned

Installation is mandatory.

```text
Automatically installs
```

---

### Published

Application becomes available for installation.

```text
Control Panel
→ Programs and Features
→ Install Application
```

---

# Scripts in Group Policy

## Startup Script

Runs when computer starts.

Location:

```text
Computer Configuration
→ Policies
→ Windows Settings
→ Scripts
→ Startup
```

---

## Shutdown Script

Runs during shutdown.

Location:

```text
Computer Configuration
→ Policies
→ Windows Settings
→ Scripts
→ Shutdown
```

---

## Logon Script

Runs when user signs in.

Location:

```text
User Configuration
→ Policies
→ Windows Settings
→ Scripts
→ Logon
```

---

## Logoff Script

Runs when user signs out.

Location:

```text
User Configuration
→ Policies
→ Windows Settings
→ Scripts
→ Logoff
```

---

# Inheritance and Overrides

Group Policies follow inheritance.

Example:

```text
Domain
 └── Sales OU
      └── InsideSales OU
```

Policies flow downward automatically.

---

## Block Inheritance

Prevents parent policies from applying.

Example:

```text
Sales OU
→ Block Inheritance
```

Result:

```text
Domain-level GPOs blocked
```

---

## Enforced

Overrides Block Inheritance.

Example:

```text
Corporate Security Policy
→ Enforced
```

Result:

```text
Applies regardless of Block Inheritance
```

---

## Password Policy Exception

Password policies are special.

Even if:

```text
Block Inheritance Enabled
```

Password policies still apply.

---

# Security Filtering

By default:

```text
Authenticated Users
```

receive the GPO.

---

## Example

Create security group:

```text
InsideSales
```

---

### Configure Filtering

```text
GPO
→ Scope Tab
→ Security Filtering
```

Remove:

```text
Authenticated Users
```

Add:

```text
InsideSales
```

Result:

```text
Only InsideSales members receive policy
```

---

# WMI Filtering

WMI Filtering applies policies based on system characteristics.

---

## Example: Minimum 4GB RAM

Create WMI Filter:

```sql
SELECT * FROM Win32_ComputerSystem
WHERE TotalPhysicalMemory >= 4294967296
```

Result:

```text
Only computers with 4GB RAM or more receive the policy
```

---

## Example: Specific Manufacturer

```sql
SELECT * FROM Win32_ComputerSystem
WHERE Manufacturer = "Dell Inc."
```

Result:

```text
Applies only to Dell computers
```

---

# Testing Policy Application

## Force Policy Update

Execute:

```powershell
gpupdate /force
```

Result:

```text
Immediately refreshes policies
```

---

## Verify Policy Application

Execute:

```powershell
gpresult /r
```

Displays:

- Applied User Policies
- Applied Computer Policies

---

## Generate HTML Report

Execute:

```powershell
gpresult /h c:\temp\gpreport.html
```

Open:

```text
c:\temp\gpreport.html
```

The report shows:

- Applied GPOs
- Denied GPOs
- Security Filtering Results
- WMI Filter Results
- Processing Details

---

# Group Policy Refresh Intervals

## Member Computers and Servers

Automatically refresh every:

```text
90 – 120 Minutes
```

---

## Domain Controllers

Automatically refresh every:

```text
5 Minutes
```

---

# Best Practices

## Recommended

✔ Create separate GPOs for separate functions

✔ Use descriptive names

✔ Use Security Filtering where appropriate

✔ Test in a lab OU before production deployment

✔ Back up GPOs regularly

✔ Document all changes

✔ Use Starter GPOs for standardization

---

## Avoid

❌ Excessive modifications to Default Domain Policy

❌ Excessive modifications to Default Domain Controllers Policy

❌ Linking unnecessary GPOs at the Domain root

❌ Complex WMI filters without testing

---

# Lab Summary

In this lab, you successfully:

- Managed GPOs using GPMC
- Examined GPO storage in AD DS and SYSVOL
- Created and linked new GPOs
- Configured Computer and User policies
- Used Policies and Preferences
- Deployed MSI software
- Implemented startup and logon scripts
- Configured Security Filtering and WMI Filtering
- Managed Block Inheritance and Enforced settings
- Performed policy updates using `gpupdate /force`
- Generated troubleshooting reports using `gpresult /h`
- Followed Microsoft best practices for Group Policy administration in Windows Server 2022 and the **thantzinaung.com** domain environment.