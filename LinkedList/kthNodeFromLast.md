# k<sup>th</sup> node from end of linked list

| input | output |
| --- | --- |
| `list`: linked list<br>`k`: number | `n`: k<sup>th</sup> element from end |

<br>

```
input: 
1 2 3 4 5 6 7
3

output:
5
```

<br>

> approach :

1. initialize two pointers
    * p = head
    * q = head
2. move pointer `q` to k<sup>th</sup> node
3. move both pointer `p` and `q` till `q` reaches end of linked list
4. when `q` reached end `p` is at k<sup>th</sup> node from the end
5. return `data` of `p`<sup>th</sup> node

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

    def kthNodeFromEnd(self, k):
        p, q = self.head, self.head

        while k and q:
            q = q.next
            k -= 1
        
        if q is None and k:
            return -1

        while q:
            q = q.next
            p = p.next

        return p.data

llist = LinkedList()

arr = list(map(int, input().split()))

for item in arr:
    llist.insert(item)

k = int(input())

print(llist.kthNodeFromEnd(k))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)