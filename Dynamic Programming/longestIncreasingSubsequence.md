# Lenght of longest increasing sub-sequence

| input | output |
| --- | --- |
| `arr[]`: sequence | `n`: length of longest <br> increasing subsequence |

<br>

> **example :**

```
input:
2 6 3 7 4 8 1 5

output:
4
```

<br>

> **implementation :**

```python 
def longestIncreasingSubsequence(arr, size):
    seqLength = [1] * size 

    for i in range(size):
        for j in range(i):
            if arr[i] > arr[j] and seqLength[i] < seqLength[j] + 1:
                seqLength[i] = seqLength[j] + 1

    return max(seqLength)
    
arr = list(map(int, input().split()))

print(longestIncreasingSubsequence(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n)
