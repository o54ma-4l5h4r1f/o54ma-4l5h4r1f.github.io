---
sort : 3
---

<style>
span {
	markdown: "1";
}
</style>

# RSA 

The most common Public-Key/Asymmetric-Key algorithm.

In RSA, modular exponentiation, together with the problem of prime factorisation, helps us to build a `trapdoor function`.

The private key is the secret piece of information or "trapdoor" which allows us to quickly invert the encryption function

In RSA the private key is the `modular multiplicative inverse` of the exponent `e` modulo the `totient of N`

## RSA Key Generation, Encryption, and Decryption 

> Key Generation

<span> $$ \text{Select two large primes} \ p \ \text{and} \ q \ \text{such that} \ p \ \neq \ q $$ </span>

<span> $$ n \gets p \times q $$ </span>

<span> $$ \varphi(n) \gets (p-1) \times (q-1) $$ </span>

<span> $$ \text{Select} \ e \ \text{such that} \ 1 < e < \varphi(n) \ \text{and} \ e \ \text{is coprime to} \ \varphi(n) \text{ so that there is a modular inverse } $$ </span>

The most common value for e is `0x10001` or `65537`


<span> $$ d \gets e^{-1} \mod  \varphi(n) \ \ \ \ \ \ \ \ \text{ or by solving } \ \ \ \ \ \ d \times e \equiv 1 \mod \varphi(n)   $$ </span>

<span> $$ PublicKey \gets (e, \ n) $$ </span>

<span> $$ PrivateKey \gets d $$ </span>

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
it's recommended using primes that are at least 1024 bits long, multiplying two such 1024 primes gives you a modulus that is 2048 bits large. RSA with a 2048-bit modulus is called `RSA-2048`. 
```

---

<span> $$ P \gets PlainText $$ </span>

<span> $$ C \gets CipherText $$ </span>

---


> Enccryption

<span> $$ C = P^e \mod n $$ </span>




<br>

> Exponential Complexity

<span> $$ \text{without having} \ d \ \text{it's hard to find} \ P $$ </span>

<span> $$ P = \sqrt[e]{C} \mod n $$ </span>




<br>

> Decryption

<span> $$ P = C^d \mod n $$ </span>

How ?? 

<span> $$ C^d \equiv (P^{e})^{d} \equiv P^{ed} \equiv P \mod n $$ </span>



<br>
<br>



---

## RSA Digital Signature

> Signing 

* <span> $$ \text{Encrypt the Messsage } (M) \text{ with the reciver Public Key } (e_{0}, N_{0}) $$ </span>

<span> $$ C = M^{e_{0}} \mod N_{0} $$ </span>

* <span> $$ \text{Calculate the hash/digest of the message: } H(M) \text{ and encrypt it with my Private Key (sender)} $$ </span>

<span> $$ S = H(M)^{d_{1}} \mod N_{1} $$ </span>

<br>

> Verifying

* <span> $$ \text{The receiver can decrypt the message using their Private Key}  $$ </span>

<span> $$ m = C^{d_{0}} \mod N_{0} $$ </span>

* <span> $$ \text{calculate the hash/digest of the received message: } H(M) \text{ and compare it to } s \text{ which calculated using the sender Public Key} $$ </span>

<span> $$ s = S^{e_{1}} \mod N_{1} $$ </span>

* <span> $$ \text{assert } H(m) == s $$ </span>



<br><br>

---

## Security of RSA 

### 1. Factorizable modulus (n) 

```note
RSA relies on the difficulty of the factorisation of the modulus N
```

> Example

```python
n = 3035587984187658979049949373626692753001568649909
e = 65537
c = 2325265045258945866725599932004757358522079216082
```


---



<span> $$ Factors(n) = 101^5 \times 523^2 \times 58749233^2 \times 553113283^2 $$ </span>

<span> $$ \varphi(n) = \varphi(101^5) \times \varphi(523^2) \times \varphi(58749233^2) \times \varphi(553113283^2) $$ </span>

<span> $$ \varphi(n) = (101^5 - 101^{5-1}) \times (523^2 - 523^{2-1}) \times (58749233^2 - 58749233^{2-1}) \times (553113283^2 - 553113283^{2-1})  $$ </span>

<span> $$ \varphi(n) = 2999785884764688112542820667580382134861795321600 $$ </span>

<span> $$ d = e^{-1} \mod \varphi(n) $$ </span>

<span> $$ m = c^{d} \mod n $$ </span>

---



> Using sagemath

```python
sage: factor(n)
# 101^5 * 523^2 * 58749233^2 * 553113283^2

sage: euler_phi(n)
# 2999785884764688112542820667580382134861795321600

sage: d = pow(e, -1, euler_phi(n))
# OR
sage: d = inverse_mod(e, phi)
# 1806545147014552244164976213559707067743798735873

