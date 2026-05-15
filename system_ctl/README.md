Systemctl
In Ubuntu Server 24.04, system processes such as the SSH service, Apache web server, and background jobs like cron are all controlled by a service manager called systemd. The main tool used to interact with systemd is the command-line utility: systemctl.

If you're administering a Linux server, knowing how to use systemctl is essential.

What is systemctl?
systemctl is a utility used to start, stop, manage, and inspect services (also called "units") on systems using systemd.

It replaces older tools like service, and provides a more unified, powerful way to manage everything from web servers to system power events (like rebooting).



Common systemctl Commands
Here are the most useful systemctl commands you'll need:



Start a Service
sudo systemctl start apache2
Starts the Apache web server immediately, but it won’t start automatically at boot unless enabled.



Stop a Service
sudo systemctl stop apache2
Stops the Apache service.



Restart a Service
sudo systemctl restart apache2
Useful after making configuration changes.



Reload a Service’s Configuration
sudo systemctl reload apache2
Some services can reload configuration files without restarting.



Enable a Service at Boot
sudo systemctl enable apache2
This tells Ubuntu to start Apache automatically on system boot.



Disable a Service at Boot
sudo systemctl disable apache2
Stops the service from starting automatically on reboot.



Check the Status of a Service
sudo systemctl status apache2
Gives detailed info about whether a service is running, when it started, and recent logs.



Is the Service Enabled?
sudo systemctl is-enabled apache2
Tells you whether the service is set to start on boot.



Example: Managing SSH
SSH is the most critical service for remote access. Here’s how to manage it:

Restart SSH:

sudo systemctl restart ssh
Check if SSH is running:

sudo systemctl status ssh
Make sure SSH starts on boot:

sudo systemctl enable ssh


View All Running Services
You can view a list of running services with:

systemctl list-units --type=service
Add --all to see inactive services too:

systemctl list-units --type=service --all


Bonus: Reboot and Shutdown
Did you know you can also manage power operations?

Reboot the server:

sudo systemctl reboot
Power off the system:

sudo systemctl poweroff


Security Tip
Only users with sudo or root privileges can manage most system services using systemctl. Always be careful when stopping services like SSH, or you might lock yourself out of your server.



Summary
systemctl is the go-to command for managing services on Ubuntu Server.

Use it to start, stop, enable, disable, and check service status.

Mastering this tool is essential for maintaining and troubleshooting server environments.

## Resources
[systemctl_cheat_sheet](./asset/pdf/systemctl%2BCheat%2BSheet.pdf)