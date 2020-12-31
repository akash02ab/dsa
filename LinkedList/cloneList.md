# Clone Linked List

### Given linked list with three fields (data, next , random). `next` hold the link to next node while `random` hold the any random node within the `list`.

<br>

| input | output |
| --- | --- |
| `list`: linked list | `list`: cloned linked list |

<br>

```
input:
1 2 3 4 5

output:
Original list :
(1, 2) (2, 3) (3, 5) (4, 1) (5, 4)
Cloned list :
(1, 2) (2, 3) (3, 5) (4, 1) (5, 4)

* note random pointer are generated dynamically
  it may not be same every time
```

<br>

> approach :
1. clone each node and insert cloned node in between nodes of original list

2. set the random field of newly inserted nodes

3. split original list and cloned list

<br>

> implementation :

```python
from random import choice

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.random = None

class LinkedList:
    def __init__(self):
        self.head = None
        self.nodes = []

    def insert(self, data):
        node = Node(data)

        self.nodes.append(node)

        if self.head is None:
            self.head = node
            return 

        current = self.head

        while current.next:
            current = current.next

        current.next = node

    def randomize(self):
        # insert random nodes in `random` field of each node
        current = self.head

        while current:
            node = choice(self.nodes)

            current.random = node
            current = current.next

        return self.head

    def clone(self):
        # insert new node in between original list
        current = self.head

        while current:
            node = Node(current.data)
            node.next = current.next
            current.next = node
            current = current.next.next

        # update random field of newly inserted nodes
        current = self.head

        while current:
            current.next.random = current.random.next
            current = current.next.next
        
        # split original list and cloned list
        head1 = self.head # hold original list
        head2 = self.head.next # hold cloned list
        
        if head1 is None or head2 is None:
            return head1

        current = self.head

        while current:
            temp = current.next
            current.next = temp.next if temp else None
            current = temp

        return head2 

    def printList(self, current):
        while current:
            print((current.data, current.random.data), end = ' ')            
            current = current.next
        
        print()

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item)

head = llist.randomize()

print('Original list :')
llist.printList(head)

head = llist.clone()

print('Cloned list :')
llist.printList(head)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)