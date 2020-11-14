# All pair in array with sum is X

## Using Hash table

<br>

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: n positive integers <br> x: target sum | (i, j): pair  with sum x |


```
input:
n = 6
arr = [2, 3, 3, 4, 5, 6]
x = 9

output:
(4, 5)
(3, 6)
```

```python
MAX = 1000000

def findPair(arr, n, sum):
    hash = [0] * MAX

    for i in range(n):
        temp = sum - arr[i]
        
        if temp >= 0 and hash[temp] == 1:
            print((arr[i], temp))
        
        hash[arr[i]] = 1

n = int(input())

arr = list(map(int, input().split()))

findPair(arr, n, int(input()))
```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(k)  k is the range of integers
```

<br>

---

<br>

## Using Quick sort

<br>

```python
def findPair(arr, n, sum):
    arr = Sorted(arr)

    left, right = 0, n-1

    while left < right:
        if arr[left] + arr[right] == sum:
            print((arr[left], arr[right]))
        elif arr[left] + arr[right] < sum:
            left += 1
        else:
            right -= 1

n = int(input())

arr = list(map(int, input().split()))

findPair(arr, n, int(input()))
```

```
Time and space complexity:
T(n) = O(n log(n))
S(n) = O(1)  
```