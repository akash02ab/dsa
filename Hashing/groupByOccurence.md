# Group by occurence

### Group all the occurence of elements order by their first occurence.

<br>

| input | output |
| --- | --- |
| `arr`: array if numbers | `arr`: grouped array |

<br>

> example :
```
input:
2 4 7 3 6 5 3 3 6 9

output:
[2, 4, 7, 3, 3, 3, 6, 6, 5, 9]
```
<br>

> approach :

1. create hash table containing frequency of each element

2. for each element in `array`
    * look up in hash table
    
    * store `element` in `result` array as many times as frequency
    
    * update the `frequency` in hash table to `0` 

<br>

> implementation :

```python
def groupByOccurence(arr):
    hash = {}

    for item in arr:
        if item not in hash:
            hash[item] = 1
        else:
            hash[item] += 1

    result = []
    for item in arr:
        frequency = hash[item]

        for i in range(frequency):
            result.append(item)
        
        hash[item] = 0

    return result


arr = list(map(int, input().split()))

print(groupByOccurence(arr))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)