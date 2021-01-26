# Top view of binary tree

### Top view of a binary tree is the set of nodes visible when the tree is viewed from the top.

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree | `arr[]`: top view of binary tree |

<br>

> example :

```
input:
20 -1 H
43 20 L
2 20 R
3 43 L
17 43 R
9 2 L
10 2 R
99 9 L
33 9 R
-1

output:
[3, 43, 20, 2, 10]
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

> approach :

1. build a **binary tree**

2. traverse the **binary tree** in preorder traversal

3. find the *horizontal distance* of all the nodes while traversal

4. maintain the `hash` table for newly discovered *horizontal distance*

5. keep updating the nodes whose *horizontal distance* is discovered so that, `hash` contain the bottom view

<br>

> implementation :

```python
from collections import defaultdict

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

    def buildHashTable(self, root, level, hash):
        if root is None: return        
        
        if level not in hash:
            hash[level] = root.data

        self.buildHashTable(root.left, level - 1, hash)
        
        self.buildHashTable(root.right, level + 1, hash)   
        

    def findMinMax(self, hash):
        return min(hash), max(hash)

    def bottomView(self, hash, min, max):
        bottom = []

        while min <= max:
            bottom.append(hash[min])
            min += 1
        
        return bottom

tree = BinaryTree()

arr = []
while True: 
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

hash = defaultdict(int)

tree.buildHashTable(root, 0, hash)

_min, _max, = tree.findMinMax(hash)

print(tree.bottomView(hash, _min, _max))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)