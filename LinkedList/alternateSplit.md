# Alternate split of linked list

| input | output |
| --- | --- |
| `list`: linked list | `list1`: odd split linked list <br> `list2`: even split linked list |

<br>

```
input:
1 2 3 4 5

output:
1 3 5
2 4
```

<br>

> approach :

1. initialize two pointers
    * head1 = head
    * head2 = head.next

2. start from `head` node and assign `temp` to `head.next`

3. assign `head.next` to `temp.next`

4. assign `head` to `temp`

5. repeat step 2 to 4 till end of list

6. return `head1` and `head2`

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
        node = Node(data)

        if self.head is None:
            self.head = node
            return
        
        current = self.head

        while current.next:
            current = current.next

        current.next = node

    def printList(self, head):
        while head:
            print(head.data, end = ' ')
            head = head.next

        print()

    def alternateSplit(self):
        if self.head is None or self.head.next is None:
            return self.head, None

        head1 = self.head
        head2 = self.head.next

        temp = None

        while self.head:
            temp = self.head.next
            self.head.next = temp.next if temp else None
            self.head = temp

        return head1, head2


llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item)

head1, head2 = llist.alternateSplit()

llist.printList(head1)
llist.printList(head2)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)