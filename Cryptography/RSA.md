---
sort : 2
---

# RSA 


## Mathmatics

composite number : 

prime number : 

coprime number / relativly prime number : 

congruence operator :


### mod operation

$(a+b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $+$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(a-b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $-$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(a*b)$ $mod$ $n$ $=$ $[(a$ $mod$ $n)$ $\times$ $(b$ $mod$ $n)]$ $mod$ $n;$

$(10^a)$ $mod$ $n$ $=$ $(10$ $mod$ $a)^n;$

### Euler's Phi-Function | Euler's totient Function 

$\varphi(1) = 0;$

$\varphi(p) = p-1;$ $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime$

$\varphi(m \times n) = \varphi(m) \times \varphi(n);$ $\ \ \ \ \ \ m \ and \ n \ are \ coprimes$

$\varphi(p^e) = p^e - p^{e-1};$	$\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ p \ is \ prime$






---


## Rquirements

```bash
$ docker pull sagemath/sagemath

$ docker run -it sagemath/sagemath
# OR 
$ docker run -p 8888:8888 sagemath/sagemath-jupyter
```