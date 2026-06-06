# Creating and Managing Active Directory Domain Services (AD DS) Users and Organizational Units: Hands-On Lab

## Lab Objectives

I this lab :

* Navigate Active Directory management tools.
* Create and manage Organizational Units (OUs).
* Create and configure user accounts.
* Apply account management best practices.
* Configure advanced user restrictions.
* Delegate administrative control over OUs.
* Remove accidental deletion protection when required.

---

# 1. Active Directory Management Tools

## Active Directory Users and Computers (ADUC)

**Active Directory Users and Computers (ADUC)** is the traditional Microsoft management console used for administering Active Directory objects, including:

* Users
* Groups
* Computers
* Organizational Units (OUs)

Launch ADUC from:

```
Server Manager → Tools → Active Directory Users and Computers
```

or

```
dsa.msc
```

from the Run dialog.

## Active Directory Administrative Center (ADAC)

**Active Directory Administrative Center (ADAC)** is the newer administrative interface introduced with Windows Server 2008 R2 and later versions. ADAC provides:

* Modern management interface
* PowerShell integration
* Advanced administrative capabilities
* Fine-Grained Password Policy management

Launch ADAC from:

```
Server Manager → Tools → Active Directory Administrative Center
```

---

# 2. Understanding OUs vs. Containers

Before creating objects, it is important to distinguish between Organizational Units and system containers.

## Organizational Units (OUs)

OUs are represented by a **folder icon containing a small book**.

Examples:

* Sales
* Finance
* HR
* IT

OUs can:

* Contain users, groups, computers, and other OUs.
* Have Group Policies linked to them.
* Be delegated to specific administrators.

## System Containers

Containers are default Active Directory objects that resemble folders but are not OUs.

Examples:

* Users
* Computers

These containers:

* Cannot have Group Policies directly linked.
* Cannot be delegated in the same manner as OUs.

### Important Note

The **Domain Controllers** object is actually an OU even though it is created automatically during domain setup.

---

# 3. Creating Organizational Units (OUs)

## Scenario

Create departmental OUs for:

* Sales
* Finance
* Human Resources

## Procedure

### Step 1: Open ADUC

Navigate to:

```
Server Manager → Tools → Active Directory Users and Computers
```

### Step 2: Select the Domain

Expand your domain.

Example:

```
thantzinaung.com
```

### Step 3: Create the OU

1. Right-click the domain.
2. Select:

```
New → Organizational Unit
```

### Step 4: Enter OU Name

Example:

```
Sales
```

### Step 5: Verify Protection Setting

Ensure the checkbox remains selected:

```
Protect container from accidental deletion
```

### Step 6: Click OK

Repeat for:

* Finance
* HR

and also add each ou user ou and computer ou
---

# 4. Organizational Design Best Practices

Organizations commonly structure OUs using one of the following models.

## Department-Based Structure

```
thantzinaung.com
│
├── Sales
├── Finance
├── HR
├── IT
└── Operations
```

## Location-Based Structure

```
thantzinaung.com
│
├── Yangon
├── Mandalay
├── Naypyidaw
└── Saging
```

## Hybrid Structure

```
thantzinaung.com
│
├── Yangon
│   ├── Sales
│   ├── Finance
│   └── HR
│
└── Mandalay
    ├── Sales
    ├── Finance
    └── HR
```

---

# 5. Managing Accidental Deletion Protection

## Overview

By default, newly created OUs are protected from accidental deletion.

This protection prevents administrators from unintentionally deleting:

* OUs
* Users
* Groups
* Other AD objects

## Attempting to Delete a Protected OU

If you attempt to delete a protected OU, you will receive an access-denied style error even when logged in as a Domain Admin.

---

## Bypassing Accidental Deletion Protection

### Step 1: Enable Advanced Features

In ADUC:

```
View → Advanced Features
```

Ensure a checkmark appears next to Advanced Features.

### Step 2: Open OU Properties

1. Right-click the target OU.
2. Select:

```
Properties
```

### Step 3: Open Object Tab

Select:

```
Object
```

If the Object tab is not visible, verify that Advanced Features is enabled.

### Step 4: Remove Protection

Uncheck:

```
Protect object from accidental deletion
```

### Step 5: Apply Changes

Click:

```
Apply
```

then

```
OK
```

### Step 6: Delete the OU

Right-click the OU and select:

```
Delete
```

The OU can now be removed.

---

# 6. Creating User Accounts

## Scenario

Create a user account for:

```
Aung Zaw
```

in the Sales OU.

## Step 1: Open the Target OU

Navigate to:

```
Sales OU
```

## Step 2: Create New User

Right-click the OU.

Select:

```
New → User
```

## Step 3: Enter User Information

Example:

### First Name

```
John
```

### Last Name

```
Smith
```

### Full Name

```
Aung Zaw
```

### User Logon Name (UPN)

```
aungzaw@thantzinaung.com
```

### Pre-Windows 2000 Logon Name

Example:

```
AZAW
```

### Notes

The User Principal Name (UPN):

