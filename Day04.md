**Task: Service User Creation without Home Directory**

In response to the latest tool implementation at xfusionCorp Industries, the system admins require the creation of a service user account. Here are the specifics:

Create a user named mark in App Server 3 wihtout a home directory.

**Solution:**
To create a service user like mark on App Server 3 without a home directory, you will use the useradd command with the -M flag.

In the Stratos Datacenter, service accounts often don't require a home directory because they are used purely to run background processes or tools, rather than for a human to log in and store personal files.

The Implementation Command
Execute the following command on App Server 3:

sudo useradd -M mark
Breakdown of the Flag
-M: (Note the capital M) This is the "no-create-home" flag. It tells the system: "Create the user, but do not create a directory for them in /home."

mark: The username for the new service account.

Verification
You can verify that the user exists but has no physical home directory by running these two checks:

Check the User Database:

grep mark /etc/passwd
You will notice it still lists /home/mark as the default path in the configuration, but the -M flag ensures the folder itself wasn't actually built.

Verify the Directory Absence:

ls /home/mark
Expected Output: ls: cannot access /home/mark: No such file or directory

Pro-Tip for Service Users
If this account is truly for a tool or service and won't be used by a person, it is often combined with the non-interactive shell we discussed earlier to maximize security:

sudo useradd -M -s /sbin/nologin mark
