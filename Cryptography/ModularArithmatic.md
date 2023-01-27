---
sort : 1 
---

# Modular Arithmetic

## Concepts and Definitions

*Modular arithmetic* : is a system of arithmetic for integers, which considers the remainder. 

*Modulo and Modulus* : It is basically an operator which is denoted by `mod` and in programming uses `%` symbol. 
 
<img src="https://latex.codecogs.com/svg.image?x \mod N, \ \ a \rightarrow dividend, N \rightarrow divisor \ (Modulus \ | \ Moduli)"/> 

*congruence operator* : `≡` is the symbol for congruence, which means the values A and B are in the same equivalence class. i.e. `2 ≡ 12 (mod 10)`  ==> `2 mod 10 = 12 mod 10` 

```
if m | a then a ≡ 0 mod m
```

*identity element / neutral element* : The element of a set of numbers that when combined with another number under a particular binary operation leaves the second number unchanged

<img src="https://latex.codecogs.com/svg.image?a + 0 = a"/>

<img src="https://latex.codecogs.com/svg.image?a \times 1 = a"/>

*inverse element* : is another element in the set that, when combined on the right or the left through the binary operation, always gives the identity element as the result.

<img src="https://latex.codecogs.com/svg.image?a + b = 0 \rightarrow 5 + (-5) = 0"/>

<img src="https://latex.codecogs.com/svg.image?a \times b = 1 \rightarrow 5 \times ({1 \over 5}) = 1"/>



*The integers modulo p define a field, denoted by*

<img src="https://latex.codecogs.com/svg.image?F_{p} = \left\{ 0,1,...,p-1 \right\}"/> 

under both addition and multiplication there is an inverse element `b` for every element `a` in the set, such that `a + b = 0` and `a * b = 1`.

If the modulus is not prime, the set of integers modulo n define a ring.  <img src="https://latex.codecogs.com/svg.image?F_{n}"/> 







<br>

---


## Modular arithmetic properties


<img src="https://latex.codecogs.com/svg.image?(a+b) \mod n = [(a \mod n) + (b \mod n)] \mod n;"/>

<img src="https://latex.codecogs.com/svg.image?(a-b) \mod n = [(a \mod n) - (b \mod n)] \mod n;"/>

<img src="https://latex.codecogs.com/svg.image?(a\times b) \mod n = [(a \mod n)\times (b \mod n)] \mod n;"/>

<img  src="https://latex.codecogs.com/svg.image?10^a \mod n = (10 \mod n)^a;"/>


---------------------------------------------
> Properties of addition

<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a + b = c, \ then \ a \ (mod\ N) + b \ (mod\ N) \equiv c \ (mod\ N);"/>


<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), \ then \ a + k \equiv b + k \ (mod\ N); \  \text{for any integer} \ k"/>

<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N) \ and \ c \equiv d \ (mod\ N), then \ a + c \equiv b + d \ (mod\ N);"/>

<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then -a \equiv -b \ (mod\ N);"/>

---------------------------------------------
> Properties of multiplication

<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \times b = c, then \ a \ (mod\ N) \times b \ (mod\ N) \equiv c \ (mod\ N);"/>

<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<img  src="https://latex.codecogs.com/svg.image?\text{What is} \ (8 \times 16) \ (mod\ 7) ?"/>

<p> since </p>

<img  src="https://latex.codecogs.com/svg.image?8 \equiv 1 \ (mod\ 7) \ \text{and} \ 16 \equiv 2 \ (mod\ 7)"/>

<p> we have </p>

<img  src="https://latex.codecogs.com/svg.image?(8 \times 16) \equiv (1 \times 2) \equiv 2 \ (mod\ 7)"/>


</div>

</details>





<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ ka \equiv kb \ (mod\ N); \  \text{for any integer} \ k"/>




<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), and \ c \equiv d \ (mod\ N)\ , then \ \ ac \equiv bd \ (mod\ N);"/>






















---------------------------------------------
> Properties of Exponentiation

<img  src="https://latex.codecogs.com/svg.image?\text{If} \ a \equiv b \ (mod\ N), then \ a^{k} \equiv b^{k} \ (mod\ N); \  \text{for any positive integer} \ k"/>



<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<img  src="https://latex.codecogs.com/svg.image?\text{What is} \ 3 ^{16} \ (mod\ 4) \ ?"/>

