# Merge two sorted linked list

| input | output |
| --- | --- |
| `list1`: linked list<br>`list2`: linked list | `list`: merged linked list |

<br>

```
input:
2 4 7
3 5 6

output:
2 3 4 5 6 7
```

<br>

> approach :

1. initialize `mergeList` pointer to list having smaller first element

2. initialize a pointer `tail` point to `mergeList`

3. compare node of both the list, make `next` of `tail` to node having lower value

4. advance `tail` to newly inserted node

5. advance `head` of list having lower value

6. repeat step 3 to 5 untill either `head` of list1 or list2 reaches last node

7. make `tail` point no remainig list if any

<br>

> implementaion :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head1 = None
        self.head2 = None

    def insert(self, data, llist):
        node = Node(data)

        if llist is 1 and self.head1 is None:
            self.head1 = node
            return

        if llist is 2 and self.head2 is None:
            self.head2 = node
            return 

        current = self.head1 if llist is 1 else self.head2

        while current.next:
            current = current.next

        current.next = node

    def merge(self):
        if self.head1 is None or self.head2 is None:
            return self.head1 if self.head1 else self.head2

        mergeList, tail = None, None

        if self.head1.data <= self.head2.data:
            mergeList = self.head1
            self.head1 = self.head1.next
        else:
            mergeList = self.head2
            self.head2 = self.head2.next

        tail = mergeList

        while self.head1 and self.head2:
            if self.head1.data <= self.head2.data:
                tail.next = self.head1
                tail = tail.next
                self.head1 = self.head1.next
            else:
                tail.next = self.head2
                tail = tail.next
                self.head2 = self.head2.next

        tail.next = self.head1 if self.head1 else self.head2

        return mergeList

    def printList(self, head):
        while head:
            print(head.data, end = ' ')
            head = head.next
    

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item, 1)

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item, 2)

head = llist.merge()

llist.printList(head)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)