sage: m = pow(c, d, n)
# 3545233643812369207

sage: bytes.fromhex(hex(m)[2:])
# b'13371337'
```


<br>



### 2. Small exponent (e) 

> Example
```python
n = 882564595536224140639625987659416029426239230804614613279163
e = 3
c = 44558912828464771189852064661426808927281111089587712743 
```

---

<span> $$ \text{Since } \ c = p^{e} \mod n $$ </span>

<span> $$ \text{So } \ p = \sqrt[e]{c} \mod n $$ </span>



---


> Using sagemath

```python

sage: c.nth_root(3, True)
# (3545233643812369207, True)       # it has to be True !! 

sage: bytes.fromhex(hex(c.nth_root(3, True)[0])[2:])
# b'13371337'
```


### 3. Small private key (d)

> Wiener's theorem

<span> $$ \text{Let } n = pq \text{ with } q < p < 2q. \ \text{ Let } d < \frac{1}{3} n^{\frac{1}{4}} $$ </span>

<span> $$ \text{Given } n \text{ and } e  \text{ with } ed \equiv 1 \ (mod\ \varphi(n)) \text{ , the attacker can efficiently recover d d }$$ </span>

> Example

```python
n = 0x98020da1cd75a815cb2ea78731feddaf930540cd6089807fa2ce5c38450fbcdd7948cc3950fb6cfb7d53360f09693546f574340a6fb229539f62a0d6c93cf7ab26817f01ece66b909b76eba0366877b64be776c850ca11b04dd5f869e59b415ab34c9d4fd00065b38ca3da4043c9b737c17be29e8214d62c6ea27dcfdceeda19be3dceef8b514f429659a4201d5f767235082b416f69101fd0cc7ccb4a8b4304ba8715eb70beba8b99a0a78c75a047345d606a69ba30970ed2fc4a4117c975d2016095efee91d8f29b2a97ad80b48212955049c49cc8bb7d64c1304be6cb710798fa0e9a68006efd3619a5cca4a152f072136040f291dfbb15615be354a2226d
e = 0x834730dff6696bd9560b1c3b590b6f0ce57873e0419f8c39fc57129b8d45795616ab9e19495ba3cf4021e43f7be831d986e5dc374f8310eb98b41da2db62dfa70baf7e6b0b812850f1f0f8a4e943deabd1ce78b36173626576ea740f8216184c0472be520b978081ced49172cd3ce0a6b0c1389bcf8127efd42a20c00ed754da90d4feddbf3923963f289c090eb6e9174377a86b8f02c49e818db55e99f4e92befd28eaef8ec56f4eb7ea688256ed6ae20ac370cbb6890bc6508c14445581802235cae1365a4d348d462d01ab12287caca602580b5bed3aaf29d10c78638c5d838c9111a7f1ff0cd479086b65d97f8f9e30db5e7642b94d32799dddccc067373
c = 0xe21de316dde3f855ee12d699f7c83374ad8b886c1d5563e0ab3ff4fc212101962db8adee80ef2ca146bdcdb181e70fc0b89174d9ce74608a9d64d4e1d422207a89c8951a0dbdc73a76117cbe16a2b08e5c3a1ab0f31d6befa9bf6df6a4aa3354fecb6b751e61394c27e0f7d4f022bd56b0948119084fec178c716293b106ba8bb1bc07a045f4eb3d44bbdf27955f5b4446e04c37e54fa7fda10b6ab6b1a736865fb189985e80736dd507e91b10edcc5d6197b6f1cf37692913b52fb772997d5a417c852a31521fabcdcee209355bc14b9bea49f6dbb50a96bd97803486559d896e2274506d8aaf2ce5159217f302c0a3fa1e86b5409c68b8982627cfa50e572
```
Big Thanks to [orisano](https://github.com/orisano/owiener) 

```python
from Crypto.Util.number import *
import owiener

d = owiener.attack(e, n)

long_to_bytes(pow(c, d, N))
# b'13371337'
```


### Encryption with multiple different exponents

> Example

```python
n = 21068309492183809789891952276557604449981629795930147243582403378665878487879254152133466782955676270709173380248244745757959383636842986220258252114469226878147550354975386522434762471514228133076204045847317982761324736433177120622266373049928404638470748357179536706098889074434169289046193593808252250331821544151318049451392028296091565444896477098766588798017317367072459718236488638954923592271664639581309312438878187988755290853044507211345148418959934057551058963743797490797782707797177396538960266033836461616412903292917845823772764906008193494662258552245781674964109957701949719906413325250654484076397

