**Task: Process Limit Adjustment**

In the Stratos Datacenter, our application server 1 is encountering performance degradation due to excessive processes held by the nfsuser user. To mitigate this issue, we need to enforce limitations on its maximum processes. Please set the maximum process limits as specified below:
a. Set the soft limit to 1026
b. Set the hard limit to 2025

**Solutions:**

To mitigate the performance degradation caused by nfsuser on App Server 1, you need to modify the PAM (Pluggable Authentication Modules) limits. In the Stratos Datacenter, these limits prevent a single user from exhausting system resources (like processes or open files), which can lead to a "fork bomb" scenario or general system instability.

1. Edit the Limits Configuration
You will need to add these specific constraints to the /etc/security/limits.conf file. This file defines the limits for users or groups upon login.

sudo vi /etc/security/limits.conf
2. Add the User Limits
Scroll to the end of the file and append the following lines exactly as shown. Ensure there are no typos in the username or the values:

Plaintext
nfsuser    soft    nproc    1026
nfsuser    hard    nproc    2025

**Breakdown of the Configuration**
Column,Value,Description
Domain,nfsuser,The specific user account these rules apply to.
Type,soft,"The threshold where the user gets a warning, but can temporarily exceed up to the hard limit."
Type,hard,The absolute maximum. The kernel will refuse to create more processes beyond this.
Item,nproc,Short for number of processes.
Value,1026 / 2025,The specific limits requested by the Nautilus team.

3. Verification
To verify that the limits have been applied, you can use the ulimit command. However, since these limits are loaded at login, you must switch to the nfsuser to see them in action:

# Switch to nfsuser
sudo su - nfsuser

# Check the soft limit
ulimit -Su

# Check the hard limit
ulimit -Hu
Expected Output:

Soft: 1026

Hard: 2025

Why separate Soft and Hard limits?
The Soft Limit is like a "manager's warning"—it's the value the kernel actually enforces, but the user can increase it themselves up to the Hard Limit. The Hard Limit can only be increased by the root user, acting as a final safety ceiling for the Stratos DC infrastructure.
