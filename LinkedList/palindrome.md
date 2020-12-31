# Check if linked list is palindrome or not

| input | output |
| --- | --- |
| `list`: linked list | `boolean`: True or False |

<br>

```
input:
a b b a

output:
True
```

<br>

> approach :

1. find the middle node of the linked list

2. split the linked list into two half by middle node

3. reverse the second half of the linked list

4. compare the first half and second half

5. if both the list are equal than the list is palindrome otherwise it is not

6. fix the original linked list

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

    def middleNode(self):
        slowPtr = self.head
        fastPtr = self.head
        previous = None

        while fastPtr and fastPtr.next:
            previous = slowPtr
            slowPtr = slowPtr.next
            fastPtr = fastPtr.next.next

        previous.next = None
        return slowPtr

    def reverse(self, head):
        previous, current, nzxt = None, head, head.next

        while current:
            current.next = previous
            previous = current
            current = nzxt
            nzxt = nzxt.next if nzxt else None

        return previous

    def isPalindrome(self):
        # divide the list in two halves
        firstHalf = self.head
        secondHalf = self.middleNode()

        # reverse the second half of list
        secondHalf = self.reverse(secondHalf)
        
        # check if palindrome or not
        first = firstHalf
        second = secondHalf
        flag = True
        
        while first:
            if first.data is not second.data:
                flag = False
                break
            
            first = first.next
            second = second.next

        # again reverse the second half of list
        secondHalf = self.reverse(secondHalf)

        # fix the linked list to original state
        while firstHalf.next:
            firstHalf = firstHalf.next
        
        firstHalf.next = secondHalf
        
        # flag will remain true if linked list is plaindrome, otherwise false
        return flag

llist = LinkedList()

arr = list(map(str, input().split()))

for item in arr:
    llist.insert(item)

print(llist.isPalindrome())
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)