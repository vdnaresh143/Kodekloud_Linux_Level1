**Task: File Permission Correction**

After conducting a security audit within the Stratos DC, the Nautilus security team discovered misconfigured permissions on critical files. To address this, corrective actions are being taken by the production support team. Specifically, the file named /etc/hosts on Nautilus App 3 server requires adjustments to its Access Control Lists (ACLs) as follows:
1. The file's user owner and group owner should be set to root.
2. Others should possess read only permissions on the file.
3. User ammar must not have any permissions on the file.
4. User garrett should be granted read only permission on the file.

**Solution:**

To address these security audit findings on Nautilus App 3, you will need to combine standard Linux file permissions with Access Control Lists (ACLs). While standard permissions handle the owner and "others," ACLs allow for the specific, granular restrictions requested for users like ammar and garrett.

1. Set Ownership and Standard Permissions
First, ensure the file is owned by root and that the general public ("others") can only read it.

# Set user and group owner to root
sudo chown root:root /etc/hosts

# Set standard permissions: Owner (read/write), Group (read), Others (read)
sudo chmod 644 /etc/hosts
2. Apply Specific ACLs
Standard permissions aren't enough to single out ammar or garrett specifically. For this, we use the setfacl command.

To deny ammar all permissions:

sudo setfacl -m u:ammar:--- /etc/hosts
To grant garrett read-only permission:

sudo setfacl -m u:garrett:r-- /etc/hosts
3. Verification
To confirm that both the standard permissions and the new ACL entries are active, use the getfacl command:

getfacl /etc/hosts
Expected Output:

Plaintext
# file: etc/hosts
# owner: root
# group: root
user::rw-
user:ammar:---
user:garrett:r--
group::r--
mask::r--
other::r--
Key Differences to Note
The "+" Sign: If you run ls -l /etc/hosts now, you will notice a + sign at the end of the permission string (e.g., -rw-r--r--+). This indicates that an ACL is currently protecting the file.

Order of Precedence: Linux checks permissions in a specific order: Owner → Specific User ACL → Group → Specific Group ACL → Others. Because ammar is explicitly listed with ---, they will be blocked even though "others" have read access.
