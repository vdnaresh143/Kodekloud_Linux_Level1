**Task: Secure Root SSH Access**

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.
Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

**Solution:**

To disable direct root SSH login across the Stratos Datacenter App Servers, you need to modify the SSH daemon configuration file on each server. This is a standard hardening procedure to ensure that administrators must log in as a regular user and then use sudo, providing a clear audit trail.

You will need to perform these steps on App Server 1, 2, and 3.

1. Edit the SSH Configuration
Open the sshd_config file using a text editor like vi or nano:

sudo vi /etc/ssh/sshd_config
2. Locate and Modify the Directive
Search for the line containing PermitRootLogin.

It might be commented out with a #.

It might be set to yes or prohibit-password.

Change it to no:

Plaintext
PermitRootLogin no
3. Validate the Syntax
Before restarting the service, it is a best practice to check the configuration for syntax errors to avoid locking yourself out of the server:

sudo sshd -t
(If there is no output, the configuration is valid.)

4. Restart the SSH Service
For the changes to take effect, you must restart the SSH daemon:

sudo systemctl restart sshd
Verification
To verify the protocol is active, try to SSH directly into the server as root from your jump host or workstation:

ssh root@<App-Server-IP>
Expected Result: The server should deny the connection or repeatedly ask for a password even if the correct one is entered, eventually resulting in a "Permission denied" message.
