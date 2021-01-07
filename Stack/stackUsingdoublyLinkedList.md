# Stack operation

### Implement stack operation like push, pop, find middle and delete middle in O(1).

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.previous = None
        self.next = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.middle = None
        self.count = 0
        
    def push(self, data):
        node = Node(data)

        self.count += 1

        if self.head is None:
            self.head = node
            self.middle = node
            return
        
        self.head.next = node
        node.previous = self.head
        self.head = self.head.next

        if self.count % 2 == 1:
            self.middle = self.middle.next

    def pop(self):
        if self.head is None:
            return 'Underflow'
        
        self.count -= 1
        
        poped = self.head.data

        self.head = self.head.previous
        if self.head: self.head.next = None 

        if self.count % 2 == 0:
            self.middle = self.middle.previous

        return poped

    def findMiddle(self):
        return self.middle.data if self.middle else None

    def deleteMiddle(self):
        self.middle = self.middle.previous
        self.middle.next = self.middle.next.next
        self.middle.next.previous = self.middle
        self.count -= 1

dlList = DoublyLinkedList()

dlList.push(1)
print('middle: ', dlList.findMiddle())
dlList.push(2)
print('middle: ', dlList.findMiddle())
dlList.push(3)
print('middle: ', dlList.findMiddle())
dlList.deleteMiddle()
print('middle: ', dlList.findMiddle())
dlList.push(4)
print('middle: ', dlList.findMiddle())
dlList.push(5)
print('middle: ', dlList.findMiddle())
dlList.push(6)
print('middle: ', dlList.findMiddle())
dlList.push(7)
print('middle: ', dlList.findMiddle())
dlList.push(8)
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
print('pop: ', dlList.pop())
print('middle: ', dlList.findMiddle())
```

> **Time and space complexity :**
<br>T(n) = O(1)
<br>S(n) = O(1)