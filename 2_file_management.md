# 2. File management

## Linux directory tree

```bash
[root@devschool-01 ~]$ tree -d -L 2 /
/                 # root file system
├── bin           # user executable commands
├── boot          # kernel, boot configuration files
├── dev           # (V) device nodes for physical hardware and virtual devices
├── etc           # system configuration files
├── home          # user home directories
├── opt           # additional software
├── proc          # (V) current state of the running kernel
├── root          # home directory for root user
├── sbin          # system administration commands
├── sys           # (V) info about hotplug hardware devices
├── tmp           # temporary files, usually automatically deleted at reboot
├── usr           # system resources files
│   ├── lib       # shared libraries used by commands, kernel, programs
│   ├── lib64     # shared libraries used by commands, kernel, programs
│   ├── libexec   # binaries run by other programs
│   ├── local     # custom commands, libraries, programs
│   ├── share     # man pages, documentation, sample configuration files
│   └── src       # source code
└── var           # data that changes frequently
    ├── lock      # lock files for devices and other resources shared by multiple applications
    ├── log       # system log files
    ├── run       # information about the system that is valid until the system is next booted
    ├── spool     # cron jobs, mail messages, print jobs
    └── tmp       # temporary files, are not deleted automatically
```

## File and Directory Permissions
Linux is a multi-user operating system that allows hundreds of users to log in and work concurrently.
System administrators can grant user access to files and directories, with appropriate rights that allow them to their job whilst enforcing system security.

### Permission Classes
- **User (u)**: The owner of a file/directory
- **Group (g)**: The members of the file/directory's group
- **Others (o)**: Any users that are not part of the *user* or *group* classes

### Permission Types
- **Read (r/4)**: view/copy file/directory contents
- **Write (w/2)**: view/copy/move/delete file/directory
- **Execute (x/1)**: execute file, access directory

### Access Permissions

| Octal | Symbolic | Description             |
| ----- | -------- | ----------------------- |
| 0     | ---      | no permissions          |
| 1     | --x      | execute only            |
| 2     | -w-      | write only              |
| 3     | -wx      | write and execute       |
| 4     | r--      | read only               |
| 5     | r-x      | read and execute        |
| 6     | rw-      | read an write           |
| 7     | rwx      | read, write and execute |

### Access rights commands
- chown
- chgrp
- chmod

### Special permissions
Linux offers three other types of permissions, called **special permission bits** that may be set on executable files or directories to allow them to respond differently for certain operations.

- **setuid** bit: has effect only on files, provides non-owners the ability to run executables with the privileges of the owner
- **setgit** bit: has effect on files and directories, used for group collaboration (alters the standard behavior so that the group of the files created inside the directory, will not be that of the user who created them, but that of the parent directory)
- **sticky** bit: set on directories with effect on its files, all the files in directory will be modifiable only by their owners. A typical case is the */tmp* directory. Typically, this directory is writable by all users on the system, but a user cannot delete files owned by other users

### Default permissions
Linux assigns default permissions to a file or directory at the time of its creation. Default permissions are calculated based on the **umask** (user mask) value subtracted from a preset value called *initial permissions* (777 for directories, 666 for files).

|                     | Directory | Files |
| ------------------- | --------- | ----- |
| initial permissions |   777 -   | 666 - |
| umask               |   002     | 002   |
| default permissions |   775     | 664   |

### Control attributes
There are certain **attributes** that may be set on a file or directory in order to control what can or cannot be done to it. For example, you can enable attributes on a file or directory so that no users, including root, can delete, modify, rename, or compress it.

The commands to list or change attributes are **lsattr** and **chattr**.

## Inodes, soft links, hard links
Each file within a file system has associated metadata information such as file’s type, size, permissions, owner’s name, owner’s group name, last access/modification time, ACL settings, link count, number of allocated blocks, and pointers to the location in the file system where the file data is actually stored.

That metadata is stored in a 128 byte space on disk which is called **inode** (index node).
The inode is assigned a unique numeric identifier that is used by the kernel for accessing, tracking, and managing the file.
The inode does not store the file’s name in its metadata. The file name and corresponding inode number mapping is maintained in the directory’s metadata.

A **soft link** (a.k.a. a symbolic link or a symlink) associates one file with another (similar to a shortcut in Windows). Each soft link has a unique inode number that stores the path to the file it is linked with.

A **hard link** associates one or more files with a single inode number, making all files indistinguishable from one another. This implies that the files will have identical permissions, ownership, time stamp, and file contents. Changes made to any of the files will be reflected in the other linked files as well.

## Useful commands
```bash
chmod u=x file          # set only execute rights to file for the user (owner)
chmod og= file          # set no rights for group and others on file
chmod g+x file          # add execute rights for the group
chmod g-x file          # remove execute rights for group
chmod u+rw,og= file     # add read and write rights for user, remove every right for group and others

chmod 777 file          # add all rights to everyone for file
chmod 400 file          # add only read rights to user

chmod --reference=file1 file2 # permissions of file1 will be copied to file2

chmod -R 744 /tmp/tmp_dir # set 744 to all files and directories recursively

chown user file         # set user as the owner of file

chgrp -R group /path/to/directory # group will now be the owner of directory and everything in it

stat file               # display file details
stat -c "%a" file       # check permissions for file 

ln -s source_file_path symbolic_link_source_file_path
# ln -s /usr/bin /bin

ln source_file_path hard_link_source_file_path

df -h         # shows information about file system disk usage

du -h /var    # shows information about directory and file sizes on disk
du -h --max-depth=1 /usr | sort -rh
              # shows information about directory and file sizes on disk
              # only on the first level of directories
              # sort output in reversed order and human readable format

find /usr -type d
              # find and print all directories in /usr
find /var/log -type f -name "*.log"
              # find and print all files with .log extention in /var/log
find / -user alice
              # find directories and files owned by alice
find / -group billing
              # find directories and files owned by billing group
find / -type f -size +10M -exec ls -lh {} \;
              # find files larger than 10MB and list them in long format
```

### Practice
- create a file under your user. (644 <=> rw-r--r--)
- test write permissions with other users not from the same group as the owner (it should not work)
- change permissions to (? <=> rwxrw-r--)
- test again with someone from the same group.

- create two links on the file (hard and soft), print differences.

- find all files with .so extension.

```To err is human ... to really f*ck up requires the root password.```
