**Task: Default GUI Boot Configuration**

With the installation of new tools on the app servers within the Stratos Datacenter, certain functionalities now necessitate graphical user interface (GUI) access.
Adjust the default runlevel on all App servers in Stratos Datacenter to enable GUI booting by default. It's imperative not to initiate a server reboot after completing this task.

**Solution:**

To adjust the default runlevel for GUI access across the Stratos Datacenter App Servers without rebooting, you will need to change the systemd target.

In modern Linux distributions (like those used in the Nautilus project), "runlevels" have been replaced by "targets." To enable a GUI by default, you must switch from the multi-user.target (command line) to the graphical.target.

The Implementation Command
You will need to run this command on App Server 1, 2, and 3:

sudo systemctl set-default graphical.target
Breakdown of the Command
systemctl: The central tool for controlling the systemd init system and services.

set-default: This specifically changes the "boot-up" destination for the next time the server starts.

graphical.target: This is the equivalent of the old Runlevel 5, which initializes the display manager and the desktop environment.

Verification
To ensure the change has been registered correctly without rebooting the server, run:

systemctl get-default
Expected Output: graphical.target

⚠️ Important Note on Reboots
As per your instructions, do not run reboot. While the setting is now "default," the server's current session will remain in the command-line interface. 
If you actually needed to switch to the GUI right now without a reboot, you would use sudo systemctl isolate graphical.target, but for this specific task, set-default is the only requirement.


