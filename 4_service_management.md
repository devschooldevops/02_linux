# 4. Service management

## The Linux Boot Process
Linux requires an initialization system during its boot and startup process.
At the end of the boot process, the Linux kernel loads the **init daemon** (a system and service management mechanism) and passes control over to it and the startup process begins.
During this step, the kernel initializes the first user space process, the init process with process ID 1, and then goes idle unless called again.
Init daemon prepares the user space and brings the Linux host into an operational state by starting all other processes on the system.

Below is a simplified overview of the entire Linux boot and startup process:
- The system powers up. The BIOS does minimal hardware initialization and hands over control to - the boot loader
- The boot loader calls the kernel.
- The kernel loads an initial RAM disk that loads the system drives and then looks for the root file system
- Once the kernel is set up, it loads the init daemon
- init daemon takes over and continues to mount the host’s file systems and start services


## systemd
- **systemd** (system daemon) is a system and service management mechanism used by modern Linux distributions.
- it has replaced older service management systems (SysVinit, Upstart)
- introduced parallel processing of startup scripts
- improved handling of service dependencies
- it is backwards compatible with SysVinit scripts as described in the Linux Standard Base (LSB) specification
- systemd is the first process that starts at boot, and it is the last process that terminates at shutdown

### systemd Units
systemd introduces the concept of **systemd units** and there are several types, such as a service unit, mount unit, socket unit and slice unit. Units are defined in unit configuration files, which include information about the unit type and its behavior.

| Unit type  | Description |
| -----------| ----------- |
| Target     | A group of units that defines a synchronization point which is used at boot time to start the system in a particular state |
| Service    | A unit of this type starts, stops, restarts or reloads a service daemon such as Apache webserver |
| Socket     | A unit of this type activates a service when the service receives incoming traffic on a listening socket |
| Device     | A unit of this type implements device-based activation such as a device driver |
| Mount      | A unit of this type controls the file-system mount point |
| Automount  | A unit of this type provides and controls on-demand mounting of file systems |
| Swap       | A unit of this type encapsulates/activates/deactivates swap partition |
| Path       | A unit of this type monitors files/directories and activates/deactivates a service if the specified file or directory is accessed |
| Timer      | A unit of this type activates/deactivates specified service based on a timer or when the set time is elapsed |
| Snapshot   | A unit that creates and saves the current state of all running units. This state can be used to restore the system later |
| Slice      | A group of units that manages system resources such as CPU, and memory |
| Scope      | A unit that organizes and manages foreign processes |


The following table briefly explains the terms that the systemd uses to describe the status of units.

| Status         | Description |
| -------------- | ----------- |
| loaded         | The unit's configuration file has been successfully read and processed |
| active exited  | Successfully executed the one-time configuration and after execution, the unit is neither running an active process nor waiting for an event |
| active running | Successfully executed the one-time configuration and after execution, the unit is running one or more active processes |
| active waiting | Successfully executed the one-time configuration and after execution, the unit is waiting for an event |
| inactive dead  | Either the one-time configuration failed to execute or not executed yet |

### systemd targets
systemd replaces traditional SysVinit **runlevels** with predefined groups of units called **targets**.
Targets are usually defined according to the intended use of the system, and ensure that required dependencies for that use are met.
The following table shows some standard preconfigured targets, the sysVinit runlevels they resemble and the use case they address.

| Target     | Runlevel | Usage                                                                                |
| ---------- | -------- |--------------------------------------------------------------------------------------|
| rescue     | 1        | single user mode, for recovery of critical system components or configuration        |
| multi-user | 2        | non-graphical multi-user console access, via local TTYs or network                   |
| graphical  | 5        | a GUI session. Typically provides the user with a fully featured desktop environment |
| custom     | 4        | systemd allows any number of custom defined targets                                  |


## systemd cheat sheet
```bash
systemctl list-units --type=service # list all loaded service units
systemctl status NAME               # check status for NAME service unit
systemctl is-enabled NAME           # check if NAME service is enabled
systemctl start|stop|restart NAME   # start|stop|restart NAME service
systemctl enable|disable NAME       # enable|disable NAME service
systemctl get-default               # get default target
```

## Practice
- (Service) play with firewalld (Red Hat) or ufw (Debian), add a rule, make it persistent
- (Service) start httpd (or nginx) service and make sure the change is persistent across reboots

```Linux is user-friendly, but it's just very selective about who its frieds are.```
