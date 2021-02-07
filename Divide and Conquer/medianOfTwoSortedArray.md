# Median of two sorted array

| input | output |
| --- | --- |
| `arr1`: sorted array <br> `arr2`: sorted array | `n`: median of two arrays |

<br>

> **example :**

```
input:
1 3 5 7
2 4 6 8

output:
4.5
```

<br>

> **implementation :**

```python
def median(arr, size):
    return (arr[size//2] + arr[size//2 - 1]) / 2 if size % 2 == 0 else arr[size//2]

def getMedianOfTwoArray(arr1, arr2, size):
    if size == 1:
        return (arr1[0] + arr2[0]) // 2
    if size == 2:
        return (max(arr1[0], arr2[0]) + min(arr1[1], arr2[1])) / 2
    
    median1 = median(arr1, size)
    median2 = median(arr2, size)
    
    if median1 == median2:
        return median1
    
    if median1 < median2:
        if size % 2 == 0:
            return getMedianOfTwoArray(arr1[size//2 - 1 : size], arr2[0 : size//2 + 1], size//2 + 1)
        else:
            return getMedianOfTwoArray(arr1[size//2 : size], arr2[0 : size//2 + 1], size//2 + 1)
    else:
        if size % 2 == 0:
            return getMedianOfTwoArray(arr1[0 : size//2 + 1], arr2[size//2 - 1 : size], size//2 + 1)
        else:
            return getMedianOfTwoArray(arr1[0 : size//2 + 1], arr2[size//2 : size], size//2 + 1)

arr1 = list(map(int, input().split()))
arr2 = list(map(int, input().split()))

print(getMedianOfTwoArray(arr1, arr2, len(arr1)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(log(n))
<br> S(n) = O(1)