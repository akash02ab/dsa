# Vertical order traversal of binary tree

### Find the horizontal distance of each node, for each node at position `(x, y)`, its left and right children will be at positions `(x - 1, y - 1)` and `(x + 1, y - 1)` respectively. <br> Print the nodes that occurs in increasing order of horizontal distance.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree | `arr[]`: vertical order traversal of binary tree |

<br>

> example :

```
input:
20 -1 H
8 20 L
22 20 R
4 8 L
12 8 R
10 12 L
14 12 R
-1

output:
[4, 8, 10, 20, 12, 14, 22]
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

3. store all the nodes in `hash` according to their *horizontal distance*

4. find the `min` and `max` key in `hash` table

5. print all the node values in `hash` table from `min` key to `max` key

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

    def buildHashTable(self, root, level):
        if root is None: return

        hash = defaultdict(list)
        
        hash[level].append(root.data)

        temp1 = self.buildHashTable(root.left, level - 1)

        if temp1: 
            for key in temp1:
                if key in hash:
                    for item in temp1[key]:
                        hash[key].append(item)
                else:
                    hash[key] = temp1[key]
        
        temp2 = self.buildHashTable(root.right, level + 1)   
        
        if temp2:
            for key in temp2:
                if key in hash:
                    for item in temp2[key]:
                        hash[key].append(item)
                else:
                    hash[key] = temp2[key]

        return hash

    def findMinMax(self, hash):
        return min(hash), max(hash)

    def verticalOrderTraversal(self, hash, min, max):
        vertical = []

        while min <= max:
            vertical += hash[min]
            min += 1
        
        return vertical

tree = BinaryTree()

arr = []
while True: 
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

hash = tree.buildHashTable(root, 0)

_min, _max, = tree.findMinMax(hash)

print(tree.verticalOrderTraversal(hash, _min, _max))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)