# Count number of time a string occur as a subsequence of other string

| input | output |
| --- | --- |
| `string`: string1 <br> `string`: string2 | `n`: count of occurence <br> of string2 in string1 |

<br>

> **example :**

```
input:
abbcab
ab

output:
4
```

<br>

> **implementation :**

```python 
def countSubsequence(string1, string2):
    length1 = len(string1) + 1
    length2 = len(string2) + 1

    CS = [[0 for i in range(length2)] for j in range(length1)]

    for i in range(length1):
        CS[i][0] = 1

    for i in range(1, length1):
        for j in range(1, length2):
            if string1[i-1] == string2[j-1]:
                CS[i][j] = CS[i-1][j-1] + CS[i-1][j]
            else:
                CS[i][j] = CS[i-1][j]
    
    return CS[length1 - 1][length2 - 1]

string1 = input()
string2 = input()

print(countSubsequence(string1, string2))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)