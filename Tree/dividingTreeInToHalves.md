# Check if removing edge can divide the tree into two halves

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `boolean`: `True` if division is possible, <br> `False` otherwise |

<br>

> example :

```
input:
2 -1 H
1 2 L
3 2 R
8 1 R
9 3 L
4 3 R
6 8 L
7 9 R
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

> approach :

1. build a **binary tree**

2. count the `total` number of nodes in **binary tree**

3. count the total nodes for each subtree in **binary tree**

4. if at any point the `node count` is equal to half the `total node count` then division is possible

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

    def countNode(self, root, size):
        if root is None: return 0

        count = 1 + self.countNode(root.left, size) + self.countNode(root.right, size)

        if count == size - count:
            self.result = True
        
        return count

    def isLeaf(self, node):
        return node.left is None and node.right is None 

    def countTotalNode(self, root):
        if root is None:
            return 0
        if self.isLeaf(root):
            return 1
        
        return 1 + self.countTotalNode(root.left) + self.countTotalNode(root.right)
    
    def isdivisionPossible(self, root):
        if root is None: return True 

        totalNode = self.countTotalNode(root)
        
        self.countNode(root, totalNode)

        return self.result

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.isdivisionPossible(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)