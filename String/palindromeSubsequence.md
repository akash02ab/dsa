# Minimum number of palindromic subsequence to be removed to empty a binary string

| input | output |
| --- | --- |
| `string`: binary string | `n`: count of removal steps |

<br>

> example :

```
input:
1011

output:
2
```

```
input:
1001

output:
1
```

<br>

> appraoch :

1. the input only contains binary string

2. if the binary string is palindromic remove the whole string, so only `1` palindromic string is removed

3. else, find the subsequence of palindromic string *(let's assume all 1's)*, remove it then *remove all 0's*, thus `2` palindromic string is removed

<br>

> implementation :

```python
def checkPalindrome(string):
    left, right = 0, len(string) - 1

    while left < right:
        if string[left] != string[right]:
            return False
        
        left += 1
        right -= 1

    return True        

def minimumRemovals(string):
    if string == '':
        return 0

    return 1 if checkPalindrome(string) else 2

string = input()

print(minimumRemovals(string))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)