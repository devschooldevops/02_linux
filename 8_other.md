## SSH, SCP

ssh is a program for logging into a remote machine and for executing commands on a remote machine.  It is intended to provide secure encrypted communications between two untrusted hosts over an insecure network.

```bash
[local_user@local_host ~]$ ssh remote_user@remote_host
# input password
[remote_user@remote_host ~]$ ls
# you are now connected to the remote host


# you can also run individual commands on remote host
[local_user@local_host ~]$ ssh remote_user@remote_host 'command'
# example
[local_user@local_host ~]$ ssh remote_user@remote_host rmdir /home/username_on_remote_machine/empty_dir


# we can copy files from local to remote
[local_user@local_host ~]$ scp local_file remote_user@remote_host:/home/remote_user/dest
# we can also copy dirs from remote to local
[local_user@local_host ~]$ scp -r remote_user@remote_host:/path/to/dir /home/local_user/dir
```

## Archives
### tar
```bash
# create archive with files or/and dirs
# c -> create , z -> compress with gzip, v -> verbose, f -> name of archive
tar -czvf archive_name.tar.gz  file1 file2

# peek inside archive
tar -tf archive_name.tar.gz

# extract contents
# x -> extract
tar -xvf archive_name.tar.gz -C /path/to/dir
```
### zip
```bash
# create archive with files or/and dirs
zip  archive_name.zip  file1 file2

# peek inside archive
unzip -l archive_name.zip

# extract contents
unzip archive_name.zip -d /path/to/dir
```