# k<sup>th</sup> largest element

<br>

| input | output |
| --- | --- |
| `arr`: array of integers <br> `k`: +ve integer | `n`: k<sup>th</sup> largest element |

<br>

> example :

```
input:
2 4 7 3 6 5 9 8 1
3

output:
7
```

<br>

> appraoch :

1. build **min heap** with first `k` elements

2. for rest of `n - k` elements:
    * replace root of **heap** if element greater than root element is found
    * `minHeapify` to maintain **min heap** property

3. return the root of **min heap**

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

def kLargestElement(arr, k):
    heap = []
    # add first k element to heap
    for i in range(k):
        heap.append(arr[i])

    # build min heap
    buildMinHeap(heap, k)

    ''' 
    for rest of (n - k) elements if any element larger that root of heap is found
    replace root with next largest element and minHeapify
    '''
    for i in range(k, len(arr)):
        if heap[0] < arr[i]:
            heap[0] = arr[i]
            minHeapify(heap, 0, k)
    
    return heap[0]

arr = list(map(int, input().split()))
k = int(input())
print(kLargestElement(arr, k))
```

> **Time and space complexity :**
<br>T(n) = O((n - k) log(k))
<br>S(n) = O(k)