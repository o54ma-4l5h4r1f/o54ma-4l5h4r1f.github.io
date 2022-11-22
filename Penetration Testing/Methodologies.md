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





> Scanning (Active vs. Passive) 

An `Active` vulnerability scanner directly interact with the systems by sending a probe request or requesting a probe response. e.g.

* Scanning IP Blocks (ex: [Nmap](#))

* Vulnerability Scanning (ex: [Nmap](#), [Nikto](#))

* Wordlist Scanning / Brute Forcing & crawling (ex: [Dirb](#), [DirBuster](#), [GoBuste](#), s3recon, GCPBucketBrute)
	* its goal is the identification of content and infrastructure (web directories and DNS subdomains) rather than the discovery of valid credentials.

	* Wordlists used in these scans may contain generic, commonly used names and file extensions or terms specific to a particular software



On the opposite `passive` scanners watches the network’s traffic flow to collect information about its systems and endpoints, Unlike Active scanning it doesn't involve direct interaction with the target.

  











## References

* https://attack.mitre.org/