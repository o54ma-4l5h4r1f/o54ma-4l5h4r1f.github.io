---
sort : 1 
---


<!-- 

from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad
import hashlib
import os
from secret import shared_secret

FLAG = b'crypto{????????????????????????????}'


def encrypt_flag(shared_secret: int):
    # Derive AES key from shared secret
    sha1 = hashlib.sha1()
    sha1.update(str(shared_secret).encode('ascii'))
    key = sha1.digest()[:16]
    # Encrypt flag
    iv = os.urandom(16)
    cipher = AES.new(key, AES.MODE_CBC, iv)
    ciphertext = cipher.encrypt(pad(FLAG, 16))
    # Prepare data to send
    data = {}
    data['iv'] = iv.hex()
    data['encrypted_flag'] = ciphertext.hex()
    return data


print(encrypt_flag(shared_secret))

----------------------------------------------------------------------------

from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad
import hashlib


def is_pkcs7_padded(message):
    padding = message[-message[-1]:]
    return all(padding[i] == len(padding) for i in range(0, len(padding)))


def decrypt_flag(shared_secret: int, iv: str, ciphertext: str):
    # Derive AES key from shared secret
    sha1 = hashlib.sha1()
    sha1.update(str(shared_secret).encode('ascii'))
    key = sha1.digest()[:16]
    # Decrypt flag
    ciphertext = bytes.fromhex(ciphertext)
    iv = bytes.fromhex(iv)
    cipher = AES.new(key, AES.MODE_CBC, iv)
    plaintext = cipher.decrypt(ciphertext)

    if is_pkcs7_padded(plaintext):
        return unpad(plaintext, 16).decode('ascii')
    else:
        return plaintext.decode('ascii')


shared_secret = ?
iv = ?
ciphertext = ?

print(decrypt_flag(shared_secret, iv, ciphertext))





-->



# Cryptography with Python and Sagemath 

> HELP !!

```python
# to know more about any build-function
help(bin)
help(int)
help(hex)

help(bytes)

from Crypto.Util.number import *
help(long_to_bytes)

# And So On 
```

> Radix/Base representation of numbers

```python
# base10 --> bin  
bin(ord('A'))                   # 0b1000001
bin(10)                         # '0b1010'

# base10 --> hex 
hex(ord('A'))                   # '0x41'
hex(10)                         # '0xa'

# bin --> base10
print(0b1000001)                # 65
int('0b1000001', 2)             # 65 

# hex --> base10
print(0x41)                     # 65
int('0x41', 16)                 # 65
```






> Strings - Bytes

```python
S = 'AAAAAA'
B = b'AAAAAA'

print(S.encode())               # b'AAAAAA'
print(B.decode())               #  'AAAAAA'
```





> Long/Numbers - Bytes

```python
# hex[2:] to bytes
bytes.fromhex('41')             # b'A'


from Crypto.Util.number import *

# hex to bytes
long_to_bytes(int('41', 16))    # b'A'
long_to_bytes(int('0x41', 16))  # b'A'

# long to bytes
long_to_bytes(65)               # b'A'
# bytes to long 
bytes_to_long(b'A')             # 65

# bytes to hex
b'AAA'.hex()                    # '414141'

# bytes to hex as bytes ^^
import codecs
codecs.encode(b'AAA', 'hex')    # b'414141'
```


> base64

```python
from base64 import *
b64encode(b'A')                 # b'QQ=='

import codecs
codecs.encode(b'A', 'base64')   # b'QQ==\n'
```



> ROT13 

```python
import codecs

codecs.encode('AAA', 'rot_13')  # 'NNN'
```




> XOR 

```python
from pwn import *

# xor each char with Number/Char/Str
xor('ABCD', 10)                 # b'KHIN'
xor('ABCD', 0xa)                # b'KHIN'

xor('ABCD', 'A')                # b'\x00\x03\x02\x05'
xor('ABCD', 'AB')               # b'\x00\x00\x02\x06'

xor('A', 'A', 'B', 'A', 'B')    # b'A'
```






> GCD

```python
def Mygcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)

Mygcd(16, 6)

# OR
import math
math.gcd(16, 6)
```

```python
sage: gcd(16, 6)
2 
```



> Extended GCD (XGCD)

<span> $$ a \times u + b \times v = \gcd(a,b) $$ </span> 

```python
sage: xgcd(26513, 32321)
# (1, 10245, -8404) ==> # (gcd(a,b), u,  v)
```









> Hashing

```python
import hashlib 

M = b'13371337'
D = hashlib.sha256(M).digest()
# b'\xac?\xbb4t\x80\x123\xa38\xe0\xf2z\xf3Gws\xad\x87r\xd3\\\x87\xf7\r\x94\x89\x83{\xab\xb3Z'
H = hashlib.sha256(M).hexdigest()
# 0xac3fbb3474801233a338e0f27af3477773ad8772d35c87f70d9489837babb35a

print(hashlib.algorithms_available)
# {'sha224', 'sha3_224', 'sha3_384', 'sha3_512', 'sha512', 'md4', 'sha1', 'sm3', 'sha512_256', 'sha384', 'ripemd160', 'blake2b', 'shake_128', 'md5-sha1', 'shake_256', 'blake2s', 'whirlpool', 'md5', 'sha3_256', 'sha512_224', 'sha256'}
```



















> RSA operations (Factorization / Modular Inverting / euler_phi)

```bash
$ factordb 16
# 2 2 2 2
```

```python
n = 882564595536224140639625987659416029426239230804614613279163
e = 65537
c = 77578995801157823671636298847186723593814843845525223303932 

# ----------------------
# factordb API 
from factordb.factordb import FactorDB
f = FactorDB(n)
f.connect()

print(f.get_factor_list())
# [857504083339712752489993810777, 1029224947942998075080348647219]

p, q = 857504083339712752489993810777, 1029224947942998075080348647219

# ----------------------

phi = (p-1) * (q-1)
# 882564595536224140639625987657529300394956519977044270821168

# ----------------------

from Crypto.Util.number import inverse
print(inverse(e, phi))
# 121832886702415731577073962957377780195510499965398469843281

# ----------------------

p = pow(c, d, n)
# 13371337
```

```python
n = 882564595536224140639625987659416029426239230804614613279163
e = 3
c = 44558912828464771189852064661426808927281111089587712743 

from gmpy2 import iroot
print(bytes.fromhex(hex(iroot(c, 3)[0])[2:]))
# b'13371337'
```

using sagemath


```python
sage: n = 882564595536224140639625987659416029426239230804614613279163
sage: e = 65537
sage: c = 77578995801157823671636298847186723593814843845525223303932 

# ----------------------
# check http://factordb.com/
sage: factor(n)
# 857504083339712752489993810777 * 1029224947942998075080348647219

sage: p, q = 857504083339712752489993810777, 1029224947942998075080348647219

# ----------------------

phi = (p-1) * (q-1)
# 882564595536224140639625987657529300394956519977044270821168

# OR 

sage: phi = euler_phi(n)
# 882564595536224140639625987657529300394956519977044270821168

# ----------------------

sage: inverse_mod(e, phi)
121832886702415731577073962957377780195510499965398469843281

# ----------------------

sage: p = pow(c, d, n)
# 13371337
```


```python
sage: n = 882564595536224140639625987659416029426239230804614613279163
sage: e = 3
sage: c = 44558912828464771189852064661426808927281111089587712743 

sage: c.nth_root(3, True)
# (3545233643812369207, True)       # it has to be True !! 

sage: bytes.fromhex(hex(c.nth_root(3, True)[0])[2:])
# b'13371337'
```













