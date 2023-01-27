---
sort : 1 
---

# Modular Arithmetic

## Concepts and Definitions

*Modular arithmetic* : is a system of arithmetic for integers, which considers the remainder. 

*Modulo and Modulus* : It is basically an operator which is denoted by `mod` and in programming uses `%` symbol. 
 
<img src="http://latex.codecogs.com/svg.image?x \mod N, \ \ a \rightarrow dividend, N \rightarrow divisor \ (Modulus)"/> 

*congruence operator* : `≡` is the symbol for congruence, which means the values A and B are in the same equivalence class. i.e. `2 ≡ 12 (mod 10)`  ==> `2 mod 10 = 12 mod 10` 

```
if m | a then a ≡ 0 mod m
```

*identity element / neutral element* : The element of a set of numbers that when combined with another number under a particular binary operation leaves the second number unchanged

<img src="http://latex.codecogs.com/svg.image?a + 0 = a"/>

<img src="http://latex.codecogs.com/svg.image?a \times 1 = a"/>

*inverse element* : is another element in the set that, when combined on the right or the left through the binary operation, always gives the identity element as the result.

<img src="http://latex.codecogs.com/svg.image?a + b = 0 \rightarrow 5 + (-5) = 0"/>

<img src="http://latex.codecogs.com/svg.image?a \times b = 1 \rightarrow 5 \times ({1 \over 5}) = 1"/>



*The multiplicative group modulo p*

<img src="http://latex.codecogs.com/svg.image?F_{p} = \left\{ 0,1,...,p-1 \right\}"/> 

under both addition and multiplication there is an inverse element `b` for every element `a` in the set, such that `a + b = 0` and `a * b = 1`.







<br>

---


## Modular arithmetic properties


<img src="http://latex.codecogs.com/svg.image?(a+b) \mod n = [(a \mod n) + (b \mod n)] \mod n;"/>

<img src="http://latex.codecogs.com/svg.image?(a-b) \mod n = [(a \mod n) - (b \mod n)] \mod n;"/>

<img src="http://latex.codecogs.com/svg.image?(a\times b) \mod n = [(a \mod n)\times (b \mod n)] \mod n;"/>

<img  src="http://latex.codecogs.com/svg.image?10^a \mod n = (10 \mod n)^a;"/>


---------------------------------------------
> Properties of addition

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a + b = c, \ then \ a \ (mod\ N) + b \ (mod\ N) \equiv c \ (mod\ N);"/>


<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), \ then \ a + k \equiv b + k \ (mod\ N); \  \text{for any integer} \ k"/>

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N) \ and \ c \equiv d \ (mod\ N), then \ a + c \equiv b + d \ (mod\ N);"/>

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then -a \equiv -b \ (mod\ N);"/>

---------------------------------------------
> Properties of multiplication

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \times b = c, then \ a \ (mod\ N) \times b \ (mod\ N) \equiv c \ (mod\ N);"/>

 What is (8×16)(mod7)?(8×16)(mod7)?

Since 8≡1(mod7)8≡1(mod7) and 16≡2(mod7)16≡2(mod7), we have

(8×16)≡(1×2)≡2(mod7). □(8×16)≡(1×2)≡2(mod7)


<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ ka \equiv kb \ (mod\ N); \  \text{for any integer} \ k"/>

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), and \ c \equiv d \ (mod\ N)\ , then \ \ ac \equiv bd \ (mod\ N);"/>






















---------------------------------------------
> Properties of Exponentiation

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ a^{k} \equiv b^{k} \ (mod\ N); \  \text{for any positive integer} \ k"/>



<details style="dispaly=flex;"><summary>EXAMPLES</summary>

<img  src="http://latex.codecogs.com/svg.image?\text{What is} \ 3 ^{16} \ (mod\ 4) \ ?"/>

<p>we observe that</p>

<img  src="http://latex.codecogs.com/svg.image?3^{2} \equiv 9 \equiv 1 \ (mod\ 4)"/>

<p>so</p>

<img  src="http://latex.codecogs.com/svg.image?3^{16} \ (mod\ 4) \equiv (3^{2})^{8} \ (mod\ 4) \equiv (1)^{8} \ (mod\ 4) \equiv 1 \ (mod\ 4)"/>

</details>






```python
def modinv(a, m):
    gcd, x, y = egcd(a, m)
    if gcd != 1:
        return None  # modular inverse does not exist
    else:
        return x % m

```

<br>

---

## Euler's Phi-Function | Euler's totient Function 

<img  src="http://latex.codecogs.com/svg.image?\varphi(1) = 0;"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(p) = p-1;\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(m \times n) = \varphi(m) \times  \varphi(n);$ $\ \ \ \ \ \ m \ and \ n \ are \ coprimes"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(p^e) = p^e - p^{e-1};\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

<br>

---

## Fermat's Little Theorem 

knwing that <img  src="http://latex.codecogs.com/svg.image?p"/> is a prime number

<img  src="http://latex.codecogs.com/svg.image?a^{p} \equiv a \ (mod \ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-1} \equiv 1 \ (mod \ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-2} \mod p = a^{-1} \mod p"/>


---

## Euler's Theorem 

<img  src="http://latex.codecogs.com/svg.image?a^{\varphi(n)} \equiv 1 \ (mod \ n)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{k \times \varphi(n) + 1} \equiv a \ (mod \ n)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{\varphi(n) - 1} \mod n = a^{-1} \mod n"/>