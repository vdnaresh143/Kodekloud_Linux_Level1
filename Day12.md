**Task: Secure Data Transfer**

A Nautilus developer has stored confidential data on the jump host within Stratos DC. To ensure security and compliance, this data must be transferred to one of the app servers. Given developers lack direct access to these servers, the system admin team has been enlisted for assistance.
Copy /tmp/nautilus.txt.gpg file from jump server to App Server 2 placing it in the directory /home/code.

**Solutions:**

To move a file from the Jump Host to App Server 2 (stapp02), the standard tool is scp (Secure Copy). Since developers can't access the app servers directly, you'll be using the Jump Host as the starting point for the transfer.

The Implementation Command
Run this command from your terminal on the Jump Host:

scp /tmp/nautilus.txt.gpg steve@stapp02:/home/code

**Breakdown of the Command**

Component,  Purpose
scp,The command for securely copying files over an SSH connection.
/tmp/nautilus.txt.gpg,The source path of the file on the Jump Host.
steve@stapp02,The destination user (steve) and server hostname/IP (stapp02).
:/home/code,The destination directory on the app server.

Important Considerations
Permissions: If the /home/code directory is owned by root, the user steve might not have permission to write to it directly. If the transfer fails with a "Permission denied," you may need to copy it to steve's actual home directory first, then log into the server and move it using sudo:

Step 1 (on Jump Host): scp /tmp/nautilus.txt.gpg steve@stapp02:~

Step 2 (on App Server 2): sudo mv ~/nautilus.txt.gpg /home/code/

Verification: Once the transfer is complete, log into App Server 2 and verify the file exists:

ssh steve@stapp02
ls -l /home/code/nautilus.txt.gpg
