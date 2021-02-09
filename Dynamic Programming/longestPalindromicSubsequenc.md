# Longest palindromic subsequence

| input | output |
| --- | --- |
| `string`: sequence | `n`: length of longest palnidrome |

<br>

> **example :**

```
input:
management

output:
5
```
```
longest palindrome for given sequence:-
nemen
```
<br>

> **implementation :**

```python 
def longestPalindromicSubsequence(string):
    size = len(string)

    LPS = [[0 for i in range(size + 1)] for j in range(size + 1)]

    for i in range(size):
        LPS[i][i] = 1

    for i in range(2, size + 1):
        for j in range(size - i + 1):
            k = j + i - 1
            if string[j] == string[k] and i == 2:
                LPS[j][k] = 2
            elif string[j] == string[k]:
                LPS[j][k] = LPS[j+1][k-1] + 2
            else:
                LPS[j][k] = max(LPS[j][k-1], LPS[j+1][k])
    
    return LPS[0][size - 1]
    
string = input()

print(longestPalindromicSubsequence(string))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)