---
sort : 1
---

# Mathematics Of Cryptography

## Concepts and Definitions

*_gcd_* : Greatest common divisor of two numbers is the greatest common factor number that divides them

*_lcm_* : Least common multiple of two numbers is the lowest number that can be divisible by both numbers

_*composite number*_ : have more than two factors

*_prime number_* : only divisible by 1 and it self

*_coprime numbers / relativly prime numbers_* : do not have any common factor other than 1 `gcd(num1, num2) = 1`

_*congruence operator*_ : `≡` is the symbol for congruence, which means the values A and B are in the same equivalence class. i.e. `2 ≡ 12 (mod 10)`  ==> `2 mod 10 = 12 mod 10` 

*_number factorization_* : breaking down a number as the multiplication of prime numbers 


<br>

---

## Integer Factorization

![https://en.wikipedia.org/wiki/Integer_factorization](https://en.wikipedia.org/wiki/File:PrimeDecompositionExample.svg)



<br>

---

## GCD & LCM

<img src="http://latex.codecogs.com/svg.image?\text{let} \ a = p_1^{x_1} \times p_2^{x_2} \times ... \times p_k^{x_k}"/>

<img src="http://latex.codecogs.com/svg.image?\text{and} \ b = p_1^{y_1} \times p_2^{y_2} \times ... \times p_k^{y_k}"/>

<br>

<img src="http://latex.codecogs.com/svg.image?\text{then} \ \gcd(a, b) = p_1^{min(x1, y1)} \times p_2^{min(x_2, y_2)} \times ... \times p_k^{min(x_k, y_k)}"/>

<img src="http://latex.codecogs.com/svg.image?\text{and } \ \text{lcm}(a, b) = p_1^{max(x_1, y_1)} \times p_2^{max(x_2, y_2)} \times ... \times p_k^{max(x_k, y_k)}"/>






<br>

---

## Primality Test

given a number <img src="http://latex.codecogs.com/svg.image?n"/> how can we determain if it's prime or not

> Divisibility test

check whether <img src="http://latex.codecogs.com/svg.image?n"/> is divisible by any prime number between 2 and <img src="http://latex.codecogs.com/svg.image?\sqrt{n}"/>

```cpp
// https://en.wikipedia.org/wiki/Primality_test
bool IsPrime(int n)
{
    if (n == 2 || n == 3)
        return true;

    if (n <= 1 || n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i += 6)
    {
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    }

    return true;
}
```

> [For More](https://en.wikipedia.org/wiki/Primality_test)





<br>

---

## mod operation

<img src="http://latex.codecogs.com/svg.image?(a+b) \mod n = [(a \mod n) + (b \mod n)] \mod n;"/>

<img src="http://latex.codecogs.com/svg.image?(a-b) \mod n = [(a \mod n) - (b \mod n)] \mod n;"/>

<img src="http://latex.codecogs.com/svg.image?(a\times b) \mod n = [(a \mod n)\times (b \mod n)] \mod n;"/>

<img  src="http://latex.codecogs.com/svg.image?10^a \mod n = (10 \mod n)^a;"/>


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