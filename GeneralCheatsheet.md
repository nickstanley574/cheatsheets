# GENERAL CHEATSHEET

## GIT

One line git log

`git log --pretty=oneline`

## Nagios Core

 Nagios Core, is a free and open source computer-software application that monitors systems, networks and infrastructure. Nagios offers monitoring and alerting services for servers, switches, applications and services ([wikipedia.com](https://en.wikipedia.org/wiki/Nagios)).

Verify Nagios Configurations: `nagios -v /<pathtofile>/nagios.cfg`

Nagios Exit Codes:
* 0: OK
* 1: WARNING
* 2: CRITICAL
* 3: UNKNOWN


## PASS

https://www.passwordstore.org/
https://git.zx2c4.com/password-store/about/

## GPG

GPG, or GNU Privacy Guard, is a public key cryptography implementation. This allows for the secure transmission of information between parties and can be used to verify that the origin of a message is genuine ([digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages)).

## GlusterFS

Gluster is a free and open source software scalable network filesystem. ([gluster.org](https://www.gluster.org/))

GlusterFS is a distributed file system defined to be used in user space, i.e. File System in User Space (FUSE). It is a software based file system which accounts to its own flexibility feature ([tecmint.com](https://www.tecmint.com/introduction-to-glusterfs-file-system-and-installation-on-rhelcentos-and-fedora/)).

http://docs.gluster.org/en/latest/Quick-Start-Guide/Quickstart/

http://docs.gluster.org/en/latest/CLI-Reference/cli-main/

Check gluster georep status `$ gluster volume geo-replication status`

Add peer `$ gluster peer probe <host name>`

Remove peer `$ gluster peer detach <host name>`

List the status of all known peers  ` $ gluster peer status`

```
  998  pwd
 1003  lsof | grep mnt
 1006  service smb stop
 1007  lsof | grep mnt
 1008  umount /mnt/gluster
 1010  mount -t glusterfs localhost:content-storage /mnt/gluster
 1015  service smb status
 1016  service smb restart
 1017  service smb status
```

## Puppet

Puppet programs are called manifests. Manifests are composed of puppet code and their filenames use the `.pp` extension. The default main manifest in Puppet installed via apt is `/etc/puppet/manifests/site.pp` ([digitalocean.com](https://www.digitalocean.com/community/tutorials/getting-started-with-puppet-code-manifests-and-modules)).

`init.pp` is the 'main' class for a module. `site.pp` is where you define site specific configuration/properties ([ask.puppet.com](https://ask.puppet.com/question/29853/difference-between-initpp-and-sitepp-and-does-each-override-other-in-case-of-same-setting-mentioned-in-the-two-files/)).

**Dependencies to install puppet**

**Query PuppetDB**

curl
```
curl -G 'http://172.0.0.1:8080/v3/nodes' --data-urlencode 'query=["=", ["fact", "<fact_key>"], "< fact_value >"]'
curl -G 'http://172.0.0.1:8080/v3/facts' --data-urlencode 'query=["=","certname","< certname >"]'
```
python
```
payload = {'query': '["=", ["fact", "fact_key"], "fact_value"]'}
response = requests.get('http://172.0.0.1:8080/v3/nodes', params=payload)
data = response.json()
response_dic = data[0]
print response_dic['name']
```
Exported Resources Query
* All Exported Resources Globally: `["=", "exported", true]`
* Exported Resources by Node:  `[ "and",["=", "exported", true],["=", "certname", "<certname>"]]`

## LINUX

Linux is a name that broadly denotes a family of free and open-source software operating systems built around the Linux kernel. Typically, Linux is packaged in a form known as a Linux distribution for both desktop and server use ([wikipedia.org](https://en.wikipedia.org/wiki/Linux)).

Unix trademarked as UNIX) is a family of multitasking, multiuser computer operating systems that derive from the original AT&T Unix, development starting in the 1970s at the Bell Labs research center by Ken Thompson, Dennis Ritchie, and others ([wikipedia.org](https://en.wikipedia.org/wiki/Unix)).

Linux is a Unix clone written from scratch by Linus Torvalds with assistance from a loosely-knit team of hackers across the Net. It aims towards POSIX compliance ([cyberciti.biz](https://www.cyberciti.biz/faq/what-is-the-difference-between-linux-and-unix/)).

### Mounting

In order to access a filesystem in Linux you first need to mount it. Mounting a filesystem simply means making the particular filesystem accessible at a certain point in the Linux directory tree ([leepingcomputer.com](https://www.bleepingcomputer.com/tutorials/introduction-to-mounting-filesystems-in-linux/)).

#### `mount` & `umount` Commands

The `mount` command serves to attach the filesystem found on some device to the big file tree. Conversely, the `umount` command will detach it again ([linux.die.net](https://linux.die.net/man/8/mount)).

Mount command format: `$ mount -t <type> <device> <dir>`


#### Mount Config Files
* `/etc/fstab` is a system configuration file on Linux and other Unix-like operating systems that contains information about major filesystems on the system ([linfo.org](http://www.linfo.org/etc_fstab.html)).
* `/etc/mtab` This file lists all currently mounted filesystems along with their initialization options ([linuxquestions.org](https://www.linuxquestions.org/questions/linux-newbie-8/difference-between-mtab-and-fstab-924190/)).
* `/proc/mounts` The kernel provides the info in /proc/mounts in file form, but `/proc/mounts` does not exist as a file on any hard disk. Looking at `/proc/mounts` is looking at information that comes directly from the kernel ([linux-training.be](http://linux-training.be/sysadmin/ch07.html)).


### GREP (Global Regular Expression Print)
a command-line utility for searching plain-text data sets for lines that match a regular expression.

The grep utilities are a family of Unix tools, including grep, egrep, and fgrep, that perform repetitive searching tasks. The tools in the grep family are very similar, and all are used for searching the contents of files for information that matches particular criteria ([kb.ui](https://kb.iu.edu/d/afiy)).

### Piping and Redirection

A *pipe* is a form of redirection that is used in Linux and other Unix-like operating systems to send the output of one program to another program for further processing ([linfo.org](http://www.linfo.org/pipes.html)).

Piping and redirection is the means by which we may connect the output streams (STDIN (0), STDOUT (1), STDERR (2)) between programs and files to direct data in interesting and useful ways.

https://ryanstutorials.net/linuxtutorial/piping.php

### pam_limits

pam_limits sets parameters on system resources on a per-user (or per-group) basis. Using these tools, you can limit everything, from the maximum number of files a user can have open to the amount of CPU time ([serverwatch.com](https://www.serverwatch.com/server-tutorials/set-user-limits-with-pamlimits-and-limits.conf.html)).  

The pam_limits.so module applies ulimit limits, nice priority and number of simultaneous login sessions limit to user login sessions. This description of the configuration file syntax applies to the /etc/security/limits.conf file and \*.conf files in the /etc/security/limits.d directory .  The syntax of the lines is as follows: `<domain> <type> <item> <value>` ([linux-pam.org](http://www.linux-pam.org/Linux-PAM-html/sag-pam_limits.html)).

### ssh

SSH, also known as Secure Socket Shell, is a network protocol that provides administrators with a secure way to access a remote computer. SSH also refers to the suite of utilities that implement the protocol. Secure Shell provides strong authentication and secure encrypted data communications between two computers connecting over an insecure network such as the Internet ([searchsecurity.techtarget.com](http://searchsecurity.techtarget.com/definition/Secure-Shell)).

The ssh program on a host receives its configuration from either the command line or from configuration files `~/.ssh/config` and `/etc/ssh/ssh_config`. Command-line options take precedence over configuration files. The user-specific configuration file `~/.ssh/config` is used next. Finally, the global `/etc/ssh/ssh_config` file is used. The first obtained value for each configuration parameter will be used ([ssh.com](https://www.ssh.com/ssh/config/)).

### Screen

The screen program allows you to use multiple windows in Unix. In other words the screen command lets you detach from a terminal session and then attach it back at a later time. To be able to do that you should be in a screen session ([dasunhegoda.com](http://dasunhegoda.com/unix-screen-command/263/)).

**Command Line**
* Start screen with desired name: `$ screen -S <name>`
* List all active screens with number: 	`$ screen -ls`
* Re-attach to screen with number		`$ screen -r <number>`
* `screen -D -r <1234.somescreensession>`

**Keyboard**
* De-attach from current screen: crtl + a + d (`C-a d`).
* switch to next screen: crtl + a + n (`C-a n`)
* switch to pervious screen: crtl + a + p (`C-a p`)

### Logical Volume Management (LVM)
```
$ lvcreate -L <size> -n <lvm_name>  <physical>
$ lvcreate -L 30G    -n webserver01 guests
$ lvremove <lv_name>
$ lvextend -L+15G /dev/main/var
$ resize2fs dev/main/var
```

### Volume Management

Display information about volume groups  - `$ vgs`

Display information about logical volumes - `$ lvs`

Display information about physical volumes - `$ pvs`

### I/O

#### iostat

The iostat command stands for input-output statistics. This command is used to generate input-output statistics for device, partitions the network file system, generate the report for Central Processing Unit (CPU) ([linuxnix.com](https://www.linuxnix.com/15-iostat-command-examples-linux-unix/)).

```
$ iostat
Linux 2.6.32-696.16.1.el6.x86_64 (hostname) 	04/06/2012 	_x86_64_	(24 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.96    0.00    1.16    0.72    0.00   97.16

Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
sda               5.36       205.06        35.12 2248309862  385101408
sdb             899.66    178116.09     59256.16 1952900850816 649696533097
dm-0              0.73         3.19         2.64   35011424   28990848
dm-1              3.96        71.16        15.42  780257642  169121400
dm-2            900.30    178115.56     59256.08 1952895029287 649695667813
dm-3              0.04         0.36         0.00    3904648          0
dm-4              0.18         0.17         0.08    1813169     865284
dm-5              3.55       126.55        16.08 1387531186  176261216
dm-6              0.05         0.17         0.26    1817898    2841736
dm-7              0.09         3.65         0.46   40052570    5035960
```

**CPU Utilization Report**

* `%user` - Show the % of CPU utilization that occurred while executing at the user (appz) level
* `%nice` - Show the % of CPU utilization that occurred while executing at the user level with *nice* priority.
* `%system` - Show the % of CPU utilization that occurred while executing at the system (kernel) level.
* `%iowait` - Show the & of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request.
* `%steal` - Show the percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor.
* `%idle` - Show the percentage of time that the CPU or CPUs were idle and the system did not have an outstanding disk I/O request.

**Device Utilization Report**
* `Device` - This column gives the device (or partition) name as listed in the /dev directory.
* `tps` - Indicate the number of transfers per second that were issued to the device. A transfer is an I/O request to the device. Multiple logical requests can be combined into a single I/O request to the device. A transfer is of indeterminate size.
* `Blk_read/s` - Indicate the amount of data read from the device expressed in a number of blocks (kilobytes, megabytes) per second. Blocks are equivalent to sectors and therefore have a size of 512 bytes.
* `Blk_wrtn/s` - Indicate the amount of data written to the device expressed in a number of blocks (kilobytes, megabytes) per second.
* `Blk_read` - The total number of blocks (kilobytes, megabytes) read.
* `Blk_wrtn` - The total number of blocks (kilobytes, megabytes) written.

#### File: `/proc/diskstats`

```
   8       0 sda 37026218 8578109 2248313534 95521346 21738347 29070869 385130784 15724422 0 70112880 111213210
```
* Field 1   -- # of reads issued
* Field 2   -- # of reads merged
* Field 3   -- # of sectors read
* Field 4   -- # of milliseconds spent reading
* Field 5   -- # of writes completed
* Field 6   -- # of writes merged
* Field 7   -- # of sectors written
* Field 8   -- # of milliseconds spent writing
* Field 9   -- # of I/Os currently in progress
* Field 10  -- # of milliseconds spent doing I/Os
* Field 11  -- weighted # of milliseconds spent doing I/Os

https://www.mjmwired.net/kernel/Documentation/iostats.txt


### free

The free command provides information about unused and used memory and swap space on any computer running Linux or another Unix-like operating system ([linfo.org](http://www.linfo.org/free.html)).

```
$ free -m
              total        used        free      shared  buff/cache   available
Mem:          15886        7183        1938          16        6764        8302
Swap:             0           0           0
```

total -
used -
free
shared -
buff/cahce -
available

Swap:

Swap space in Linux is used when the amount of physical memory (RAM) is full. If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. While swap space can help machines with a small amount of RAM, it should not be considered a replacement for more RAM. Swap space is located on hard drives, which have a slower access time than physical memory.

Swap space can be a dedicated swap partition (recommended), a swap file, or a combination of swap partitions and swap files.

### ps (process status)

It provides a snapshot of the current processes along with detailed information like user id, cpu usage, memory usage, command name etc. ([linux.com](https://www.linux.com/blog/10-basic-examples-linux-ps-command))

Useful Commands:
* Show cpu & mem usage of a pid: `$ ps -p 3845 -o %cpu,%mem,cmd` or ``$ ps -p "`pidof <process_name>`" -o %cpu,%mem,cmd``

### Secure Copy (SCP)
* Download full directory: `$ scp -r user@<remotehost>:<from: directory> <to: directory>`
* Download one file: `$ scp user@<remotehost>:<from: directory/file> <to: directory>`
* Upload Directory: `$ scp -r <from: directory> user@<remotehost>:<to: directory>`
* Upload file: `scp <from: directory/file> user@<ipaddress>:<to: directory>`

### htop

 This is htop, an interactive process viewer for Unix systems. It is a text-mode application (for console or X terminals) and requires ncurses ([hisham.hm](https://hisham.hm/htop/)).  

 The option -u can be used to display processes of a given user: `# htop -u <user>`
 Through -s option provided by htop, you can sort any column of the process information in the htop window: `# htop -s PID`

 htop -s PID

### RPM (Red-hat Package Manager)

A program for installing, uninstalling, and managing software packages in Linux. RPM files provide an easy way for software to be distributed, installed, upgraded, and removed since the files are "packaged" in one place ([lifewire.com](https://www.lifewire.com/rpm-file-2622217))

a “package” refers to a compressed file archive containing all of the files that come with a particular application ([internetblog.org.uk](https://www.internetblog.org.uk/post/1520/what-is-a-linux-package/)).  

```
Usage: rpm [OPTION...]
  -a, --all                        query/verify all packages
  -f, --file                       query/verify package(s) owning file
  -l, --list                       list files in package
  -v, --verbose                    provide more detailed output
  -h, --hash                       print hash marks as package installs (good with -v)
  -r, --requires                   list capabilities required by package(s)
  -p, --provides                   list capabilities that this package provides
```

* Check an Installed RPM Package . . . . . . . . . . . `# rpm -q <package>`
* List all files of an installed RPM package . . . . . `# rpm -ql <package>`
* Upgrade a RPM Package with status . . . . . . . . `# rpm -Uvh <package>`
* List All Installed RPM Packages . . . . . . . . . . . .  `# rpm -qa`
* List Recently Installed RPM Packages . . . . . . . `# rpm -qa --last`
* Removing a Package Syntax . . . . . . . . . . . . . . .`# rpm -e <package>`
* Check what RPM Package a file is belongs to . `# rpm -qf </path/to/file>`
* Information of Installed RPM Package . . . . . . .  `# rpm -qi <package>`
* Import an RPM GPG key . . . . . . . . . . . . . . . . . . `# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6`
* Show scripts related to a RPM package . . . . . .`# rpm -q --scripts <package>`
* Show all config files for a RPM package . . . . . .`# rpm -qc  <package>` or `rpm -q --configfiles <package>`

### File Permission
```
F = File 
R = Read Permission
W = Write Permission 
X = Execute Permission

    4 2 1   4 2 1   4 2 1
-   - - -   - - -   - - -
F   R W X   R W X   R W X
    owner   group   other

rwx = 7   = 111 in binary
rw- = 6   = 110 in binary
r-x = 5   = 101 in binary
r—- = 4   = 100 in binary

rwx rwx rwx = 111 111 111 = 7 7 7
rw- rw- rw- = 110 110 110 = 6 6 6
rwx --- --- = 111 000 000 = 7 0 0
```
**Common Permissions**
* `777` (`rwx rwx rwx`) No restrictions
* `755` (`rwx r-x r-x`) Owner has full rights all other and read and execute
* `700` (`rwx --- ---`) Owner is the only user that have any rights
* `666` (`rw- rw- rw-`) Read and Write to all users

**Permissions Commands**
* Modify file access rights: `$ chmod`
* Change file ownership: `$ chown`
* Change a file's group ownership: `$ chgrp`
* `$ chown nstanley:infa backlog/ -R `
* `$ chmod 0775 backlog/ -R`

### Filesystem

 A filesystem is a hierarchy of directories (also referred to as a directory tree) that is used to organize files on a computer or storage media. On computers running Linux or other Unix-like operating systems, the directories start with the root directory, which is the directory that contains all other directories and files on the system and which is designated by a forward slash ( / ). The currently accessible filesystem is the filesystem that can be accessed on a computer at a given time ([tutorialspoint.com](https://www.tutorialspoint.com/unix/unix-file-system.html)).

 **Directory & Description** - [tutorialspoint.com](https://www.tutorialspoint.com/unix/unix-file-system.html)

* `/` - This is the root directory which should contain only the directories needed at the top level of the file structure
* `/bin` - This is where the executable files are located. These files are available to all users
* `/dev` - These are device drivers
* `/etc` - Supervisor directory commands, configuration files, disk configuration files, valid user lists, groups, ethernet, hosts, where to send critical messages
* `/lib` - Contains shared library files and sometimes other kernel-related files
* `/boot` - Contains files for booting the system
* `/home` - Contains the home directory for users and other accounts
* `/mnt`  - Used to mount other file systems.
* `/proc` - Contains all processes marked as a file by process number or other information that is dynamic to the system
* `/tmp`  - Holds temporary files used between system boots
* `/usr`  - Used for miscellaneous purposes, and can be used by many users. Includes administrative commands, shared files, library files, and others
* `/var`  - Typically contains variable-length files such as log and print files and any other type of file that may contain a variable amount of data
* `/sbin` - Contains binary (executable) files, usually for system administration.
* `/kernel` - Contains kernel files


"On a UNIX system, everything is a file; if something is not a file, it is a process."

### ls

The ls command is used to list the names of the files and folders within the file system ([lifewire.com](https://www.lifewire.com/uses-of-linux-ls-command-4054227)).

* formats the output of a directory: `ls --format=comma`,`ls --format=vertical`
* Sort output: `ls --sort=extension`, `ls --sort=time`

### netstat

netstat ("network statistics") is a command-line tool that displays network connections (both incoming and outgoing), routing tables, and a number of network interface (network interface controller or software-defined network interface) and network protocol statistics ([computerhope.com](https://www.computerhope.com/unix/unetstat.htm))

list out all the network (socket) connections on a system: `$ netstat -anp | grep LIST`
List all tcp ports: `$ netstat -at`
List all udp ports: `$ netstat -au`
List only listening ports: `$ netstat -l`
List only listening TCP Ports: `$ netstat -lt`
List only listening UDP Ports: `$ netstat -lu`
Show statistics for all ports: `$ netstat -s`
Display PID and program names in output:  `$ netstat -p`
Print netstat information continuously: `$ netstat -c`
Show the list of network interfaces: `$ netstat -i`

LISTENING means that a service is listening for connections on that port. Once a connection is established it will be ESTABLISHED, and you'll have a matching foreign address on the line. Other states you might see during the setup and shutdown stages include SYN_SENT and TIME_WAIT. All that only applies to TCP; because UDP is connectionless there's no state to list ()[tomshardware.com](http://www.tomshardware.com/answers/id-2821740/netstat-listening-means.html)).

(https://www.thegeekstuff.com/2010/03/netstat-command-examples/)

### iptables

Iptables is a command-line firewall utility that uses policy chains to allow or block traffic. When a connection tries to establish itself on your system, iptables looks for a rule in its list to match it to. If it doesn’t find one, it resorts to the default action. ([howtogeek.com](https://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/))

Iptables is used to set up, maintain, and inspect the tables of IP packet filter rules in the Linux kernel. Several different tables may be defined. Each table contains a number of built-in chains and may also contain user-defined chains. Each chain is a list of rules which can match a set of packets. Each rule specifies what to do with a packet that matches. This is called a 'target', which may be a jump to a user-defined chain in the same table ([linux.die.net](https://linux.die.net/man/8/iptables)).

Per iptables manual, there are currently 3 types of tables:

* FILTER – this is the default table, which contains the built in chains for:
  * INPUT  – packages destined for local sockets
  * FORWARD – packets routed through the system
  * OUTPUT – packets generated locally
* NAT – a table that is consulted when a packet tries to create a new connection. It has the following built-in:
  * PREROUTING – used for altering a packet as soon as it’s received
OUTPUT – used for altering locally generated packets
POSTROUTING – used for altering packets as they are about to go out
MANGLE – this table is used for packet altering. Until kernel version 2.4 this table had only two chains, but they are now 5:
PREROUTING – for altering incoming connections
OUTPUT – for altering locally generated  packets
INPUT – for incoming packets
POSTROUTING – for altering packets as they are about to go out
FORWARD – for packets routed through the box

(https://www.tecmint.com/linux-iptables-firewall-rules-examples-commands/)


### EPEL

The EPEL repository is an additional package repository that provides easy access to install packages for commonly used software. This repo was created because Fedora contributors wanted to use Fedora packages they maintain on RHEL and other compatible distributions. The EPEL repository can be used with the following Linux Distributions: Red Hat Enterprise Linux (RHEL), CentOS, Scientific Linux, and Oracle Linux. ([liquidweb.com](https://www.liquidweb.com/kb/enable-epel-repository/)).

```
yum install epel-release
```

### SElinux
Security-Enhanced Linux (SELinux) is a mandatory access control (MAC) security mechanism implemented in the kernel ([wiki.centos.org](https://wiki.centos.org/HowTos/SELinux)).

Modes:
* Enforcing: The default mode which will enable and enforce the SELinux security policy on the system, denying access and logging actions
* Permissive: In Permissive mode, SELinux is enabled but will not enforce the security policy, only warn and log actions. Permissive mode is useful for troubleshooting SELinux issues
* Disabled: SELinux is turned off

Commands:
* To see the current status of SELinux: `# getenforce`
* detailed SELinux related information: `# sestatus`
* Display current state of booleans: `# sestatus -b` or `# getsebool -a`
* For a list of Booleans, an explanation of what each one is, and whether they are on or off: `# semanage boolean -l`

Reference:
*  ["Working with Selinux Booleans" - access.redhat.com ](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security-enhanced_linux/sect-security-enhanced_linux-working_with_selinux-booleans)

**audit2allow** - Automatically create rules to allow actions based on deny logs from SELinux.

```
cat /var/log/audit/audit.log | audit2allow
cat /var/log/audit/audit.log | grep apache | audit2allow
```
**audit2why** - Get more detailed output (human readable) from the SELinux log.
```
cat /var/log/audit/audit.log | audit2why
```

```
1002  semanage --help
1003  semanage --list
1004  ls -lZ `which pd-send`
1008  rpm -qf `which pd-send`
1009  rpm -ql pdagent
1011  rpm -qf `which pd-send`
1012  getsebool -a
1013  getsebool -a | grep nagios
1014  getsebool -a | grep fuse

```

### `top`

`top` is a task manager program found in many Unix-like operating systems. It produces an ordered list of running processes selected by user-specified criteria, and updates it periodically ([wikipedia.org](https://en.wikipedia.org/wiki/Top)).

```
$ top
top - 15:26:45 up  3:02,  9 users,  load average: 3.55, 3.20, 3.18
Tasks: 232 total,   1 running, 231 sleeping,   0 stopped,   0 zombie
Cpu(s): 60.7%us,  0.7%sy,  0.0%ni, 38.2%id,  0.0%wa,  0.0%hi,  0.2%si,  0.2%st
Mem:  16331748k total,  7031884k used,  9299864k free,   163452k buffers
Swap:  2031612k total,        0k used,  2031612k free,   655676k cached
```
* Line 1 - The time, How long the computer has been running, Number of users, Load average
* The load average shows the system load time for the last 1, 5 and 15 minutes.
* Line 2 - Total number of tasks, Number of running tasks, Number of sleeping tasks, Number of stopped tasks, Number of zombie tasks

### logrotate

“Log rotation” refers to the practice of archiving an application’s current log, starting a fresh log, and deleting older logs. The system usually runs logrotate once a day, and when it runs it checks rules that can be customized on a per-directory or per-log basis ([support.rackspace.com](https://support.rackspace.com/how-to/understanding-logrotate-utility/)).

By default logrotate is invoked once a day using a cron scheduler from location `/etc/cron.daily/`

Logrotate's configuration is done by editing two separate configuration files: `/etc/logrotate.conf` and for service specific configuration files stored in `/etc/logrotate.d/`.

```
/var/log/apache2/* {  # the directives inside the block apply to all logs inside /var/log/apache2
weekly                # means that the tool will attempt to rotate the logs on a weekly basis.
rotate 3              # only 3 rotated logs should be kept. Thus, the oldest file will be removed on the fourth subsequent run.
size 10M              # he minimum size for the rotation to take place to 10M.
compress              # compress and delaycompress are used to tell that all rotated logs,
delaycompress         # with the exception of the most recent one, should be compressed.
}
```
https://www.tecmint.com/install-logrotate-to-manage-log-rotation-in-linux/

```
/var/log/apache2/*.log {
        weekly
        missingok
        rotate 52
        compress
        delaycompress
        notifempty
        create 640 root adm
        sharedscripts
        postrotate
            /etc/init.d/apache2 reload > /dev/null
        endscript
        prerotate
            if [ -d /etc/logrotate.d/httpd-prerotate ]; then \
                    run-parts /etc/logrotate.d/httpd-prerotate; \
            fi; \
        endscript
}
```

Let's go through the options - [serversforhackers.com](https://serversforhackers.com/c/managing-logs-with-logrotate):

  * `weekly` - Rotate logs once per week. Available options are daily, weekly, monthly, and yearly.
  * `missingok` - If no \*.log files are found, don't freak out
  * `rotate 52` - Keep 52 files before deleting old log files (Thats a default of 52 weeks, or one years worth of logs!)
  *  `compress` - Compress (gzip) log files
      * `delaycompress` - Delays compression until 2nd time around rotating. As a result, you'll have one current log, one older log which remains uncompressed, and then a series of compressed logs. More info on its specifics.
      * `compresscmd` - Set which command to used to compress. Defaults to gzip.
      *  `uncompresscmd` - Set the command to use to uncompress. Defaults to gunzip.
  * `notifempty` - Don't rotate empty files
  * `create 640 root adm` -  Create new log files with set `permissions/owner/group`, This example creates file with user root and group adm.
  * `sharedscripts` - Run postrotate script after all logs are rotated. If this is not set, it will run postrotate after each matching file is rotated.
  * `postrotate` - Scripts to run after rotating is done. In this case, Apache is reloaded so it writes to the newly created log files. Reloading Apache (gracefully) lets any current connection finish before reloading and setting the new log file to be written to.
  * `prerotate` - Run before log rotating begins

### cURL

curl is a tool to transfer data from or to a server, using one of the supported protocols (HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, DICT, TELNET, LDAP or FILE). The command is designed to work without user interaction. It offers proxy support, user authentication, FTP uploading, HTTP posting, SSL connections, cookies, file transfer resume, Metalink, and many other features, listed below. ([computerhope.com](https://www.computerhope.com/unix/curl.htm))

### wget

GNU Wget is a free utility for non-interactive download of files from the Web. It supports HTTP, HTTPS, and FTP protocols, as well as retrieval through HTTP proxies ([gnu.org](https://www.gnu.org/software/wget/manual/wget.html)).

* D/L a single file: `# wget http://example.com/file.iso`
* D/L a file but save it locally under a different name: `# wget ‐‐output-document=filename.html example.com`
* D/L a list of sequentially numbered files from a server: `# wget http://example.com/images/{1..20}.jpg`
* Store number of URL’s in text file and download them: `# wget -i /wget/tmp.txt`
* Resume uncompleted D/L: `# wget -c http://example.com/file.iso`
* D/L files in background: `# wget -b /wget/log.txt http://example.com/file.iso`
* Restrict download speed limits: `# wget -c --limit-rate=100k http://example.com/file.iso`
* Redirect wget Logs to a log File: `# wget -o download.log http://example.com/file.iso`

### ausearch

ausearch - a tool to query audit daemon logs; a tool that can query the audit daemon logs based for events based on different search criteria.
([linux.die.net](https://linux.die.net/man/8/ausearch))

 ```
 Options:
 -f, --file file-name
       Search for an event based on the given filename.

 -m, --message message-type | comma-sep-message-type-list
       Search for an event matching the given message type. You may also enter a comma separated list of message types.

 -te, --end [end-date] [end-time]
       Search for events with time stamps equal to or before the given end time. The format of end time depends on your locale. If the date is omitted, today is assumed. If the time is omitted, now is assumed.

       You may also use the word: now, recent, today, yesterday, this-week, week-ago, this-month, this-year. Today means starting now. Recent is 10 minutes ago. Yesterday is 1 second after midnight the previous day. This-week means starting 1 second after midnight on day 0 of the week determined by your locale (see localtime). This-month means 1 second after midnight on day 1 of the month. This-year means the 1 second after midnight on the first day of the first month.

 -ts, --start [start-date] [start-time]
       Search for events with time stamps equal to or after the given end time. The format of end time depends on your locale. If the date is omitted, today is assumed. If the time is omitted, midnight is assumed.

       You may also use the word: now, recent, today, yesterday, this-week, this-month, this-year. Today means starting at 1 second after midnight. Recent is 10 minutes ago. Yesterday is 1 second after midnight the previous day. This-week means starting 1 second after midnight on day 0 of the week determined by your locale (see localtime). This-month means 1 second after midnight on day 1 of the month. This-year means the 1 second after midnight on the first day of the first month.
 ```

### Name Spaces

temp temp temp

### Fail2Ban

Fail2ban attempts to alleviate these issues by providing an automated way of not only identifying possible break-in attempts, but acting upon them quickly and easily in a user-definable manner. Log files contain interesting information, especially about failed logins. This information can be used to ban an offensive host. This is exactly what Fail2ban does. It scans log files and detects patterns which correspond to possible breakin attempts and then performs actions. Most of the time, it consists of adding a new rule in a firewall chain and sending an e-mail notification to the system administrator ([fail2ban.org](https://www.fail2ban.org/wiki/index.php/MANUAL_0_8)).


**Commands**
* unban a ip: `fail2ban-client set <jail> unbanip <ipaddress>`

**References**
* ["How Fail2Ban Works to Protect Services on a Linux Server" - digitalocean.com  ](https://www.digitalocean.com/community/tutorials/how-fail2ban-works-to-protect-services-on-a-linux-server)
* [How To Protect SSH with Fail2Ban on Ubuntu 14.04 - digitalocean.com ](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)

### VIM (Vi IMproved)

**Block Comment Out**

1) Enter VISUAL BLOCK mode: `CTRL + V` (`C-v`)
2) Move the cursor down: `j`
3) Enter INSERT mode: `Shift + I` (`S-i`)
4) Enter comment character: `#`,`//`, etc ..
5) Exit INSERT mode: `esc`

**Decomment**
1)  Enter VISUAL BLOCK mode: `CTRL + V` (`C-v`)
2) Remove comment char: `x`

https://unix.stackexchange.com/questions/120615/how-to-comment-multiple-lines-at-once#120617
https://vi.stackexchange.com/questions/598/faster-way-to-move-a-block-of-text

**Basic search and replace**

* Find each occurrence of 'foo' (in all lines), and replace it with 'bar: `:%s/foo/bar/g`
* Find each occurrence of 'foo' (in the current line only), and replace it with 'bar' `:s/foo/bar/g`
* Change each 'foo' to 'bar', but ask for confirmation first: `:%s/foo/bar/gc`
* Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation. `:%s/\<foo\>/bar/gc`

**Switch between open Windows**

* Control+W (`C-w`) followed by `w` to toggle between open windows and,
* Control+W  (`C-w`) followed by `h`/`j`/`k`/`l` to move to the **left**/**bottom**/**top**/**right** window accordingly.

### `history` & `fc` commands

The `fc` command line utility for listing, editing and re-executing commands previously entered into an interactive shell. The `fc` command is a shell builtin meaning the command comes from the shell rather than the operating system ([shapeshed.com](https://shapeshed.com/unix-fc/)).

**Edit and re-executing the last command:**
```
$ echo "Hello World 000"
Hello World 000
$ fc
...file edited ...
echo "Hello World 111"
Hello World 111
```
**How to edit and re-execute a previous command:**
```
$ fc -l
1011	 du -ah | sort -n -r | head -n 5
1012	 du -a | sort -n -r | head -n 5
1013	 du -hs * | sort -rh | head -5
1014	 du -Sh | sort -rh | head -5
1015	 du -Sh | sort -rh | head -10
1016	 find -type f -exec du -Sh {} + | sort -rh | head -n 5
1017	 du -a /home | sort -n -r | head -n 5
1018	 man fc
1019	 echo "hello 1"
1020	 echo "hello 2"
1021	 man fc
1022	 echo "hello 1"
1023	 clear
1024	 echo "Hello World 000"
1025	 echo "Hello World 111"
1026	 ll
$ fc 1014
...file edited ...
du -Sh | sort -rh | head -10
...
...
...
```

### du (_disk usage_)
Reports the sizes of directory trees inclusive of all of their contents and the sizes of individual files. This makes it useful for tracking down space hogs, i.e., directories and files that consume large or excessive amounts of space on a hard disk drive (HDD) or other storage media ([linfo.org](http://www.linfo.org/du.html)).

* Biggest directories in the current working directory: `# du -Sh | sort -rh | head -5`
* Display the largest files: `# find -type f -exec du -Sh {} + | sort -rh | head -n 5`
* Summary of a grand total disk usage size of an directory use : `du -sh /home`

References:
- [Find Top Large Directories and Files Sizes in Linux (tecmint.com)](https://www.tecmint.com/find-top-large-directories-and-files-sizes-in-linux/)

### Cron

Cron is the name of program that enables unix users to execute commands or
scripts (groups of commands) automatically at a specified time/date ([unixgeeks.org](http://www.unixgeeks.org/security/newbie/unix/cron-1.html)).s

Cron is a system daemon used to execute desired tasks (in the background) at designated times. A crontab file is a simple text file containing a list of commands meant to be run at specified times. It is edited using the crontab command. The commands in the crontab file (and their run times) are checked by the cron daemon, which executes them in the system background ([help.ubuntu.com](https://help.ubuntu.com/community/CronHowto)).

Crontab (CRON TABle) is a file which contains the schedule of cron entries to be run and at specified times. File location varies by operating systems:
* Mac OS X: `/usr/lib/cron/tabs/`
* BSD Unix: `/var/cron/tabs/`
* Solaris, HP-UX, Debian, Ubuntu: `/var/spool/cron/crontabs/`
* AIX, Red Hat Linux, CentOS, Ferdora: `/var/spool/cron/`
```
usage:	crontab [-u user] file
	crontab [-u user] [ -e | -l | -r ]
		(default operation is replace, per 1003.2)
	-e	(edit user's crontab)
	-l	(list user's crontab)
	-r	(delete user's crontab)
	-i	(prompt before deleting user's crontab)
	-s	(selinux context)
```
Cron Format:
```
<Minute> <Hour> <Day_of_the_Month> <Month_of_the_Year> <Day_of_the_Week> <Year>

* * * * * *
| | | | | |
| | | | | + -- Year              (range: 1900-3000)
| | | | + ---- Day of the Week   (range: 1-7, 1 standing for Monday)
| | | + ------ Month of the Year (range: 1-12)
| | + -------- Day of the Month  (range: 1-31)
| + ---------- Hour              (range: 0-23)
+ ------------ Minute            (range: 0-59)
```
**Helpful cron commands**

* List all cron jobs for all users: `$ for user in $(cut -f1 -d: /etc/passwd); do crontab -u $user -l; done`

[crontab.guru](crontab.guru) - "The quick and simple editor for cron schedule expressions."


### `time` Command
The time command runs the specified program command with the given arguments. When command finishes, time writes a message to standard output giving timing statistics about this program run. These statistics consist of The elapsed real time between invocation and termination (real). The user CPU time (user). The system CPU time (sys). ([computerhope.com](https://www.computerhope.com/unix/utime.htm))

```
time puppet agent -t
Info: Using configured environment 'dev'
Info: Retrieving pluginfacts
Info: Retrieving plugin
Info: Loading facts
...
Info: Applying configuration version '1525968162'
Notice: Applied catalog in 14.04 seconds

real	0m49.543s
user	0m25.478s
sys	0m3.355s
```

**Real, User and Sys process time statistics ([stackoverflow.com](https://stackoverflow.com/questions/556405/what-do-real-user-and-sys-mean-in-the-output-of-time1#556411
))**
* **Real** is wall clock time - time from start to finish of the call. This is all elapsed time including time slices used by other processes and time the process spends blocked (for example if it is waiting for I/O to complete).
* **User** is the amount of CPU time spent in user-mode code (outside the kernel) within the process. This is only actual CPU time used in executing the process. Other processes and time the process spends blocked do not count towards this figure.
* **Sys** is the amount of CPU time spent in the kernel within the process. This means executing CPU time spent in system calls within the kernel, as opposed to library code, which is still running in user-space. Like 'user', this is only CPU time used by the process. See below for a brief description of kernel mode (also known as 'supervisor' mode) and the system call mechanism.

## Networking Overview
*Default Gateway* - The device that passes traffic from the local subnet to devices on other subnets.

*Subnet Mask* - a number that defines a range of IP addresses that can be used in a network

*Netmask* -  a 32-bit mask used to divide an IP address into subnets and specify the network's available hosts.
The terms netmask and subnet mask are often used interchangeably. However, subnet masks are used primarily in network configurations, while netmasks typically refer to classes of IP addresses.

*Genmask* - The netmask for the destination net; 255.255.255.255 for a host destination and 0.0.0.0 for the default route.

*CIDR Notation* - CIDR notation is a compact representation of an IP address and its associated routing prefix. The notation is constructed from an IP address, a slash ('/') character, and a decimal number. The number is the count of leading 1 bits in the routing mask, traditionally called the network mask. The IP address is expressed according to the standards of IPv4 or IPv6.

A **Class A** netmask defines a range of IP addresses in which the first three digit section is the same, but the other sections may each contain any number between 0 and 255. **Class B** addresses have the same first two sections, but the numbers in the second two sections can be different. Class C addresses have the same first three sections and only the last section can have different numbers. Therefore, a **Class C** I.P. address range may contain up to 256 addresses.

IPv4
```
Class: _A_   _B_   _C_
       192 . 168 . 203 . 50
       network address   host address
```

Subnet Cheatsheet:

|   /   | Addresses | Hosts |     Netmask     |
| :---: |   :---:   | :---: |      :---:      |
|  /30  |     4     |   2   | 255.255.255.252 |
|  /29  |     8     |   6   | 255.255.255.248 |
|  /28  |     16    |   14  | 255.255.255.240 |
|  /27  |     32    |   30  | 255.255.255.224 |
|  /26  |     64    |   62  | 255.255.255.192 |
|  /25  |     128   |   126 | 255.255.255.128 |
|  /24  |     256   |   254 | 255.255.255.0   |


## Random Commands
* Shows top ten command usage: `$ history | awk '{CMD[$2]++;count++;}END { for (a in CMD)print CMD[a] " " CMD[a]/count*100 "% " a;}' | grep -v "./" | column -c3 -s " " -t | sort -nr | nl |  head -n10`
* `$ openssl x509 -text -in <file.pem> Shows Certificate Information`

## Common Sayings

* "Not perfect but perfect is the enemy of good."

## ascii
ASCII stands for American Standard Code for Information Interchange. Computers can only understand numbers, so an ASCII code is the numerical representation of a character such as 'a' or '@' or an action of some sort. ([asciitable.com](http://www.asciitable.com/))

It is a code for representing 128 English characters as numbers, with each letter assigned a number from 0 to 127 ([webopedia.com](https://www.webopedia.com/TERM/A/ASCII.html)).

[ASCII Quick Lookup - rapidtables.com ](https://www.rapidtables.com/code/text/ascii-table.html)

## Samba
Samba is an extremely useful networking tool for anyone who has both Windows and Unix systems on his network. Running on a Unix system, it allows Windows to share files and printers on the Unix host, and it also allows Unix users to access resources shared by Windows systems. Samba is a suite of Unix applications that speak the Server Message Block (SMB) protocol. Microsoft Windows operating systems and the OS/2 operating system use SMB to perform client-server networking for file and printer sharing and associated operations ([samba.org](https://www.samba.org/samba/docs/using_samba/ch01.html)).

```
smbd — server to provide SMB/CIFS services to clients


Usage: smbd [OPTION...]
  -D, --daemon                            Become a daemon (default)
  -i, --interactive                       Run interactive (not a daemon)
  -F, --foreground                        Run daemon in foreground (for daemontools, etc.)
  --no-process-group                      Don't create a new process group
  -S, --log-stdout                        Log to stdout
  -b, --build-options                     Print build options
  -p, --port=STRING                       Listen on the specified ports
  -P, --profiling-level=PROFILE_LEVEL     Set profiling level
```





## Shells
At its base, a shell is simply a macro processor that executes commands. The term macro processor means functionality where text and symbols are expanded to create larger expressions. A Unix shell is both a command interpreter and a programming language. As a command interpreter, the shell provides the user interface to the rich set of GNU utilities. The programming language features allow these utilities to be combined. Files containing commands can be created, and become commands themselves. These new commands have the same status as system commands in directories such as /bin, allowing users or groups to establish custom environments to automate their common tasks ([gnu.org](https://www.gnu.org/software/bash/manual/html_node/What-is-a-shell_003f.html#What-is-a-shell_003f)).

### Bash
Bash is the shell, or command language interpreter, for the GNU operating system. The name is an acronym for the ‘Bourne-Again SHell’, a pun on Stephen Bourne, the author of the direct ancestor of the current Unix shell sh, which appeared in the Seventh Edition Bell Labs Research version of Unix ([gnu.org](https://www.gnu.org/software/bash/manual/html_node/What-is-a-shell_003f.html#What-is-a-shell_003f)).

To execute a script file with the bash executable found in the PATH environment variable by using the executable env, the first line of a script file must indicate the absolute path to the env executable with the argument bash: `#!/usr/bin/env bash` ([books.goalkicker.com](http://books.goalkicker.com/BashBook/))

* ["Safe ways to do things in bash" - github.com/anorda" ](https://github.com/anordal/shellharden/blob/master/how_to_do_things_safely_in_bash.md)
* ["What is a Bash Script? Lets Dive in " - yanstutorials.net](https://ryanstutorials.net/bash-scripting-tutorial/bash-script.php)

## Elasticsearch

Elasticsearch is an open-source, RESTful, distributed search and analytics engine built on Apache Lucene. ([aws.amazon.com](https://aws.amazon.com/elasticsearch-service/what-is-elasticsearch/))

Elasticsearch is a distributed, JSON-based search and analytics engine designed for horizontal scalability, maximum reliability, and easy management. ([elastic.co](https://www.elastic.co/products/elasticsearch))

https://www.elastic.co/guide/en/elasticsearch/reference/current/_basic_concepts.html

## pstree

The pstree command shows running processes as a tree ([computerhope.com](https://www.computerhope.com/unix/pstree.htm)).

* By default, pstree shows the processes of all users as a tree: `pstree`
* To view the command-line arguments of each process: `pstree -a`


https://codeyarns.com/2017/11/21/pstree-cheatsheet/

## Katello

Katello brings the full power of content management alongside the provisioning and configuration capabilities of Foreman ([theforeman.org](https://theforeman.org/plugins/katello/)).

Parts of Katello Project:
* **Foreman:** Provisioning and Configuration Management
* **Pulp:** Patch and Content Management
* **Candlepin:** Subscription and Entitlement Management
* **Katello:** Unified workflow and webUI for content (Pulp) and subscriptions (Candlepin).

[Katello Project -- github](https://github.com/Katello)

## Docker

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. Unlike a virtual machine, rather than creating a whole virtual operating system, Docker allows applications to use the same Linux kernel as the system that they're running on and only requires applications be shipped with things not already running on the host computer ([opensource.com](https://opensource.com/resources/what-docker)).

A container image is a lightweight, stand-alone, executable package of a piece of software that includes everything needed to run it: code, runtime, system tools, system libraries, settings ([docker.com](https://www.docker.com/what-container)).


**Virtual Machine vs. a container** - The way virtual machines work, however, is by packaging the operating system and code together. The operating systems on the virtual machines believes that it has a server to its own, but in reality, it’s sharing the server with a bunch of other virtual machines — all of which run their own operating systems and don’t know of each other. Underneath it all is the host os that makes all of these guests believe they are the most important thing in the world ([techcrunch.com](https://techcrunch.com/2016/10/16/wtf-is-a-container/)). A container consists of an entire runtime environment: an application, plus all its dependencies, libraries and other binaries, and configuration files needed to run it, bundled into one package. By containerizing the application platform and its dependencies, differences in OS distributions and underlying infrastructure are abstracted away ([cio.com](https://www.cio.com/article/2924995/software/what-are-containers-and-why-do-you-need-them.html)).


Docker File - a script, composed of various commands (instructions) and arguments listed successively to automatically perform actions on a base image in order to create (or form) a new one. They are used for organizing things and greatly help with deployments by simplifying the process start-to-finish ([digitalocean.com](https://www.digitalocean.com/community/tutorials/docker-explained-using-dockerfiles-to-automate-building-of-images)). The docker file is like a cooking recipe.  

####Resources & References**
* ["Docker Cheat Sheet" - github.com/wsargent ](https://github.com/wsargent/docker-cheat-sheet)
* ["Getting Started: FAQs" - docker-curriculum.com ](https://docker-curriculum.com/)





## Jenkins

Jenkins offers a simple way to set up a continuous integration or continuous delivery environment for almost any combination of languages and source code repositories using pipelines, as well as automating other routine development tasks. While Jenkins doesn’t eliminate the need to create scripts for individual steps, it does give you a faster and more robust way to integrate your entire chain of build, test, and deployment tools than you can easily build yourself ([infoworld.com](https://www.infoworld.com/article/3239666/devops/what-is-jenkins-the-ci-server-explained.html)).

## Splunk

Splunk is a software technology which provides the engine for monitoring, searching, analyzing, visualizing and acting on voluminous streams of real-time machine data. Its wide application and suitability make it a versatile technology (https://intellipaat.com/blog/what-is-splunk/).

https://www.splunk.com/pdfs/solution-guides/splunk-quick-reference-guide.pdf

## SAML

Security Assertion Markup Language (SAML) is an XML-based framework for authentication and authorization between two entities: a Service Provider and an Identity Provider. The Service Provider agrees to trust the Identity Provider to authenticate users. In return, the Identity provider generates an authentication assertion, which indicates that a user has been authenticated. SAML is a standard single sign-on (SSO) format. Authentication information is exchanged through digitally signed XML documents ([auth0.com](https://auth0.com/blog/how-saml-authentication-works/)).

## Regular Expression (Regular Expression)


## HTTP/HTTPS

### HTTP basic authentication

HTTP provides a general framework for access control and authentication, via an extensible set of challenge-responseauthentication schemes, which can be used by a server to challenge a client request and by a client to provide authentication information ([RFC7235](https://tools.ietf.org/html/rfc7235)). In the case of a "Basic" authentication, the exchange must happen over an HTTPS (TLS) connection to be secure ([developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)).

#### Protocol

**["Basic access authentication" - en.wikipedia.org ](https://en.wikipedia.org/wiki/Basic_access_authentication)**
> **Server Side:**
> When the server wants the user agent to authenticate itself towards the server, the server must respond appropriately to unauthenticated requests. To unauthenticated requests, the server should return a response whose header contains a HTTP 401 Unauthorized status and a WWW-Authenticate field.
>
> **Client side**
> When the user agent wants to send authentication credentials to the server, it may use the Authorization field. The Authorization field is constructed as follows: (1) The username and password are combined with a single colon **(`:`)**. (2) The resulting string is encoded into an octet sequence. (3) The resulting string is encoded using a variant of Base64.(4) The authorization method and a space (e.g. "Basic ") is then prepended to the encoded string.
>
> For example, if the browser uses `Aladdin` as the username and `OpenSesame` as the password, then the field's value is the base64-encoding of `Aladdin:OpenSesame`, or `QWxhZGRpbjpPcGVuU2VzYW1l`. Then the Authorization header will appear as:`Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l`






## Dell OpenManage Server Administrator - OMSA
The best way to install OMSA is to install the `srvadmin-all` metapackage, which installs all OMSA components ([inux.dell.com](http://linux.dell.com/repo/hardware/omsa.html))

```
$ rpm -qf /opt/dell/srvadmin/bin/omreport
srvadmin-omacore-8.1.0-4.94.3.el6.x86_64
```

```
omreport storage pdisk controller=0|egrep "^ID |Status|State|Failure"
```


### `omreport`
The omreport command allows you to see detailed information about your system components. You can retrieve summaries for many system components at one time, or you can get details about a specific component ([cs.uwaterloo.ca](https://cs.uwaterloo.ca/~brecht/servers/docs/PowerEdge-2600/en/Dosa/CLI/cli_cc4r.htm)).

**Commands**
* Help: `# omreport -?`
* Shows key facts for all system components, including main system chassis, software, and storage.: `# omreport system summary`
* Chassis Component Properties: `# omreport chassis pwrmonitoring`


### `racadm`
The Dell RACADM (Remote Access Controller Admin) utility is a command line tool that allows for remote or local management of Dell Servers via the iDRAC or DRAC ([en.community.dell.com](http://en.community.dell.com/techcenter/systems-management/w/wiki/3205.racadm-command-line-interface-for-drac).


## Concepts

### Data structure

### Public Key Encryption

### Memory Leak

### big-Θ notation

https://www.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/big-o-notation

## Terms

* CENTOS - Community ENTerprises Operating System
* KVM - Kernel Base Virtual Machine
* VPS - Virtual Privare Servers
* idrac - An integrated Dell Remote Access Controller (iDRAC) with Lifecycle Controller is embedded in every Dell PowerEdge server. It provides functionality that helps you deploy, update, monitor and maintain Dell PowerEdge servers with or without a systems management software agent. Because it is embedded within each server from the factory, the Dell iDRAC with Lifecycle Controller requires no operating system or hypervisor to work.
* VPS - Virtual Private Servers
* XEN - Open Source Industry Standard for Virtualization
* proxy - a proxy server is a server that acts as an intermediary for requests from clients seeking resources from other servers.

## OTHER:
fab utils.fact_lookup:"lrs-de-lcfapp*","memorysize_mb",prod | cut -d" " -f2 | awk '{ SUM += $1} END { printf "%4.3f\n",SUM }'


### depmod, lsmod, /lib/modules/



* testing sign commit 
User space: https://en.wikipedia.org/wiki/User_space
