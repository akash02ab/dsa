# Find the maximum difference between two elemenets in an array such that larger element has higher index than smaller one.

| input | output |
| --- | --- |
| n: size of arr <br> arr[n]: array of size n | d: maximum difference between two elements |

```
n = 7
arr[] = [4, 3, 10, 2, 9, 1, 6]

maxDifference pair = [[10, 3], [9, 2]]

d = 7
```

```python
def maximumDifference(arr, n):
    maxDiff = 0
    currMin = a[0]

    for i in range(1, n):
        if currMin > arr[i]:
            currMin = arr[i]
        else:
            currDiff = a[i] - currMin
            if currDiff > maxDiff:
                maxDiff = currDiff

    return maxDiff

n = int(input())

arr = list(map(int, input().split()))

d = maximumDifference(arr, n)

print(d)
```

```
Time and Space complexity:
T(n) = O(n)
S(n) = O(1)
```