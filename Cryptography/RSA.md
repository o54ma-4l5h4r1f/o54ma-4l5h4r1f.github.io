---
sort : 2
---

# RSA 

In RSA, modular exponentiation, together with the problem of prime factorisation, helps us to build a `trapdoor function`.

The private key is the secret piece of information or "trapdoor" which allows us to quickly invert the encryption function

In RSA the private key is the `modular multiplicative inverse` of the exponent `e` modulo the `totient of N`

## RSA Key Generation, Encryption, and Decryption 

> Key Generation

<img  src="https://latex.codecogs.com/svg.image?\text{Select two large primes} \ p \ \text{and} \ q \ \text{such that} \ p \ \neq \ q"/>

<img  src="https://latex.codecogs.com/svg.image?n \gets p \times q"/>

<img  src="https://latex.codecogs.com/svg.image?\varphi(n) \gets (p-1) \times (q-1)"/>

<img  src="https://latex.codecogs.com/svg.image?\text{Select} \ e \ \text{such that} \ 1 < e < \varphi(n) \ \text{and} \ e \ \text{is coprime to} \ \varphi(n)"/>

The most common value for e is `0x10001` or `65537`


<img  src="https://latex.codecogs.com/svg.image?d \gets e^{-1} \mod  \varphi(n)"/>

<img  src="https://latex.codecogs.com/svg.image?PublicKey \gets (e, \ n)"/>

<img  src="https://latex.codecogs.com/svg.image?PrivateKey \gets d"/>

---

```tip
The Keys sizes could be different {512, 1024, 2048, 4096} -- the bigger the harder to crack -- 
```

> Public/Private Key Example

```
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCsw8csUzHDGkMrL22b7psQc8yn
YVq4g7ipnxr2ehESpVJiu3WtBNqA01bDbdNL6fFHYHto+nD2Hm7JE/pJqRXt15u2
D7WQMsHRM28FZSQF4ByUabQTwsZaRpPxkS9VVXgj7cJajDkK8zd32ag8J41J0o8S
JWQGNtR87JEyFbIXfQIDAQAB
-----END PUBLIC KEY-----
```


```
-----BEGIN RSA PRIVATE KEY-----
MIICWwIBAAKBgQCsw8csUzHDGkMrL22b7psQc8ynYVq4g7ipnxr2ehESpVJiu3Wt
BNqA01bDbdNL6fFHYHto+nD2Hm7JE/pJqRXt15u2D7WQMsHRM28FZSQF4ByUabQT
wsZaRpPxkS9VVXgj7cJajDkK8zd32ag8J41J0o8SJWQGNtR87JEyFbIXfQIDAQAB
AoGAXZ1Yd7Q86rN4YhY5Fp2ceLXG14vxVLpLfd4xBg3u4mOi2M0rXq2amOPrx8nj
DOefTkYBmUjbnQGwllS08uUkc+7OsCqiByRom5XldCoI7r33GfDFOQ2zUo19THy5
ssFUebRy09eapxn/JwJgk1TX6SxuWEIe1Lo3exLzybftzwECQQDwEr4OawS+97/d
bgRACgXiVB08fBXhjAiM8MGQzqgngzQcT0K9Xp4QRtYffJVvDjS/KQKSTifAFAFi
MOnf8RN1AkEAuDno4sSBXweaMv2HhW62aVq4DpoEx3mjyN0TGAki3Qzn6R6aeOCM
Oc325U+nfTAHuPl9qhpCoVcUhfGUE+ea6QJAWTOtmK/dCJQHn2AEhkLzIsB8SIAW
pUKh3rSKR6LxyhSvJSGyO6jPdF7Nqs9guu39XVYAlZoinPUR+okQLVxnDQJAM4gf
WK9W8NoTjAfXDL/3TmkN6yeyBopEAj+0w5hqpCKkDFV/KCjHkLPISESLuTziLB+9
wwMteCv/lagJn7e9YQJANxre+t8nL2c9R3whiFjmyF30gkPfVWfOEjsfDMIvXosZ
wI0JiY2XRTBK5mknIv5Z46sQAtPPkHy317FQsuCOTA==
-----END RSA PRIVATE KEY-----
```

```note
these public and private keys came only from two prime numbers
```

---

<img  src="https://latex.codecogs.com/svg.image?P \gets PlainText"/>

<img  src="https://latex.codecogs.com/svg.image?C \gets CipherText"/>

---


> Enccryption

<img  src="https://latex.codecogs.com/svg.image?C = P^e \mod n"/>




<br>

> Exponential Complexity

