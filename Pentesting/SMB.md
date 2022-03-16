---
sort : 6 
---

# SMB/CIFS

```note
SMB : Server Message Block Protocol, it is a client-server protocol used for sharing files, printers, serial ports and other resources on a network. Thus, a client application can `read`, `create`, `update` files and `execute` commands on the remote server.

You use it basically every time you use Windows to access a file share, a printer, or any other ressource located on the network.

port numbers `139` and `445` 
```

```note 
`CIFS` stands for "Common Internet File System"

CIFS is a dialect of SMB. That is, CIFS is a particular implementation of the Server Message Block protocol, created by Microsoft.
```



## Nmap

### Recommended scripts
```bash
$ ls /usr/share/nmap/scripts | grep "smb"

--script smb-enum*,smb-ls,smb-mbenum,smb-os-discovery,smb-s*,smb-vuln*,smbv2* -p445 
```

### examples
```
PORT     STATE SERVICE       VERSION
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds

139/tcp  open  netbios-ssn   Samba smbd 3.X - 4.X 
445/tcp  open  netbios-ssn   Samba smbd 3.0.20-Debian   
```

```note
Microsoft DS is the name given to port 445 which is used by SMB

An open source implementation of SMB exists with the name of Samba, which is commonly used to easily use Linux and Windows together in a network.
```



### Ports 139 , 445 

> `NetBIOS` is an acronym for Network Basic Input/Output System. It allows applications on separate computers to communicate over a local area network. `Asstrictly an API`, NetBIOS is `not` a networking protocol. NetBIOS normally runs over TCP/IP via the NetBIOS over TCP/IP (`NBT`) protocol. This results in each computer in the network having both an IP address and a `NetBIOS name` corresponding to a (possibly different) `host name`. Simply saying, it is a protocol that allows communication of files and printers through the `Session Layer of the OSI Model` in a LAN.

> `SMB` is a network file sharing protocol that requires an open port on a computer or server to communicate with other systems. SMB ports are generally port numbers 139 and 445. 

<br>

--- 

## Tools 

### smbclient
`smbclient` command launches an ftp-like client to access SMB/CIFS resources on the servers.


