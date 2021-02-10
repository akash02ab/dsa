# Longest palindromic substring 

| input | output |
| --- | --- |
| `string` | `string`: maximum length <br>  substring which is palindrome |

<br>

> **example :**

```
input:
carbonnodrac

output:
onno
```

<br>

> **implementation :**

```python
def longestPalindromicSubstring(string):
    size = len(string)

    LPS = [[False for i in range(size)] for j in range(size)]

    for i in range(size):
        LPS[i][i] = True 
    
    start = 0
    maxLen = 0
    for i in range(size - 1):
        if string[i] == string[i + 1]:
            LPS[i][i + 1] = True 
            start = i
            maxLen = 2 
    
    for k in range(3, size):
        for i in range(size - k + 1):
            j = i + k - 1

            if LPS[i + 1][j - 1] and string[i] == string[j]:
                LPS[i][j] = True 

                if k > maxLen:
                    start = i
                    maxLen = k 
    
    end = start + maxLen      
    return string[start : end]

string = input()

print(longestPalindromicSubstring(string))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)

<br>

> **O(1) space approach :**

<br>

> **implementation :**

```python 
def longestPalindromicSubstring(string):
    size = len(string)
    start = end = maxLen = 0

    for i in range(1, size - 1):
        j = i
        k = i - 1
        # with i and (i-1) as center find longest even length palindrome 
        while k >= 0 and j < size and string[j] == string[k]:
            if maxLen < (j - k + 1):
                maxLen = j - k + 1
                start = k
                end = j + 1
            
            k -= 1
            j += 1
        
        j = i - 1
        k = i + 1
        # with i an center find longest odd length palindrome
        while j >= 0 and k < size and string[j] == string[k]:
            if maxLen < (k - j + 1):
                maxLen = k - j + 1
                start = j 
                end = k + 1 
            
            j -= 1
            k += 1
        
    return string[start : end]

string = input()

print(longestPalindromicSubstring(string))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(1)