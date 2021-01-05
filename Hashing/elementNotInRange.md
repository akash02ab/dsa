# Element not in range

### Given array and a range [low, high]. Find the elements that are in range but not in array.

<br>

| input | output |
| --- | --- |
| `arr`: array of integers <br> `range`: [low, high]| `arr`: missing elements |

<br>

> example :
```
input:
52 9 3 5 50 15 51 45 32
48 53

outpu:
[48, 49, 53]
```

<br>

> approach :

1. sort the array

2. for all elements in range [`low`, `high`]
    * apply **binary search** in `array`
    
    * if element is not found add it to `result` array

3. return `result` array

<br>

> implementation :

```python
def binarySearch(arr, target):
    end = len(arr) - 1
    start = 0

    while start <= end:
        mid = (start + end) // 2

        if arr[mid] == target:
            return True
        elif arr[mid] > target:
            end = mid - 1
        else:
            start = mid + 1
    
    return False

def printMissing(arr, low, high):
    arr.sort()

    result = []
    for item in range(low, high + 1):
        if not binarySearch(arr, item):
            result.append(item)

    return result

arr = list(map(int, input().split()))

low, high = map(int, input().split())

print(printMissing(arr, low, high))
```

> **Time and space complexity :**
<br>T(n) = O(n logn + m logn)
<br>*(sorting and searching m elements in range)*
<br>S(n) = O(1)

<br>

> approach :

1. maintain `hash` table for all elements in `array`

2. for all elements in range [`low`, `high`]
    * look in hash table
    
    * if element not in `hash` table add to `result` array

3. return `result` array

<br>

> implementation :

```python
def printMissing(arr, low, high):
    hash = {}

    for item in arr:
        if item not in hash:
            hash[item] = 1

    result = []
    for item in range(low, high + 1):
        if item not in hash:
            result.append(item)

    return result

arr = list(map(int, input().split()))

low, high = map(int, input().split())

print(printMissing(arr, low, high))
```

> **Time and space complexity:**
<br>T(n) = O(m + n)
<br>*(m = elements in range, n = elements in array)*
<br>S(n) = O(n)
