**Task: Data Backup for Developer**

The jump host server hosts a directory named /data, serving as a repository for various developers non-confidential data. Developer john has requested a copy of their data stored in /data/john. The System Admin team has provided the following steps to fulfill this request:
a. Create a compressed archive named john.tar.gz of the /data/john directory.
b. Transfer the archive to the /home directory on the Jump Host Server.

**Solution:**
To fulfill John's request on the Jump Host Server, you will need to use the tar utility. This tool is standard for creating compressed archives (often called "tarballs") in Linux environments like the Nautilus project.

The Implementation Command
Run the following command to create and compress the archive in one step:

sudo tar -czf /home/john.tar.gz -C /data john

**Breakdown of the Flags**
Flag,   Function
-c,Create: Tells tar to start a new archive.
-z,Gzip: Compresses the archive using the gzip algorithm to save space (required for .gz).
-f,File: Specifies the name and destination of the resulting file (/home/john.tar.gz).
-C,"Change Directory: This is a ""cleanliness"" flag. It moves into /data before archiving john. This ensures that when John extracts the file later, he doesn't get a long chain of empty folders like data/john/...."

Alternative Method (Step-by-Step)
If you prefer to create the file in your current directory first and then move it, you can use these two commands:

Create the archive:

sudo tar -czvf john.tar.gz /data/john
Move it to /home:

sudo mv john.tar.gz /home/
(Note: Using the -v flag stands for "verbose," which will list every file as it is being added to the archive, helping you verify the progress.)

Verification
To ensure the archive was created correctly and contains the expected data, you can "list" the contents without extracting them:

tar -tf /home/john.tar.gz

