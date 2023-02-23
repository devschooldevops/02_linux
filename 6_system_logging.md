# 6. System logging

Log files are files that contain messages about the system, including the kernel, services, and applications running on it.
There are different log files for different information. For example, there is a default system log file, a log file just for security messages, and a log file for cron tasks. Everything from kernel events to user actions can be logged, allowing you to see almost any action performed on your servers.

Log files can be very useful when trying to troubleshoot a problem with the system such as trying to start a service or when looking for unauthorized login attempts to the system.

In RHEL7 log files are controlled by a daemon called **rsyslogd**.


## Linux System Logs
Linux has a special directory for storing logs called **/var/log**.
This directory contains logs from the OS itself, services, and various applications running on the system.

Some of the most important Linux system logs include:
- **/var/log/messages** stores all global system activity data, including startup messages
- **/var/log/secure** stores all security-related events such as logins, root user actions, and output from pluggable authentication modules (PAM)
- **/var/log/cron** stores information about scheduled tasks (cron jobs)
- **/var/log/maillog** contains information about emails relayed by the loca mail server
- **/var/log/yum** yum logs

## Log file rotation
With the amount of logging that is possible, you need to be able to control the size of log files.
This is done using the **logrotate** command, which is usually run as a cron job.

The general idea behind the logrotate command is that log files are periodically backed up and a new log is started.
Several generations of log are kept, and when a log ages to the last generation, it may be archived/deleted.

## Journalctl
Logs are usually dispersed throughout the system, handled by different daemons and processes, and can be fairly difficult to interpret when they span multiple applications.
Systemd attempts to address these issues by providing a centralized management solution for logging all kernel and userland processes. The system that collects and manages these logs is known as the **journal**.

## Cheat sheet
```bash
tail -n 100 /var/log/messages  # print last 100 lines
tail -f /var/log/secure        # follow log

journalctl            # every journal entry that is in the system will be displayed
journalctl -b         # journal entries collected since the most recent reboot
journalctl -k         # display only kernel messages
journalctl -n 20      # display last 20 messages
journalctl -f         # actively follow the logs as they are being written
journalctl -p err     # filter messages by priority
journalctl -u sshd    # filter messages by service unit
journalctl -u crond --since today

last                  # show listing of last logged in users
lastb                 # show listing of users logged in since the last boot

less logfile          # go through the logfile

grep pattern file     # search for pattern in file
```

## Practice
- Search in /var/log/secure for activity from your user.
- Search in yum logs, see recent updates/installs.

```The only problem with troubleshooting is that sometimes trouble shoots back.```
