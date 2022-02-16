+++
title = "Intro"
weight = 5
+++

## Introduction 

Linux ia an Open source operating system inspired by unix, it was introduced by Linus torvalds. An operating system is the software that directly manages a system’s hardware and resources, like CPU, memory, and storage. The OS sits between applications and hardware and makes the connections between all of your software and the physical resources that do the work.

Linux is the name of the operating system kernel, various supporting software and libraries are necessary to make a complete operating system from a kernel (an engine is not sufficient to build a car). Many of these - such as the compiler, the C libraries, and the shell - are part of the GNU project. The GNU project included a huge effort to create a non-proprietary operating system, writing open-source equivalents of software and open-source implementations of standards

--- 
## Booting Process 

1) POST is part of BIOS and beginning stages of BIOS operation after power on computer, BIOS having POST inside it. As soon as machine is powered on, System firmware runs POST, it checks everything working correctly Input/Output devices, RAM, hard drives, PC Hardware.if found working correctly, then it will go to next step.

2) The system firmware searches for a bootable device, either configured in the UEFI boot firmware or by searching for a Master Boot Record (MBR) on all disks, BIOS (basic input output system) checks for bootable device, it could be Hard disk, cd drive, USB. BIOS then checks for MBR(master boot record) in hard disk it is always first sector of bootable disk with size 512 bytes(446- primary boot loader, 64- partition table, 2- magic number).

3) Primary boot loader contains address of main boot loader (MBR is very small) Main boot loader is GRUB2 which resides inside a file system /boot at that time your system doesn't have access to file system, so who helps system to go inside the file system i.e MBR. Bootloader in MBR points to GRUB2.

4) GRUB2 (grand unified bootloader) version 2 loads config file /boot/grub2/grub.cfg and displays menu where you can select which kernel to boot. It loads vmlinuz kernel image(/boot/vmlinuz4.1) file into memory and extract content of Initramfs image (initramfs4.1) into a temporary, memory-based file system (tmpfs). Initramfs is an archive contains all kernel modules and drivers.The initial RAM disk (initrd) is an initial root file system that is mounted before the real root file system.

5) kernel initialize hardware, try to mount root file system but kernel requires modules and drivers for initialize the hardware, it takes all those things from Initramfs. KERNEL executes /sbin/init from initramfs as first process having process (PID1) on RHEL8, init has been replaced with Systemd & /sbin/init file is soft link to systemd. (ls -l /sbin/init)

6) Systemd executes Initrd.target with the help of initramfs, it executes all units for Initrd.target that includes mounting root file system on disk at /sysroot directory. on RHEL8 runlevels are called as targets, Total 7 targets will be present.

7) It switches root file system permanently from /sysroot to / directory, Kernel root filesystem switched from initramfs root (/sysroot) to system root filesystem(/)

8) Systemd looks for default target and this file /etc/systemd/system/default.target to boot up the machine it links to graphical.target system target file defines the services that system starts.

### Runlevels 

The standard LINUX kernel supports these seven different runlevels :

0) System halt i.e the system can be safely powered off with no activity.(Shuts down system)
1) Single user mode.(Does not configure network interfaces, start daemons, or allow non-root logins)
2) Multiple user mode with no NFS(network file system),(Does not configure network interfaces or start daemons).
3) Multiple user mode under the command line interface and not under the graphical user interface.
4) Undefined (Not used/User-definable)
5) Multiple user mode under GUI (graphical user interface) and this is the standard runlevel for most of the LINUX based systems.(X11, As runlevel 3 + display manager(X))
6) Reboot which is used to restart the system.

Changing runlevels with systemd:

The runlevel target can be changed by using the systemctl isolate command :

```bash
systemctl isolate multi-user.target
```

```bash
systemctl isolate graphical.target
```

To view what targets are available you can issue the list-units:

```bash
systemctl list-units --type=target
```

To list available targets:

```bash
ls -l /lib/systemd/system/runlevel
```

Changing the default runlevel:

```bash
systemctl set-default multi-user.target
```

To get the currently set default:

```bash
systemctl get-default
```



## File System Structure 

Linux directory structure is like a tree that begins with a top level directory called “Root”. Rest of the directories brach off this “Root” directory.

In Linux, everything is a file. Or, more accurately, everything is represented as being a file.

* / – this is known as “root”, The single, top level directory in Linux.Every other directory of the Linux file system branches off from this directory.

* /bin - essential user command binaries, commands we use daily like (ls), cp, (cat), some of the applications and programs you can run.

* /boot - static Boot Files,This is where all the needed files for Linux to boot are kept, for example, the GRUB boot loader’s files and your Linux kernels are stored here.
initramfs-5.15.19_1.img, vmlinuz-5.15.19_1.

* /dev - Device Files,This is where your physical devices are mounted, such as your hard drives, USB drives, optical drives, /dev/sda represents the first SATA drive in the system.whereas your USB thumb drive might be mounted under /dev/sde.

* /etc - Configuration Files, The /etc directory contains configuration files, which can generally be edited. Note that the /etc/ directory contains system-wide configuration files.whereas users can also store configuration files under their own /home folders.

* /home - Home Folders, home folder for each user. This home folder contains the user’s data files and user-specific configuration files.The Desktop, Documents, Downloads, Photos, and Videos folders are all stored under the /home/username directory.

* /lib - Essential Shared Libraries, The /lib directory contains libraries needed by the essential binaries in the /bin and /sbin folder. Libraries needed by the binaries in the /usr/bin folder are located in /usr/lib.

* /media - Removable Media, Another place where external devices such as optical drives and USB drives can be mounted. This varies between different Linux distros.

* /mnt - Temporary Mount Points,this directory is where system administrators mounted temporary file systems while using them. to mount things manually.

* /opt - Optional Packages, contains subdirectories for optional software packages. It’s commonly used by proprietary software that doesn’t obey the standard file system hierarchy.

* /proc - Kernel & Process Files, The “processes” folder where a lot of system information is represented as files, It contains Pseudo files that contain information about system processes and resources 

> cat /proc/cpuinfo - it gives info about CPU 

> cat /proc/uptime - uptime 

* /root - Root Home Directory, The /root directory is the home directory of the root user. Instead of being located at /home/root, it’s located at /root.

* /sbin - system binaries, The /sbin directory is similar to the /bin directory. It contains essential binaries that are generally intended to be run by the root user for system administration.Only system admins will use these commands like (adduser), You can use these applications with the sudo command that temporarily concedes you superuser.

* /srv - service directory, this is where service data is stored, if you run a web server or ftp server you would stores files that will be accessed by external users here.

* /tmp - Temporary Files, Applications store temporary files in the /tmp directory. These files are generally deleted whenever your system is restarted.

* /usr - User Binaries & Read-Only Data, The /usr directory contains applications and files used by users, as opposed to applications and files used by the system. For example, non-essential applications are located inside the /usr/bin directory instead of the /bin directory and non-essential system administration binaries are located in the /usr/sbin directory instead of the /sbin directory. Libraries for each are located inside the /usr/lib directory.

* /var — Variable Data Files, This is where variable data is kept, usually system logs but can also include other types of data as well.

## Blank 

In the 
