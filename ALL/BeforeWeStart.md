---
sort : 3
---

# Before We Start

## Contemplate :

* searchsploit for every service Nmap shows --> and not every exploit you find should eveitually work !!	 

```
searchsploit vsftpd 2.3.4
```


## WEB  
	- Having a proxy listening and intercept all requests while testing ==> {MITM, Burp}
	- Investigate the URL and all pages that accessible ==> {}
	- Find subdomains in the app ==> {}
	- Enumerate Dir and pages ==> {ffuf / fuzz / durb / gobuster}
	- Listing all input vectors that potentially talk to the back end ==> {}
		- URL parameters 
		- Forms inputs 
	- Understand how the app functions and the logic of the app ==> {NO Scanners}
	- 



## Pinging 
Pinging is normally the first step involved in hacking the target. Ping uses `ICMP` (Internet Control Messaging Protocol) to determine whether the target host is reachable or not, Ping sends out ICMP `Echo` packets to the target host, if the target host is alive it would respond back with ICMP Echo reply packets.

### Usage
```bash
$ ping -c 3 $IP 
```


<br>
<br>

-------- 



## Port Scanning

After we tested our network connectivity with ping, it's time to determining which ports on the network are open and could be receiving or sending data, This will help us to determine what services may be running on the system.

```warning
nmap is so noisy tool especially with the -A option
```

### Usage
```bash
$ nmap -A -sV -sS -vvv -T4 -Pn -oN nmap.log -p- $IP[/CIDR]
```

### Options


| Option                | Usage                                                                    |
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


> [Why -Pn ??](https://informationsecurity.medium.com/nmap-pn-no-ping-option-analysis-d9aaa95be5b0) when our packets are blocked by a firewall?

<br>

### Default Ports


|   PORT   |    SERVICE    |       VERSION Example       |
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



```note
Filtered Nmap ports cannot determine whether the port is open because packet filtering prevents its probes from reaching the port. The filtering could be from a dedicated firewall device, router rules, or host-based firewall software. These ports frustrate attackers because they provide so little information. Sometimes they respond with ICMP error messages such as type 3 code 13 (destination unreachable: communication administratively prohibited), but filters that simply drop probes without responding are far more common. This forces Nmap to retry several times just in case the probe was dropped due to network congestion rather than filtering. This slows down the scan dramatically.
```

<br>

----

## Directory Busting

### Gobuster

```bash
$ gobuster dir --timeout 20s --delay 0ms --threads 10 -q -u http://$IP:$PORT/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt [-x php,html,txt] 
```

### Dirbuster 

```bash
$ dirb http://$IP/ /usr/share/dirb/wordlists/common.txt [-R] [-X] [-w]
```

### [Wfuzz](https://book.hacktricks.xyz/pentesting-web/web-tool-wfuzz) 
```bash
$ wfuzz -u http://$IP/FUZZ.php -w /usr/share/wordlists/dirb/big.txt -c -t 100 --hc 404,403 [-d] [-b] [-H] [--follow]

$ wfuzz -c -z file,users.txt -z range,1-10 --sc 200 http://$IP/page.php?user=FUZZ&id=FUZ2Z      # notice the 2 in the middle Z2Z
```

### ffuf 
```bash
$ ffuf -w params.txt:PARAM -w values.txt:VAL -u https://$IP/?PARAM=VAL -mr "VAL" -c [-H]
```

### Turbo Intruder - Burp

<p align="left">
  <img src='./../assets/images/9.png'> 
</p>


-----


### Installing Wordlists
 
[Seclists](https://github.com/danielmiessler/SecLists)

> /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-big.txt <br>
> /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt

[Dirb](https://github.com/v0re/dirb/tree/master/wordlists)
> /usr/share/dirb/wordlists/common.txt

[Dirbuster](https://github.com/daviddias/node-dirbuster/tree/master/lists) 
> /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt

<br>

### Generating Wordlists

#### CeWL
it's a tool that spiders a given URL, up to a specified depth, and returns a list of words which can then be used for password cracking, Or create a list of email addresses found in mailto links, Optionally, CeWL can follow external links. <br>

```bash
cewl https://$IP -w list.out           # check --help for more
```
