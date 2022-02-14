---
sort: 1
---

# ping
# /etc/hosts

# nmap 


## nmap services

PORT   STATE SERVICE
23/tcp open  telnet         

```bash
$ telnet <IP> <Port>
Login : username
Password : passwd
```

Account Misconfiguration Vuls:
root:root


```note
FTP : File Transfer Protocol, uses client-server communicaition model
FileZilla one popular GUI FTP program
running usually on port (21 tcp)
SFTP is the secure version of FTP   
vsFTPd 3.0.3 is one example on FTP services names/versions

```


PORT   STATE SERVICE
21/tcp open  ftp


```bash
$ ftp
Name : anonymous
Password: `null`
230 Login successful.
```


--------

# Windows Machine

```note
SMB : Server Message Block Protocol, uses client-server communicaition model
port numbers 139 and 445
smbclient command launches an ftp-like client to access SMB/CIFS resources on servers.
```


PORT    STATE SERVICE
445/tcp open  microsoft-ds    


```bash 
$ smbclient -L <IP>
Enter WORKGROUP\o54ma's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        WorkShares      Disk

$ smbclient //<IP>/WorkShares     
Enter password: 
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Mon Mar 29 04:22:01 2021
  ..                                  D        0  Mon Mar 29 04:22:01 2021
  Amy.J                               D        0  Mon Mar 29 05:08:24 2021
  James.P                             D        0  Thu Jun  3 04:38:03 2021


smb: \> cd James.P
smb: \James.P\> ls
  .                                   D        0  Thu Jun  3 04:38:03 2021
  ..                                  D        0  Thu Jun  3 04:38:03 2021
  flag.txt                            A       32  Mon Mar 29 05:26:57 2021

smb: \James.P\> get flag.txt
getting file \James.P\flag.txt of size 32 as flag.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \James.P\> exit
```


------
# win / misconfiguration


```note 
RDP : Remote Desktop Protocol
```




SSH uses public key cryptography




xfreerdp : name of the tool that we can use to initiate a desktop projection to our host using the terminal


what is the switch used --> switch means flag --> flag means cli options of the commands -l -s -a .... 