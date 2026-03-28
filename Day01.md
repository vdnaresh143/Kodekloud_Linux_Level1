**Task: Custom Apache User Setup**

In response to heightened security concerns, the xFusionCorp Industries security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications:
a. Create a user named james on App server 3 within the Stratos Datacenter.
b. Assign a unique UID 1040 and designate the home directory as /var/www/james.
Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

**Solutions:**

To complete this task on App Server 3, you will need to execute the command mentioned, followed by a few cleanup steps to ensure the user is fully functional and secure within the Stratos Datacenter environment.

Since we are creating a custom Apache user for a web application, the command we provided is the correct starting point. Here is the step-by-step execution:

1. Create the User
Run the following command to set the specific UID and home directory as requested:

sudo useradd -u 1040 -d /var/www/james -m james

2. Verify the Creation
It is a good habit in these lab environments to verify that the system applied your flags correctly. You can check the /etc/passwd file:

grep james /etc/passwd

Expected Output: james:x:1040:1040::/var/www/james:/bin/sh
(This confirms the UID is 1040 and the path is correct.)

3. Set Permissions (Best Practice)
Since this user is "tailored for an application," you'll likely want to ensure that the user james actually owns their new home directory so they can upload or edit web files:

sudo chown james:james /var/www/james
sudo chmod 755 /var/www/james



