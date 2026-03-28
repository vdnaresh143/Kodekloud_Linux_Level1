**Task: SElinux Installation and Configuration**

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 3 in the Stratos Datacenter:
Install the required SELinux packages.
Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

**Solution:**

To initiate the SELinux rollout and testing on App Server 2, you need to ensure the necessary tools are present while explicitly setting the "boot-time" state to disabled. In the Stratos Datacenter, managing the configuration file is the only way to guarantee the status after the upcoming maintenance reboot.

1. Install SELinux Packages
First, install the core SELinux management utilities. These will be essential when the team is ready to begin active configuration.

sudo yum install -y selinux-policy-targeted selinux-utils policycoreutils
2. Permanently Disable SELinux
To fulfill the requirement that SELinux remains disabled after the scheduled reboot, you must modify the main configuration file. Changing the status via setenforce 0 would only affect the current session, which your instructions say to disregard.

Edit the configuration file:

sudo vi /etc/selinux/config
Locate the line starting with SELINUX= and change it to:

Plaintext
SELINUX=disabled
3. Verification
Since you are not rebooting the server now, you can verify that the file itself is correctly configured for the next boot by checking its content:

cat /etc/selinux/config | grep ^SELINUX=
Expected Output: SELINUX=disabled

Important Context for Stratos DC
The "No Reboot" Rule: Because you aren't rebooting, the output of the sestatus command might still show Enforcing or Permissive for the current runtime. This is expected behavior based on your task constraints.

SELINUXTYPE: Ensure you do not accidentally change the SELINUXTYPE=targeted line; only the main SELINUX= directive should be modified.

**Solution2:**

Login to AppServer3

getenforece

cat /etc/os-release

sudo yum install selimux*
if this command is not working try with the below one
sudo yum install -y selinux-policy-targeted policycoreutils libselinux-utils

sestatus

cat /etc/selinux/config  --> you can see SELINUX=enforcing

sudo vi /etc/selinux/config  --> modify the SELINUX=disable

check and confirm button to complete the task

