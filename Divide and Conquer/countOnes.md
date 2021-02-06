# Given array of only 0's and 1's. All the 0's appear before 1's. Count the number of 1's in the array

<br>

| input | output |
| --- | --- |
| `arr[]`: stream of 0's followed by 1's | `n`: count of 1's |

<br>

> **example :**

```
input:
0 0 0 0 1 1 1 1 1 1 1

output:
7
```

<br>

> **approach :**

1. find the first occurence of `1` in array using binary search
    
    * find `middle` element
    
    * if `middle` element is `1` and `left` of middle element is `0`:
        * return the `index` of `middle` element
    
    * if `middle` elemnet is `1` then look for first one in *left subarray*
    
    * if `middle` element is `0` then look for first one in *right subarray*

2. count the number of one's
    * `count = size of array - index of first one`

3. return count

<br>

> **implementation :**

```python
def getFirstOne(arr, start, end):
    if start > end:
        return -1
    
    middle = (start + end) // 2

    if (middle == 0 or arr[middle - 1] == 0) and arr[middle] == 1:
        return middle
    
    if arr[middle] == 1:
        return getFirstOne(arr, start, middle - 1)
    else:
        return getFirstOne(arr, middle + 1, end)

def countNumberOfOnes(arr):
    size = len(arr)
    first = getFirstOne(arr, 0, size - 1)

    if first == -1:
        return 0
    return size - first

arr = list(map(int, input().split()))

print(countNumberOfOnes(arr))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)