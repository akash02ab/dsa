# Seach in sorted rotated array

| input | output |
| --- | --- |
| `arr[]`: sorted rotated array <br> `k`: key | `i`: index of key |

<br>

> **example :**

```
input:
6 7 8 9 10 1 2 3 4 5
9

output:
3
```

<br>

> **approach :**

1. find the `middle` element

2. compare `middle` element with `first` element
    
    * if `firs`t element is less than or equal to `middle` element then array till `middle` is in correct sorted order
        
        * if `key` is in range(`start`, `middle`) then look in *left subarray*
        
        * else look for `key` in *right subarray*

    * if `first` element is greater than `middle` element then array is increasing order till some point then again, another increasing sequence start again
        
        * if `key` is in range(`middle`, `end`) then look in *right subarray*

        * else look for `key` in *left subarray*

3. return the index of `key` element

<br>

> **implementation :**

```python
def searchInSortedRotatedArray(arr, start, end, key):
    if start > end: return -1

    middle = (start + end) // 2

    if arr[middle] == key: return middle

    if arr[start] <= arr[middle]:
        if key >= arr[start] and key <= arr[middle]:
            return searchInSortedRotatedArray(arr, start, middle - 1, key)
        else:
            return searchInSortedRotatedArray(arr, middle + 1, end, key)
    else:
        if key >= arr[middle] and key <= arr[end]:
            return searchInSortedRotatedArray(arr, middle + 1, end, key)
        else:
            return searchInSortedRotatedArray(arr, start, middle - 1, key)


arr = list(map(int, input().split()))

key = int(input())

print(searchInSortedRotatedArray(arr, 0, len(arr) - 1, key))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)

