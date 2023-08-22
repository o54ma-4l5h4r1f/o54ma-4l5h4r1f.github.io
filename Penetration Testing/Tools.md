---
sort : 3
---

# Tools / Scripts / softwares

## Namp 

A tool used to Gather Victim Network Information, such as which IP addresses are actively in use as well as more detailed information about hosts assigned these addresses, namp scan may range from simple pings (ICMP requests and responses) to more nuanced scans that may reveal host software/versions via server banners or other network artifacts. 

nmap scans victims for vulnerabilities that can be used during targeting. Vulnerability scans typically check if the configuration of a target host/application (ex: software and version) potentially aligns with the target of a specific exploit the adversary may seek to use.

> generally 

```bash
$ nmap -A -sV -sS -vvv -Pn -p- [IP]/24 

$ sudo nmap -A -sV -sS -v --script default -Pn [IP]

$ nmap -T4 -sC -sV -Pn -p- --min-rate=1000 -oN nmap.log [IP]
```



> Nmap Automator 

```bash
# https://github.com/21y4d/nmapAutomator

$ sudo ./nmapAutomator.sh --host 10.1.1.1 --type All
$ ./nmapAutomator.sh -H 10.1.1.1 -t Basic
$ ./nmapAutomator.sh -H academy.htb -t Recon -d 1.1.1.1
$ ./nmapAutomator.sh -H 10.10.10.10 -t network -s ./nmap
```

> Gospider

```bash
# https://github.com/jaeles-project/gospider

$ sudo apt-get install golang
$ GO111MODULE=on go install github.com/jaeles-project/gospider@latest
$ find / -name gospider 2>/dev/null

# based on what you gonna find
$ cp /home/user/go/bin/gospider /usr/local/bin/
$ gospider -h
$ gospider -s http://10.129.29.189/ -d 3 --js --robots --sitemap --subs | sort
```



