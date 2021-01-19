# Print all elements in sorted order in row and column wise sorted matrix

<br>

| input | output |
| --- | --- |
| `k`: number of rows in matrix <br> `arr[][]`: 2D row-wise sorted matrix | `arr[]`: all elements of matrix in sorted order |

<br>

> example :

```
input:
4
56 63 71
18 24 32 48
11 19 21 56 64
12 15 20

output:
[11, 12, 15, 18, 19, 20, 21, 24, 32, 48, 56, 56, 63, 64, 71]
```

<br>

> approach :

1. build **min heap** using first element of all `k` rows

2. add the root of **min heap** to `result` array

3. replace root of **min heap** with `next` element of same row

4. `minHeapify` to maintain **min heap** property

5. repeat step 2-4 for every element in `matirx`

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

def printSortedMatrix(matrix, k):
    heap = []
    # store item, row and next column in heap
    for i in range(k):
        heap.append([matrix[i][0], i, 1])
    # build min heap with first element of all k rows
    buildMinHeap(heap, k)

    result = []

    count = 0
    INT_MAX = 10**18
    
    # replace other element in matrix to root of head and minHeapify
    while count < k:
        [item, row, next] = heap[0]
        
        result.append(item)
        
        if(next < len(matrix[row])):
            heap[0] = [matrix[row][next], row, next + 1]
        else:
            heap[0] = [INT_MAX, row, next + 1]
            count += 1
        
        minHeapify(heap, 0, k)

    return result

k = int(input())

matrix = []

for _ in range(k):
    arr = list(map(int, input().split()))
    matrix.append(arr)

print(printSortedMatrix(matrix, k))
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup> log(k))
<br>T(n) = O(k)