```
azaw@thantzinaung.com
```

resembles an email address and is commonly used for sign-in.

The Pre-Windows 2000 logon name:

```
azaw
```

is limited to **20 characters**.

Click:

```
Next
```

---

# 7. Configuring Password Options

Enter an initial password.

Example:

```
P@ssw0rd123!
```

Available options include:

### User Must Change Password at Next Logon

Recommended for most users.

### User Cannot Change Password

Typically used for service accounts.

### Password Never Expires

Use with caution.

This option bypasses the standard domain password expiration policy.

### Account Is Disabled

Creates the account in a disabled state until activation is required.

Click:

```
Next → Finish
```

---

# 8. Account Lifecycle Best Practice

## Do Not Immediately Delete User Accounts

When an employee leaves the organization, the recommended practice is:

### Disable the Account

instead of deleting it immediately.

### Benefits

* Preserves audit history.
* Maintains mailbox and file ownership references.
* Allows quick restoration if access is required later.
* Reduces the risk of accidental data loss.

## Disabling a User

1. Right-click the user.
2. Select:

```
Disable Account
```

### Visual Indicator

Disabled accounts display a:

**Small black downward arrow**

on the user icon.

## Re-enabling a User

1. Right-click the account.
2. Select:

```
Enable Account
```

---

# 9. Advanced User Restrictions

## Configuring Logon Hours

Logon Hours control when users may access the domain.

### Procedure

1. Open user Properties.
2. Select:

```
Account Tab
```

3. Click:

```
Logon Hours
```

4. Select time blocks.
5. Configure:

```
Allow
```

or

```
Deny
```

### Example

Allow:

```
Monday-Friday
08:00-17:00
```

### Important Behavior

If a user is already logged in when their allowed time expires:

* They remain logged in.
* They cannot log back in once they sign out.

---

## Configuring Logon To Restrictions

This feature limits users to specific computers.

### Procedure

1. Open user Properties.
2. Select:

```
Account Tab
```

3. Click:

```
Log On To
```

4. Select:

```
The following computers
```

5. Add approved workstation names.

### Example

```
SALES-PC01
SALES-PC02
SALES-PC03
```

The user can only sign in to the listed devices.

---

# 10. Delegating Control of an OU

## Scenario

A departmental assistant needs authority to:

* Create users
* Reset passwords
* Unlock accounts

without becoming a Domain Admin.

Delegation of Control provides this capability.

---

## Step 1: Open ADUC

Navigate to the desired OU.

Example:

```
Sales
```

## Step 2: Launch Delegation Wizard

Right-click the OU.

Select:

```
Delegate Control
```

Click:

```
Next
```

## Step 3: Add the User or Group

Select:

```
Add
```

Choose the user or security group that will receive delegated rights.

Example:

```
Sales Assistant
```

Click:

```
Next
```

---

## Step 4: Choose Delegated Tasks

Common options include:

### Reset User Passwords

Allows password resets and account unlocks.

### Create, Delete, and Manage User Accounts

Allows management of users within the OU.

### Create, Delete, and Manage Groups

Allows group administration.

### Custom Task to Delegate

Provides granular permission assignment.

Select the required permissions and click:

```
Next → Finish
```

---

# 11. Verifying Delegated Permissions

## Enable Advanced Features

In ADUC:

```
View → Advanced Features
```

## View Security Permissions

1. Right-click the OU.
2. Select:

```
Properties
```

3. Open:

```
Security Tab
```

4. Click:

```
Advanced
```

Review:

* Assigned users/groups
* Delegated permissions
* Inheritance settings

This provides a detailed view of all delegated rights on the OU.

---

# Lab Summary

In this lab you learned how to:

* Use ADUC and ADAC for Active Directory administration.
* Distinguish Organizational Units from system containers.
* Create and organize OUs.
* Create and configure user accounts.
* Apply password and account settings.
* Follow the best practice of disabling accounts instead of deleting them.
* Remove accidental deletion protection using Advanced Features.
* Configure logon restrictions.
* Delegate administrative control of departmental OUs.
* Verify delegated permissions using the Security tab.

These skills form the foundation of day-to-day Active Directory administration and support secure delegation of administrative responsibilities within an enterprise environment.

---

![createAndManageAD_User_and_OU](./asset/image/createAndManageAD_User_and_OU.png)
![01](./asset/image/01.png)
![02](./asset/image/02.png)
![03](./asset/image/03.png)
![04](./asset/image/04.png)
![05](./asset/image/05.png)
![06](./asset/image/06.png)
![07](./asset/image/07.png)
![08](./asset/image/08.png)
![09](./asset/image/09.png)
![10](./asset/image/10.png)
![11](./asset/image/11.png)
![12](./asset/image/12.png)
![13](./asset/image/13.png)
![14](./asset/image/14.png)
![15](./asset/image/15.png)
![16](./asset/image/16.png)
![17](./asset/image/17.png)
![18](./asset/image/18.png)
![19](./asset/image/19.png)
![20](./asset/image/20.png)