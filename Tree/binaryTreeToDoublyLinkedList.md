# Binary tree to doubly linked list

### Convert the binary tree into doubly linked list, in such a way that the order of nodes in doubly linked list represent the inorder traversal of binary tree.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to bulid binary tree | `arr[]`: inorder traversal of BT stored in form of DLL |

<br>

> example :

```
input: 
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
-1

output:
4 2 5 1 3
```

<br>

> approach :

1. convert left sub-tree into doubly linked list

2. convert right sub-tree into doubly linked list

3. join the root, left sub-tree and right sub-tree

<br>

> implementation :

```python
class Node: 
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None
    
    def findNode(self, root, key):
        if root is None: return

        if root.data == key: return root

        temp1 = self.findNode(root.left, key)
        if temp1: return temp1
        temp2 = self.findNode(root.right, key)
        return temp2
    
    def insert(self, data):
        [value, parent, child] = data
        node = Node(int(value))

        if self.root is None:
            self.root = node
            return 
        
        ptr = self.findNode(self.root, int(parent))

        if child is 'L':
            ptr.left = node
        else:
            ptr.right = node 
        
    def getRootNode(self):
        return self.root 
    
    def convertToDoublyLinkedList(self, root):
        if(root.left):
            lst = self.convertToDoublyLinkedList(root.left)
            # goto tail of linked list and merge with root
            while lst.right: lst = lst.right
            lst.right = root
            root.left = lst
        
        if(root.right):
            rst = self.convertToDoublyLinkedList(root.right)
            # goto head of linked list and merge with root
            while rst.left: rst = rst.left
            rst.left = root
            root.right = rst

        return root

    def printDoublyLinkedList(self, head):
        # head contain the root of binary tree
        # goto head of linked list
        while head.left:
            head = head.left
        # print the linked list which is inorder traversal of binary tree
        while head:
            print(head.data, end = ' ')
            head = head.right
        print()

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

head = tree.convertToDoublyLinkedList(root)

tree.printDoublyLinkedList(head)
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n)