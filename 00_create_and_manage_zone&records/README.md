# Home Lab Documentation – Create and Manage DNS Zones and Records

## Lab Information

| Item              | Value                   |
| ----------------- | ----------------------- |
| Domain Name       | thantzinaung.com        |
| Domain Controller | TZA-DC1                 |
| DC IP Address     | 192.168.1.100           |
| Member Server     | TZA-SVR1                |
| Server IP Address | 192.168.1.200           |
| DNS Service       | Microsoft DNS           |
| Environment       | Windows Server Home Lab |

---

# Objective

This lab demonstrates how to create and manage DNS Zones and DNS Records in an Active Directory environment. The exercise covers:

* Forward Lookup Zones
* Reverse Lookup Zones
* DNS Zone Types
* Dynamic Updates
* DNS Records
* Zone Replication
* DNS Management
* Name Resolution Verification

---

# 1. Overview of DNS Lookup Types

DNS translates human-readable host names into IP addresses and vice versa.

## Forward Lookup Zone

Forward Lookup Zones resolve a host name to an IP address.

### Example

| Host Name                 | IP Address    |
| ------------------------- | ------------- |
| TZA-DC1.thantzinaung.com  | 192.168.1.100 |
| TZA-SVR1.thantzinaung.com | 192.168.1.200 |

Query:

```text
TZA-SVR1.thantzinaung.com
```

Result:

```text
192.168.1.200
```

Forward Lookup Zones are required for Active Directory functionality.

---

## Reverse Lookup Zone

Reverse Lookup Zones resolve an IP address back to a host name.

### Example

Query:

```text
192.168.1.100
```

Result:

```text
TZA-DC1.thantzinaung.com
```

Reverse lookups are useful for:

* Troubleshooting
* Security auditing
* Network management
* Mail server validation

---

# 2. DNS Zone Types and Storage

DNS databases can be stored in different ways depending on the zone type.

## Active Directory Integrated Primary Zone

### Characteristics

* Requires a Domain Controller
* Stored inside Active Directory
* Automatically replicated between Domain Controllers
* Supports Secure Dynamic Updates

### Storage Location

```text
Active Directory Database (NTDS.dit)
```

### Lab Example

```text
Zone Name: thantzinaung.com
Server: TZA-DC1
Type: AD Integrated Primary
```

### Benefits

* Fault tolerance
* Secure updates
* Simplified administration

---

## Standard Primary Zone

### Characteristics

* Can exist on a non-domain controller
* Writable database
* Stores records locally

### Storage Location

```text
C:\Windows\System32\DNS
```

Example:

```text
thantzinaung.com.dns
```

---

## Secondary Zone

### Characteristics

* Read-only copy
* Receives updates from Primary DNS server
* Used for redundancy

### Benefits

* Load balancing
* High availability
* Disaster recovery

---

## Stub Zone

### Characteristics

Contains only:

* SOA Record
* NS Records
* Glue A Records

### Purpose

Used to identify authoritative DNS servers for another zone.

Benefits:

* Reduces DNS traffic
* Improves name resolution efficiency

---

# 3. Configuring Dynamic Updates

Dynamic Updates allow clients to automatically register DNS records.

Navigate:

```text
DNS Manager
→ Zone Properties
→ General Tab
→ Dynamic Updates
```

---

## Allow Only Secure Dynamic Updates

### Recommended Setting

Available only for:

```text
AD Integrated Zones
```

Features:

* Authentication required
* Prevents unauthorized updates
* Best security practice

---

## Allow Non-Secure and Secure Dynamic Updates

Features:

* Any device can register records
* Easier setup

Risk:

* Unauthorized systems may create false records
* Potential DNS poisoning

---

## Do Not Allow Dynamic Updates

Features:

* All records created manually
* Fully static DNS environment

Use Cases:

* Highly controlled environments
* Special-purpose servers

---

# 4. Understanding Core DNS Records

DNS records define resources within a DNS zone.

---

## SOA (Start of Authority)

The first record loaded when the zone starts.

Contains:

* Primary DNS server
* Administrator email
* Serial Number
* Refresh Interval
* Retry Interval

### Example

```text
thantzinaung.com
```

Primary Server:

```text
TZA-DC1.thantzinaung.com
```

The serial number increases whenever the zone changes.

Secondary servers compare serial numbers to determine whether replication is required.

---

## NS (Name Server) Record

Defines authoritative DNS servers.

### Example

```text
TZA-DC1.thantzinaung.com
```

Purpose:

* Identifies DNS servers responsible for the zone
* Supports replication

---

## A (Host) Record

Maps host names to IPv4 addresses.

