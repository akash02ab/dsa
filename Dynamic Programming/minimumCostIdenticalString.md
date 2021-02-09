# Find minimum cost to convert string1 to string2

### Only deletion operation is allowed in both the string, and cost of performing deletion in string1 is `s` and `p` in string2.

<br>

| input | output |
| --- | --- |
| `string1` <br> `string2` <br> `s`: cost of deletion in string1 <br> `p`: cost of deletion in string2 | `n`: minimum cost to make <br> both the strings identical |

<br>

> **example :**

```
input:
october
november
1 2

output:
11
```

<br>

> **implementation :**

```python
def longestCommonSubsequence(string1, string2, length1, length2):
    LCS = [[0 for i in range(length2 + 1)] for j in range(length1 + 1)]

    for i in range(1, length1 + 1):
        for j in range(1, length2 + 1):
            if string1[i-1] == string2[j-1]:
                LCS[i][j] = 1 + LCS[i-1][j-1]
            else:
                LCS[i][j] = max(LCS[i-1][j], LCS[i][j-1])
    
    return LCS[length1][length2]

def getMinimumCost(string1, string2, cost1, cost2):
    length1 = len(string1)
    length2 = len(string2)
    lenOfLCS = longestCommonSubsequence(string1, string2, length1, length2)

    return cost1 * (length1 - lenOfLCS) + cost2 * (length2 - lenOfLCS)

string1 = input()
string2 = input()
s, p = map(int, input().split())

print(getMinimumCost(string1, string2, s, p))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)