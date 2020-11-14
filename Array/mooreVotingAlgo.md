# Moore Voting Algorithm

## Find an element that occurs more than n/2 times in an array in O(1) space complexity

| input | output |
| --- | --- |
| arr[n]: array of size n | n: majority element if exists else -1 |

```
input: [1, 1, 1, 1, 2, 4, 5]
output: 1

input: [1, 1, 2, 3, 5]
output: -1
```

```python
def getMajorityElement(arr, size):
    majorityIndex, count = 0, 1
    
    for i in range(1, size):
        if arr[i] == arr[majorityIndex]:
            count += 1
        else:
            count -= 1

        if count == 0:
            majorityIndex = i
            count = 1

    return arr[majorityIndex]

def isMajorityElement(arr, size, majorityElement):
    count = 0

    for i in range(size):
        if arr[i] == majorityElement:
            count += 1
    
    return count > (size // 2)

arr = list(map(int, input().split()))

m = getMajorityElement(arr, len(arr))

if isMajorityElement(arr, len(arr), m):
    print(m)
else:
    print(-1)
```

```
Time and Space complexity:
T(n) = O(n)
S(n) = O(1)
```