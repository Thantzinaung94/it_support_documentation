# Secure Ubuntu Server 26.04: SSH Key Authentication and Disable Password Logins

### Important Note :: firstly change default port (port 22 to port 2222 or other you like - in here I setup 8834 port) | if you want to change port go setup : 6 and return setup : 1 (setup:1 have to setup in client computer which you connect) | in here a little complicate


One of the most effective ways to secure your Ubuntu Server is to use **SSH key authentication** and then disable password-based logins entirely. This greatly reduces the chances of unauthorized access, especially from brute-force attacks and automated bots.

In this guide, you will learn:

- What SSH keys are
- How to generate and use them
- How to disable password authentication safely
- How to change the default SSH port
- Best practices to avoid locking yourself out

---

# Why Use SSH Key Authentication?

Passwords can be guessed, cracked, or stolen. SSH keys are cryptographic credentials that provide a much stronger authentication method.

## Benefits of SSH Keys

- Nearly impossible to brute-force
- More secure than passwords
- Protected with an optional passphrase
- Easy to revoke or rotate
- Ideal for automation and scripts

---

# How SSH Key Authentication Works

SSH authentication uses two files:

| Key Type | Purpose |
|---|---|
| Private Key | Stored securely on your local computer |
| Public Key | Copied to the Ubuntu server |

The server checks whether the private key matches the public key stored in:

```bash
~/.ssh/authorized_keys
```

If the keys match, access is granted.

---

# Step 1 — Generate an SSH Key Pair

Run the following command on your **local machine** (Windows, macOS, or Linux):

```bash
ssh-keygen
```

You will see something similar to:

```text
Generating public/private rsa key pair.
Enter file in which to save the key (/home/youruser/.ssh/id_rsa):
```

Press **Enter** to use the default location.

Next, you may set a passphrase:

```text
Enter passphrase (empty for no passphrase):
```

A passphrase adds another layer of security and is highly recommended.

---

## Generated Files

SSH keys are stored in:

```bash
~/.ssh/
```

You will see:

| File | Description |
|---|---|
| `id_rsa` | Private key (keep secret) |
| `id_rsa.pub` | Public key (safe to share) |

> ⚠️ Never share your private key.

---

# Step 2 — Copy the Public Key to Your Ubuntu Server

Use the following command:

For Ubuntu client desktop :

```bash
ssh-copy-id youruser@your-server-ip

(or)

ssh-copy-id -p youport youruser@your-server-ip
```

Example:

```bash
ssh-copy-id ubuntu@192.168.1.100

(or)

ssh-copy-id -p 8834 thantzinaung@192.168.1.100
```
---

For Windows 11 Client Computer :
open powershell and type as following command -
```bash
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh -p 8834 thantzinaung@192.168.1.100 "cat >> ~/.ssh/authorized_keys"
```

for PuTTY :
    stage 1 : open - PuTTYgen > load > choose ssh-key > save private key
    stage 2 : open - PuTTY > change port (e.g 8834 important) > connection / SSH / Auth / Credentials / click - browse and choose .ppk where you save it > go session > save it

---

You will be prompted for your server password one final time.

The public key will automatically be added to:

```bash
~/.ssh/authorized_keys

cat ~/.ssh/authorized_keys
```

---

# Step 3 — Test SSH Key Login

Now connect to your server:

```bash
ssh youruser@your-server-ip

(or)

ssh -p yourport youruser@your-server-ip
```

Example:

```bash
ssh ubuntu@192.168.1.100

(or)

ssh -p 9934 thantzinaung@192.168.1.100
```

If everything works correctly:

- You will log in without a password
- If you configured a passphrase, you will enter the passphrase instead

> ⚠️ Do not continue until SSH key authentication works successfully.

---

# Step 4 — Disable Password Authentication

Once SSH key login is verified, disable password-based authentication.

Edit the SSH configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

Find or add the following settings:

```ini
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
PubkeyAuthentication yes
```

---

## Disable Root Login (Recommended)

Also set:

