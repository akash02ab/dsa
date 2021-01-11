# Find maximum element in min heap

| input | output |
| --- | --- |
| `arr`: heap | `n`: maximum element |

<br>

```
input:
2 4 7 3 6 5

output:
7
```

<br>

> appraoch :

1. create min heap

2. look for leaf nodes

3. find maximum element among leaf nodes
    
    `leaf node starts from (size + 1) / 2`

<br>

> implementation :

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def minHeapify(arr, index, size):
    left = 2 * index + 1
    right = 2 * index + 2
    smallest = index

    if left < size and arr[left] < arr[index]:
        smallest = left
    if right < size and arr[right] < arr[smallest]:
        smallest = right
    if smallest is not index:
        swap(arr, index, smallest)
        minHeapify(arr, index, smallest)

def buildMinHeap(arr, size):
    for i in range(size//2, -1, -1):
        minHeapify(arr, i, size)

def findMaxElement(arr, size):
    max = -99999

    for i in range((size + 1) // 2, size, 1):
        if arr[i] > max:
            max = arr[i]
    
    return max

arr = list(map(int, input().split()))

size = len(arr)

buildMinHeap(arr, size)

print(findMaxElement(arr, size))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)