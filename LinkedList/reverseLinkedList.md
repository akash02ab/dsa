# Reverse Linked List

| input | output |
| --- | --- |
| `arr[]`: elements of linked list<br>from head to tail | `list`: reversed linked list |

<br>

```
input:
2 4 7 3 6 5

output:
5 6 3 7 4 2
```

<br>

> approach :

1. initalize three pointers
    * previous = `None`
    * current = head
    * nzxt = head.next
2. make current node point to previous node
    ```
    current.next = previous
    ```
3. move previous node to current node
    ```
    previous = current
    ```
4. move current node to next node
    ```
    current = next
    ```
5. move nzxt node to next node
    ```
    nzxt = nzxt.next
    ```
6. repeat from step 2 to 5 untill current node reaches the end of list
7. make head pointer point to new start of list
    ```
    head = previous
    ```
<br>

> iterative implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insertNode(self, data):
        node = Node(data)

        if self.head is None:
            self.head = node
            return

        current = self.head

        while current.next:
            current = current.next
        
        current.next = node

    def reverse(self):
        previous = None
        current = self.head
        nzxt = self.head.next

        while current:
            current.next = previous
            previous = current
            current = nzxt
            if nzxt: nzxt = nzxt.next

        self.head = previous        

    def printList(self):
        pointer = self.head

        while pointer:
            print(pointer.data, end = ' ')
            pointer = pointer.next

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insertNode(item)

print('Linked List:')
llist.printList()

llist.reverse()

print('\nReversed Linked List:')
llist.printList()
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)

<br>

> recursive implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insertNode(self, data):
        node = Node(data)

        if self.head is None:
            self.head = node
            return

        current = self.head

        while current.next:
            current = current.next
        
        current.next = node

    def reverse(self, head):
        if head is None or head.next is None:
            return head

        node = self.reverse(head.next)
        head.next.next = head
        head.next = None
        return node  

    def printList(self):
        pointer = self.head

        while pointer:
            print(pointer.data, end = ' ')
            pointer = pointer.next

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insertNode(item)

print('Linked List:')
llist.printList()

llist.head = llist.reverse(llist.head)

print('\nReversed Linked List:')
llist.printList()

```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)