# the receiver private key, where he expect to decrypt the message with
d =  19602718711786995946839670200343769231899229773963234792852400830436058080685737212395967735646600052417778878813150862975553462859261357915969722407740734494647013527407252687261042555930155531970043949336676319526680497706978873938455512089942082457919485074447926961327159588947415580625582388013482547579474088509449256221453170334623047864325209173600307690519092701672368375939732215641929253869633928127857413467181885211793148220486335471982852044132533882366032988688974831546213660980672648176350845470613278989917877353300088081498041957314715085077511568239085729640151310505216113844471467154269887107777
# the receiver public exponent used in generating (d)
e = 0x10001

# but these are the exponents that used for encryption instead !! 
exponents = [110059, 94603, 83243, 71237, 110731]

c5 = 10233787827865692277934634962907296044097817679155019239740226585598320947392719245121573980234599498872785686931195627011035378353300181235509314890665220769412705527800863926831076117303941626475601421989803666372985919958904956893709001136051149258456600903782963070615351639057903447626626643417786754138827115608819080134688350171254157270112771284801449923977489391574731612848906889660334934772180429038668005323892636972282704204235647148555338635816410764913020447266754435149012266377493361008407290358720418021346452628408371946471843322466974149740998323156526380754314565414967513057673996836357836230639
```



<span> $$ C_{1} = P^{e_{1}} \mod n \ \ \ \ \ \ \ \ \ $$ </span>
<span> $$ C_{2} = C_{1}^{e_{2}} \mod n \ \ \ \ \ \ \ \ \  $$ </span>
<span> $$ C_{3} = C_{2}^{e_{3}} \mod n \ \ \ \ \ \ \ \ \ \text{.....} $$ </span>

<span> $$ \text{So } \  C_{5} = P^{e_{1} \times e_{2} \times e_{3} \times e_{4} \times e_{5}} \mod n \ \ \ \ \ \ \ \ \  $$ </span>

<span> $$ \text{Assume that } E = e_{1} \times e_{2} \times e_{3} \times e_{4} \times e_{5} $$ </span>

<span> $$ \text{And we know that }\  e \times d \equiv 1 \ (mod\ \varphi(n)) \ \ \ \text{ So we can find the inverse of the equation } \ $$ </span>
<span> $$ C^d \equiv (P^{e})^{d} \equiv P^{ed} \equiv P \mod n $$ </span>



<span> $$ \text{From that } \ C_{5}^d \equiv (P^{e_{1} \times e_{2} \times e_{3} \times e_{4} \times e_{5}})^{d} \equiv P^{Ed} \equiv P \mod n $$ </span>

<span> $$ \text{So we need just to find a proper value of } d \text{ that allow as to inverse the equation, and lets call it } D $$ </span>


<span> $$ D \times E \equiv 1 \ (mod\ \varphi(n)) \ \ \rightarrow \ \ $$ </span>
<span> $$ D = E^{-1} \mod \varphi(n) $$ </span>

<span> $$ P = C_{5}^{D} \mod n $$ </span>

---

<span> $$ \text{But how  can we find } \varphi(n) \text{ ?? } $$ </span>

<span> $$ \text{From the relation } \ ed - 1 = k \varphi(n) \ \text{ we can decode the message without computing } \varphi(n) \text{ or factoring } n $$ </span>

[How ??](https://crypto.stackexchange.com/questions/5889/calculating-rsa-private-exponent-when-given-public-exponent-and-the-modulus-fact) 



<!-- How ?? 

<span> $$ \text{From the second Euler's Theorem } $$ </span>

<span> $$ a^{k \times \varphi(n) + 1} \equiv a \ (mod \ n) $$ </span>

<span> $$ \log_{a}{(a^{k \times \varphi(n) + 1})} \equiv \log_{a}{(a)} \ (mod \ n) $$ </span>

<span> $$ k \times \varphi(n) + 1 \equiv 1 \ (mod \ n) $$ </span>

<span> $$ k \times \varphi(n) + 1 \equiv 1 \equiv e \times d \ (mod \ n) $$ </span>

<span> $$ ed - 1 = k \times \varphi(n) $$ </span> -->

```note
Am not a mathematician, so correct me if my derivation were wrong ^^ 
```

```python
from Crypto.Util.number import *
from factordb.factordb import FactorDB

exponents = [106979, 108533, 69557, 97117, 103231]

E = 1
for e in exponents:
	E *= e

D = pow(E, -1, e*d-1)

print(long_to_bytes(pow(c5, D, n)))
```




<!-- ### e | p-1  and  e | q-1

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

--- -->

<!-- https://hackmd.io/fmdfFQ2iS6yoVpbR3KCiqQ?view#cryptobaby-rsa -->

---




<!-- https://raw.githubusercontent.com/mimoo/RSA-and-LLL-attacks/master/boneh_durfee.sage -->


## References

* https://mathsci.kaist.ac.kr/cms/wp-content/uploads/2017/11/NumberTheory_Sage.pdf