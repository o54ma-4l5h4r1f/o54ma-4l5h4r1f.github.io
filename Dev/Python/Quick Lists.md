---
sort :
--- 

# Quik Lists 

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