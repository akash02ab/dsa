# Longest non-overlapping repeated substring 

| input | output |
| --- | --- |
| `string`: original string | `string`: longest non-overlapping <br> repeated substring |

<br>

> **example :**

```
input:
fastfuriousfaster

output:
fast
```

<br>

> **implementation :**

```python 
def longestNonOverlappingRepeatedSubstring(string): 
    n = len(string) 
    LNRS = [[0 for x in range(n + 1)] for y in range(n + 1)] 
  
    result = "" 
    resultLen = 0 
  
    # building table in bottom-up manner 
    index = 0
    for i in range(1, n + 1): 
        for j in range(i + 1, n + 1): 
            # (j-i) > LNRS[i-1][j-1] to remove overlapping 
            if (string[i - 1] == string[j - 1] and LNRS[i - 1][j - 1] < (j - i)): 
                LNRS[i][j] = LNRS[i - 1][j - 1] + 1
  
                # updating maximum length of the substring  
                # and updating the finishing index of the suffix 
                if (LNRS[i][j] > resultLen): 
                    resultLen = LNRS[i][j] 
                    index = max(i, index) 
                  
            else: 
                LNRS[i][j] = 0
  
    # If we have non-empty result, then insert  
    # all characters from first character to  
    # last character of string 
    if (resultLen > 0): 
        for i in range(index - resultLen + 1, index + 1): 
            result = result + string[i - 1] 
  
    return result

string = input()

print(longestNonOverlappingRepeatedSubstring(string))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)