# Docker Container Installation and Nginx Web Server on Ubuntu Server

## Objective

This document explains how to:

1. Install Docker Engine on Ubuntu Server
2. Pull and run an Nginx web server container
3. Test the Nginx web server from a client machine or browser

---

# 1. Environment Information

| Component | Details |
|---|---|
| Operating System | Ubuntu Server |
| Container Platform | Docker |
| Web Server | Nginx |
| Client Access | Web Browser / Curl Command |

---

# 2. Update Ubuntu Server

Before installing Docker, update the package repository and system packages.

```bash
sudo apt update
sudo apt upgrade -y
```

---

# 3. Install Docker Engine

## Step 1 — Install Required Packages

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

---

## Step 2 — Add Docker Official GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

---

## Step 3 — Add Docker Repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## Step 4 — Update Package Index

```bash
sudo apt update
```

---

## Step 5 — Install Docker Engine

```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

---

# 4. Verify Docker Installation

Check Docker version:

```bash
docker --version
```

Example output:

```bash
Docker version 28.x.x, build xxxxxxx
```

Check Docker service status:

```bash
sudo systemctl status docker
```

Expected status:

```bash
active (running)
```

---

# 5. Enable Docker Service

Enable Docker to start automatically during boot.

```bash
sudo systemctl enable docker
```

---

# 6. Test Docker Installation

Run the test container:

```bash
sudo docker run hello-world
```

Expected result:

```bash
Hello from Docker!
```

This confirms Docker is successfully installed and working.

---

# 7. Pull Nginx Docker Image

Download the Nginx image from Docker Hub.

```bash
sudo docker pull nginx
```

List downloaded images:

```bash
sudo docker images
```

Example output:

```bash
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    xxxxxxxxxxxx   x days ago    xxxMB
```

---

# 8. Run Nginx Container

Run the Nginx web server container in detached mode.

```bash
sudo docker run -d -p 80:80 --name nginx-server nginx
```

## Command Explanation

| Option | Description |
|---|---|
| `-d` | Run container in background |
| `-p 80:80` | Map port 80 from container to host |
| `--name nginx-server` | Assign container name |
| `nginx` | Docker image name |

---

# 9. Verify Running Container

Check running containers:

```bash
sudo docker ps
```

Example output:

```bash
CONTAINER ID   IMAGE   COMMAND                  STATUS
xxxxxxxxxxxx   nginx   "/docker-entrypoint…"   Up xx seconds
```

---

# 10. Test Nginx Web Server

## Method 1 — Test on Ubuntu Server

Use curl command:

```bash
curl http://localhost
```

Expected result:

```html
Welcome to nginx!
```

---

## Method 2 — Test from Web Browser

Open a web browser on the client machine.

Enter:

```text
http://SERVER-IP
```

Example:

```text
http://192.168.1.100
```

Expected page:

```text
Welcome to nginx!
```

---

# 11. Docker Container Management Commands

## Show Running Containers

```bash
sudo docker ps
```

---

## Show All Containers

```bash
sudo docker ps -a
```

---

## Stop Container

```bash
sudo docker stop nginx-server
```

---

## Start Container

```bash
sudo docker start nginx-server
```

---

## Restart Container

```bash
sudo docker restart nginx-server
```

---

## Remove Container

```bash
sudo docker rm -f nginx-server
```

---

# 12. Firewall Configuration (Optional)

If UFW firewall is enabled, allow HTTP traffic.

```bash
sudo ufw allow 80/tcp
```

Check firewall status:

```bash
sudo ufw status
```

---

# 13. Verification Checklist

| Task | Status |
|---|---|
| Ubuntu packages updated | Completed |
| Docker installed | Completed |
| Docker service running | Completed |
| Nginx image downloaded | Completed |
| Nginx container started | Completed |
| Browser test successful | Completed |

---

# 14. Conclusion

Docker was successfully installed on the Ubuntu Server.

The Nginx container was downloaded and deployed successfully using Docker.

The web server was verified through both command-line testing and browser access.