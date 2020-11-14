# Find the element which occur odd number of times given that all other elements occurs even number of times

| input | output |
| --- | --- |
|n: size of array <br> arr[n]: array of size n | r: element occuring odd number of times |

```
n = 9
arr[] = [1, 3, 2, 1, 4, 3, 2, 1, 4]

r = 1
```

```python
def oddOccuringNumber(arr, n):
    result = 0

    for i in range(n):
        result ^= arr[i]

    return result

n = int(input())

arr = list(map(int, input().split()))

r = oddOccuringNumber(arr, n)

print(r)
```

```
Time and Space complexity:
T(n) = O(n)
S(n) = O(1)
```