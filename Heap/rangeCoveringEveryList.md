# Range (min) covering every list

### Given k-sorted list, find the min-range to which atleast one number belongs from every list.

<br>

| input | output |
| --- | --- |
| `k`: number of list <br> `arr[][]`: k-sorted list | `range`: (start - end) |

<br>

> example :

```
input:
4
15 27 35 42
12 14 16 21
10 25 55 67
23 33 41 43

output:
(21, 27)
```

<br>

> approach :

1. build a **min-heap** from first element of every list

2. find the `minimum` and `maximum` element in the **heap**
    * min = root of heap
    * max = one of leaf of heap
    * range = max - min + 1

3. update `range` if a *range shorter* than previous one is found

4. delete `root` of **heap** and add `next` element from that list to the root and `heapify`

5. repeat the above steps untill one of the `k` list is *explored* completely

<br>

> implementation :

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def minHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    smallest = index

    if left < size and arr[left][0] < arr[smallest][0]:
        smallest = left
    if right < size and arr[right][0] < arr[smallest][0]:
        smallest = right
    if index is not smallest:
        swap(arr, index, smallest)
        minHeapify(arr, smallest, size)

def buildMinHeap(arr, size):
    for index in range(size//2 - 1, -1, -1):
        minHeapify(arr, index, size)

def findSmallestRange(arr, k):
    heap = []
    # add first element of each list to heap
    for i in range(k):
        heap.append([arr[i][0], i, 0])
        
    # build a min heap
    buildMinHeap(heap, len(heap))

    # initialize start, end and range
    start, end, _range = 0, 0, 999999
    while True:
        # get the root element of the heap
        [min, row, current] = heap[0]

        # find the max element from leaf node of heap
        max = 0
        size = len(heap)
        for i in range(size // 2, size):
            if heap[i][0] > max:
                max = heap[i][0]

        # compute range if a smaller range is found than update
        if _range > max - min + 1:
            start = min
            end = max
            _range = max - min + 1
        
        # replace root element if with next element of list
        if current < len(arr[row]) - 1:
            next = current + 1
            heap[0] = [arr[row][next], row, next]
            minHeapify(heap, 0, size)
        else:
            return start, end


k = int(input())

arr = []
for _ in range(k):
    temp = list(map(int, input().split()))
    arr.append(temp)

print(findSmallestRange(arr, k))
```

> **Time and space complexity :**
<br>T(n) = O(nk)
<br>S(n) = O(k)