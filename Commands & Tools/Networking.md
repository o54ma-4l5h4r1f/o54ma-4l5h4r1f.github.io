---
sort : 1
---

# Namp 

> generally 
```bash
$ nmap -A -sV -sS -vvv -Pn -p- [IP]/24 

$ sudo nmap -A -sV -sS -v --script default -Pn [IP]

$ nmap -T4 -sC -sV -Pn -p- --min-rate=1000 -oN nmap.log [IP]
```

> Automator 
```bash
# https://github.com/21y4d/nmapAutomator

$ sudo ./nmapAutomator.sh --host 10.1.1.1 --type All
$ ./nmapAutomator.sh -H 10.1.1.1 -t Basic
$ ./nmapAutomator.sh -H academy.htb -t Recon -d 1.1.1.1
$ ./nmapAutomator.sh -H 10.10.10.10 -t network -s ./nmap
```


> Default Ports 

|        PORT       | STATE |   SERVICE   |       NMAP VERSION EXAMPLE     |
|:-----------------:|:-----:|:-----------:|:------------------------------:|
| 21/tcp            | open  | ftp         | vsftpd 3.0.3                   |
| 22/tcp            | open  | ssh         | OpenSSH 7.2p2 Ubuntu           |
| 25/tcp            | open  | smtp        | Exim stmpd 4.92                |
| 80/tcp            | open  | http        | Apache  httpd 2.4.18           |
| 139/tcp           | open  | netbios-ssn | Samba (smbd) workgroup         |
| 445/tcp           | open  | netbios-ssn | Samba (smbd) 4.3.11-Ubuntu     |
