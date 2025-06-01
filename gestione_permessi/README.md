# File and Directory Permissions Management in Linux

## Project Description
As a security professional, part of my job is to ensure that users on my team are 
authorized with the appropriate permissions. For this reason, in this project I checked 
the permissions for all files in the directory, including any hidden files, to make sure 
that permissions align with the authorization that should be given. If they do not match, 
I needed to modify the permissions to authorize the appropriate users and remove any 
unauthorized access.
To complete this task, I performed the following activities:

## 1. Check File and Directory Details
**Objective:** In this activity, I explored the permissions of the `projects` directory 
and the files it contains.
`/home/researcher2` was the current working directory. Then, I navigated to the `projects` 
directory (the command to complete this step is: `cd projects`) and listed the contents 
and permissions of the `projects` directory. I used the `ls -la` command to list the 
permissions of files and directories, including hidden files.

```bash
researcher2@482705c7a73c:~:$ cd projects
researcher2@482705c7a73c:~/projects$ ls -la
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Dec 17 14:58 .
drwxr-xr-x 3 researcher2 research_team 4096 Dec 17 15:38 ..
-rw----w-- 1 researcher2 research_team   46 Dec 17 14:58 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Dec 17 14:58 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Dec 17 14:58 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Dec 14 14:58 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_t.txt
researcher2@482705c7a73c:~/projects$
```

## 2. Describe the Permissions String
In the `/home/researcher2/projects` directory, there are five files. 
One of these is the document called `project_k.txt`. The permissions for this file are:

* User: read, write;
* Group: read, write;
* Other: read, write.

## 3. Change File Permissions
**Objective**: The organization does not allow others to have write access to any files. So, I 
removed unauthorized access and strengthened security on the system.

First, I checked whether any files in the projects directory had write permissions for the 
`other` owner type.
The command to complete this step is: `ls -la`.
The file `project_k.txt` has write permissions for other users.

I changed the permissions of the file identified in the previous step so that the `other`owner type did not have write permissions.
The command is: `chmod o-w project_k.txt`.

```bash
researcher2@482705c7a73c:~/projects$ chmod o-w project_k.txt
researcher2@482705c7a73c:~/projects$ ls -l
total 20
drwx--x--- 2 researcher2 research_team 4096 Dec 17 14:58 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Dec 17 14:58 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_t.txt
researcher2@482705c7a73c:~/projects$
```

## Explanation of the chmod command
The chmod command modifies permissions on files and directories. It is necessary to identify the file or directory for 
which you want to adjust permissions.
The first argument, added directly after the chmod command, indicates how to modify the permissions.

There are three owner types:

* u (user): represents the user owner of the file.
* g (group): represents the group owner of the file.
* o (other): represents all other users.
The `+` sign means we want to add permissions, while the `-` sign means we want to remove 
permissions.

## 4. Change Permissions on a Hidden File
**Objective**: The file `.project_x.txt` is a hidden file that has been archived and should not be modified by anyone. 
The user and group should be able to read this file.

To list the contents and permissions of the current directory and check if the group has read or write permissions, I used the command: `ls -la`. This command displays permissions 
to files and directories, including hidden files.
Then, I changed the permissions of the file `.project_x.txt` so that both the user and the group can read, but not write to, the file.

```bash
researcher2@482705c7a73c:~/projects$ ls -la
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Dec 17 14:58 .
drwxr-xr-x 3 researcher2 research_team 4096 Dec 17 15:38 ..
-rw----w-- 1 researcher2 research_team   46 Dec 17 14:58 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Dec 17 14:58 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Dec 17 14:58 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_t.txt
researcher2@482705c7a73c:~/projects$ chmod u-w,g-w,g+r .project_x.txt
```

## 5. Change Directory Permissions
**Objective**: The files and directories in the projects directory belong to the `researcher2` user. Only the `researcher2` user should be allowed to access the drafts directory and its 
contents. So, I used a Linux command to modify the permissions accordingly.

First, I checked the permissions of the drafts directory. I used the command: `ls -l`.
The group has execute permissions and therefore has access to the drafts directory.
I removed the execute permission for the group from the drafts directory.
The command to complete this step is: `chmod g-x drafts`.

```bash
researcher2@482705c7a73c:~/projects$ ls -l
total 20
drwx--x--- 2 researcher2 research_team 4096 Dec 17 14:58 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Dec 17 14:58 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 17 14:58 project_t.txt
researcher2@482705c7a73c:~/projects$ chmod g-x drafts
```

## Hidden Files and Directories Note (Contextualized)

Hidden files and directories are special files and folders that are not normally visible when listing the contents of a directory using standard commands. They are commonly used 
for configuration files and directories that should not be tampered with by regular users.
