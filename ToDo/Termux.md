---
sort : 8
---


# Termux 

## Configurations

```bash
# Set up access for Termux to your to mobile’s storage with 
$ termux-setup-storage
```

## packages to install

```bash
# to install sudo 
pkg install tsu
```



## Passwd 

```bash
# to set a new password for the default Termux user
$ passwd 
```



## SSHd

```bash
$ apt install openssh

# Start SSH server on your mobile
$ sshd 
# the ssh daemon will be running on port 8022 

# on any other device 
$ ssh -p 8022 u0_****@hostname 
password : **********

# when you done
$ pkill sshd
```



## Mosh 

```bash
$ pkg install mosh

# Start mosh server on your mobile
$ mosh-server 

# on any other device 
$ mosh --ssh="ssh -p 8022" u0_****@hostname 
password : **********

# when you done
$ pkill mosh-server
```
