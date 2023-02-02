---
sort : 1
---

<style>
span {
	markdown: "1";
}
</style>


# Mathematics Of Cryptography

## Concepts and Definitions

*gcd* : Greatest common divisor and sometimes known as the highest common factor of two numbers is the greatest common factor number that divides them both without a remainder

*lcm* : Least common multiple of two numbers is the lowest number that can be divisible by both numbers

*composite number* : have more than two factors

*prime number* : only divisible by 1 and it self

*coprime numbers / relativly prime numbers* : do not have any common factor other than 1 `gcd(num1, num2) = 1`

*number factorization* : breaking down a number as the multiplication of prime numbers 

*dividend vs divisor vs qoutient*

<span> $$ \frac{24 \ \leftarrow  \ dividend}{6 \ \leftarrow \ divisor} = 4 \ \leftarrow \ qoutient $$ </span>

*a divides b* - without a remainder -

<span> $$ a \ \vert \ b, \ \ a \rightarrow divisor, \ b \rightarrow dividend $$ </span>

*a does not divides b* 

<span> $$ a \not\vert \ b, \ \ a \rightarrow divisor, \ b \rightarrow dividend $$ </span>


<br>

---

## Integer Factorization

By the fundamental theorem of arithmetic, every positive integer has a unique prime factorization.  

<span> $$ n = p_1^{e_1} \times p_2^{e_2} \times ... \times p_k^{e_k} $$ </span>



<br>

---

## GCD & LCM

<span> $$ \text{let} \ a = p_1^{x_1} \times p_2^{x_2} \times ... \times p_k^{x_k} $$ </span>

<span> $$ \text{and} \ b = p_1^{y_1} \times p_2^{y_2} \times ... \times p_k^{y_k} $$ </span>

<br>

<span> $$ \text{then} \ \gcd(a, b) = p_1^{min(x1, y1)} \times p_2^{min(x_2, y_2)} \times ... \times p_k^{min(x_k, y_k)} $$ </span>

<span> $$ \text{and } \ \text{lcm}(a, b) = p_1^{max(x_1, y_1)} \times p_2^{max(x_2, y_2)} \times ... \times p_k^{max(x_k, y_k)} $$ </span>


```note
if gcd(a,b) = x, then x <= a OR x <= b  
```


```note
We say that for any two integers a,b, if gcd(a,b) = 1 then a and b are coprime integers.

If a and b are prime, they are also coprime. 

If a is prime and b < a then a and b are coprime.
```


<span> $$ \text{lcm}(a, b) = \frac{|a \ . \ b|}{\text{gcd}(a, b)} $$ </span>


<br>

> Euclidean Algorithm / Euclid's Algorithm

is an efficient method for computing the greatest common divisor (GCD) of two integers (numbers)

```python
def gcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)
```

<br>

>  Extended Euclidean algorithm  -->  (Bézout's identity or Bézout's lemma)

is an efficient way to find integers <span> $$ u, v $$ </span> such that

<span> $$ a \times u + b \times v = \gcd(a,b) $$ </span>


```note
this algorithm used in modular inverse arithmatic.
```

```python
def egcd(a, b):
    if a == 0:
        return b, 0, 1
    else:
        gcd, u, v = egcd(b % a, a)
        return gcd, v - (b // a) * u, u

# returns gcd, u, v 
```












<br>

---

## Primality Test

given a number <span> $$ n $$ </span> how can we determain if it's prime or not

> Divisibility test

check whether <span> $$ n $$ </span> is divisible by any prime number between 2 and <span> $$ \sqrt{n} $$ </span>

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

## XOR 

```note
xor properties:

Commutative: A ⊕ B = B ⊕ A
Associative: A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C
Identity: A ⊕ 0 = A
Self-Inverse: A ⊕ A = 0 
```
