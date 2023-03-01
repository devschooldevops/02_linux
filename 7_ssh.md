## SSH, SCP

ssh is a service for logging into a remote machine and for executing commands on that machine.  It is intended to provide secure encrypted communications between two untrusted hosts over an insecure network.

```bash
# check if sshd is running
systemctl status sshd
```

```bash
[local_user@local_host ~]$ ssh remote_user@remote_host
# input password

[remote_user@remote_host ~]$ ls
# you are now connected to the remote host

[remote_user@remote_host ~]$ bash
# switch to bash terminal


# you can also run individual commands on remote host
[local_user@local_host ~]$ ssh remote_user@remote_host 'command'
# example
[local_user@local_host ~]$ ssh remote_user@remote_host rmdir /home/username_on_remote_machine/empty_dir


# we can copy files from local to remote
[local_user@local_host ~]$ scp local_file remote_user@remote_host:/home/remote_user/dest
# we can also copy dirs from remote to local
[local_user@local_host ~]$ scp -r remote_user@remote_host:/path/to/dir /home/local_user/dir
```