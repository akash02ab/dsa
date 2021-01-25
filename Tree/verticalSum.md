# Vertical sum of binary tree

### Find the horizontal distance of each node, for each node at position `(x, y)`, its left and right children will be at positions `(x - 1, y - 1)` and `(x + 1, y - 1)` respectively. <br> Find the sum of nodes that have same horizontal distance.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree | `arr[]`: vertical order traversal of binary tree |

<br>

> example :

```
input:
20 -1 H
15 20 L
25 20 R
12 15 L
18 12 R
23 25 L
27 25 R
-1

output:
0 : 43
-1 : 33
-2 : 12
1 : 25
2 : 27
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> appraoch :

1. build a **binary tree**

2. find the *horizontal distance* of each node

3. store the sum of values of node in `hash` according to their *horizontal distance*

4. return `hash` table

5. print the sum of nodes according to their *horizontal distance*

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
    
    def bulildHash(self, root, level):
        if root is None: return

        hash = defaultdict(int)

        hash[level] += root.data
        
        temp1 = self.bulildHash(root.left, level - 1)
        if temp1:
            for key in temp1:
                hash[key] += temp1[key]
        
        temp2 = self.bulildHash(root.right, level + 1)
        if temp2:
            for key in temp2:
                hash[key] += temp2[key]
        
        return hash

    def verticalSum(self, hash):
        for level, sum in hash.items():
            print(f'{level} : {sum}')
    

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

hash = tree.bulildHash(root, 0)

tree.verticalSum(hash)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)