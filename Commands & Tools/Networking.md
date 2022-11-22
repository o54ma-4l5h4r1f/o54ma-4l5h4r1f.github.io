---
sort : 1
---

## Namp 

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




> Filtered ports ??

means that nmap cannot determine whether the port is open or not, because packet filtering prevents its probes from reaching the port. 

The filtering could be from a dedicated `firewall device`, `router rules`, or `host-based firewall software`. 

These ports frustrate attackers because they provide so little information. Sometimes they respond with ICMP error messages such as type 3 code 13 (destination unreachable: communication administratively prohibited), but filters that simply drop probes without responding are far more common. This forces Nmap to retry several times just in case the probe was dropped due to network congestion rather than filtering. This `slows down` the scan dramatically.


```danger
It's a very noisy tool, learn proxy-chains to hide your self.  
```

<br><br> 

## Nikto

Nikto is a web server vulnerability scanner that can be used for reconnaissance in a manner similar to Nessus and OpenVAS. It can detect a variety of different vulnerabilities but is also not a stealthy scanner. Scanning with Nikto can be effective but is `easily detectable` by an intrusion detection or prevention system (like most active reconnaissance tools).

```bash 
$ sudo apt-get install nikto 

$ nikto -update # Update scan engine plugins
$ nikto -h <Hostname/IP address> -output <filename> 
```


<br><br>









