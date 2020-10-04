# Maximum OR value pair in an array

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: n distinct integers | m: maximum OR value of two integer |

```
n = 4
arr = [8, 9, 3, 7, 4]

m = 9 | 7 = 15
```

```python
def maxORpair(arr, n):
    maxVal = max(arr)
    m = 0

    for i in range(n):
        m = max(m, (maxVal | arr[i]))
    
    return m

n = int(input())

arr = list(map(int, input().split()))

m = maxORpair(arr, n)

print(m)
```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(1)
```