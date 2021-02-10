# Count palindromic substring

| input | output |
| --- | --- |
| `string` | `n`: number of palindromic substring |

<br>

> **example :**

```
input:
carrom

output:
7
```

<br>

> **implementation :**

```python 
def countPalindromicSubstring(string):
    size = len(string)

    PS = [[False for i in range(size)] for j in range(size)]

    COUNT = [[0 for i in range(size)] for j in range(size)]

    for i in range(size):
        PS[i][i] = True
        COUNT[i][i] = 1
    
    for i in range(size - 1):
        if string[i] == string[i + 1]:
            PS[i][i + 1] = True 
            COUNT[i][i + 1] = 3
        else:
            COUNT[i][i + 1] = 2
    
    for k in range(2, size):
        for i in range(size - k):
            j = i + k

            if PS[i + 1][j - 1] and string[i] == string[j]:
                PS[i][j] = True

            if PS[i][j]:
                COUNT[i][j] = 1 + COUNT[i][j - 1] + COUNT[i + 1][j] - COUNT[i + 1][j - 1]
            else:
                COUNT[i][j] = COUNT[i][j - 1] + COUNT[i + 1][j] - COUNT[i + 1][j - 1]
    
    return COUNT[0][size - 1]

string = input()

print(countPalindromicSubstring(string))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)