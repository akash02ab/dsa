# Find the maximum occuring character in a string

| input | output |
| --- | --- |
| `string`: string that may <br> include special char | `char`: max occuring character |

<br>

> example :

```
input:
vancityReynolds

output:
y
```

<br>

> approach :

1. for each character of string
    * maintain the hash table 
        * key contains the character
        * value contains the character count

2. find the character having maximum count

<br>

> implementation 

```python
from collections import defaultdict

def maxOccuringChar(string):
    hash = defaultdict(int)

    for char in string:
        hash[char] += 1

    return max(hash)

string = input()

print(maxOccuringChar(string))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)
<br>*(ascii value ranges from 0 to 255, thus constant space)*