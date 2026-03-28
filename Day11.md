**Task: String Replacement**

At xFusionCorp Industries, the Stratos Datacenter houses a jump host server that stores template XML files essential for the Nautilus application. Prior to their use, these files need to be populated with valid data. As part of regular maintenance, the system administration team utilizes various string and file manipulation commands to prepare these templates.
Your task is to substitute all occurrences of the string Text with Maritime within the XML file located at /root/nautilus.xml on the jump host server.

**Solution:**

As you already in jumphost its not required to login any of the AppServers to perform this task. Follow the below commands to execute:

Sudo cat /root/nautilus.xml  --> to view file content

Sudo vi /root/nautilus.xml  --> edit the file

:%s/Text/Marine/g  --> it will change from Text to Marine as per the task

Click enter to change all

Now click esc :x to save and exit

That is we have successfully changes the string from Text to Marine on the nautilus..xml file located on root directory



