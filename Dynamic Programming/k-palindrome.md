# Check whether given string can be converted into palindrome after atmost k deletion

| input | output |
| --- | --- |
| `string` <br> `k`: number of deletion | `boolean`: `True` if string becomes palindrome <br> after k deletion, `Fasle` otherwise |

<br>

> **example :**

```
input:
lirowil
2

output:
True
```

<br>

> **implementation :**

```python
def longestCommonSubsequence(str1, str2):
    size = len(str1)

    LCS = [[0 for i in range(size + 1)] for j in range(size + 1)]

    for i in range(1, size + 1):
        for j in range(1, size + 1):
            if str1[i-1] == str2[j-1]:
                LCS[i][j] = 1 + LCS[i-1][j-1]
            else:
                LCS[i][j] = max(LCS[i-1][j], LCS[i][j-1])
    
    return LCS[size][size]

def kPalindrome(string, k):
    l = longestCommonSubsequence(string, string[::-1])

    if len(string) - l <= k:
        return True 
    return False 

string = input()

k = int(input())

print(kPalindrome(string, k))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)