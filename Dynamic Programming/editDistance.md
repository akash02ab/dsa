# Edit distance

### Given two words `word1` and `word2`. Convert `word1` into `word2` using minimum number of operations. The operation are : **insert**, **replace** and **delete**.

<br>

> **example :**

```
input:
forgery
nightmare

output:
8
```

<br>

> **implementation :**

```python
def minEditDistance(str1, str2, len1, len2):
    ED = [[0 for i in range(len2 + 1)] for j in range(len1 + 1)]

    for i in range(len1 + 1):
        for j in range(len2 + 1):
            if i == 0:
                ED[i][j] = j
            elif j == 0:
                ED[i][j] = i 
            elif str1[i - 1] == str2[j - 1]:
                ED[i][j] = ED[i - 1][j - 1]
            else:
                ED[i][j] = 1 + min(ED[i][j - 1], ED[i - 1][j], ED[i - 1][j - 1])
    
    return ED[len1][len2]

string1 = input()
string2 = input()

print(minEditDistance(string1, string2, len(string1), len(string2)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(m * n)
<br> S(n) = O(m * n)