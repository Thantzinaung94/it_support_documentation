# Fix Internet Connection Error in Hyper-V Debian Server

When running a Debian Server inside Microsoft Hyper-V, you may encounter internet connection issues where the virtual machine cannot access the internet or resolve domain names.

This guide explains how to fix the issue by creating an external virtual switch and configuring DNS settings manually.

---

# Problem Symptoms

Your Debian Server VM may show issues like:

- Cannot access the internet
- `ping google.com` fails
- `apt update` cannot connect
- DNS resolution errors
- Network adapter connected but no internet

Example error:

```bash
Temporary failure resolving 'deb.debian.org'
```

---

# Solution Overview

The fix involves:

1. Creating an External Virtual Switch in Hyper-V
2. Connecting the Debian VM to that switch
3. Configuring DNS servers manually
4. Rebooting the server
5. Testing connectivity

---

# Step 1 — Create an External Virtual Switch in Hyper-V

Open:

```text
Hyper-V Manager
```

Then:

```text
Hyper-V Manager
→ Virtual Switch Manager
→ New Virtual Network Switch
→ External
→ Create Virtual Switch
```

Configure the switch:

| Setting | Value |
|---|---|
| Name | Debian_Network |
| Connection Type | External Network |
| Network Adapter | Qualcomm Atheros QCA9388 Wireless Network Adapter |

Click:

```text
Apply → OK
```

---

# Step 2 — Attach the Debian VM to the New Switch

In Hyper-V Manager:

```text
Right Click Debian-Server VM
→ Settings
→ Network Adapter
→ Virtual Switch
→ Select "Debian_Network"
→ Apply
→ OK
```

This connects the Debian virtual machine to your physical wireless network adapter.

---

# Step 3 — Configure DNS Servers in Debian

Open the terminal inside Debian Server.

Edit the DNS configuration file:

```bash
sudo nano /etc/resolv.conf
```

Add the following lines:

```text
nameserver 8.8.8.8
nameserver 1.1.1.1
```

Explanation:

| DNS Server | Provider |
|---|---|
| 8.8.8.8 | Google DNS |
| 1.1.1.1 | Cloudflare DNS |

Save the file:

```text
CTRL + O
ENTER
CTRL + X
```

---

# Step 4 — Reboot Debian Server

Restart the virtual machine:

```bash
sudo reboot
```

---

# Step 5 — Test Internet Connectivity

After reboot, test network connectivity.

## Test DNS Resolution

```bash
ping -c 4 google.com
```

Expected result:

```text
64 bytes from ...
```

---

## Test Raw Internet Connectivity

```bash
ping -c 4 8.8.8.8
```

If this works, the VM has internet access.

---

# Verify IP Address

You can also verify your network interface received an IP address:

```bash
ip a
```

Look for an address like:

```text
192.168.x.x
```

---

# Common Causes of Hyper-V Internet Issues

| Cause | Fix |
|---|---|
| No virtual switch | Create External Switch |
| Wrong adapter selected | Choose correct Wi-Fi adapter |
| DNS not configured | Add DNS servers |
| VM disconnected from switch | Attach VM network adapter |
| DHCP issue | Reboot VM or renew IP |

---

# Useful Network Commands

## Show Network Interfaces

```bash
ip a
```

## Show Routing Table

```bash
ip route
```

## Restart Networking

```bash
sudo systemctl restart networking
```

## Check DNS Configuration

```bash
cat /etc/resolv.conf
```

---

# Final Result

After completing these steps:

- Debian Server should access the internet normally
- DNS resolution should work
- `apt update` should function correctly
- Hyper-V networking should be stable

---

# Conclusion

Hyper-V Debian networking issues are commonly caused by incorrect virtual switch configuration or missing DNS settings. By creating an External Virtual Switch and manually adding DNS servers, you can quickly restore internet connectivity to your Debian virtual machine.

![Fix Internet Connection Error in Hyper-V Debian Server](./asset/image/Fix%20Internet%20Connection%20Error%20in%20Hyper-V%20Debian%20Server.png)