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
This file stores the encryptes user' password along with other info

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
- **user_liet**: a comma delimited list of users assigned to the group. The user' primary group is defined in /etc/password

## Configuration files
The files mentioned above contain only user and group information and attributes.
There are additional files/directories that configure default values for various attributes.

- /etc/default/useradd
- /etc/login.defs
- /etc/skel/

## Common commands (demo)
- useradd
- groupadd
- passwd
- usermod
- chage
- userdel
- groupdel

```Passwords are like underwear. Change them often, don't share them, don't leave them out for others to see.```

## DIY Lab (15min)
- create a user named *alice* with UID and GID set to *3001*
- create a user named *bob* with home directory in */opt*
- create a user named *john* with comment field set to *John Doe*
- create a user named *minecraft* with:
  - UID *9990*
  - GID *9990*
  - home directory in */usr/games*
  - do not create the home directory
  - no login privileges
- set a password for alice
- create a group named *bilinq* with GID 9001
- add *alice* and *bob* to the *billing* group
- configure password aging for *alice* with **chage** command:
  -  password validity 31 days
  -  the user should receivewarnings 7 days before password expiration
- lock *minecraft* account

## Solutions for DIY Lab

