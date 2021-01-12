# k Largest Elements

### Find the 1<sup>th</sup> largest, 2<sup>th</sup> largest upto k<sup>th</sup> largest element in the array.

<br>

| input | output |
| --- | --- |
| `arr`: array of integers <br> `k`: +ve integer | `arr`: k largest elements |

<br>

> example :

```
input:
12 45 33 2 43 59 28
3

output:
[43, 45, 59]
```

<br>

> approach :

1. build **min heap** of first `k` elements in array

2. for remainnig `n - k` elements
    * if root of **min heap** is less than `current` element
        * swap `root` and `current` index
        * `min heapify` to maintain **min heap**

3. return first `k` elements in the array

<br>

> implementation :

```python
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
        swap(arr, smallest, index)
        minHeapify(arr, smallest, size)
    
def buildMinHeap(arr, size):
    for index in range(size//2 -1, -1, -1):
        minHeapify(arr, index, size)

def kLargestElements(arr, size, k):
    buildMinHeap(arr, k)

    for index in range(k, size):
        if arr[index] > arr[0]:
            swap(arr, 0, index)
            minHeapify(arr, 0, k)

    return arr[0 : k]

arr = list(map(int, input().split()))

k = int(input())

print(kLargestElements(arr, len(arr), k))
```

> **Time and space complexity :**
<br>T(n) = O(k + (n - k)logk)
<br>*`k` to build heap and `(n-k)logk` to compare and heapify rest of element*
<br>S(n) = O(1)