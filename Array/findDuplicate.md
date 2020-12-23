# Find duplicate elements in O(n) time and O(1) extra space

| input | output |
| --- | --- |
|n: size of array<br>arr[n]: array of n elements | arr[]: array of duplicate elements |

<br>

> constraint : ` -n > arr[i] > n`

<br>

```
input:
7
1 2 3 1 3 6 6

output:
[1, 3, 6]
```

```python
def findRepeating(arr, n):
    duplicate = []
    
    for i in range(n):
        if arr[abs(arr[i])] >= 0:
            arr[abs(arr[i])] = - arr[abs(arr[i])]
        else:
            duplicate.append(abs(arr[i]))

    return duplicate

n = int(input())

arr = list(map(int, input().split()))

print(findRepeating(arr, n))
```

> Time and space complexity:
<br> `T(n) = O(n)`
<br> `S(n) = O(1)`