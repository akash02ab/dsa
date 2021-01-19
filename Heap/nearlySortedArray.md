# Sort a nearly sorted array

### A k-sorted array is an array where each element is at most k distance away from its target position in the sorted array.

<br>

| input | output |
| --- | --- |
| `arr`: nearly k-sorted array <br> `k`: sortedness of array | `arr`: completely sorted array |

<br>

> example :

```
input:
13 21 11 18 23 54 61 57
4

output:
[11, 13, 18, 21, 23, 54, 57, 61]
```

<br>

> approach :

1. build a **min heap** with first `k`-elements

2. for rest of the `n - k` elements:
    * add root of **heap** to `result` array
    * replace root of **heap** with next element
    * `minHeapify` to maintain **min heap** property

3. result contain `n - k` element and rest of the element is present in **min heap**
    * concatenate `heap` with `result` array

4. return `result` array

<br>

> implementation :

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def minHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    smallest = index

    if left < size and arr[smallest] > arr[left]:
        smallest = left
    if right < size and arr[smallest] > arr[right]:
        smallest = right
    if index is not smallest:
        swap(arr, index, smallest)
        minHeapify(arr, smallest, size)

def buildMinHeap(arr, size):
    for index in range(size//2 - 1, -1, -1):
        minHeapify(arr, index, size)

def sortK(arr, k):
    heap = []
    # add first k element to heap
    for i in range(k):
        heap.append(arr[i])

    # build min heap
    buildMinHeap(heap, k)

    result = []

    # add root of heap to result and replace with next element
    for i in range(k, len(arr)):
        result.append(heap[0])
        heap[0] = arr[i]
        minHeapify(heap, 0, k)

    # concatenate heap with result
    result += heap
    
    return result

arr = list(map(int, input().split()))

k = int(input())

print(sortK(arr, k))
```

> **Time and space complexity :**
<br>T(n) = O(n log(k))
<br>S(n) = O(k)