# Find the number of inversion in an array

| input | output |
| --- | --- |
| `arr[]`: array of integers | `n`: inversion count |

<br>

> **example :**

```
input:
2 4 7 3 6 5

output:
5
```

<br>

> **implementation :**

```python
def merge(arr, temp, left, middle, right):
    inversionCount = 0

    i = k = left
    j = middle

    while i <= middle - 1 and j <= right:
        if arr[i] <= arr[j]:
            temp[k] = arr[i]
            i += 1
            k += 1
        else:
            inversionCount += (middle - i)
            temp[k] = arr[j]
            j += 1
            k += 1
    
    while i < middle:
        temp[k] = arr[i]
        i += 1
        k += 1
    
    while j <= right:
        temp[k] = arr[j]
        j += 1
        k += 1

    arr[left : right + 1] = temp[left : right + 1]
    
    return inversionCount

def mergeSort(arr, temp, left, right):
    inversionCount = 0

    if left < right:
        middle = (left + right) // 2
        inversionCount += mergeSort(arr, temp, left, middle)
        inversionCount += mergeSort(arr, temp, middle + 1, right)
        inversionCount += merge(arr, temp, left, middle + 1, right)
    
    return inversionCount

def countInversion(arr, size):
    temp = [0] * size
    return mergeSort(arr, temp, 0, size - 1)

arr = list(map(int, input().split()))

print(countInversion(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(log(n))
<br> S(n) = O(1)