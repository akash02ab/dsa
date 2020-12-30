# Find intersection node in linked list

| input | output |
| --- | --- |
| `list1`: linked list <br> `list2`: linked list | `n`: intersecting point of linked list |

<br>

```
input:
1 2 3 4 5 6 7 8
12 34 6 7 8

output:
6
```

<br>

> appraoch :
1. find the lenght of both linked list
    ```
    l1 = length of list1
    l2 = length of list2
    ```
2. find the absolute difference of their lengths
    ```
    diff = |l1 - l2|
    ```
3. move the `head` of longer list as much as value of `diff`

4. move the `head` of both list simultaneously untill `node` of both the list are equal 

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head1 = None
        self.head2 = None

    def getNode(self, head, target):
        while head:
            if head.data == target:
                return head

            head = head.next

        return None

    def insert(self, data, llist):
        node = Node(data)
        head = self.head1 if llist is 1 else self.head2

        if head is None and llist is 1:
            self.head1 = node
            return 
        elif head is None and llist is 2:
            self.head2 = node
            return
        
        temp = None

        while head.next:
            head = head.next

        if llist is 2: temp = self.getNode(self.head1, data)

        if temp:
            head.next = temp
            return 1
        else:
            head.next = node
            return 0

    def countNode(self, head):
        count = 0

        while head:
            count += 1
            head = head.next

        return count

    def getIntersectionPoint(self, diff, head1, head2):
        while diff:
            head1 = head1.next
            diff -= 1

        while head1 and head2:
            if head1 == head2:
                return head1.data

            head1 = head1.next
            head2 = head2.next

        return -1

    def intersectionNode(self):
        l1 = self.countNode(self.head1)
        l2 = self.countNode(self.head2)

        diff = abs(l1 - l2)

        return self.getIntersectionPoint(diff, self.head1, self.head2) if (l1 > l2) else self.getIntersectionPoint(diff, self.head2, self.head1)  

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item, 1)

arr = list(map(int, input().split()))

for item in arr:
    if llist.insert(item, 2):
        break

print(llist.intersectionNode())
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)