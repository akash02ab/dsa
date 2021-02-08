# Maximum sum of increasing sub-sequence


| input | output |
| --- | --- |
| `arr[]`: array of integers | `n`: maximum sum of <br> increasing subsequence |

<br>

> **example :**

```
input:
9 4 5 7 3 6 8 1

output:
24
```

<br>

> **implementation :**

```python
def maxSum(arr, n):
    sum = arr.copy()

    for i in range(n):
        for j in range(i):
            if arr[i] > arr[j] and sum[i] < sum[j] + arr[i]:
                sum[i] = sum[j] + arr[i]
    
    return max(sum)

arr = list(map(int, input().split()))

print(maxSum(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n)