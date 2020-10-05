# Binary Search

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: sorted array of n elements <br> x: target element | i: index of target element |

```
input:
n = 5
arr = [1, 3, 5, 6, 9]
x = 6

output:
3
```

```python
def binarySearch(arr, size, target):
    l, r = 0, size-1

    while l <= r:
        m = l + (r - l) // 2
        if arr[m] == target:
            return m
        elif arr[m] > target:
            r = m - 1
        else:
            l = m + 1

    return -1

n = int(input())

arr = list(map(int, input().split()))

index = binarySearch(arr, n, int(input()))

print(index)
```

```
Recurrence relation:
T(n) = T(n / 2) + 1 , if n > 1
T(n) = 1 , if n = 1 
```

```
Time and Space complexity:
T(n) = O(n log(n))
S(n) = O(1)
```