# Merge K sorted linked list

| input | output |
| --- | --- |
| `k`: number of linked list <br> `list`: linked list | `list`: k sorted linked list |

<br>

```
input:
8
1 3 5
2 6 9
10 18
4 8
7 11
12 13 14
15 16 19
18

output:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 18 18 19
```

<br>

> approach :

1. sort two list at a time
    * first and last
    * second and second last
    * third and third last
    <br>and so on . . . upto last list

2. reduce the length of list array by half

3. again repeat step 1 and 2 untill all the list are combined

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self, k):
        self.head = [None] * k

    def insert(self, data, llist):
        node = Node(data)

        if self.head[llist] is None:
            self.head[llist] = node
            return

        current = self.head[llist]

        while current.next:
            current = current.next

        current.next = node

    def merge(self, list1, list2):
        if list1 is None:
            return list2
        
        if list2 is None:
            return list1

        mergeList, tail = None, None

        if list1.data <= list2.data:
            mergeList = list1
            list1 = list1.next
        else:
            mergeList = list2
            list2 = list2.next

        tail = mergeList

        while list1 and list2:
            if list1.data <= list2.data:
                tail.next = list1
                tail = tail.next
                list1 = list1.next
            else:
                tail.next = list2
                tail = tail.next
                list2 = list2.next

        tail.next = list1 if list1 else list2

        return mergeList

    def mergeKsortedList(self, last):
        while last:
            start, end = 0, last

            while start < end:
                self.head[start] = self.merge(self.head[start], self.head[end])
                start += 1
                end -= 1

                if start >= end:
                    last = end

        return self.head[0]

    def printList(self, head):
        while head:
            print(head.data, end = ' ')
            head = head.next

k = int(input())

llist = LinkedList(k)

for i in range(k):
    arr = list(map(int, input().split()))

    for item in arr:
        llist.insert(item, i)

head = llist.mergeKsortedList(k - 1)

llist.printList(head)
```

> **Time and space complexity :**
<br>T(n) = O(nk logk)
<br>S(n) = O(1)