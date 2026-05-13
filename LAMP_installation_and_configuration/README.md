# Advanced: LAMP Installation and Configuration on Ubuntu Server 24.04

## What Is the LAMP Stack?

LAMP is a popular open-source software stack used to host and develop dynamic websites and web applications.

- **L – Linux** (Ubuntu Server)
- **A – Apache** (Web Server)
- **M – MySQL / MariaDB** (Database Server)
- **P – PHP** (Server-Side Scripting Language)

These components work together to deliver dynamic web content to users through a web browser.

---

# Lab Objective

The objective of this lab is to:

- Install and configure the Apache web server
- Install and secure the MySQL database server
- Install PHP and required modules
- Configure Apache to process PHP files
- Test PHP functionality
- Create a MySQL database and user
- Apply proper file permissions for web applications

---

# Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Server 24.04 |
| Web Server | Apache2 |
| Database Server | MySQL Server |
| Scripting Language | PHP |
| Package Manager | APT |

---

# Step 1: Update the Server

Before installing packages, update the package index and upgrade existing packages.

```bash
sudo apt update
sudo apt upgrade -y
```

### Explanation

- `apt update` refreshes package information
- `apt upgrade -y` upgrades installed packages automatically

---

# Step 2: Install Apache Web Server

Install Apache using APT.

```bash
sudo apt install apache2 -y
```

Enable Apache to start automatically at boot:

```bash
sudo systemctl enable apache2
```

Start the Apache service:

```bash
sudo systemctl start apache2
```

Check Apache service status:

```bash
sudo systemctl status apache2
```

---

## Test Apache Web Server

Open a browser and access:

```text
http://your-server-ip
```

You should see the default Apache web page.

---

# Step 3: Install MySQL Database Server

Install MySQL Server:

```bash
sudo apt install mysql-server -y
```

Check MySQL service status:

```bash
sudo systemctl status mysql
```

Enable MySQL to start automatically:

```bash
sudo systemctl enable mysql
```

---

## Secure MySQL Installation

Run the MySQL security script:

```bash
sudo mysql_secure_installation
```

### Recommended Security Options

During setup, configure the following:

- Set a root password
- Remove anonymous users
- Disable remote root login
- Remove test databases
- Reload privilege tables

---

## Test MySQL Login

Enter the MySQL shell:

```bash
sudo mysql
```

Exit the shell:

```sql
exit;
```

---

# Step 4: Install PHP and Required Modules

Install PHP with Apache and MySQL support:

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

Install additional PHP modules:

```bash
sudo apt install php-cli php-curl php-gd php-mbstring php-xml php-zip -y
```

---

## Verify PHP Installation

Check the installed PHP version:

```bash
php -v
```

Example output:

```text
PHP 8.x.x (cli)
```

---

# Step 5: Configure Apache to Use PHP

Apache prioritizes `index.html` by default. Modify the configuration to prioritize `index.php`.

Open the Apache directory configuration file:

```bash
sudo nano /etc/apache2/mods-enabled/dir.conf
```

Find this line:

```apache
DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
```

Change it to:

```apache
DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
```

Save the file and restart Apache:

```bash
sudo systemctl restart apache2
```

---

# Step 6: Test PHP Processing

Create a PHP test file:

```bash
sudo nano /var/www/html/info.php
```

Add the following content:

```php
<?php
phpinfo();
?>
```

Save and exit the editor.

---

## Test PHP in Browser

Open the following URL:

```text
http://your-server-ip/info.php
```

If PHP is working correctly, a PHP information page will appear.

---

## Remove the PHP Test File

For security reasons, remove the test file after verification:

```bash
sudo rm /var/www/html/info.php
```

---

# Step 7: Create a MySQL Database and User (Optional)

Enter the MySQL shell:

```bash
sudo mysql
```

Create a new database:

```sql
CREATE DATABASE myappdb;
```

Create a new database user:

```sql
CREATE USER 'myappuser'@'localhost' IDENTIFIED BY 'securepassword';
```

Grant privileges to the user:

```sql
GRANT ALL PRIVILEGES ON myappdb.* TO 'myappuser'@'localhost';
```

Reload privilege tables:

```sql
FLUSH PRIVILEGES;
```

Exit MySQL:

```sql
EXIT;
```

---

# Step 8: Configure File Permissions

When deploying a PHP application inside `/var/www/html/myapp`, proper permissions are required.

Change ownership:

```bash
sudo chown -R www-data:www-data /var/www/html/myapp
```

Set directory permissions:

```bash
sudo chmod -R 755 /var/www/html/myapp
```

---

## Permission Explanation

| Command | Purpose |
|---|---|
| `chown` | Changes file ownership |
| `www-data` | Default Apache user |
| `chmod 755` | Grants proper read/execute permissions |

---

# Useful Apache Commands

## Restart Apache

```bash
sudo systemctl restart apache2
```

## Reload Apache Configuration

```bash
sudo systemctl reload apache2
```

## Stop Apache

```bash
sudo systemctl stop apache2
```

## Start Apache

```bash
sudo systemctl start apache2
```

---

# Useful MySQL Commands

## Login to MySQL

```bash
sudo mysql
```

## Show Databases

```sql
SHOW DATABASES;
```

## Show Users

```sql
SELECT User, Host FROM mysql.user;
```

---

# Firewall Configuration (Optional)

If UFW firewall is enabled, allow Apache traffic:

```bash
sudo ufw allow 'Apache'
```

Check firewall status:

```bash
sudo ufw status
```

---

# Verification Checklist

| Task | Status |
|---|---|
| Apache Installed | ✅ |
| MySQL Installed | ✅ |
| PHP Installed | ✅ |
| PHP Processing Tested | ✅ |
| Database Created | ✅ |
| File Permissions Configured | ✅ |

---

# Troubleshooting

## Apache Service Not Running

Check Apache status:

```bash
sudo systemctl status apache2
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

---

## PHP File Downloads Instead of Executing

Ensure PHP module is installed:

```bash
sudo apt install libapache2-mod-php -y
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

---

## MySQL Access Denied Error

Try logging in with sudo:

```bash
sudo mysql
```

---

# Summary

You now have a fully functional LAMP stack running on Ubuntu Server 24.04.

The server includes:

- Apache Web Server
- MySQL Database Server
- PHP Scripting Language

This environment can now host dynamic websites and web applications such as:

- WordPress
- Laravel
- Nextcloud
- phpMyAdmin

---

# Next Steps

You can continue by learning:

- Apache Virtual Hosts
- SSL Certificates with Let's Encrypt
- Database Backups
- PHP Application Deployment
- Web Server Security Hardening

This LAMP environment serves as a strong foundation for Linux web hosting and full-stack web development.