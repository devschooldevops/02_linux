# 3. Managing software
**RHEL** is essentially a set of RPM packages grouped together to form an operating system. It is built around the Linux kernel and includes thousands of packages that are digitally signed, tested, and certified.

A software package is a group of files organized in a directory structure and metadata that makes up a software application. Files contained in a package include installable scripts, configuration files, library files, commands, and related documentation.

All metadata related to packages are stored at a central location and includes information such as package versioning, the location it is installed at, checksum values, and a list of included files with their attributes.

Usually software packages follow a standard naming convention.

```plaintext
name.version.release.architecture
```

## Useful yum and rpm commands
```bash
yum list all                # List installed and available packages from repositories
yum list installed          # List only installed packages
yum list available          # List only available packages
yum list kernel             # List installed and available kernel packages

yum search KEYWORD          # Search package details for the given string
yum info KEYWORD            # Display details about a package or group of packages

yum check-update            # Check for updates
yum update                  # Perform updates
yum update package_name     # Update custom package

yum install package_name    # Install package

yum erase package_name      # Remove package
yum remove package_name     # Remove package
yum autoremove              # Cleanup unused packages
```

## Useful apt commands
```bash
apt list                    # List installed and available packages from repositories
apt list --installed        # List only installed packages

apt search KEYWORD          # Search package details for the given string
apt info KEYWORD            # Display details about a package or group of packages

apt update                  # Check for updates
apt upgrade                 # Perform updates
apt-get install --only-upgrade package_name   # Update custom package

apt install package_name    # Install package

apt remove package_name     # Remove package
apt purge package_name      # Remove package + config
apt autoremove              # Cleanup unused packages
```

More commands [here](https://www.baeldung.com/linux/yum-and-apt).

## Practice
- search the package containing the Epel repository configuration file and install it
- install Apache web server
- find packages containing a file named nptd
- install the package **sl** from the official download site (add apt or rpm to your search query) and execute the **sl** command
- find which package owns the */etc/centos-release* file
- find what other files were installed by the above packet

## Solutions for DIY Lab


```Planning is for those who don't know how to troubleshoot.```

