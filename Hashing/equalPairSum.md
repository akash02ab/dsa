# Equal pair sum

### Find all four pair elements `i`, `j`, `k` and `l` in an array such that `i + j` `=` `k + l`.

<br>

| input | output |
| --- | --- |
| `n`: number of elements <br> `arr`: array of `n` elements | `arr`: all equal sum pair |

<br>

> example :

```
input:
7
6 2 3 4 5 10 1

output:
[([6, 2], [3, 5]), 
 ([6, 3], [4, 5]), 
 ([6, 5], [10, 1]), 
 ([6, 1], [2, 5]), 
 ([6, 1], [3, 4]), 
 ([2, 5], [3, 4]), 
 ([2, 3], [4, 1]), 
 ([2, 4], [5, 1])]
```

<br>

> appraoch :

1. make a `hash` table containg sum of all subarray possible
    * *key* contains **sum**
    * *value* contains **array** of **sum** pairs

2. look for all elements in hash table
    * find if any element in hash table has more than one sum pair
    * add it to `result` array

3. return `result` array

<br>

> implementation :

```python
from collections import defaultdict

def equalSumPair(arr, n):
    hash = defaultdict(list)

    for i in range(n):
        for j in range(i + 1, n):
            sum = arr[i] + arr[j]
            hash[sum].append([arr[i], arr[j]])

    result = []

    for pair in hash:
        m = len(hash[pair])
        
        if m >= 2:
            for i in range(m):
                for j in range(i + 1, m):
                    result.append((hash[pair][i], hash[pair][j]))

    return result
            

n = int(input())

arr = list(map(int, input().split()))

print(equalSumPair(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n<sup>2</sup>)