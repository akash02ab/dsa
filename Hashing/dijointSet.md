# Disjoint set

### Check whether two sets are disjoint or not.

<br>

| input | output |
| --- | --- |
| `set1`: first array <br> `set2`: second array | `boolean`: `True` if two `set` are disjoint, <br> `False` otherwise |

<br>

```
input:
2 4 1 3 5
6 7 9 8 13 43

output:
True
```
```
input:
3 6 9 12 15
6 12 18 24 30 36

output:
False
```

<br>

> approach :

1. **sort** first `set`

2. for each element of second `set` apply **binary search** on first `set`

3. if element is found in first `set`, than the `sets` are not disjoint

<br>

> implementation :

```python
def binarySearch(arr, target):
    end = len(arr)
    start = 0

    while start < end:
        mid = (start + end) // 2

        if arr[mid] == target:
            return True
        elif arr[mid] > target:
            end = mid - 1
        else:
            start = mid + 1
    
    return False


def isDisjoint(arr1, arr2):
    arr1.sort()

    for item in arr2:
        if binarySearch(arr1, item):
            return False
    
    return True

arr1 = list(map(int, input().split()))

arr2 = list(map(int, input().split()))

print(isDisjoint(arr1, arr2))
```
> **Time and space complexity :**
<br>T(n) = O(m logm + n logm)
<br>*to sort set1 it takes m logm and to search for n elements in set2 it takes n logm*
<br>S(n) = O(1)

<br>

> approach :

1. for each item of `set1` create hash table

2. for each item of `set2` look in hash table

3. if any item from `set2` is present in hash table, than `sets` are not disjoint

4. if no item is present in hash table, than `sets` are disjoint

<br>

> implementation :

```python
def isDisjoint(arr1, arr2):
    hash = {}

    for item in arr1:
        hash[item] = 1
    
    for item in arr2:
        if item in hash:
            return False
    
    return True

arr1 = list(map(int, input().split()))

arr2 = list(map(int, input().split()))

print(isDisjoint(arr1, arr2))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)