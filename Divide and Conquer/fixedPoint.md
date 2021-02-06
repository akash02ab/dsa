# Find fixed point in array

### Given sorted array of non-repeating elements, a fixed point is when arr[index] is equal to index.

<br>

| input | output |
| --- | --- |
| `arr[]`: sorted array | `n`: fixed point |

<br>

> **example :**

```
input:
-1 0 1 3 5 6

output:
3
```

> **implementation :**

```python
def findFixedPoint(arr, start, end):
    if start > end: return -1

    middle = (start + end) // 2

    if arr[middle] == middle:
        return middle 
    
    if arr[middle] > middle:
        return findFixedPoint(arr, start, middle - 1)
    else:
        return findFixedPoint(arr, middle + 1, end)

arr = list(map(int, input().split()))

print(findFixedPoint(arr, 0, len(arr) - 1))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)