```ini
PermitRootLogin no
```

This prevents direct SSH access to the root account.

---

# Step 5 — Restart the SSH Service

Apply the configuration changes:

```bash
sudo systemctl restart ssh
```

Before closing your current session:

- ✅ Open a **second terminal window** and test SSH access again.

This prevents accidental lockouts.

---

# Step 6 — Change the Default SSH Port (Optional but Recommended)

## setup port 
You can setup port number you want : like 2222 or other 8834 , 9984 , 9983 and more...
 ---

 ```bash
port 8834
 ```

 ---

## Allow the New Port Through the Firewall

If using UFW:

```bash
sudo ufw allow 8834/tcp
```

---

## Verify SSH Is Listening on the New Port

Run:

```bash
ss -tulpn | grep 8834
```

Example output:

```text
tcp   LISTEN 0      128          0.0.0.0:8834       0.0.0.0:*
```

---


Changing the SSH port reduces automated scanning and attack attempts.

Ubuntu Server 26.04 may use `ssh.socket` with systemd socket activation.

---

## Edit the SSH Socket Configuration

Run:

```bash
sudo systemctl edit ssh.socket
```

Add:

```ini
[Socket]
ListenStream=
ListenStream=8834
```

### Explanation

| Line | Purpose |
|---|---|
| `ListenStream=` | Clears the default port |
| `ListenStream=8834` | Sets SSH to listen on port 8834 |

---

## Reload systemd

```bash
sudo systemctl daemon-reload
```

---

## Restart the SSH Socket

```bash
sudo systemctl restart ssh.socket
```

---

## Connect Using the New Port

Use:

```bash
ssh -p 8834 youruser@your-server-ip
```

Example:

```bash
ssh -p 8834 ubuntu@192.168.1.100
```

---

# Step 7 — Remove Access to Port 22 (Optional)

After verifying the new port works correctly:

```bash
sudo ufw delete allow OpenSSH
```

Or:

```bash
sudo ufw deny 22/tcp
```

> ⚠️ Only do this after confirming the new SSH port is functioning.

---

# Additional SSH Hardening Tips

## Use Fail2Ban

Fail2Ban blocks repeated failed login attempts.

Install:

```bash
sudo apt install fail2ban -y
```

Enable:

```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## Restrict SSH Access by IP

Allow only trusted IP addresses:

```bash
sudo ufw allow from 192.168.1.100 to any port 8834 proto tcp
```

---

## Keep Ubuntu Updated

Regular updates patch security vulnerabilities.

```bash
sudo apt update
sudo apt upgrade -y
```

---

# What If You Get Locked Out?

If you disable password authentication and lose access:

- Use a physical console
- Use cloud provider console access
- Use a virtual KVM
- Restore authorized keys from recovery mode

Cloud providers often allow SSH key resets from the control panel.

---

# Useful SSH Commands

| Command | Description |
|---|---|
| `ssh-keygen` | Generate SSH keys |
| `ssh-copy-id user@host` | Copy public key to server |
| `ssh user@host` | Connect via SSH |
| `ssh -p 8834 user@host` | Connect using custom port |
| `sudo systemctl restart ssh` | Restart SSH service |
| `sudo systemctl restart ssh.socket` | Restart SSH socket |
| `sudo ufw allow 8834/tcp` | Allow custom SSH port |
| `ss -tulpn` | Show listening ports |

---

# Security Best Practices

- Always use SSH keys instead of passwords
- Use a strong passphrase
- Disable root login
- Change the default SSH port
- Keep a backup SSH key
- Test changes before closing sessions
- Enable a firewall
- Keep the server updated

---

# Summary

SSH key authentication is one of the most important security improvements you can make on Ubuntu Server 26.04.

In this guide, you learned how to:

- Generate SSH keys
- Copy keys to your server
- Disable password authentication
- Disable root login
- Change the SSH port using `ssh.socket`
- Configure UFW firewall rules
- Verify secure SSH access

Using these techniques significantly reduces the risk of brute-force attacks and unauthorized access to your server.