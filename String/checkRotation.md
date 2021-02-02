# Check wheater given strings are rotations to each other

| input | output |
| --- | --- |
| `string1`<br> `string2` | `boolean`: `True` if two strings are rotation <br> of one another, `False` otherwise |

<br>

> example :

```
input:
park
rkpa

output:
True
```

```
input:
park
prka

output:
False
```

> approach :

1. if length of both the strings are not equal then return `False`

2. concatenate first string to itself and store in variable `temp`

3. check if `string2` is substring of `temp`
    * if yes then `string2` is rotation of `string1`, return `True`
    * if no then return `False`

<br>

> implementation :

```python
def isSubString(str1, str2):
    if str1.find(str2) == -1:
        return False
    return True

def checkRotation(str1, str2):
    if len(str1) != len(str2):
        return False 
    
    temp = str1 + str1

    if isSubString(temp, str2):
        return True
    return False

str1 = input()
str2 = input()

print(checkRotation(str1, str2))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)