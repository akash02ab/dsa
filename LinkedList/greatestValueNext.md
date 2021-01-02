# Greatest value next

### Find the greatest value node in the linked list on its right side

| input | output |
| --- | --- |
| `list`: linked list | `list`: linked list with<br>updated random field |

<br>

```
input:
2 4 7 3 6 5

output:
7 7 6 6 5 None
```

<br>

> approach :
1. reverse the `linked list`

2. find the `maximum` value seen so far

3. update the `random` field of each node

4. again reverse the `linked list`

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.random = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert(self, data):
        node = Node(data)

        if self.head is None:
            self.head = node
            return 

        current = self.head

        while current.next:
            current = current.next

        current.next = node

    def reverseList(self):
        previous = None
        current = self.head 
        nzxt = self.head.next if self.head else None

        while current:
            current.next = previous
            previous = current
            current = nzxt
            nzxt = nzxt.next if nzxt else None

        return previous

    def greatestNodeNext(self):
        head = self.reverseList()
        self.head = head
        maxSoFar = head

        head = head.next if head else None

        while head:
            head.random = maxSoFar

            if maxSoFar.data < head.data:
                maxSoFar = head

            head = head.next

        head = self.reverseList()
    
        return head

    def printNextRandomPointer(self, head):
        while head:
            print(head.random.data if head.random else None, end = ' ')
            head = head.next
    

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item)

head = llist.greatestNodeNext()

llist.printNextRandomPointer(head)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)