<img  src="https://latex.codecogs.com/svg.image?\text{without having} \ d \ \text{it's hard to find} \ P"/>

<img  src="https://latex.codecogs.com/svg.image?P = \sqrt[e]{C} \mod n"/>




<br>

> Decryption

<img  src="https://latex.codecogs.com/svg.image?P = C^d \mod n"/>



<br>
<br>



---

## RSA Digital Signature

> Signing 

* <img src="https://latex.codecogs.com/svg.image?\text{Encrypt the Messsage } (M) \text{ with the reciver Public Key } (e_{0}, N_{0})"/>

<img src="https://latex.codecogs.com/svg.image?C = M^{e_{0}} \mod N_{0}"/>

* <img src="https://latex.codecogs.com/svg.image?\text{Calculate the hash/digest of the message: } H(M) \text{ and encrypt it with my Private Key (sender)}"/>

<img src="https://latex.codecogs.com/svg.image?S = H(M)^{d_{1}} \mod N_{1}"/>

<br>

> Verifying

* <img src="https://latex.codecogs.com/svg.image?\text{The receiver can decrypt the message using their Private Key} "/>

<img src="https://latex.codecogs.com/svg.image?m = C^{d_{0}} \mod N_{0}"/>

* <img src="https://latex.codecogs.com/svg.image?\text{calculate the hash/digest of the received message: } H(M) \text{ and compare it to } s \text{ which calculated using the sender Public Key}"/>

<img src="https://latex.codecogs.com/svg.image?s = S^{e_{1}} \mod N_{1}"/>

* <img src="https://latex.codecogs.com/svg.image?\text{assert } H(m) == s"/>



<br><br>

---

## Security of RSA 

```note
RSA relies on the difficulty of the factorisation of the modulus N
```

### composite n

```python
n = 221714271158005222817666050308401368660908569227103024781696324826668748920975811165767447795834564642795098601291978741922902819199320110937373351090463

e = 65537

c = 160930470215067586469213742102075611729542022493476227556730912294132645473152698241299604162900818400257202075639989539138794561481634623996775425889791
```
---

<img src="https://latex.codecogs.com/svg.image?Factors(n) = 57809^2  \times 64453^4 \times 1552903013 \times 3157061689^6 \times 13572582255211282411^3"/>

<img  src="https://latex.codecogs.com/svg.image?\varphi(n) = \varphi(57809^2) \times \varphi(64453^4) \times \varphi(1552903013) \times \varphi(3157061689^6) \times ...."/>

<img  src="https://latex.codecogs.com/svg.image?\varphi(n) = (57809^2 - 57809^{2-1}) \times (64453^4 - 64453^{4-1}) \times (1552903013 - 1) \times ...."/>

---



> Using sagemath-jupyter

```python
sage: n = 2217142711580052228176660503084013686609085692271030247816963248266687489209758111657674477958345646427950
sage: c = 160930470215067586469213742102075611729542022493476227556730912294132645473152698241299604162900818400257202075639989539138794561481634623996775425889791
sage: e = 65537

sage: factor(n)
57809^2 * 64453^4 * 1552903013 * 3157061689^6 * 13572582255211282411^3

sage: euler_phi(n)
221706995777480047771091424858177886182028780813158869290993820998591911017519886643133477122748491365418408960856494933081583289090477887715693950545920

sage: d = pow(e, -1, euler_phi(n))
sage: d
123229942401792356991585628474126765948285127465110367146238489975368227758902557498045732504544902802509977313839808671855025931484487205941980614561793

sage: m = pow(c, d, n)
sage: m
9840580446378271804953504217010097672185393062349354822601887857687208843940453000453640400053524525949

sage: bytes.fromhex(hex(m)[2:])
b'FLAG{Starting_easily_welcome_to_the_finals}'
```

<!-- <iframe src="https://codeshare.io/Qn1nWe" frameBorder="0" width="100%" height="250"></iframe> -->



<br>

### e | p-1  and  e | q-1

```python
n = 57996511214023134147551927572747727074259762800050285360155793732008227782157
e = 17
cipher = 19441066986971115501070184268860318480501957407683654861466353590162062492971
# from factordb.com
p, q = 172036442175296373253148927105725488217, 337117592532677714973555912658569668821
```

```python
sage: (p - 1) / e
10119790716193904309008760417983852248

sage: (q - 1) / e
19830446619569277351385641921092333460
```

---

<!-- https://hackmd.io/fmdfFQ2iS6yoVpbR3KCiqQ?view#cryptobaby-rsa -->

---


## References

* https://mathsci.kaist.ac.kr/cms/wp-content/uploads/2017/11/NumberTheory_Sage.pdf