<p>we observe that</p>

<img  src="https://latex.codecogs.com/svg.image?3^{2} \equiv 9 \equiv 1 \ (mod\ 4)"/>

<p>so</p>

<img  src="https://latex.codecogs.com/svg.image?3^{16} \ (mod\ 4) \equiv (3^{2})^{8} \ (mod\ 4) \equiv (1)^{8} \ (mod\ 4) \equiv 1 \ (mod\ 4)"/>

</div>

</details>


```note
The last digit of a number is equivalent to the number taken modulo 10.
```








---

## Fermat's Little Theorem 

knwing that <img  src="https://latex.codecogs.com/svg.image?p"/> is a prime number

* <img  src="https://latex.codecogs.com/svg.image?a^{p} \equiv a \ (mod \ p)"/>

* <img  src="https://latex.codecogs.com/svg.image?a^{p-1} \equiv 1 \ (mod \ p)"/>

* <img  src="https://latex.codecogs.com/svg.image?a^{-1} \equiv a^{p-2} \ (mod\ p)"/>


<details style="dispaly=flex;"><summary>HOW ?</summary>

<div style="border-style: double; padding: 4px">

<img  src="https://latex.codecogs.com/svg.image?a^{p-1} \equiv 1 \ (mod\ p)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?a^{p-1} \times a^{-1} \equiv a^{-1} \ (mod\ p)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?a^{p-2} \times a \times a^{-1} \equiv a^{-1} \ (mod\ p)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?a^{p-2} \equiv a^{-1} \ (mod\ p)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?a^{p-2} \mod p = a^{-1}"/>

</div>

</details>




---

## Euler's Phi-Function | Euler's totient Function 

* <img  src="https://latex.codecogs.com/svg.image?\varphi(1) = 0;"/>

* <img  src="https://latex.codecogs.com/svg.image?\varphi(p) = p-1;\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

* <img  src="https://latex.codecogs.com/svg.image?\varphi(m \times n) = \varphi(m) \times  \varphi(n);$ $\ \ \ \ \ \ m \ and \ n \ are \ coprimes"/>

* <img  src="https://latex.codecogs.com/svg.image?\varphi(p^e) = p^e - p^{e-1};\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime"/>

<br>


---

## Euler's Theorem 

* <img  src="https://latex.codecogs.com/svg.image?a^{\varphi(n)} \equiv 1 \ (mod \ n)"/>

* <img  src="https://latex.codecogs.com/svg.image?a^{k \times \varphi(n) + 1} \equiv a \ (mod \ n)"/>

* <img  src="https://latex.codecogs.com/svg.image?a^{-1} \equiv a^{\varphi(n) - 1} \ (mod\ n)"/>









---

## Modular Inverse

<img  src="https://latex.codecogs.com/svg.image?\text{A modular inverse of an integer} \ b \ (mod\ n) \ \text{is the integer} \ b^{-1} \text{ such that :}"/>

<img  src="https://latex.codecogs.com/svg.image?b \times b^{-1} \equiv 1 \ (mod\ n)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?\text{So for any element} \ g \ \text{in the field} \ F_{p} \ (not \ F_{n}) \ \text{there exists a unique integer } d \ \text{in the field such that}"/>  

<img  src="https://latex.codecogs.com/svg.image?g \times d \equiv 1 \ (mod\ p)"/>




<details style="dispaly=flex;"><summary>EX1</summary>

<div style="border-style: double; padding: 4px">

<img  src="https://latex.codecogs.com/svg.image?\text{What is the inverse element:} \ 3 \times d \equiv 1 \ (mod\ 13) \ ?"/>

<p>From the third Fermat's Little Theorem</p>

<img  src="https://latex.codecogs.com/svg.image?d \equiv 3^{-1} \equiv 3^{p-2} \ (mod\ p)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{-1} \equiv 3^{13-2} \ (mod\ 13)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{-1} \equiv 9 \ (mod\ 13)"/>

<p>hence</p>

<img  src="https://latex.codecogs.com/svg.image?3 \times 3^{-1} \equiv 1 \ (mod\ 13)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3 \times 9 \equiv 1 \ (mod\ 13)"/>

<p>finally</p>

<img  src="https://latex.codecogs.com/svg.image?d = 9"/>

