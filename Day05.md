Task: Temporary User Setup with Expiry

As part of the temporary assignment to the Nautilus project, a developer named jim requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:

Create a user named jim on App Server 3 in Stratos Datacenter. Set the expiry date to 2026-12-07, ensuring the user is created in lowercase as per standard protocol.

Solutions:

To create a temporary user for the Nautilus project on App Server 3, you will use the useradd command with the -e (expiry) flag. Setting an expiration date is a standard security practice for contractors or temporary assignments within the Stratos Datacenter.

The Implementation Command
Run the following command on App Server 3:

sudo useradd -e 2026-12-07 jim
Breakdown of the Command
sudo: Provides the necessary administrative permissions.

useradd: The utility used to create a new user.

-e 2026-12-07: This sets the expiry date. The format must be YYYY-MM-DD. Once this date passes, the account will automatically be disabled by the system.

jim: The username, kept in lowercase as per protocol.

Verification
It is important to confirm that the expiration date was correctly recorded in the system's shadow file. You can use the chage (change age) command to view the account's aging information:

sudo chage -l jim
Expected Output:

Plaintext
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
Account expires                                         : Dec 07, 2026
Password inactive                                       : never

Additional Configuration
If jim needs a home directory to store project files, you should include the -m flag in your initial command:
sudo useradd -m -e 2026-12-07 jim
