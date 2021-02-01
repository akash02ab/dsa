# Reverse the perfect binary tree at alternate levels

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `arr`: preorder traversal of reversed <br> binary tree at alternate level |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
6 3 L
7 3 R
8 4 L
9 4 R
10 5 L
11 5 R
12 6 L
13 6 R
14 7 L
15 7 R
-1

output:
1 3 4 15 14 5 13 12 2 6 11 10 7 9 8
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perfrom **preorder traversal** on **binary tree**

3. if `level` is even `swap` the node values

4. goto *left* for first node and goto *right* for second node

5. again goto *right* for first node and goto *left* for second node

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
        self.result = False

    def findNode(self, root, key):
        if root is None: return

        if root.data == key:
            return root

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

    def swap(self, root1, root2):
        root1.data, root2.data = root2.data, root1.data

    def reverseAlternate(self, root1, root2, level):
        if root1 is None or root2 is None:
            return
        
        if level % 2 == 0:
            self.swap(root1, root2)
        
        self.reverseAlternate(root1.left, root2.right, level + 1)
        self.reverseAlternate(root1.right, root2.left, level + 1)

    def preorder(self, root):
        if root:
            print(root.data, end = ' ')
            self.preorder(root.left)
            self.preorder(root.right)   

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

tree.reverseAlternate(root.left, root.right, 0)

tree.preorder(root)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)