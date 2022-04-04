# 3. Managing software
**RHEL** is essentially a set of RPM packages grouped together to form an operating system. It is built around the Linux kernel and includes thousands of packages that are digitally signed, tested, and certified.

A software package is a group of files organized in a directory structure and metadata that makes up a software application. Files contained in a package include installable scripts, configuration files, library files, commands, and related documentation.

All metadata related to packages is stored at a central location and includes information such as package versioning, the location it is installed at, checksum values, and a list of included files with their attributes.

Usually sofware packages follow a standard naming convention.

```plaintext
name.version.release.architecture
```

## Usefull yum and rpm commands
```bash
yum search KEYWORD          # Search package details for the given string
yum info KEYWORD            # Display details about a package or group of packages
yum provides */KEYWORD      # Find what package provides the given value
rpm -ql package_name        # List files in package
rpm -qf file_name           # Find packege that owns the file
```

## DIY Lab (15min)
- yum: search the package containig the Epel repository configuration file and install it
- yum: install Apache web server
- yum: find packages containig a file named nptd
- rpm: install the package from [this url](https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/s/sl-5.02-1.el7.x86_64.rpm) and execute the **sl** command
- rpm: find which package owns the */etc/centos-release* file
- rpm: find what other files were installed by the above packet

## Solutions for DIY Lab


```Planning is for those who don't know how to troubleshoot.```