</div>

</details>


<details style="dispaly=flex;"><summary>EX2</summary>

<div style="border-style: double; padding: 4px">

<img  src="https://latex.codecogs.com/svg.image?\text{What is the inverse element:} \ 3 \times d \equiv 1 \ (mod\ 10) \ ?"/>

<p>Notice that n = 10, which is not a prime number </p>
<p>But since g and n are relatively prime, we will apply the third Euler's Theorem</p>

<img  src="https://latex.codecogs.com/svg.image?d \equiv 3^{-1} \equiv 3^{\varphi(n)-1} \ (mod\ n)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{-1} \equiv 3^{\varphi(10)-1} \ (mod\ 10)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{-1} \equiv 3^{3} \ (mod\ 10) \ \ \ \leftarrow \varphi(10) = \varphi(2) \times \varphi(5) = 4"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{-1} \equiv 7 \ (mod\ 10)"/>

<p>hence</p>

<img  src="https://latex.codecogs.com/svg.image?3 \times 3^{-1} \equiv 1 \ (mod\ 10)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3 \times 7 \equiv 1 \ (mod\ 10)"/>

<p>finally</p>

<img  src="https://latex.codecogs.com/svg.image?d = 7"/>

</div>

</details>

<br>

```python
from Crypto.Util.number import inverse
inverse(3, 13)

#====================================================
def egcd(a, b):
    if a == 0:
        return b, 0, 1
    else:
        gcd, u, v = egcd(b % a, a)
        return gcd, v - (b // a) * u, u

def modinv(a, n):
    gcd, x, y = egcd(a, n)
    if gcd != 1:
        return None  # modular inverse does not exist
    else:
        return x % n

modinv(3, 13)
```



---

## Quadratic Residue

If q and n are coprime integers, then q is called a quadratic residue modulo n if the following congruence has a solution

* <img  src="https://latex.codecogs.com/svg.image?x^{2} \equiv q \ (mod\ n), \ where \ x \in F_{n}"/>

Likewise, if it has no solution, then it is called a quadratic non-residue modulo n. 

```
So the square root of the Quadratic Residue modulo an integer equal ±x  

And the square root of the None Quadratic Residue modulo an integer does not exist !! 
```

if n is a prime number you will find out that exactly half of the integers between 1 and p−1 are squares mod p, that is, the congruence 

* <img  src="https://latex.codecogs.com/svg.image?x^{2} \equiv q \ (mod\ p), \ where \ x \in F_{p}"/>

has a <img  src="https://latex.codecogs.com/svg.image?\frac{p-1}{2}"/> solution



<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<p>Find ALL  quadratic residues mod 5 </p>

<img  src="https://latex.codecogs.com/svg.image?0^{2} \ (mod\ 5)  = 0 \ \leftarrow q"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?1^{2} \ (mod\ 5)  = 1"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?2^{2} \ (mod\ 5)  = 4"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?3^{2} \ (mod\ 5)  = 4"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?4^{2} \ (mod\ 5)  = 1"/>

<p> So the quadratic residues mod 5 are 1,4 and the non-residues are 2,3 </p>

</div>

</details>

<br>


```note
A number that is congruent to 0 mod p is neither a residue nor a non-residue. 
```

> Euler’s criterion

A number `x` is square root of `q` under modulo `p` if 

<img  src="https://latex.codecogs.com/svg.image?x^{2} \equiv q \ (mod\ p)"/>


<br>

>  Properties of quadratic (non-)residues

* <img  src="https://latex.codecogs.com/svg.image?\text{Quadratic Residue} \times \text{Quadratic Residue} = Quadratic Residue"/>

* <img  src="https://latex.codecogs.com/svg.image?\text{Quadratic Residue} \times \text{Quadratic Non-Residue} = Quadratic Non-Residue"/>

* <img  src="https://latex.codecogs.com/svg.image?\text{Quadratic Non-Residue} \times \text{Quadratic Non-Residue} = Quadratic Residue"/>

an easy way to remember this : 

<img  src="https://latex.codecogs.com/svg.image?\text{Quadratic Residue} \leftarrow 1, \ \ \ \text{Quadratic Non-Residue} \leftarrow 0"/>	




<br>

> Legendre symbol

