# Is given binary tree a sum tree or not

### A sum tree is one whose sum of child node is equal to parent node. This property follows for all the nodes except leaf nodes.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build a binary tree | `boolean`: `True` if binary tree is sum tree, <br> `False` if it is not sum tree |

<br>

> example :

```
input:
10 -1 H
3 10 L
4 10 R
1 3 L
2 3 R
-1

output:
True
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> appraoch :

1. bulid a **binary tree**

2. if left and right leaf exist then find their sum and compare to parent

3. if sum parent node matches their child sum than return `True`

4. otherwise return `False`

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
    
    def isLeaf(self, node):
        if node.left is None and node.right is None: 
            return True
        
        return False

    def sumTree(self, root):
        if root is None: return False
        
        if self.isLeaf(root): return True

        leftSum = rightSum = 0

        if self.sumTree(root.left) and self.sumTree(root.right):
            if self.isLeaf(root.left): 
                leftSum = root.left.data
            else:
                leftSum = 2 * root.left.data
            
            if self.isLeaf(root.right): 
                rightSum = root.right.data
            else:
                rightSum = 2 * root.right.data

            return root.data == leftSum + rightSum
        
        return False

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.sumTree(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)