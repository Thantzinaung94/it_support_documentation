# Package Installation and Management in Ubuntu Server

## Objective

This document explains package installation and management in Ubuntu Server using common package management tools such as APT, DPKG, and Snap. It also includes essential commands for updating, installing, removing, and searching software packages.

---

# Package Managers in Ubuntu

Ubuntu uses several package management systems to install and maintain software.

| Package Manager | Description |
|---|---|
| APT | Advanced Package Tool used for managing `.deb` packages from repositories |
| DPKG | Low-level package management tool for installing local `.deb` files |
| Snap | Package management system for containerized applications |
| Flatpak | Universal Linux package management system |
| AppImage | Portable application format without installation |

---

# 1. APT (Advanced Package Tool)

APT is the default package manager in Ubuntu. It downloads software from online repositories and automatically handles dependencies.

## Update Package Repository

```bash
sudo apt update
```

### Description

- Refreshes package lists from repositories
- Checks for available software updates

---

## Upgrade Installed Packages

```bash
sudo apt upgrade
```

### Description

- Upgrades all installed packages to the latest version

---

## Install a Package

```bash
sudo apt install nginx
```

### Description

- Installs the Nginx web server package

---

## Install Multiple Packages

```bash
sudo apt install git curl wget
```

### Description

- Installs multiple packages in one command

---

## Remove a Package

```bash
sudo apt remove nginx
```

### Description

- Removes the package but keeps configuration files

---

## Completely Remove a Package

```bash
sudo apt purge nginx
```

### Description

- Removes package including configuration files

---

## Remove Unused Dependencies

```bash
sudo apt autoremove
```

### Description

- Cleans unnecessary packages installed as dependencies

---

## Search for a Package

```bash
apt search apache2
```

### Description

- Searches package repositories for matching software

---

## Display Package Information

```bash
apt show nginx
```

### Description

- Displays package details such as version, dependencies, and description

---

## List Installed Packages

```bash
apt list --installed
```

### Description

- Shows all installed packages

---

# 2. DPKG (Debian Package Manager)

DPKG is a low-level package management tool used for handling local `.deb` package files.

---

## Install a Local `.deb` Package

```bash
sudo dpkg -i package.deb
```

### Description

- Installs a local Debian package file

---

## Remove a Package

```bash
sudo dpkg -r package-name
```

### Description

- Removes an installed package

---

## List Installed Packages

```bash
dpkg -l
```

### Description

- Displays all installed packages

---

## Check if a Package is Installed

```bash
dpkg -l | grep nginx
```

### Description

- Searches installed packages for Nginx

---

## Display Package Information

```bash
dpkg -s nginx
```

### Description

- Shows package status and details

---

## Extract Package Contents

```bash
dpkg -x package.deb directory/
```

### Description

- Extracts package contents without installing

---

# 3. Snap Package Manager

Snap is a modern package system developed by Canonical for distributing containerized applications.

---

## Check Snap Version

```bash
snap version
```

---

## Search Snap Packages

```bash
snap find vlc
```

### Description

- Searches Snap Store for applications

---

## Install a Snap Package

```bash
sudo snap install vlc
```

### Description

- Installs VLC media player as a Snap package

---

## List Installed Snap Packages

```bash
snap list
```

---

## Update Snap Packages

```bash
sudo snap refresh
```

### Description

- Updates installed Snap applications

---

## Remove a Snap Package

```bash
sudo snap remove vlc
```

---

# 4. Flatpak

Flatpak is another universal package management system for Linux distributions.

---

## Install Flatpak

```bash
sudo apt install flatpak
```

---

## Add Flathub Repository

```bash
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

---

## Install Application

```bash
flatpak install flathub org.videolan.VLC
```

---

## List Installed Flatpak Applications

```bash
flatpak list
```

---

## Remove Flatpak Application

```bash
flatpak uninstall org.videolan.VLC
```

---

# 5. AppImage

AppImage allows applications to run without installation.

---

## Make AppImage Executable

```bash
chmod +x application.AppImage
```

---

## Run AppImage

```bash
./application.AppImage
```

---

# Essential Package Management Commands

| Command | Purpose |
|---|---|
| `sudo apt update` | Update package repository |
| `sudo apt upgrade` | Upgrade installed packages |
| `sudo apt install package` | Install package |
| `sudo apt remove package` | Remove package |
| `sudo apt purge package` | Remove package with config |
| `sudo apt autoremove` | Remove unused dependencies |
| `apt search package` | Search package |
| `apt show package` | Show package information |
| `apt list --installed` | List installed packages |
| `dpkg -l` | List installed packages |
| `sudo dpkg -i file.deb` | Install local `.deb` file |
| `snap find package` | Search Snap package |
| `sudo snap install package` | Install Snap package |
| `snap list` | List Snap packages |
| `sudo snap refresh` | Update Snap packages |

---

# Verification Commands

## Verify Installed Software

```bash
which nginx
```

or

```bash
nginx -v
```

---

## Verify Snap Installation

```bash
snap list
```

---

## Verify Installed `.deb` Packages

```bash
dpkg -l | less
```

---

# Best Practices

- Always run `sudo apt update` before installing packages
- Use trusted repositories only
- Remove unused packages regularly using `autoremove`
- Keep the system updated for security
- Prefer APT for system packages
- Use Snap or Flatpak for isolated applications

---

# Conclusion

Ubuntu provides multiple package management tools for installing and maintaining software. APT and DPKG are essential for traditional Debian packages, while Snap and Flatpak provide modern containerized applications with simplified dependency management. Understanding these tools helps administrators efficiently manage Ubuntu servers and desktop environments.