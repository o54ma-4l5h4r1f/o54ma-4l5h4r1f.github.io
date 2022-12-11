---
sort : 2
---

# RSA 


## Mathmatics

composite number : 

prime number : 

coprime number / relativly prime number : 

congruence operator :

Factorization : 

gcd :

lcm : 


<br>
<br>


### mod operation

$(a+b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $+$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(a-b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $-$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(a*b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $\times$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(10^a)$ $mod$ $n$ $=$ $(10$ $mod$ $a)^n;$

<br>
<br>


### Euler's Phi-Function | Euler's totient Function 

$\varphi(1) = 0;$

$\varphi(p) = p-1;$ $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime$

$\varphi(m \times n) = \varphi(m) \times \varphi(n);$ $\ \ \ \ \ \ m \ and \ n \ are \ coprimes$

$\varphi(p^e) = p^e - p^{e-1};$	$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime$

<br>
<br>
<br>



---

## Procedure

> Key Generation

Select two large primes $p$ and $q$ such that $p \neq q$ 

$n \gets p \times q$

$\varphi(n) \gets (p-1) \times (q-1)$

Select $e$ such that $1 < e < \varphi(n)$ and $e$ is coprime to $\varphi(n)$ 

$d \gets e^{-1} \mod \varphi(n)$

$PublicKey \gets (e, \ n)$

$PrivateKey \gets d$

---

```tip
The Keys sizes could be different {512, 1024, 2048, 4096} -- the bigger the harder to crack -- 
```

```PublicKey 1024 bit
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCsw8csUzHDGkMrL22b7psQc8yn
YVq4g7ipnxr2ehESpVJiu3WtBNqA01bDbdNL6fFHYHto+nD2Hm7JE/pJqRXt15u2
D7WQMsHRM28FZSQF4ByUabQTwsZaRpPxkS9VVXgj7cJajDkK8zd32ag8J41J0o8S
JWQGNtR87JEyFbIXfQIDAQAB
-----END PUBLIC KEY-----
```

```privateKey 1025 bit
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

$P \gets PlainText$

$C \gets CipherText$

---


> Enccryption


$C = P^e \mod n$

<br>

> Exponential Complexity

without having $d$ it's hard to find $P$ 

$P = \sqrt[e]{C} \mod n$



<br>

> Decryption

$P = C^d \mod n$


<br>
<br>
<br>


---
<!-- 
## Rquirements

```bash
$ docker pull sagemath/sagemath

$ docker run -it sagemath/sagemath
# OR 
$ docker run -p 8888:8888 sagemath/sagemath-jupyter
``` -->



## Security of RSA 

### composite $n$

> Ex1 : 

```python
n = 221714271158005222817666050308401368660908569227103024781696324826668748920975811165767447795834564642795098601291978741922902819199320110937373351090463

e = 65537

c = 160930470215067586469213742102075611729542022493476227556730912294132645473152698241299604162900818400257202075639989539138794561481634623996775425889791
```
---

$Factors(n) = 57809^2 \times 64453^4 \times 1552903013 \times 3157061689^6 \times 13572582255211282411^3$

$\varphi(n) = \varphi(57809^2) \times \varphi(64453^4) \times \varphi(1552903013) \times \varphi(3157061689^6) \times \varphi(13572582255211282411^3)$

$\varphi(n) = (57809^2 - 57809^{2-1}) \times (64453^4 - 64453^{4-1}) \times (1552903013 - 1) \times ....$

---

knowing $\varphi(n)$ and $e$ we can get $d$ easly (the private key)

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



$$
\begin{aligned}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{aligned}
$$
