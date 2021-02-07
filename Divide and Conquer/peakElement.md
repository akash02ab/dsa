# Find peak element in an array which is first increasing then decreasing

| input | output |
| --- | --- |
| `arr[]`: original array | `n`: peak element |

<br>

> **example :**

```
input:
2 4 7 6 5 3 1

output:
7
```

<br>

> **implementation :**

```python
def getPeakElement(arr, start, end):
    if start == end: 
        return arr[start]
    
    if end == start + 1 and arr[start] >= arr[end]:
        return arr[start]
    
    if end == start + 1 and arr[start] < arr[end]:
        return arr[end]
    
    middle = (start + end) // 2

    if arr[middle] > arr[middle + 1] and arr[middle] > arr[middle - 1]:
        return arr[middle]
    
    if arr[middle] > arr[middle + 1] and arr[middle] < arr[middle - 1]:
        return getPeakElement(arr, start, middle - 1)
    
    else:
        return getPeakElement(arr, middle + 1, end)

arr = list(map(int, input().split()))

print(getPeakElement(arr, 0, len(arr) - 1))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)