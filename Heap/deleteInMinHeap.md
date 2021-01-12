# Delete in min heap

| input | output |
| --- | --- |
| `arr`: min heap <br> `n`: target to delete | `arr`: min heap after deletion |

<br>

> example :

```
input:
8 2 5 4 6 3 1
4

output:
[1, 2, 3, 5, 6, 8]
```

<br>

> approach:

1. create **min heap**

2. look for `target` element

3. if `target` is found swap with last element in heap

4. delete the last element

5. heapify to reform **min heap**

<br>

> implementation :

```python
# Delete an arbritary element from min heap
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def minHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    smallest = index

    if left < size and arr[left] < arr[smallest]:
        smallest = left
    if right < size and arr[right] < arr[smallest]:
        smallest = right
    if smallest is not index:
        swap(arr, index, smallest)
        minHeapify(arr, smallest, size)

def buildMinHeap(arr, size):
    for i in range(size//2 - 1, -1, -1):
        minHeapify(arr, i, size)

def deleteInMinHeap(arr, target):
    index = -1
    
    for i in range(len(arr)):
        if arr[i] is target:
            index = i
            break
    
    if index is not -1:
        arr[index] = arr[len(arr) - 1]
        arr.pop()
        minHeapify(arr, index, len(arr))
    
    return arr


arr = list(map(int, input().split()))

target = int(input())

buildMinHeap(arr, len(arr))

print(deleteInMinHeap(arr, target))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)