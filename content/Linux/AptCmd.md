+++
title = "AptCmd"
weight = 5
+++

apt is a command-line utility for installing, updating, removing, and otherwise managing deb packages on Ubuntu, Debian, and related Linux distributions.

*Update package database:*
apt update only updates the database of the packages.
```bash
sudo apt update
```

*Upgrade installed packages:*
Once you have updated the package database, you can now upgrade the installed packages.
```bash
sudo apt upgrade
```

There is another way to provide a complete upgrade by using the command below:
```bash
sudo apt full-upgrade
```

full-upgrade works the same as upgrade except that if system upgrade needs the removal of a package already installed on the system, it will do that. Whereas, the normal upgrade command won’t do this.

### Difference between apt update and apt upgrade:

Though it sounds like when you do an apt update, it will update the packages and you’ll get the latest version of the package. But that’s not true. apt update only updates the database of the packages.

For example, if you have XYZ package version 1.3 installed, after apt update, the database will be aware that a newer version 1.4 is available.  When you do an apt upgrade after apt update, it upgrades the installed packages to the newer version.

*Convenient way to update Ubuntu system:*
```bash
sudo apt update && sudo apt upgrade -y
```

*Install new packages:*
```bash
sudo apt install mplayer
```

*Remove installed packages:*
```bash
sudo apt remove mplayer
```

Another way of uninstalling packages is to use purge. The command is used in the following manner:
```bash
sudo apt purge mplayer
```

### Difference between Remove and Purge

>  apt remove just removes the binaries of a package. It leaves residue configuration files.
>  apt purge removes everything related to a package including the configuration files.

*Search for packages:*
search for a given package in the list of the available packages
```bash
apt search mplayer
```

*content of a package:*
This will show information about the given packages like its dependencies, installation and download size.
```bash
apt show mplayer
```

*List upgradable:*
see all the packages that have a newer version ready to be upgraded.
```bash
apt list --upgradable
```

To list all available packages use the following command
```bash
sudo apt list
```

To find out whether a specific package is installed
```bash
sudo apt list | grep mpv
```

see all the installed packages on the system
```bash
apt list --installed
```

list all the packages available for your system
```bash
apt list --all-versions
```

*Clean your system:*
command removes libs and packages that were installed automatically to satisfy the dependencies of an installed package. If the package is removed, these automatically installed packages, though useless, remains in the system.
```bash
sudo apt autoremove
```

*Install local deb files:*
```bash
apt install /full/path/file.deb
```

