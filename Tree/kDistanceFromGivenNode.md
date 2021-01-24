# k distance from given node

### Print all the nodes that are k distance from the given node.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree <br> `k, key`: level of tree, value of node | `arr[]`: all the nodes in `k`<sup>th</sup> level |

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
2 8

output:
10 14 22
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. find the target node

3. move to left subtree and right subtree and decrease the level

4. if level is equal to `0`
    * print the node value 

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
    
    def KdistanceNodesDown(self, root, k):
        if root is None or k < 0: return 
        
        if k == 0:
            print(root.data, end = ' ')
        else:
            self.KdistanceNodesDown(root.left, k - 1)
            self.KdistanceNodesDown(root.right, k - 1)
        
    def KdistanceNodesFromKey(self, root, key, k):
        if root is None: return -1

        if root.data == key:
            self.KdistanceNodesDown(root, k)
            return 0
        
        dl = self.KdistanceNodesFromKey(root.left, key, k)

        if dl != -1:
            if dl + 1 == k:
                print(root.data, end = ' ')
            else:
                self.KdistanceNodesDown(root.right, k - dl - 2)            
            
            return 1 + dl
        
        dr = self.KdistanceNodesFromKey(root.right, key, k)

        if dr != -1:
            if dr + 1 == k:
                print(root.data, end = ' ')
            else:
                self.KdistanceNodesDown(root.left, k - dr -2)
            
            return 1 + dr
        
        return -1

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

k, key = map(int, input().split())

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

tree.KdistanceNodesFromKey(root, key, k)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)