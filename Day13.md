**Task: Restrict Cron Access**

In alignment with security compliance standards, the Nautilus project team has opted to impose restrictions on crontab access. Specifically, only designated users will be permitted to create or update cron jobs.
Configure crontab access on App Server 2 as follows: Allow crontab access to jim user while denying access to the garrett user.

**Solution:**

To restrict crontab access on App Server 2, you will use the cron allow and deny files located in /etc/. This is the standard Linux method for managing which users can schedule background tasks.

In the Stratos Datacenter, these files act as a whitelist and a blacklist.

1. Allow User 'jim'
To explicitly allow jim, you need to add his username to the cron.allow file. If this file doesn't exist, creating it automatically denies everyone else who isn't listed (depending on system defaults).

Run this on App Server 2:

echo "jim" | sudo tee -a /etc/cron.allow
2. Deny User 'garrett'
To explicitly deny garrett, you add his username to the cron.deny file.

Run this on App Server 2:

echo "garrett" | sudo tee -a /etc/cron.deny
How Linux Evaluates These Files
The system follows a specific logic when deciding if a user can run crontab -e:

Check cron.allow: If it exists, only users listed there can use cron. (Jim is safe here).

Check cron.deny: If cron.allow doesn't exist, it checks this file. Since Garrett is here, he is blocked.

If neither exists: Depending on the OS config, usually only root or all users can use cron.

3. Verification
You should test the configuration by switching to those users (if you have their passwords or via sudo) and attempting to open the crontab:

For Jim (Should work):

sudo su - jim -c "crontab -e"
For Garrett (Should fail):

sudo su - garrett -c "crontab -e"
Expected Error: You (garrett) are not allowed to use this program (crontab)

**Solutions2:**

login to appserver2

check the ID's are exists

id jim
id garrett

check the below commands is created or not to allow or deny cron access
cat /etc/cron.allow

cat /etc/cron.deny

if not created, create using sudo with the below commands

sudo vi /etc/cron.allow
click i and add jim user to allow permissions
:x

sudo vi /etc/cron.deny
click i and add garret user to deny permissions
:x

now check the permissions while login in to jim user and garrett user

sudo su - jim
crontab -e

sudo su - garrett
crontab -e

We habe successfully completed the task to verfy while click on check confirmation button
