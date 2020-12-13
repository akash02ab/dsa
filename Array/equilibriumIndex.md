# Equilibrium index of an array

> Sum of all the elements from 0 to i is equal to sum of all the elements from (i + 1) to n

| input | output |
| --- | --- |
| arr[]: array of integers | index: equilibrium index |

```python
def equilibriumIndex(arr, size):
    rightSum = 0

    for i in range(size):
        rightSum += arr[i]

    leftSum = 0
    for index in range(size):
        rightSum -= arr[index]
        leftSum += arr[index]
        
        if leftSum == rightSum:
            return index
        
    return -1

arr = list(map(int, input().split()))

result = equilibriumIndex(arr, len(arr))

print(result)
```

> Time and space complexity:
<br> T(n) = O(n)
<br> S(n) = O(1)