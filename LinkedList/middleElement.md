# Middle element of liked list

| input | output |
| --- | --- |
| `list`: linked list | `n`: middle element |

<br>

```
input:
1 2 3 4 5 6

output:
4
```

<br>

> approach :
1. initialize two pointers
 * fast pointer = head
 * slow pointer = head
2. move fast pointer skip two nodes at a time and slow pointer by one
3. by the time fast pointer reaches the last node slow pointer will be in the middle node
4. return the data of node pointed by slow pointer

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert(self, data):
        node =  Node(data)

        if self.head is None:
            self.head = node
            return 

        current = self.head

        while current.next:
            current = current.next

        current.next = node

    def middleElement(self):
        slowPtr = self.head
        fastPtr = self.head

        while fastPtr and fastPtr.next:
            slowPtr = slowPtr.next
            fastPtr = fastPtr.next.next

        return slowPtr.data


llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item)
    
print(llist.middleElement())
```
> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)