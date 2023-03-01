# 1. Managing Users and Groups
In order for an authorized person to gain access to the system, a user account must be created on the system.
User and group account information is stored in several files:
- /etc/passwd
- /etc/shadow
- /etc/group
- /etc/gshadow

## /etc/passwd
The /etc/passwd file contains all user's properties. Each line contains information about one user account.
There are seven fields per line entry separated by a colon (:).

```plaintext
user_name:x:UID:GID:comments:home_directory:shell
```

- **user_name**: `/^[a-z0-9-_]+$/`. Should not use uppercase letters or special characters
- **x**: password placeholder
- **UID**: a unique number. UIDs between 0 and 999 are reserved for system accounts
- **GID**: a number that corresponds with a group entry in */etc/group*
- **comments**: info about the user
- **home_directory**: default location is */home/user_name*
- **shell**: user's default shell

## /etc/shadow
This file stores the encrypted user' password along with other info

```plaintext
user_name:encypted_passords:lastchg_days:min_days:max_days:warn_days:inactive_days:disabled_days:
```

- **user_name**:
- **encypted_passords**: May be empty. An exclamation mark shows that the user is locked
- **lastchg_days**: number of days in epoch time since the password was changed
- **min_days**: minimum numer of days that must pass before the user can change the passwords
- **max_days**: maximum number of days before the user gets password expiration warnings
- **warn_days**: number of days for which the user gets password expiration warnings
- **inactive_days**: maximum number of days for user inactivity
- **disabled_days**: number of days in epoch time after which the account expires

Most of the above parameters can be changed with *password*, *usermod* and/or *chage* commands.

## /etc/group
This file contains group information.
Every user must be a member of at least one group, which is called *primary group*.
Additional groups may be created and users assigned to them.

```plaintext
group_name:x:GID:user_list
```

- **group_name**: a unique group name
- **x**: password placeholder. Usually group passwords are not used. It may contain an encrypted password
- **GID**: group ID
- **user_list**: a comma delimited list of users assigned to the group. The user' primary group is defined in /etc/password

## /etc/sudoers
This file contains users and groups privileges. We use the **visudo** command to edit this file (visudo also validates sudoers file syntax)

```bash
[your_user@your_machine ~]$ sudo visudo
```

```bash
# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# Or allow members of group wheel to execute any command
%wheel   ALL=(ALL:ALL) ALL
```
The explanation for root is as follows:
```bash
root ALL=(ALL:ALL) ALL The first field indicates the username that the rule will apply to (root).
root ALL=(ALL:ALL) ALL The first “ALL” indicates that this rule applies to all hosts.
root ALL=(ALL:ALL) ALL Second “ALL” indicates that the root user can run commands as all users.
root ALL=(ALL:ALL) ALL Third “ALL” indicates that the root user can run commands as all groups.
root ALL=(ALL:ALL) ALL The last “ALL” indicates these rules apply to all commands.
```

Your user is in the sudo group and is allowed to execute all commands with sudo. You can check this with:
```bash
[your_user@your_machine ~]$ groups your_user
```
or in the above-mentioned /etc/groups file.


## Configuration files
The files mentioned above contain only user and group information and attributes.
There are additional files/directories that configure default values for various attributes.

- /etc/default/useradd
- /etc/login.defs
- /etc/skel/

## Common commands
- whoami
- id
- useradd
- groupadd
- su
- passwd
- usermod
- chage
- userdel
- groupdel
- visudo

```bash
sudo useradd new_user

sudo groupadd new_group

sudo passwd new_user

# login as new_user
su new_user

su # no args means login as root

# usermod examples:
# add user to group
sudo usermod -a -G new_group new_user
# change the primary group
sudo usermod -g new_group new_user

id new_user

# change home dir
usermod -d new_home_dir new_user

sudo userdel new_user

sudo groupdel new_group
```

```Passwords are like underwear. Change them often, don't share them, don't leave them out for others to see.```

## Practice
- create a user named *alice*
- create a user named *bob*
- create a user named *john*
- create a group named *friends*
- add *alice* and *bob* to the *friends* group
- delete user *john* with his home dir
- create a user *king* and add him in the sudoers file with root privileges, then test them (run something with sudo)