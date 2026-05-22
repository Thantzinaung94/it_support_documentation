# Firewall Management with Firewalld in AlmaLinux Server — Hands-on Lab

## Overview

In this hands-on lab, manage firewall security on an AlmaLinux server using `firewalld`. Firewalld is the default firewall management tool in AlmaLinux and other Red Hat-based distributions. It provides a dynamic way to manage firewall rules, services, ports, and network zones without restarting the firewall service.

- Understand firewall concepts in Linux
- Install and manage firewalld
- Configure firewall zones
- Allow and block network services
- Open and close ports
- Enable firewall rules permanently
- Verify and troubleshoot firewall configurations

---

# What is Firewalld?

`firewalld` is a dynamic firewall management daemon that uses zones and services instead of manually configuring complex `iptables` rules.

It provides:

- Dynamic firewall rule updates
- Zone-based trust management
- Service-based configurations
- Runtime and permanent rule management
- IPv4 and IPv6 support

---

# Firewall Concepts

## Zones

Zones define the trust level of network connections.

### Common Zones

| Zone | Description |
|---|---|
| public | Default untrusted network |
| trusted | All traffic accepted |
| home | Trusted home network |
| work | Trusted work environment |
| internal | Internal network |
| dmz | Demilitarized zone |
| block | Incoming connections rejected |
| drop | Packets silently dropped |

---

## Runtime vs Permanent Rules

| Type | Description |
|---|---|
| Runtime | Active until reboot |
| Permanent | Saved permanently |

To make runtime rules permanent:

```bash
sudo firewall-cmd --runtime-to-permanent
```

---

# Lab Requirements

- AlmaLinux Server
- Root or sudo privileges
- Network connectivity

---

# Step 1 — Install Firewalld

Check whether firewalld is installed:

```bash
rpm -q firewalld
```

Install firewalld if missing:

```bash
sudo dnf install firewalld -y
```

---

# Step 2 — Start and Enable Firewalld

Start the service:

```bash
sudo systemctl start firewalld
```

Enable at boot:

```bash
sudo systemctl enable firewalld
```

Check status:

```bash
sudo systemctl status firewalld
```

---

# Step 3 — Verify Firewall Status

Check whether firewalld is running:

```bash
sudo firewall-cmd --state
```

Expected output:

```text
running
```

---

# Step 4 — View Active Zones

Display active firewall zones:

```bash
sudo firewall-cmd --get-active-zones
```

Example output:

```text
public
  interfaces: eth0
```

---

# Step 5 — List Current Firewall Rules

List all firewall settings:

```bash
sudo firewall-cmd --list-all
```

Example output:

```text
public (active)
  target: default
  services: cockpit dhcpv6-client ssh
  ports:
```

---

# Step 6 — Allow SSH Service

Allow SSH traffic:

```bash
sudo firewall-cmd --add-service=ssh
```

Make it permanent:

```bash
sudo firewall-cmd --permanent --add-service=ssh
```

Reload firewall:

```bash
sudo firewall-cmd --reload
```

Verify:

```bash
sudo firewall-cmd --list-services
```

---

# Step 7 — Open a Specific Port

Open TCP port `8080`:

```bash
sudo firewall-cmd --add-port=8080/tcp
```

Permanent rule:

```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
```

Reload rules:

```bash
sudo firewall-cmd --reload
```

Verify:

```bash
sudo firewall-cmd --list-ports
```

---

# Step 8 — Remove a Service or Port

Remove HTTP service:

```bash
sudo firewall-cmd --remove-service=http
```

Permanent removal:

```bash
sudo firewall-cmd --permanent --remove-service=http
```

Remove a port:

```bash
sudo firewall-cmd --remove-port=8080/tcp
```

Reload firewall:

```bash
sudo firewall-cmd --reload
```

---

# Step 9 — List Available Services

View predefined services:

```bash
sudo firewall-cmd --get-services
```

Common services include:

- ssh
- http
- https
- ftp
- samba
- dns

---

# Step 10 — Configure Firewall Zones

## View Available Zones

```bash
sudo firewall-cmd --get-zones
```

## Check Default Zone

```bash
sudo firewall-cmd --get-default-zone
```

## Change Default Zone

Set default zone to `home`:

```bash
sudo firewall-cmd --set-default-zone=home
```

## Assign Interface to a Zone

```bash
sudo firewall-cmd --zone=public --change-interface=eth0
```

Permanent assignment:

```bash
sudo firewall-cmd --permanent --zone=public --change-interface=eth0
```

Reload:

```bash
sudo firewall-cmd --reload
```

---

# Step 11 — Enable HTTP and HTTPS

Allow web traffic:

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
```

Reload firewall:

```bash
sudo firewall-cmd --reload
```

Verify:

```bash
sudo firewall-cmd --list-services
```

---

# Step 12 — Block ICMP(Internet Control Message Protocol) Ping Requests

Block ping responses:

```bash
sudo firewall-cmd --permanent --add-icmp-block=echo-request
```

Reload:

```bash
sudo firewall-cmd --reload
```

List ICMP blocks:

```bash
sudo firewall-cmd --list-icmp-blocks
```

---

# Step 13 — Rich Rules

Rich rules provide advanced firewall configurations.

## Allow SSH from Specific IP

```bash
sudo firewall-cmd --permanent \
--add-rich-rule='rule family="ipv4" \
source address="192.168.1.100" \
service name="ssh" accept'
```

Reload:

```bash
sudo firewall-cmd --reload
```

## Block an IP Address

```bash
sudo firewall-cmd --permanent \
--add-rich-rule='rule family="ipv4" \
source address="192.168.1.50" reject'
```

Reload firewall:

```bash
sudo firewall-cmd --reload
```

---

# Step 14 — Reload and Restart Firewalld

Reload rules without disconnecting sessions:

```bash
sudo firewall-cmd --reload
```

Restart firewalld service:

```bash
sudo systemctl restart firewalld
```

---

# Step 15 — Verify Open Ports

Check listening ports:

```bash
sudo ss -tulnp
```

Or:

```bash
sudo netstat -tulnp
```

---

# Step 16 — Troubleshooting Firewalld

## Check Service Status

```bash
sudo systemctl status firewalld
```

## Reload Failed Rules

```bash
sudo firewall-cmd --reload
```

## View Logs

```bash
sudo journalctl -u firewalld
```

---

# Useful Firewalld Commands

| Command | Description |
|---|---|
| `firewall-cmd --state` | Check firewall state |
| `firewall-cmd --list-all` | List all rules |
| `firewall-cmd --reload` | Reload firewall |
| `firewall-cmd --get-zones` | Show zones |
| `firewall-cmd --get-services` | Show services |
| `firewall-cmd --list-ports` | Show open ports |
| `firewall-cmd --runtime-to-permanent` | Save runtime rules |

---

# Security Best Practices

- Allow only necessary services
- Use specific ports instead of broad access
- Use rich rules for tighter security
- Regularly review open ports
- Keep firewalld enabled
- Use SSH key authentication
- Restrict administrative access

---

# Conclusion

In this lab, you learned how to manage firewall security in AlmaLinux using `firewalld`.

You practiced:

- Starting and enabling firewalld
- Managing services and ports
- Working with firewall zones
- Using permanent and runtime rules
- Creating advanced rich rules
- Troubleshooting firewall configurations

`firewalld` is an essential security tool for Linux server administration and helps protect servers from unauthorized access while allowing required network services.

![Firewall management with Firewalld guide](./asset/image/Firewall%20management%20with%20Firewalld%20guide.png)