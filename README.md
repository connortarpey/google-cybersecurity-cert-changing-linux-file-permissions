# Changing File permissions in Linux

As a cybersecurity analyst working on the Google Cybersecurity Professional Certificate, one of the projects I was tasked with was to update file permissions for certain files and directories in a mock organization.

The current permissions set up did not reflect the correct level of authorization that should be given. By checking and updating these permissions, I will help keep the organization secure.

## Check file and directory details

To check for the current file permissions, I used ls - la

Here is the current file structure of the /home/researcher2/projects directory and the permissions of the files and subdirectories it contains.

<img width="682" height="197" alt="currentfilepermissions" src="https://github.com/user-attachments/assets/776c7ae5-b844-4bfb-a6b4-cdbcd6a8f928" />


Describing the permissions string


In Linux, there are three permissions:
- read (r)
- write (w)
-execute (x)

There are also three owner types:
-user (u)
-group (g)
-other (o)

When looking at 
drwxrwxrwx

1st character: This character is either a d or hyphen (-) and indicates the file type. If it’s
a d, it’s a directory. If it’s a hyphen (-), it’s a regular file.

2nd-10th characters: These characters indicate the read (r), write (w), and execute (x)
permissions for the user, group, and other owners, respectively. When one of these characters is a hyphen (-) instead, it indicates that this permission is not granted to that owner type.

Now, looking in the /home/researcher2/projects directory, there are five files with the following
names and permissions:


● project_k.txt
○ User = read, write,
○ Group = read, write
○ Other = read, write
● project_m.txt
○ User = read, write
○ Group = read
○ Other = none
● project_r.txt
○ User= read, write
○ Group = read, write
○ Other = read
● project_t.txt
○ User = read, write
○ Group = read, write
○ Other = read

There is one hidden file named .project_x.txt
● .project_x.txt
○ User = read, write
○ Group = write
○ Other = none

There is also one subdirectory inside the projects directory named drafts. The permissions
on drafts are:
● User = read, write, execute
● Group = execute
● Other = none
Changing file permissions
It was determined by the organization that the other owner type shouldn't have write access to any of their files. To comply with this, I referred to the file permissions that I previously returned and determined that project_k.txt must have the write access removed for other.

chmod o-w project_k.txt





Changing file permissions on a hidden file
The organization recently archived project_x.txt. They do not want anyone to have write access to this project, but the user and group should have read access. After looking at the current permissions I saw that the user had read and write permissions, and the group had write permissions, other had no permissions. 


I then removed write permissions from the user and group, and added read permissions to the group.

chmod u-w,g-w,g+r .project_x.txt 

Changing directory permissions
The organization determined it only wants the researcher2 user to have access to the drafts directory and its contents. This means that no one other than researcher2 should have execute
Permissions.
Again, first I checked the current permissions with ls -la

I saw that in the drafts directory, the user had the correct read write and execute permssions, but the group also had execute permissions. To mitigate this, I removed the execute permissions for the group.

chmod g-x drafts

Summary
I changed multiple permissions to match the level of authorization the organization wanted for
files and directories in the projects directory. The first step in this was using ls -la to
check the permissions for the directory. This informed my decisions in the following steps. I
then used the chmod command multiple times to change the permissions on files and
directories.

