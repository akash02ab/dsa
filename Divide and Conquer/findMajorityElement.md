# Find majority element in a sorted array

### In an array of size `n` if an element is present more than `(n / 2)` times then it's called a majoriy element.

<br>

| input | output |
| --- | --- |
| `arr[]`: sorted array | `n`: majority element |

<br>

> example :

```
input:
1 1 2 2 2 2 3

output:
2
```

<br>

> approach :

1. if an element is majority element it must present at middle

2. assume that middle element is middle element

3. search first occurence of middle element in the left part of array

4. check if middle element is present at right index
<br>where, `right = left + (size / 2)`

5. if array[middle] is equal to array[right] then majority element is found

6. else return `-1`

<br>

> implementation :

```python
def binarySearch(arr, start, end, target):
    if start <= end:
        mid = (start + end) // 2
        
        if arr[mid] == target and (mid == 0 or arr[mid] != arr[mid - 1]):
            return mid
        elif arr[mid] < target:
            return binarySearch(arr, mid + 1, end, target)
        else:
            return binarySearch(arr, start, mid - 1, target)
    
    return -1

def isMajorityElement(arr, n):
    half = n // 2
    # a majority element is alway present in middle of array
    middle = arr[half]

    # look for first occurence of middle element on the left side of array
    left = binarySearch(arr, 0, half - 1, middle)

    # if middle elemnet is not found in left part, then middle index is the first occurence
    if left == -1:
        left = half

    # to check the majority element, the right index must be atleast (left + half)
    right = left + half
    
    if arr[right] == middle:
        return middle
    
    return -1


arr = list(map(int, input().split()))

print(isMajorityElement(arr, len(arr)))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)