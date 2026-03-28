**Task: Group Creation and User Assignment**

The system admin team at xFusionCorp Industries has streamlined access management by implementing group-based access control. Here's what you need to do:
a. Create a group named nautilus_admin_users across all App servers within the Stratos Datacenter.
b. Add the user kano into the nautilus_admin_users group on all App servers. If the user doesn't exist, create it as well.
Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

**Solutions :**
To implement group-based access control across the Stratos Datacenter App servers, you will need to perform these steps on each server (App Server 1, 2, and 3).
Since you are managing multiple servers, consistency is key to ensuring the nautilus_admin_users group functions correctly for the team.

1. Create the Group
First, create the administrative group. Use the groupadd command:

sudo groupadd nautilus_admin_users

2. Manage the User 'kano'
You need to ensure the user exists before adding them to a group.

Check if the user exists:

id kano
If the user does NOT exist, create them:

sudo useradd kano
Add kano to the new group:
To add a user to a supplementary group without removing them from their current groups, use the -aG (append to group) flags:

sudo usermod -aG nautilus_admin_users kano

3. Verification
After running the commands, verify that the membership was applied correctly:

groups kano
Expected Output: kano : kano nautilus_admin_users

All App Servers:
Repeat these steps on App Server 1, App Server 2, and App Server 3. In a real-world Stratos DC scenario, maintaining identical Group IDs (GIDs) across servers is a best practice for shared file permissions, though for this specific task, the standard groupadd is usually sufficient.
