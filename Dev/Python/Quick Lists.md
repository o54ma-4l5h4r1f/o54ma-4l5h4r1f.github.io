---
sort : 1
--- 

# Quik Lists 
<!-- 

>>> li = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18]
>>> 
>>> v = iter(li)
>>> li = [(i, next(v), next(v)) for i in v]  # creates list of tuples 

-->

## list comprehension

```python
>>> [x ** 2 for x in range(7) if x % 2 == 0]
# [0, 4, 16, 36]

>>> a = [1, 2, 3]
>>> b = ['a', 'b', 'c']
>>> [[i, j] for i in a for j in b]
# [[1, 'a'], [1, 'b'], [1, 'c'], [2, 'a'], [2, 'b'], [2, 'c'], [3, 'a'], [3, 'b'], [3, 'c']]

>>> ["".join([str(i), j]) for i in a for j in b]
# ['1a', '1b', '1c', '2a', '2b', '2c', '3a', '3b', '3c']


>>> {x:chr(ord('A')+x) for x in range(10)}
# {0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F', 6: 'G', 7: 'H', 8: 'I', 9: 'J'}


>>> filp_me = {0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F', 6: 'G', 7: 'H', 8: 'I', 9: 'J'}
>>> {b:a for a,b in filp_me.items()}
# {'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6, 'H': 7, 'I': 8, 'J': 9}
```

---

## string

```python
from string import *

>>> printable
# '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'

>>> string.ascii_letters
# 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'

>>> string.punctuation
# '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

>>> ascii_lowercase
# 'abcdefghijklmnopqrstuvwxyz'

>>> ascii_uppercase
# 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

>>> hexdigits
# '0123456789abcdefABCDEF'

>>> digits
# '0123456789'

>>> whitespace
# ' \t\n\r\x0b\x0c'
```

---

## itertools

```python
from itertools import *

>>> ["".join(i) for i in product("ABC", "ABC")]
# ['AA', 'AB', 'AC', 'BA', 'BB', 'BC', 'CA', 'CB', 'CC']





>>> ["".join(i) for i in permutations("ABC")]		
>>> ["".join(i) for i in permutations("ABC", 3)]
# ['ABC', 'ACB', 'BAC', 'BCA', 'CAB', 'CBA']

>>> ["".join(i) for i in permutations("ABC",2)]
# ['AB', 'AC', 'BA', 'BC', 'CA', 'CB']		





>>> ["".join(i) for i in combinations("ABC",3)]
# ['ABC']

>>> ["".join(i) for i in combinations("ABCD",3)]
# ['ABC', 'ABD', 'ACD', 'BCD']

>>> ["".join(i) for i in combinations("ABC",2)]
# ['AB', 'AC', 'BC']






>>> ["".join(i) for i in combinations_with_replacement("ABC",2)]
# ['AA', 'AB', 'AC', 'BB', 'BC', 'CC']

>>> ["".join(i) for i in combinations_with_replacement("ABCD",3)]
# ['AAA', 'AAB', 'AAC', 'AAD', 'ABB', 'ABC', 'ABD', 'ACC', 'ACD', 'ADD', 'BBB', 'BBC', 'BBD', 'BCC', 'BCD', 'BDD', 'CCC', 'CCD', 'CDD', 'DDD']
```




---

## enumerate 

```python
>>> for i, e in enumerate(range(1,4)):
...     print(i, e) 
# 0 1
# 1 2
# 2 3


>>> for i, e in enumerate(range(1,4), start=1):
...     print(i, e) 
# 1 1
# 2 2
# 3 3
```


```note
Trying to access items by index from a generator or an iterator will raise a TypeError:
```


---

## zip 

```python
>>> a = [1, 2, 3]
>>> b = ['a', 'b', 'c']				# could be a list/set/tuple 
>>> list(zip(a, b))
# [(1, 'a'), (2, 'b'), (3, 'c')]




>>> a = [1, 2, 3]
>>> b = ['a', 'b', 'c']
>>> c = [1.2, 4.5, 5.1]
>>> list(zip(a, b, c))
# [(1, 'a', 1.2), (2, 'b', 4.5), (3, 'c', 5.1)]



>>> list(zip(range(3), b))
# [(0, 'a'), (1, 'b'), (2, 'c')]



>>> pairs = [(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd')]
>>> numbers, letters = zip(*pairs)
>>> numbers
# (1, 2, 3, 4)
>>> letters
# ('a', 'b', 'c', 'd')
```