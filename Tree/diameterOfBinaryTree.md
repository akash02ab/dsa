# Diameter of binary tree

### The diameter of a tree is the number of nodes on the longest path between two end nodes.

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
4
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. the `diameter` of a **binary tree** is the largest of the following quantities:

    * the `diameter` of left subtree
    
    * the `diameter` of right subtree
    
    * the longest path between leaves that goes through the root of tree 
    *(this can be computed from the heights of the subtrees of binary tree)*

3. return `diameter` of **binary tree**

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

    def height(self, root):
        if root is None:
            return 0

        return 1 + max(self.height(root.left), self.height(root.right))

    def diameter(self, root):
        leftHeight = rightHeight = leftDiameter = rightDiameter = 0

        if root is None:
            return 0

        leftHeight = self.height(root.left)
        rightHeight = self.height(root.right)

        leftDiameter = self.diameter(root.left)
        rightDiameter = self.diameter(root.right)
        
        return max(leftHeight + rightHeight + 1, max(leftDiameter, rightDiameter))

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

print(tree.diameter(tree.getRootNode()))
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n)