# Sort nearly sorted array using Insertion sort

| input | output |
| --- | --- |
| n: size of array<br>arr[n]: array of size n | arr[n]: sorted array |

```
input:
7
2 3 1 6 4 7 5

output:
[1, 2, 3, 4, 5, 6, 7]
```

```python
def modifiedInsertionSort(arr, n):
    for i in range(1, n):
        current = arr[i]
        
        j = i - 1
        while j >= 0 and arr[j] > current:
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = current

    return arr

n = int(input())

arr = list(map(int, input().split()))

print(modifiedInsertionSort(arr, n))
```
> Time and space complexity :
<br>T(n) = O(kn) where, k = sortness of array
<br>S(n) = O(1)