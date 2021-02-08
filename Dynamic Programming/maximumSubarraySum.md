# Maximum subarray sum

| input | output |
| --- | --- |
| `arr[]`: array of integers | `n`: max subarray sum |

<br>

> **example :**

```
input:
10 -5 -3 4 2 12 -8 -12 19

output:
20
```

<br>

> **implementation :**

```python 
def maxSubarraySum(arr, n):
    maxSoFar = 0
    currentSum = 0

    for i in range(n):
        currentSum = max(0, currentSum + arr[i])
        maxSoFar = max(currentSum, maxSoFar)
    
    return maxSoFar

arr = list(map(int, input().split()))

print(maxSubarraySum(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(1)