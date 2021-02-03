# Find the first non repeating character from stream of characters

| input | output |
| --- | --- |
| `string`: stream of char | `arr`: first non-repeating char <br> after each new occurence |

<br>

> example :

```
input:
aabcdbd

output:
['a', 'b', 'b', 'b', 'c', 'c']
```

<br>

> approach :

1. maintain two hash table
    * `singleOccurence` to store the character that occured so far and not repeated

    * `repeated` to keep track of repeated characters

2. if character is not repeated:
    * if character is not in `singleOccurence`
        * add it to `singleOccurence`
    
    * else it's now repeated
        * remove from `singleOccurence`
        * and, add it to `repeated`
    
    * if `singleOccurence` is not empty
        * there is still some non-repeating characters
        * add the first character from `singleOccurence` to `result` array

3. return `result` array

<br>

> implementation :

```python
def findFirstNonRepeating(stream):
    singleOccurence = []
    repeated = []
    result = []

    for char in stream:
        if char not in repeated:
            if char not in singleOccurence:
                singleOccurence.append(char)
            else:
                singleOccurence.remove(char)
                repeated.append(char)
        
        if len(singleOccurence):
            result.append(singleOccurence[0])

    return result

stream = input()

print(findFirstNonRepeating(stream))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)