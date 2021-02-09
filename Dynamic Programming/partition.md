# Partition 

### Partition problem is to determine whether a given set can be partitioned into two subsets such that the sum of elements in both subsets is the same.

<br>

| input | output |
| --- | --- |
| `arr[]`: array of integers | `boolean`: `True` if partition is possible, <br> `False` otherwise |

<br>

> **example :**

```
input:
4 10 5 15 3 1

output:
True
```
<br>

> **implementation :**

```python 
def findPartition(arr, size):
    sum = 0
    for i in range(size):
        sum += arr[i]
    
    if sum % 2 == 1:
        return False 
    
    partition = [[True for j in range(size + 1)] for i in range(sum//2 + 1)]
    
    for i in range(1, sum//2 + 1):
        partition[i][0] = False
    
    for i in range(1, sum//2 + 1):
        for j in range(1, size + 1):
            partition[i][j] = partition[i][j - 1]

            if i >= arr[j - 1]:
                partition[i][j] = partition[i][j] or partition[i - arr[j - 1]][j - 1]
    
    return partition[sum // 2][size]
    

arr = list(map(int, input().split()))

print(findPartition(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n * sum)
<br> S(n) = O(n * sum)