### Lab Records

| Host     | IP Address    |
| -------- | ------------- |
| TZA-DC1  | 192.168.1.100 |
| TZA-SVR1 | 192.168.1.200 |

Examples:

```text
TZA-DC1.thantzinaung.com → 192.168.1.100
```

```text
TZA-SVR1.thantzinaung.com → 192.168.1.200
```

---

## PTR Record

Used in Reverse Lookup Zones.

### Examples

```text
192.168.1.100 → TZA-DC1.thantzinaung.com
```

```text
192.168.1.200 → TZA-SVR1.thantzinaung.com
```

---

## CNAME (Canonical Name)

Creates aliases for existing host records.

### Example

| Alias      | Points To |
| ---------- | --------- |
| fileserver | TZA-SVR1  |
| www        | TZA-SVR1  |

Example:

```text
www.thantzinaung.com
```

Points To:

```text
TZA-SVR1.thantzinaung.com
```

Benefit:

If the IP changes, only the A record needs updating.

---

## MX (Mail Exchange)

Identifies mail servers responsible for email delivery.

### Example

| Priority | Mail Server           |
| -------- | --------------------- |
| 10       | mail.thantzinaung.com |

Lower numbers indicate higher priority.

Example:

```text
mail.thantzinaung.com
```

Priority:

```text
10
```

---

## SRV (Service Location)

Used heavily by Active Directory.

Provides:

* Service location
* Protocol
* Port number

Examples:

```text
_ldap._tcp.thantzinaung.com
```

```text
_kerberos._tcp.thantzinaung.com
```

These records allow domain members to locate:

* Domain Controllers
* LDAP Services
* Kerberos Authentication

---

# 5. Creating the DNS Zones

## Create Forward Lookup Zone

1. Open DNS Manager.
2. Expand TZA-DC1.
3. Right-click Forward Lookup Zones.
4. Select New Zone.
5. Choose:

```text
Primary Zone
Store the zone in Active Directory
```

6. Zone Name:

```text
thantzinaung.com
```

7. Dynamic Update:

```text
Allow only secure dynamic updates
```

8. Finish the wizard.

---

## Create Reverse Lookup Zone

1. Right-click Reverse Lookup Zones.
2. Select New Zone.
3. Choose:

```text
IPv4 Reverse Lookup Zone
```

4. Network ID:

```text
192.168.1
```

5. Dynamic Updates:

```text
Allow only secure dynamic updates
```

6. Finish.

Zone created:

```text
1.168.192.in-addr.arpa
```

---

# 6. Management and Replication Setup

## Configure Name Servers

To permit another DNS server to host or replicate the zone:

1. Open Zone Properties.
2. Select Name Servers tab.
3. Click Add.

Example:

```text
TZA-DC1.thantzinaung.com
192.168.1.100
```

Future example:

```text
TZA-DC2.thantzinaung.com
192.168.1.101
```

---

## Configure Zone Transfers

Navigate:

```text
Zone Properties
→ Zone Transfers
```

Options:

### Allow Zone Transfers

Only to:

```text
Servers listed on the Name Servers tab
```

Recommended for security.

---

## Centralized DNS Management

Manage multiple DNS servers from a single console.

Navigate:

```text
DNS Manager
→ Action
→ Connect to DNS Server
```

Benefits:

* Centralized administration
* Easier monitoring
* Simplified troubleshooting

---

# 7. Verification and Testing

## Verify A Records

Open Command Prompt:

```cmd
ping TZA-DC1
```

Expected Result:

```text
Pinging TZA-DC1 [192.168.1.100]
```

---

```cmd
ping TZA-SVR1
```

Expected Result:

```text
Pinging TZA-SVR1 [192.168.1.200]
```

---

## Verify FQDN Resolution

```cmd
ping TZA-SVR1.thantzinaung.com
```

Expected:

```text
192.168.1.200
```

---

## Verify Reverse Lookup

```cmd
nslookup 192.168.1.100
```

Expected:

```text
Name: TZA-DC1.thantzinaung.com
```

---

## Verify Alias Record

```cmd
ping www.thantzinaung.com
```

Expected:

```text
192.168.1.200
```

---

# Conclusion

In this lab, DNS infrastructure was configured for the Active Directory domain **thantzinaung.com** using **TZA-DC1 (192.168.1.100)** as the primary DNS server. Forward and Reverse Lookup Zones were created, dynamic updates were configured securely, DNS records were managed, and name resolution was validated using ping and nslookup. This configuration provides reliable hostname resolution, supports Active Directory services, and establishes a foundation for future DNS replication and high availability.
---