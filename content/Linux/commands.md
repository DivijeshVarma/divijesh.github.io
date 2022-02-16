+++
title = "Yum&RpmCmd"
weight = 5
+++

YUM (Yellowdog Updater Modified) is an open-source command-line as well as graphical-based package management tool for RPM (RedHat Package Manager) based Linux systems.

*Install a Package with YUM:*
```bash
 yum -y install firefox
```

*Removing a Package with YUM:*
```bash
 yum -y remove firefox
```

*Updating a Package using YUM:*
```bash
 yum -y update mysql
```

*List a Package using YUM:*
Use the list function to search for the specific package with a name, it gives Installed Packages and Available Packages.
```bash
 yum list openssh
```

*Search for a Package using YUM:*
When you run yum search, the command searches for package name, summaries and description.
```bash
yum search vim
```

*Get Information about a Package using YUM:*
```bash
yum info firefox
```

*List all Available Packages using YUM:*
```bash
yum list | less
```

*List all Installed Packages using YUM:*
```bash
yum list installed | less
```

*Yum Provides Function:*
Yum provides function is used to find which package a specific file belongs to.
```bash
yum provides /etc/httpd/conf/httpd.conf
```

*Check for Available Updates using Yum:*
To find how many installed packages on your system have updates available.
```bash
yum check-update
```

*exclude a particular package while updating the whole system:*
list of all the available packages to update using the following command.
```bash
yum list updates | cat -n
```

```bash
yum -x "package_name*" -x "package_name2*" update
```

*List all available Group Packages:*
In Linux, a number of packages are bundled into a particular group. Instead of installing individual packages with yum, you can install a particular group that will install all the related packages that belong to the group.To list all available groups.
```bash
yum grouplist
```

*Install Group Packages:*
```bash
yum groupinstall 'MySQL Database'
```

*Update a Group Packages:*
To update any existing installed group packages.
```bash
yum groupupdate 'DNS Name Server'
```

*Remove Group Packages:*
```bash
yum groupremove 'DNS Name Server'
```

*List Enabled Yum Repositories:*
```bash
yum repolist
```

*List all Enabled and Disabled Yum Repositories:*
```bash
yum repolist all
```

*Install a Package from a Specific Repository:*
To install a particular package from a specific enabled or disabled repository, you must use --enablerepo
```bash
yum --enablerepo=epel install phpmyadmin
```

*Interactive Yum Shell:*
Yum utility provides a custom shell where you can execute multiple commands.
```bash
yum shell
```

*Clean Yum Cache:*
to clean all cached files from the enabled repository.
```bash
yum clean all
```

*View History of Yum:*
```bash
yum history
```

*Command to install/update only the security fixes:*
```bash
yum update --security
```

*Upgrade the system with the latest releases:*
upgrade your version from 7.4 to 7.8
```bash
yum upgrade -y
```

*Downgrade the version:*
current version of "http-parser" is (2.7.1-8.el7_7.2) and revert to (2.7.1-8.el7).
```bash
yum downgrade http-parser-2.7.1-8.el7
```

---

### RPM Commands

RPM(Redhat Package Manager) is a command line package management utility used for installing, uninstalling, updating, querying and verifying software packages.

GeoIP application GeoIP-1.5.0-11.el7.x86_64.rpm is a RPM Package Library for country/city/organization to IP address.

*Information of RPM package without installing:*
We can use -qipoption (query info package) to list the information of a package.

```bash
rpm -qip GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Install RPM package:*
```bash
rpm -ivh GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Check an installed RPM package:*
```bash
rpm -q GeoIP
```

*List all files for particular installed RPM package:*
```bash
rpm -ql GeoIP
```

*List recently installed RPM packages:*
```bash
rpm -qa --last
```

*Install RPM package without dependencies:*
```bash
rpm -ivh --nodeps GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Replace RPM package installed:*
 use -ivh --replacepkgs parameters to replace a particular package installed.
```bash
rpm -ivh --replacepkgs GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Uninstall RPM package:*
```bash
rpm -ev GeoIP
```
use -e parameters to uninstall particular package installed without dependencies don't check dependencies.
```bash
rpm -e --nodeps GeoIP
```

*Upgrade RPM package installed:*
```bash
rpm -Uvh GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Query all installed package:*
use -a parameters along with q to query all installed packages on the server.
```bash
rpm -qa
```

*Query particular package:*
```bash
rpm -qa | grep GeoIP
```

*Display list of configuration file(s) for a package:*
```bash
rpm -qc GeoIP
```

*Query a file that belongs which RPM Package:*
```bash
rpm -qf /usr/lib64/libGeoIP.so.1.5.0
```

*Display list of configuration files for a command:*
```bash
rpm -qcf /usr/lib64/libGeoIP.so.1.5.0
```

*Get information for a particular package:*
```bash
rpm -qi GeoIP
```

*What dependencies a rpm file have:*
```bash
rpm -qR GeoIP
```

*Verify a RPM package:*
By using -Vp option (verify package).
```bash
rpm -Vp GeoIP-1.5.0-11.el7.x86_64.rpm
```

*Verify all RPM packages:*
```bash
rpm -Va
```
