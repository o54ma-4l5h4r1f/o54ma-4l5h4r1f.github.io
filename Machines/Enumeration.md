---
sort : 3
---

# Enumeration

## Nmap 

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

> [Why -Pn ??](https://informationsecurity.medium.com/nmap-pn-no-ping-option-analysis-d9aaa95be5b0) 


## Default Ports

|:-------------:|:-----------:|:------------------------------:|
|      PORT     |   SERVICE   |             VERSION            |
|:-------------:|:-----------:|:------------------------------:|
| 22/tcp        | ssh         | OpenSSH 7.2p2 Ubuntu           |
| 80/tcp        | http        | Apache  httpd 2.4.18           |
| 21/tcp        | ftp         | vsftpd 3.0.3                   |
| 25/tcp        | smtp        | Exim stmpd 4.92                |
| 139/tcp       | netbios-ssn | Samba (smbd) workgroup         |
| 445/tcp       | netbios-ssn | Samba (smbd) 4.3.11-Ubuntu     |
|:-------------:|:-----------:|:------------------------------:|
