---
sort : 6 
---

# Windows Fundamentals


## Remote Desktop Protocol (RDP)

The Microsoft Remote Desktop Protocol (RDP) provides remote display and input capabilities over network connections for Windows-based applications running on a server.” (`MSDN`)

Essentially, RDP allows users to control their remote Windows machine as if they were working on it locally (well, almost).

![RDP Server](https://www.cyberark.com/wp-content/uploads/2020/04/1-what_is_rdp-768x190.png "What is RDP?")



Communication in RDP is based on multiple channels, and the protocol theoretically supports up to 64,000 unique channels.

The basic functionality of RDP is to transmit a monitor (output device) from the remote server to the client and the keyboard and/or mouse (input devices) from the client to the remote server. The communication during an RDP connection will be extremely asymmetric, while most of the data will go from the server to the client. RDP communication is encrypted with RSA’s RC4 block cipher by default.

![RDP Server](https://www.cyberark.com/wp-content/uploads/2020/04/2-not_symmetric-768x368.png "Asymmetric communication")


[For more about RDP](https://www.cyberark.com/resources/threat-research-blog/explain-like-i-m-5-remote-desktop-protocol-rdp) 


## References

* https://tryhackme.com/room/windowsfundamentals1xbx

* https://www.cyberark.com/resources/threat-research-blog/explain-like-i-m-5-remote-desktop-protocol-rdp