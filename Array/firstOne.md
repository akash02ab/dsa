# Find starting index of 1 in an array of unknown size contians all 0's in the beginning and 1's in the end

| input | output |
| --- | --- |
| arr[]: array of unknown size | i: index of first 1 |

```
input:
arr[] = [0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, ......]

output:
6
```

```python
def firstIndex(arr):
    i = 1

    while 1:
        if arr[i] == 0:
            i *= 2
        else:
            for j in range(i // 2, i):
                if arr[i] == 1:
                    return i

arr = list(map(int, input().split()))

result = firstIndex(arr)

print(result)
```