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
```