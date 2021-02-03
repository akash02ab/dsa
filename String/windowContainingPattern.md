# Find the minimum size window in string that contain the pattern

| input | output |
| --- | --- |
| `string`: original string | `string`: window containing pattern |

<br>

> example :

```
input:
doing it all night all summer
mulan

output:
night all sum
```

<br>

> approach :

1. check if `string's` length is less than `pattern's` length. If yes then no such window can exist

2. store the occurence of characters of `pattern` in `hashPattern`

3. start traversing the `string`:
    * count occurence of character of `string` in `hashString`
    
    * if `string's` char mathces with `pattern's` char then increment `count`
    
    * if all characters are matched:
        
        * try to minimize the `window size`, check if any character occurring more number of times than its occurence in pattern, if yes then remove it from starting and also remove the useless characters
        
        * update the `window size` if lesser size is found and also update the start index

4. return the window

<br>

> implementation :

```python
from collections import defaultdict

def smallestWindow(string, pattern):
    hashPattern = defaultdict(int)
    hashString = defaultdict(int)

    count = start = windowLen = 0
    strLen = len(string)
    patternLen = len(pattern)
    startIndex = -1
    minLen = float('inf')

    if strLen < patternLen:
        return ''
    
    for char in pattern:
        hashPattern[char] += 1

    for i in range(strLen):
        char = string[i]

        hashString[char] += 1

        if hashPattern[char] != 0 and hashString[char] <= hashPattern[char]:
            count += 1

        if count == patternLen:
            key = string[start]
            
            while hashString[key] > hashPattern[key] or hashPattern[key] == 0:

                if hashString[key] > hashPattern[key]:
                    hashString[key] -= 1
                
                start += 1
                key = string[start]
                windowLen = i - start + 1

                if minLen > windowLen:
                    minLen = windowLen
                    startIndex = start
    
    if startIndex == -1:
        return ''
    
    return string[startIndex : startIndex + minLen]

string = input()
pattern = input()

print(smallestWindow(string, pattern))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)