The Legendre Symbol gives an efficient way to determine whether an integer is a quadratic residue modulo an odd prime p


<img  src="https://latex.codecogs.com/svg.image?\frac{q}{p} \equiv q^{(\frac{p-1}{2})} \ (mod\ p)"/>	

Legendre's Symbol obeys:

<img  src="https://latex.codecogs.com/svg.image?\left\{\frac{q}{p} = 1\right\} \ \text{if} \ q \ \text{is a quadratic residue and} \ q \not\equiv 0 \ (mod\ p)"/>	

<img  src="https://latex.codecogs.com/svg.image?\left\{\frac{q}{p} = -1\right\} \ \text{if} \ q \ \text{is a quadratic non-residue mod p}"/>	

<img  src="https://latex.codecogs.com/svg.image?\left\{\frac{q}{p} = 0\right\} \ \text{if} \ q \equiv 0 \ (mod\ p)"/>


Which means given any integer a, calculating `pow(q, (p-1)//2, p)` is enough to determine if q is a quadratic residue.


> Tonelli-Shanks algorithm

is a technique for solving for x in a congruence of the form:

<img  src="https://latex.codecogs.com/svg.image?x^{2} \equiv q \ (mod\ p)"/>

which is also the square roots modulo a prime 

```python
sage: from sage.rings.finite_rings.integer_mod import square_root_mod_prime 

sage: q = ... # the Quadratic Residue
sage: p = ... # the modulus

sage: q = Mod(q, p)

sage: square_root_mod_prime(q, p)
```

```note
Tonelli-Shanks doesn't work for composite (non-prime) moduli,

The main use-case for this algorithm is finding elliptic curve co-ordinates
```




<br>

--- 

## Chinese Remainder Theorem

gives a unique solution to a set of linear congruences if their moduli are coprime.


<img  src="https://latex.codecogs.com/svg.image?x \equiv a_{1} \mod n_{1}"/>

<img  src="https://latex.codecogs.com/svg.image?x \equiv a_{2} \mod n_{2}"/>	

<img  src="https://latex.codecogs.com/svg.image?. \ . \ ."/>

<img  src="https://latex.codecogs.com/svg.image?x \equiv a_{k} \mod n_{k}"/>

There is a unique solution :

<img  src="https://latex.codecogs.com/svg.image?x \equiv a \mod N, \ where \ N = n_{1} \times n_{2} \times ... \times n_{k}"/>



<details style="dispaly=flex;"><summary>EX</summary>

<div style="border-style: double; padding: 4px">

<p>Given the following set of linear congruences: </p>

<img  src="https://latex.codecogs.com/svg.image?x \equiv 2 \ (mod\ 5)"/>

<br>

<img  src="https://latex.codecogs.com/svg.image?x \equiv 3 \ (mod\ 11)"/>	

<br>

<img  src="https://latex.codecogs.com/svg.image?x \equiv 5 \ (mod\ 17)"/>

<p> Find the integer a such that </p>

<img  src="https://latex.codecogs.com/svg.image?x \equiv a \ (mod\ 935)"/>

<p> the Solution </p>

</div>

</details>

<br>


<img  src="https://latex.codecogs.com/svg.image?\text{1. Find} \ N = n_{1} \times n_{2} \times ... \times n_{k}"/>

<img  src="https://latex.codecogs.com/svg.image?\text{2. Find} \ N_{1} = \frac{N}{n_{1}} \ , \ N_{2} = \frac{N}{n_{2}} \ , \ ... \ , \ N_{k} = \frac{N}{n_{k}}"/>

<img  src="https://latex.codecogs.com/svg.image?\text{3. Find the multiplicative inverse of} \ N_{1} \ , \ N_{2} \ , \ ... \ , N_{k} \ \text{using the corresponding moduli} \ n_{1} \ , \ n_{2} \ , \ ... \ , \ n_{k} \ \text{call the inverse} \ N_{1}^{-1} \ , \ N_{2}^{-1} \ , \ ... \ , \ N_{k}^{-1} "/>

<img  src="https://latex.codecogs.com/svg.image?\text{4. } \ x = (a_{1} \times N_{1} \times N_{1}^{-1}) + (a_{2} \times N_{2} \times N_{2}^{-1}) + ... + (a_{k} \times N_{k} \times N_{k}^{-1})"/>
