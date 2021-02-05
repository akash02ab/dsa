# Nut and bolt problem

### Given a set of n nuts of different sizes and n bolts of different sizes. There is a one-one mapping between nuts and bolts. Match nuts and bolts efficiently. The nuts cannot be compared with other nuts similarly, bolts cannot be compared with other bolts.

<br>

| input | output |
| --- | --- |
| `arr[]`: set of nuts <br> `arr[]`: set of bolts | `arr[]`: matching nuts <br> `arr[]`: matching bolts |

<br>

> example :

```
input:
@ # $ % ^ &
$ % & ^ @ #

output:
['#', '$', '%', '&', '@', '^']
['#', '$', '%', '&', '@', '^']
```

<br>

approach :

1. perform a partition by picking last elemnet of `bolts` array as `pivot`

2. rearrange the array of `bolts` and return partition index such that all nuts smaller are on left and larger are on right

3. perforom a partition on `nuts` array using returned `index` by previous partition call

4. apply partitioning of left and right sub-array of `nuts` and `bolts`

<br>

> implementation :

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def partition(arr, start, end, pivot):
    i = j = start
    
    while j < end:
        if arr[i] < pivot:
            swap(arr, i, j)
            i += 1
        
        if arr[j] == pivot:
            swap(arr, j, end)
            j -= 1
        
        j += 1

    swap(arr, i, end)
    return i

def matchNutsBolts(nuts, bolts, start, end):
    if start < end:
        pivot = partition(nuts, start, end, bolts[end])
        partition(bolts, start, end, nuts[pivot])
        matchNutsBolts(nuts, bolts, start, pivot - 1)
        matchNutsBolts(nuts, bolts, pivot + 1, end)

nuts = list(map(str, input().split()))
bolts = list(map(str, input().split()))

size = len(nuts)

matchNutsBolts(nuts, bolts, 0, size - 1)

print(nuts)
print(bolts)
```

<br> 

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(1)