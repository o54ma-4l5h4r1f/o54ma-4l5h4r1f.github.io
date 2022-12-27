---
sort : 1
---

# Methodologies & Tactics

A penetration test, is a simulated cyber attack against your computer system to check for exploitable vulnerabilities. 

throughout this I will be following the `MITRE ATT&CK Framework` knowledge base of *adversary tactics* and *techniques* which are based on real-world observations, The OWASP Top 10 methodologies, And my prefered ways to start penetration testing on any server or domain.


## 1. Planning and Reconnaissance

By Defining the scope and goals of the test, including the systems to be addressed and the testing methods to be used. 

> Open Source Intelligence & Information Gathering

By Collecting hosts metadata about services and users, Checking informations about the domain, IP addresses, phone numbers or an email addresses, [HOW??](#)


---


> Scanning (Active vs. Passive) 

The `Active` scanner directly interact with the systems by sending a probe request or requesting a probe response. e.g.
On the opposite `passive` scanners watches the network’s traffic flow to collect information about its systems and endpoints, Unlike Active scanning it doesn't involve direct interaction with the target.

some techniques to use :

* Network & Vulnerability Scanning (ex: [Nmap](#), [Nikto](#), OpenVAS, Amass)

* URIs Scanning (ex: [Dirb](#), [DirBuster](#), [GoBuste](#), [dirsearch](#))

* Subdomains Scanning (Amass, SubBrute, s3recon, ...)

* Crawling (Hakrawler)

---

## 2. Initial Access 

Initial Access consists of techniques that use various *entry vectors* to gain their initial *foothold* within a network. Techniques used to gain a foothold include targeted _spearphishing_ and _exploiting weaknesses on public-facing services_

Footholds gained through initial access may allow for continued access, like valid accounts and use of external remote services, or may be limited-use due to changing passwords.

### Social Engineering

[Soon!](#)

### Exploit Public-Facing Application/services

can be found through online tools that scan the internet for open ports and services. Version numbers for the exposed application may provide adversaries an ability to target specific known vulnerabilities.

[Used Techniques](https://attack.mitre.org/groups/G0034/) 

> Web Exploitation

[How to begin ??](#)

---

> Other Sevices 

* [SSH](#) 
* [FTP](#) 
* [SMB](#)
* and a lot more 

---

## 3. Execution

Execution consists of techniques that result in adversary-controlled code running on a local or remote system. 
Techniques that run malicious code are often *paired with techniques from all other tactics to achieve broader goals*, like exploring a network or stealing data. [for more](https://attack.mitre.org/tactics/TA0002/)

Simple Example: uploading a php reverse shell on the webserver and execute it to gain a shell.  


---

## 4. Persistence

Persistence consists of techniques that adversaries use to keep access to systems across restarts, changed credentials, and other interruptions that could cut off their access. 
Techniques used for persistence include any access, action, or configuration changes that let them maintain their foothold on systems, such as replacing or hijacking legitimate code or adding startup code [for more](https://attack.mitre.org/tactics/TA0003/)

---

## 5. Privilege Escalation

Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network. These techniques often overlap with Persistence techniques, as OS features that let an adversary persist can execute in an elevated context. 

[How to begin ??](#)

---

## 6. Defense Evasion

Defense Evasion consists of techniques that adversaries use to avoid detection throughout their compromise. Techniques used for defense evasion include uninstalling/disabling security software or obfuscating/encrypting data and scripts. Adversaries also leverage and abuse trusted processes to hide and *masquerade* their malware

---

## 7. Credential Access

Credential Access consists of techniques for stealing credentials like account names and passwords. Techniques used to get credentials include keylogging or credential dumping. Using legitimate credentials can give adversaries access to systems, make them harder to detect, and provide the opportunity to create more accounts to help achieve their goals.

---

## ** Lateral Movement

Lateral Movement consists of techniques that adversaries use to enter and control remote systems on a network. Following through on their primary objective often requires *exploring* the network to find their target and subsequently *gaining access* to it. Reaching their objective often involves *pivoting* through multiple systems and accounts to gain. Adversaries might install their own remote access tools to accomplish *Lateral Movement* or use legitimate *credentials* with native network and operating system tools, which may be stealthier. 

---

## 8. Collection

Collection consists of techniques adversaries may use to gather information and the sources information is collected from that are relevant to following through on the adversary's objectives. Frequently, the next goal after collecting data is to steal (exfiltrate) the data. Common target sources include various drive types, browsers, audio, video, and email.

---

## 9. Command and Control

Command and Control consists of techniques that adversaries may use to communicate with systems under their control within a victim network. Adversaries commonly attempt to mimic normal, expected traffic to avoid detection.

---

## 10. Exfiltration

Exfiltration consists of techniques that adversaries may use to steal data from your network. Once they’ve collected data, adversaries often package it to avoid detection while removing it. This can include compression and encryption. Techniques for getting data out of a target network typically include transferring it over their command and control channel or an alternate channel and may also include putting size limits on the transmission.

---

## 11. Impact 

Impact consists of techniques that adversaries use to disrupt availability or compromise integrity by manipulating business and operational processes. Techniques used for impact can include destroying or tampering with data. In some cases, business processes can look fine, but may have been altered to benefit the adversaries’ goals


---

## References

* https://attack.mitre.org/
* https://portswigger.net/