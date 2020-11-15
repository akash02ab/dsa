# Seperate 0's and 1's in an array

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: array of size n <br> containing only 0's and 1's | arr[]: array having all 0's followed by 1's |

```
input:
n = 7
arr[] = [1, 0, 1, 0, 0, 1, 1]

output:
arr[] = [0, 0, 0, 1, 1, 1, 1]
```

```python
def seperate0and1(arr, n):
    leftIndex, rightIndex = 0, n-1

    while leftIndex < rightIndex:
        while arr[leftIndex] == 0 and leftIndex < rightIndex:
            leftIndex += 1
        
        while arr[rightIndex] == 1 and leftIndex < rightIndex:
            rightIndex -= 1

        if leftIndex < rightIndex:
            arr[leftIndex], arr[rightIndex] = arr[rightIndex], arr[leftIndex]

            leftIndex += 1
            rightIndex -= 1

n = int(input())

arr = list(map(int, input().split()))

seperate0and1(arr, n)

print(arr)
```

```
Time and Space complexity:
T(n) = O(n)
S(n) = O(1)
```