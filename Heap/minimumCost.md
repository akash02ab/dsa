# Given n-ropes with different lenght, connect with minimum cost

### NOTE :- Cost of connecting two smaller ropes is less than cost of connecting larger ropes.

<br>

| input | output |
| --- | --- |
| `arr`: length of ropes | `n`: minimum cost of tying all ropes |

<br>

> example :

```
input:
10 15 13 22 11

output:
163
```

<br>

> approach :

1. build a **min heap** of given array

2. `extract` two minimum length rope from **heap**
    * first_min
    * second_min

3. add to the `cost`
    * `cost = first_min + second_min`

4. `insert` the new length rope to the heap and `heapify`

5. repeat step 2-4 untill length of array becomes `1` i.e. *a single rope is formed*

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
    if smallest is not index:
        swap(arr, index, smallest)
        minHeapify(arr, smallest, size)

def buildMinHeap(arr, size):
    for index in range(size//2 - 1, -1, -1):
        minHeapify(arr, index, size)

def parent(index):
    return (index - 1) // 2

def extractMin(arr):
    temp = arr[0]
    arr[0] = arr[len(arr) - 1]
    arr.pop()
    minHeapify(arr, 0, len(arr))
    return temp

def insertMin(arr, item):
    arr.append(item)

    index = len(arr) - 1

    while index > 0 and arr[parent(index)] > arr[index]:
        swap(arr, parent(index), index)
        index = parent(index)

def minimumCost(arr):
    buildMinHeap(arr, len(arr))

    cost = 0
    while len(arr) != 1:
        first_min = extractMin(arr)
        second_min = extractMin(arr)
        cost += (first_min + second_min)
        insertMin(arr, first_min + second_min)

    return cost

arr = list(map(int, input().split()))

print(minimumCost(arr))
```

> **Time and space complexity :**
<br>T(n) = O(n log(n))
<br>S(n) = O(1)