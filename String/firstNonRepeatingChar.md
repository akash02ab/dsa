# Find the first non repeating character in the string

| input | output |
| --- | --- |
| `string`: original string | `char`: first non-repeating character |

<br>

> example:

```
input:
metalbolism

output:
e
```

<br>

> approach :

1. maintain a hash table containing count and index of each character in the string

2. look for character in hash table having count equal to `1` and lowest index

3. that index element is the first character that is non-repeating

<br>

> implementation :

```python
def nonRepeatingChar(string):
    hash = {}

    for i in range(len(string)):
        char = string[i]
        
        if char not in hash:
            hash[char] = [1, i]
        else:
            [count, index] = hash[char]
            hash[char] = [count + 1, index]
    
    firstIndex = float('inf')

    for (char, [count, index]) in hash.items():
        if count == 1 and index < firstIndex:
            firstIndex = index

    return string[firstIndex]

string = input()

print(nonRepeatingChar(string))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)
<br>*(ascii character ranges from 0 to 255, thus constant space)*