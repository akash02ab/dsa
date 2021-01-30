# Convert binary tree into sum tree

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build a binary tree | `arr[]`: preorder traversal of <br> converted sum tree |

<br>

> example :

```
input:
55 -1 H
45 55 L
9 55 R
25 45 L
20 45 R
3 9 L
4 9 R
-1

output:
55 46 26 20 9 5 4
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perform *postorder traversal* of **binary tree**

3. if node is not `leaf` node:
    * find difference with `leaf` nodes
        * difference = node - (left child + right child)
        * if difference > 0:
            * root = root - difference
        * if difference < 0:
            * recursively `increment` the leaf nodes

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
    
    def isLeaf(self, root):
        return root.left is None and root.right is None 

    def increment(self, node, difference):
        if node.left:
            node.left.data += difference
            self.increment(node.left, difference)
        elif node.right:
            node.right.data += difference
            self.increment(node.right, difference)

    def convertTree(self, root):
        if root is None or self.isLeaf(root):
            return
        
        self.convertTree(root.left)
        self.convertTree(root.right)

        if root.left:
            left = root.left.data 
        
        if root.right:
            right = root.right.data

        difference = left + right - root.data

        if difference > 0:
            root.data = root.data - difference
        
        if difference < 0:
            self.increment(root, -difference)

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

tree.convertTree(root)

tree.preorder(root)
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n)