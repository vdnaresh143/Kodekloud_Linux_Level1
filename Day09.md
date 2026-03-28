**Task: Script Execution Permissions**
In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 2 within the Stratos Datacenter.
Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 2. Additionally, ensure that all users have the capability to execute it.

**Solution:**

To ensure the automation script is ready for the backup process on App Server 2, you need to modify its file mode bits. In Linux, a file is not "executable" by default—even if it ends in .sh—until those specific permissions are granted.

The Implementation Command
Run the following command on App Server 2 to grant universal execution rights:

sudo chmod +x /tmp/xfusioncorp.sh
Breakdown of the Command
chmod: Short for "change mode," this is the standard utility for managing file permissions.

+x: This adds the execute permission. By not specifying a user category (like u for owner or g for group), Linux defaults to applying this to all users (owner, group, and others).

/tmp/xfusioncorp.sh: The full path to the script provided by the sysadmin team.

Alternative: Using Octal Notation
If you want to be extremely precise about the permissions (for example, making it readable and executable for everyone but writable only by the owner), you can use:

sudo chmod 755 /tmp/xfusioncorp.sh
Verification
To confirm that the change was successful, use the ls -l command to view the file's permission string:

ls -l /tmp/xfusioncorp.sh
Expected Output:
-rwxr-xr-x 1 root root ... /tmp/xfusioncorp.sh
(The x in the string confirms that the owner, the group, and others now have execution rights. On many systems, the filename will also turn green in the terminal to indicate it is executable.)

Testing the Script
Since you've granted the permissions, you can now test if the script runs correctly by calling it directly:

/tmp/xfusioncorp.sh

it will show the below message
Welcome To KodeKloud


