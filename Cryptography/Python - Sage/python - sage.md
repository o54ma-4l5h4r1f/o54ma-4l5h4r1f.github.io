---
sort : 1 
---

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

The Greatest Common Divisor (GCD), sometimes known as the highest common factor, is the largest number which divides two positive integers (a,b).

For a = 12, b = 8 we can calculate the divisors of a: {1,2,3,4,6,12} and the divisors of b: {1,2,4,8}. Comparing these two, we see that gcd(a,b) = 4.

Now imagine we take a = 11, b = 17. Both a and b are prime numbers. As a prime number has only itself and 1 as divisors, gcd(a,b) = 1.

We say that for any two integers a,b, if gcd(a,b) = 1 then a and b are coprime integers.

If a and b are prime, they are also coprime. If a is prime and b < a then a and b are coprime.

Think about the case for a prime and b > a, why are these not necessarily coprime?

There are many tools to calculate the GCD of two integers, but for this task we recommend looking up Euclid's Algorithm.

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








> The Extended Euclidean Algorithm for finding the inverse of a number mod n.














> 


Calculate the following integers:

11 ≡ x (mod 6)
8146798528947 ≡ y (mod 17) 		# sage: mod(8146798528947,17) # ===> 4 = y 



 
The integers modulo p define a field, denoted Fp.  ==> A finite field Fp is the set of integers {0,1,...,p-1}


modulus ?? 

identity ?? 






> Modular Inverting

sage :          inverse_mod(3, 13)



# References
* https://cryptohack.org/