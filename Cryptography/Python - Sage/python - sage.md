---
sort : 1 
---


<!-- 
## Rquirements

```bash
$ docker pull sagemath/sagemath

$ docker run -it sagemath/sagemath
# OR 
$ docker run -p 8888:8888 sagemath/sagemath-jupyter
``` -->


# Cryptography with Python and Sagemath  

```python
# hex to bytes (ascii)
bytes.fromhex('63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d') # crypto{You_will_be_working_with_hex_strings_a_lot}
```




> base64
```python
from base64 import *

b64encode(bytes.fromhex('72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf')) # b'crypto/Base+64+Encoding+is+Web+Safe/'
```

```python
from Crypto.Util.number import *

# message: HELLO
# ascii bytes: [72, 69, 76, 76, 79]
# hex bytes: [0x48, 0x45, 0x4c, 0x4c, 0x4f]
# base-16: 0x48454c4c4f
# base-10: 310400273487 

bytes_to_long(b'HELLO') 	# 310400273487
long_to_bytes(310400273487) # b'HELLO' 
```






> XOR 

XOR is a bitwise operator which returns 0 if the bits are the same, and 1 otherwise. 
```python
from pwn import *

# xor each char with 10 
xor('ABCD', 10)   # b'KHIN'
xor('ABCD', 0xa)  # b'KHIN'

xor('ABCD', 'A')  # b'\x00\x03\x02\x05'
xor('ABCD', 'AB') # b'\x00\x00\x02\x06'

xor('A', 'A', 'B', 'A', 'B') # b'A'
```


Commutative: A ⊕ B = B ⊕ A

Associative: A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C

Identity: A ⊕ 0 = A

Self-Inverse: A ⊕ A = 0 





> GCD

```python
def Mygcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)

Mygcd(66528, 52920)

# --------------------------------------
import math
math.gcd(66528, 52920)
```

```python
sage: gcd(66528, 52920)
1512 
```


> Extended GCD (XGCD)

The extended Euclidean algorithm is an efficient way to find integers u,v such that

a * u + b * v = gcd(a,b)

```python
sage: xgcd(26513, 32321)
# (1, 10245, -8404) ==> # (gcd(a,b), u,  v)
```





> RSA operations (Factorization / Modular Inverting / euler_phi)

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







# References
* https://cryptohack.org/











