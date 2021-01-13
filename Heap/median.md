# Median in stream of numbers

| input | output |
| --- | --- |
| `arr[]`: positive integers | `arr[]`: median after each insertion |

<br>

> example :

```
input:
5 15 1 3 2 8 7 9 10 6 11 4

output:
[5, 10, 5, 4, 3, 4, 5, 6, 7, 6, 7, 6]
```

<br>

> approach :

1. create two heaps
    * `minHeap`
    * `maxHeap`

2. `insert` each element one by one and perform insertion in such a way that `median` can be found directly from *root* of both or either of **heap**

3. if size of both the **heaps** are equal
    * if `current` element is smaller than effective `median`
        * `insert` into `maxHeap`
    * else
        * `insert` into `minHeap`
    
4. if size of `maxHeap` is greater than `minHeap`
    * if `current` element is smaller than effective `median`
        * `delete` `max` from `maxHeap`
        * `insert` `max` in `minHeap`
        * `insert` `current` in `maxHeap`
    * else
        * `insert` `current` in `minHeap`

5. if size of `minHeap` is greater than `maxHeap`
    * if `current` elemnt is smaller than effective `median`
        * `insert` `current` in `maxHeap`
    * else
        * `delete` `min` from `minHeap`
        * `insert` `min` in `maxHeap`
        * `insert` `current` in `minHeap`

6. update `median` after each insertion

<br>

> implementation :

```python
def size(arr):
    return len(arr)

def getRoot(arr):
    return arr[0]

def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def maxHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    largest = index

    if left < size and arr[left] > arr[largest]:
        largest = left
    if right < size and arr[right] > arr[largest]:
        largest = right
    if largest is not index:
        swap(arr, largest, index)
        maxHeapify(arr, largest, size)

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

def deleteMax(arr, size):
    max = arr[0]
    swap(arr, 0, size - 1)
    arr.pop()
    maxHeapify(arr, 0, len(arr))
    return max

def deleteMin(arr, size):
    min = arr[0]
    swap(arr, 0, size - 1)
    arr.pop()
    minHeapify(arr, 0, len(arr))
    return min

def parent(index):
    return (index - 1) // 2

def insertMax(arr, item):
    # insert new item at end
    arr.append(item)

    index = len(arr) - 1
    # maintain the max heap property
    while index > 0 and arr[parent(index)] < arr[index]:
        swap(arr, parent(index), index)
        index = parent(index)

def insertMin(arr, item):
    # insert new item at end
    arr.append(item)

    index = len(arr) - 1
    # maintain the min heap property
    while index > 0 and arr[parent(index)] > arr[index]:
        swap(arr, parent(index), index)
        index = parent(index)

def findMedian(arr):
    maxHeap = []
    minHeap = []
    result = []
    median = 0

    # for each element in array
    for current in arr:
        '''
        if size of both the heaps are equal then, sum of their sizes is always even
        inserting a new element will make the sum of heap sizes an odd number
        median is simply the middle element if both the heaps are joined
        '''
        if size(minHeap) == size(maxHeap):
            '''
            if current element is smaller than median then insert into maxHeap
            else insert into minHeap
            the size of the heap is incresed by one after insertion
            thus, median is simply root element of heap in which insertion is performed
            '''
            if current < median:
                insertMax(maxHeap, current)
                median = getRoot(maxHeap)
            else:
                insertMin(minHeap, current)
                median = getRoot(minHeap)
            
            result.append(median)
        
        elif size(minHeap) < size(maxHeap):
            '''
            if current is smaller than median then insertion is to be done in maxHeap
            but maxHeap size is already greater than that of minHeap
            inserting further in maxHeap will distort the property of finding median from root of heaps
            therefore, perform deletion on root of maxHeap and insert deleted element to minHeap
            now, insert new element in maxHeap and their sizes also become equal
            '''
            if current < median:
                max = deleteMax(maxHeap, size(maxHeap))
                insertMin(minHeap, max)
                insertMax(maxHeap, current)
            else:
                insertMin(minHeap, current)
            '''
            since, insertion makes sum of sizes of both the heap even
            thus, median is average of root of both the heaps
            '''
            median = (getRoot(minHeap) + getRoot(maxHeap)) // 2
            result.append(median)
        
        else:
            if current < median:
                insertMax(maxHeap, current)
            else:
                min = deleteMin(minHeap, size(minHeap))
                insertMax(maxHeap, min)
                insertMin(minHeap, current)

            median = (getRoot(minHeap) + getRoot(maxHeap)) // 2
            result.append(median)
    
    return result


arr = list(map(int, input().split()))

print(findMedian(arr))
```

> **Time and space complexity :**
<br>T(n) = O(n log(n))
<br>*insertion, deletion and heapify all takes O(logn) and all this operation is done for each element in array*
<br>S(n) = O(n)
<br>*both heaps are maintained separately*

