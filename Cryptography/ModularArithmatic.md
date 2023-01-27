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



*The integers modulo p define a field, denoted by*

<img src="http://latex.codecogs.com/svg.image?F_{p} = \left\{ 0,1,...,p-1 \right\}"/> 

under both addition and multiplication there is an inverse element `b` for every element `a` in the set, such that `a + b = 0` and `a * b = 1`.

If the modulus is not prime, the set of integers modulo n define a ring.  <img src="http://latex.codecogs.com/svg.image?F_{n}"/> 







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

<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<img  src="http://latex.codecogs.com/svg.image?\text{What is} \ (8 \times 16) \ (mod\ 7) ?"/>

<p> since </p>

<img  src="http://latex.codecogs.com/svg.image?8 \equiv 1 \ (mod\ 7) \ \text{and} \ 16 \equiv 2 \ (mod\ 7)"/>

<p> we have </p>

<img  src="http://latex.codecogs.com/svg.image?(8 \times 16) \equiv (1 \times 2) \equiv 2 \ (mod\ 7)"/>


</div>

</details>





<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ ka \equiv kb \ (mod\ N); \  \text{for any integer} \ k"/>




<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), and \ c \equiv d \ (mod\ N)\ , then \ \ ac \equiv bd \ (mod\ N);"/>






















---------------------------------------------
> Properties of Exponentiation

<img  src="http://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ a^{k} \equiv b^{k} \ (mod\ N); \  \text{for any positive integer} \ k"/>



<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<img  src="http://latex.codecogs.com/svg.image?\text{What is} \ 3 ^{16} \ (mod\ 4) \ ?"/>

<p>we observe that</p>

<img  src="http://latex.codecogs.com/svg.image?3^{2} \equiv 9 \equiv 1 \ (mod\ 4)"/>

<p>so</p>

<img  src="http://latex.codecogs.com/svg.image?3^{16} \ (mod\ 4) \equiv (3^{2})^{8} \ (mod\ 4) \equiv (1)^{8} \ (mod\ 4) \equiv 1 \ (mod\ 4)"/>

</div>

</details>


```note
The last digit of a number is equivalent to the number taken modulo 10.
```








---

## Fermat's Little Theorem 

knwing that <img  src="http://latex.codecogs.com/svg.image?p"/> is a prime number

1. <img  src="http://latex.codecogs.com/svg.image?a^{p} \equiv a \ (mod \ p)"/>

2. <img  src="http://latex.codecogs.com/svg.image?a^{p-1} \equiv 1 \ (mod \ p)"/>

3. <img  src="http://latex.codecogs.com/svg.image?a^{-1} \equiv a^{p-2} \ (mod\ p)"/>


<details style="dispaly=flex;"><summary>HOW ?</summary>

<div style="border-style: double; padding: 4px">

<img  src="http://latex.codecogs.com/svg.image?a^{p-1} \equiv 1 \ (mod\ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-1} \times a^{-1} \equiv a^{-1} \ (mod\ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-2} \times a \times a^{-1} \equiv a^{-1} \ (mod\ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-2} \equiv a^{-1} \ (mod\ p)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{p-2} \mod p = a^{-1}"/>

</div>

</details>


---

## Bézout's_identity ??????????????








---

## Modular Inverse

<img  src="http://latex.codecogs.com/svg.image?\text{A modular inverse of an integer} \ b \ (mod\ n) \ \text{is the integer} \ b^{-1} \text{ such that :}"/>

<img  src="http://latex.codecogs.com/svg.image?b \times b^{-1} \equiv 1 \ (mod\ n)"/>


<img  src="http://latex.codecogs.com/svg.image?\text{So for any element} \ g \ \text{in the field} \ F_{p} \ \text{there exists a unique integer } d \ \text{in the field such that}"/>  

<img  src="http://latex.codecogs.com/svg.image?g \times d \equiv 1 \ (mod\ p)"/>




<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<img  src="http://latex.codecogs.com/svg.image?\text{What is the inverse element:} \ 3 \times d \equiv 1 \ (mod\ 13) \ ?"/>

<p>From the third Fermat's Little Theorem</p>

<img  src="http://latex.codecogs.com/svg.image?d \equiv 3^{-1} \equiv 3^{p-2} \ (mod\ p)"/>

<img  src="http://latex.codecogs.com/svg.image?3^{-1} \equiv 3^{13-2} \ (mod\ 13)"/>

<img  src="http://latex.codecogs.com/svg.image?3^{-1} \equiv 9 \ (mod\ 13)"/>

<p>hence</p>

<img  src="http://latex.codecogs.com/svg.image?3 \times 3^{-1} \equiv 1 \ (mod\ 13)"/>

<img  src="http://latex.codecogs.com/svg.image?3 \times 9 \equiv 1 \ (mod\ 13)"/>

<p>finally</p>

<img  src="http://latex.codecogs.com/svg.image?d = 9"/>

</div>

</details>






>>> from Crypto.Util.number import inverse
>>> inverse(3, 13)



```python
def modinv(a, m):
    gcd, x, y = egcd(a, m)
    if gcd != 1:
        return None  # modular inverse does not exist
    else:
        return x % m

```













---

## Euler's Phi-Function | Euler's totient Function 

<img  src="http://latex.codecogs.com/svg.image?\varphi(1) = 0;"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(p) = p-1;\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(m \times n) = \varphi(m) \times  \varphi(n);$ $\ \ \ \ \ \ m \ and \ n \ are \ coprimes"/>

<img  src="http://latex.codecogs.com/svg.image?\varphi(p^e) = p^e - p^{e-1};\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

<br>


---

## Euler's Theorem 

<img  src="http://latex.codecogs.com/svg.image?a^{\varphi(n)} \equiv 1 \ (mod \ n)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{k \times \varphi(n) + 1} \equiv a \ (mod \ n)"/>

<img  src="http://latex.codecogs.com/svg.image?a^{\varphi(n) - 1} \mod n = a^{-1} \mod n"/>













