# Rearrange the string such that same characters are atleast `d` distance away

| input | output |
| --- | --- |
| `string`: original string  <br> `d`: distance between <br> similar character | `string`: rearranged string |

<br>

> **example :**

```
input:
oblivion
3

output:
oibloivn
```

<br>

> **implementation :**

```python
from collections import defaultdict

def rearrange(string, d):
    hash = defaultdict(int)

    for char in string:
        hash[char] += 1

    hash = [[k, v] for k, v in hash.items()]
    
    hash.sort(reverse = True, key = lambda x: x[1])
    
    result = [''] * len(string)
    i, n = 0, len(string)
    
    while len(hash):
        [char, frequency] = hash[0]
        
        j = i
        while frequency:
            while result[j] != '':
                j += 1
            
            if j >= n: return -1
            
            result[j] = char
            j += d
            frequency -= 1
        
        hash.pop(0)
        i += 1
    
    return ''.join(result)

string = input()
d = int(input())

print(rearrange(string, d + 1))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(1)
<br> *(ascii value ranges from 0-255, thus constant space)*
