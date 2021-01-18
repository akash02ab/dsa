# Convert min heap to max heap

| input | output |
| --- | --- |
| `arr`: min heap | `arr`: max heap |

<br>

> example :

```
input:
1 2 3 4 5

output:
[5, 4, 3, 1, 2]
```

<br>

> approach :

* for all the non-leaf node to root node
    * max heapify

<br>

> implementation :

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def maxHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    largest = index

    if left < size and arr[largest] < arr[left]:
        largest = left
    if right < size and arr[largest] < arr[right]:
        largest = right
    if index is not largest:
        swap(arr, index, largest)
        maxHeapify(arr, largest, size)

def buildMaxHeap(arr, size):
    for index in range(size//2 - 1, -1, -1):
        maxHeapify(arr, index, size)

    return arr

arr = list(map(int, input().split()))

print(buildMaxHeap(arr, len(arr)))
```
> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)