---
title: "开机自启脚本编写(Ubuntu 16.04.6)"
date: 2020-04-06 11:57
tag: init.d,运维
---
[TOC]

## 参考资料

+ [Debian 6，使用 insserv 代替 update-rc.d_运维_Sky_qing的专栏-CSDN博客](https://blog.csdn.net/Sky_qing/article/details/8941176)

+ [LSBInitScripts - Debian Wiki](https://wiki.debian.org/LSBInitScripts)

+ [openSUSE:Packaging init scripts](https://zh.opensuse.org/index.php?title=openSUSE:Packaging_init_scripts&variant=zh)
## 简要说明

Add a block like this in the init.d script:

``` bash
### BEGIN INIT INFO
# Provides:          scriptname
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start daemon at boot time
# Description:       Enable service provided by daemon.
### END INIT INFO
```

The block shown above has a special rigid format delimited by the lines

``` bash
### BEGIN INIT INFO
### END INIT INFO
```

all trailing spaces shall be ignored. On the other hand, all lines inside the block shall be of the form

``` bash
# {keyword}: arg1 [arg2...]
```

and begin with a hash character '#' in the first column followed by one single space, except for the lines following the Description keyword. The following keywords are defined

+ **Provides: boot_facility_1 [boot_facility_2...]**

>defines boot facilities provided by this init script such that when the script is run with the start argument, the specified boot facilities will be deemed present and hence other init scripts which require those boot facilities must be started at a later stage. Normally you should use the script name as boot facility (without .sh if the file name has such an ending) but one can in the exceptional case also use the name of the service(s) that the script replaces. Boot facilities provided by scripts must not start with '$'. (Virtual facility names listed below are defined outside the init.d scripts.) Facility names should be unique within the distribution, to avoid 'duplicate provides' errors when a package is installed.

+ **Required-Start: boot_facility_1 [boot_facility_2...]**

>defines facilities that must be available to start the script. Consider using virtual facility names as described below if adequate. If no boot facility is specified it means that this script can be started just after the bootstrap without local filesystems mounted, nor system logger, etc.

+ **Required-Stop: boot_facility_1 [boot_facility_2...]**

>defines facilities used by the service provided by the script. The facility provided by this script should stop before the listed facilities are stopped to avoid conflicts. Normally you would include here the same facilities as for the Required-Start keyword.

+ **Should-Start: boot_facility_1 [boot_facility_2...]**

>defines the facilities that if present should start before the service provided by the script. Nevertheless, the script can still start if the listed facilities are missing. This allows for weak dependencies which do not cause the service to fail if a facility is not available. Consider using virtual facility names as described below if adequate.

+ **Should-Stop: boot_facility_1 [boot_facility_2...]**

>defines the facilities that if present should be stopped after this service. Normally you would include here the same facilities as those used with the Should-Start keyword.

+ **Default-Start: run_level_1 [run_level_2...]**
+ **Default-Stop: run_level_1 [run_level_2...]**

>defines the run levels where the script should be started (stopped) by default. For example, if a service should run in runlevels 3, 4, and 5 only, specify "Default-Start: 3 4 5" and "Default-Stop: 0 1 2 6".

+ **Short-Description: short_description**

>provide a brief description of the actions of the init script. Limited to a single line of text.

+ **Description: multiline_description**

>provide a more complete description of the actions of the init script. May span multiple lines. In a multiline description, each continuation line shall begin with a '#' followed by tab character or a '#' followed by at least two space characters. The multiline description is terminated by the first line that does not match this criteria.

+ **X-Start-Before: boot_facility_1 [boot_facility_2...]**
+ **X-Stop-After: boot_facility_1 [boot_facility_2...]**

>provide reverse dependencies, that appear as if the listed facilities had should-start and should-stop on the package with these headers.

+ **X-Interactive: true**

>Indicates that this init script can interact with the user, requesting some input (for example, a password). This make sure the script run alone when the boot system starts scripts in parallell and have direct access to the tty.

For dependency tracking, the provides, required- and should- keywords are important, and the rest is unused. The default runlevels are used by a program to order the init scripts (e.g. insserv) to keep track of which rc#.d directory to update when a service is added for the first time, and should reflect the intent of the service.

There are some "virtual" facility names, listed in the [LSB 3.1]. These are:

" "|" "|
-|-|
$local_fs|all local filesystems are mounted. All scripts that write in /var/ need to depend on this, unless they already depend on $remote_fs.
$network|low level networking (ethernet card; may imply PCMCIA running)
$named|daemons which may provide hostname resolution (if present) are running. For example, daemons to query DNS, NIS+, or LDAP.
$portmap|daemons providing ?SunRPC/ONCRPC portmapping service as defined in RFC 1833 (if present) are running all remote
$remote_fs|all filesystems are mounted. In some LSB run-time environments, filesystems such as /usr may be remote. If the script need a mounted /usr/, it needs to depend on $remote_fs. Scripts depending on $remote_fs do not need to depend on $local_fs. During shutdown, scripts that need to run before sendsigs kills all processes should depend on $remote_fs.
$syslog|system logger is operational
$time|the system time has been set, for example by using a network-based time program such as ntp or rdate, or via the hardware Real Time Clock. Note that just depending on ntp will not result in an accurate time just after ntp started. It usually takes minutes until ntp actually adjusts the time. Also note that standard insserv.conf just lists hwclock as $time.
$all|facility supported by insserv to start a script after all the scripts not depending on $all, at the end of the boot sequence. This only work for start ordering, not stop ordering. Depending on a script depending on $all will give incorrect ordering, as the script depending on $all will be started after the script depending on it.