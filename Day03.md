Task: Linux User Setup with Non-Interactive Shell

To accommodate the backup agent tool's specifications, the system admin team at xfusionCorp_Industries requires the creation of a user with a non-interactive shell. Here's your task:

create a user named kareen with a non-interative shell on App Server3.

Solution:

To create a user with a non-interactive shell on App Server 3, you will use the useradd command with the -s (shell) flag.
In a security-conscious environment like the Stratos Datacenter, non-interactive shells are standard for "service accounts" or backup agents. This ensures that even if someone manages to compromise the account, they cannot log in to a terminal and run manual commands.

The Implementation Command
Run the following command on App Server 3:

sudo useradd -s /sbin/nologin kareen

Breakdown of the Flag
-s /sbin/nologin: This specifies the shell for the user. By pointing it to /sbin/nologin (or sometimes /usr/sbin/nologin depending on the OS version), the system will politely refuse any attempt by the user kareen to log in, often displaying a message like "This account is currently not available."

Verification: Once you have created the user, you should verify that the shell has been set correctly by checking the system's user database:

sudo cat /etc/passwd
it will shows the user details where it was created

grep kareen /etc/passwd

Expected Output:
kareen:x:1001:1001::/home/kareen:/sbin/nologin
(Note: The UID 1001 may vary based on existing users, but the last part must be /sbin/nologin.)

Since this is for a backup agent tool, the tool might eventually need to "own" certain backup directories. You can create the user and their home directory simultaneously while still disabling the shell by adding the -m flag:

sudo useradd -m -s /sbin/nologin kareen

