# Linear Search

## Linear Search array implementation

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: array element <br> x: target element | i: index of target element |

```
input:
n = 5
arr = [1, 3, 4, 2, 42]
x = 2

output:
i = 3 (array index starts at 0)
```

```python
def linearSearch(arr, size, target):
    for i in range(size):
        if arr[i] == target:
            return i
    return -1

n = int(input())

arr = list(map(int, input().split()))

target = int(input())

index = linearSearch(arr, n, target)

print(index)

```

```
Recurrence relation:
T(n) = T(n - 1) + 1
T(1) = 1 
```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(1)
```

<br>

---

<br>

## Linear Search linked list implementation

| input | output |
| --- | --- |
| n: size of linked list <br> list: singly llist of n elements <br> x: target element | i: index of target element | 

```
input:
n = 4  
list = *->1->3->7->14 (* denotes head of llist)
x = 14

output:
i = 4 (index starts at 1)

```

```python
class Node:
    def __init__(self, data):
        self.data = data
        self. next = None

class LinkedList:

    def insert(self, head, item):
        curr = head

        while curr.next is not None:
            curr = curr.next
        
        curr.next = Node(item)
        
    def linearSearch(self, head, item):
        index = 0
        
        while head.next is not None:
            if head.data == item:
                return index
            
            index += 1
            head = head.next
        
        return -1

    def printLinkedList(self, head):
        while head is not None:
            print(head.data, end = " ")
            head = head.next
        print()

llist = LinkedList()
head = Node('*')

n = int(input())

for _ in range(n):
    llist.insert(head, int(input()))

llist.printLinkedList(head)

index = llist.linearSearch(head, int(input()))

print(index)

```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(1)
```

