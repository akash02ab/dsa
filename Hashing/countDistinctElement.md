# Count distinct element

### Given an array of size `n`, count the distinct element in all window of size `k`.

<br>

| input | output |
| --- | --- | 
| `n`, `k`: size of array, size of window <br> `arr`: array of `n` elements | `arr`: count of distinct elements <br> for each window of size `k` |

<br>

> example :

```
input:
6 3
1 2 3 3 4 5

output:
[3, 1, 1, 3]
```

<br>

> approach :

1. add all the elements that fits in **one window** to the hash table and maintain their frequency

2. increase the `count` value if frequency of element becomes `1` (it means there is only **single occurence** of that element in **current window**)

3. decrement the `count` value if frequency of element is other than `1` (it means that the element is repeated)

4. slide the window and remove the *first* element from the window and add *next* element to the window

5. also update the `hash` frequency for the elements removed and added

6. add the `count` value to `result` array every time window slides

<br>

> implementation :

```python
from collections import defaultdict

'''
if val is 1 it means there is no duplicate element present in window so far
so add 1 to count, otherwise remove that element from count by substracting 1
'''
def checkCount(val):
    return 1 if val is 1 else -1

def distinctElement(arr, n, k):
    hash = defaultdict(int)

    count = 0
    result = []
    for i in range(n):
        item = arr[i]
        hash[item] += 1
        '''
        increment count by 1 if there is only single occurence of item in window,
        otherwise decrement it
        '''
        count += checkCount(hash[item])
        '''
        index reaches the window first time when i + 1 is equal to k
        for higher value of i just slide the window
        '''
        if i + 1 >= k:
            # add count to result for each sliding window
            result.append(count)

            # remove the element which is out of window when window slides
            previous = arr[i - k + 1]
            hash[previous] -= 1
            
            # update count accordingly
            count += checkCount(hash[previous])
        
    return result

n, k = map(int, input().split())

arr = list(map(int, input().split()))

print(distinctElement(arr, n, k))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(k)
