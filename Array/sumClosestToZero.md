# Find two number such that their sum is closest to zero

| input | output | 
| --- | --- |
| arr[]: array of integers | [a, b] |

```
input:
arr[] = [4, -5, 2, 9, 6, -2]

output:
[-2, 2]
```

```python
def sumClosestToZeroPair(arr):
    currSum, closestSum = 0, 999999
    l, r = 0, len(arr) - 1
    minL, minR = -1, -1

    arr.sort()

    while l < r:
        currSum = arr[l] + arr[r]

        if abs(currSum) < abs(closestSum):
            closestSum = currSum
            minL = l
            minR = r

        if currSum > 0:
            r -= 1
        else:
            l += 1

    return [arr[minL], arr[minR]]

arr = list(map(int, input().split()))

result = sumClosestToZeroPair(arr)

print(result)
```

```
Time and space complexity:
T(n) = O(n logn)
S(n) = O(1)
```



