---
sort : 3
---

# Enumeration

## Nmap 

```warning
nmap is so noisy tool especially with the -A option
```

```bash
$ nmap -A -sV -sS -vvv -T4 -Pn -oN nmap.log -p- $IP[/CIDR]
```

|-----------------------|--------------------------------------------------------------------------|
| Options               | Usage                                                                    |
|-----------------------|--------------------------------------------------------------------------|
| -A                    | OS and version detection                                                 |
| -sV                   | determine the version of the services running                            |
| -sU                   | UDP port scan                                                            |
| -sS                   | TCP SYN port scan                                                        |
| -v, -vv, -vvv         | Verbose mode                                                             |
| -p <port range>       | Port scan for port (-p 22,80) / (-p 1-65536)  or scan all ports (-p-) ,  |
| -Pn                   | skip host discovery                                                      |
| -T<0-5>               | Set timing template (higher is faster)                                   |
| -sC  --script default | Scan with the default nmap scripts  >>  /usr/share/nmap/scripts          |
|-----------------------|--------------------------------------------------------------------------|

> [Why -Pn ??](https://informationsecurity.medium.com/nmap-pn-no-ping-option-analysis-d9aaa95be5b0) when our packets are blocked by a firewall?

<br>

### Default Ports

|:--------:|:-------------:|:---------------------------:|
|   PORT   |    SERVICE    |           VERSION           |
|:--------:|:-------------:|:---------------------------:|
| 21/tcp   | ftp           | vsftpd 3.0.3                |
| 22/tcp   | ssh           | OpenSSH 7.2p2 Ubuntu        |
| 23/tcp   | telnet        | Linux Telnetd               |
| 25/tcp   | smtp          | Exim stmpd 4.92             |
| 80/tcp   | http          | Apache  httpd 2.4.18        |
| 135/tcp  | msrpc         | Microsoft Windows RPC       |
| 139/tcp  | netbios-ssn   | ....                        |
| 445/tcp  | netbios-ssn   | ....                        |
| 1433/tcp | ms-sql-s      | Microsoft SQL Server        |
| 3389/tcp | ms-wbt-server | Microsoft Terminal Services |
|:--------:|:-------------:|:---------------------------:|


```note
Filtered Nmap ports cannot determine whether the port is open because packet filtering prevents its probes from reaching the port. The filtering could be from a dedicated firewall device, router rules, or host-based firewall software. These ports frustrate attackers because they provide so little information. Sometimes they respond with ICMP error messages such as type 3 code 13 (destination unreachable: communication administratively prohibited), but filters that simply drop probes without responding are far more common. This forces Nmap to retry several times just in case the probe was dropped due to network congestion rather than filtering. This slows down the scan dramatically.
```