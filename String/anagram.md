# Check wheather two strings are anagram or not

| input | output |
| --- | --- |
| `string1` <br> `string2` | `boolean`: `True` if both the strings <br> are anagram, `False` otherwise |

<br>

> example :

```
input:
halsey
ashley

output:
True
```

<br>

> appraoch :

1. build a hash table for frequency of character in string1

2. decrement count of character from hash table while accessing the string2

3. if hash contain any negative value it means two strings are not anagram

<br>

> implementation :

```python
from collections import defaultdict

def isAnagram(str1, str2):
    if len(str1) != len(str2):
        return False 
    
    hash = defaultdict(int)

    for char in str1:
        hash[char] += 1

    for char in str2:
        hash[char] -= 1

    for key in hash:
        if hash[key] != 0:
            return False
    
    return True

str1 = input()

str2 = input()

print(isAnagram(str1, str2))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)
<br>*(hash table only contain ascii character which is constant so, constant space)*