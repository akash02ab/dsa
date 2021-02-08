# Largest sum independent set 

### Independent set of binary tree means sum of nodes which are not directly connected.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `n`: largest sum <br> of independent set |

<br>

> **example :**

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
6 3 L
7 3 R
-1

output:
23
```
```
each row contains [value, parent node, child position]
-1 at end represent end of input
```

<br>

> **implementation :**

```python 
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None 
        self.right = None 
        self.lis = None 

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


def largestIndependentSet(root):
    if root is None:
        return 0 
    
    if root.lis:
        return root.lis
    
    if root.left is None and root.right is None:
        root.lis = root.data
        return root.lis

    lisExclCurr = largestIndependentSet(root.left) + largestIndependentSet(root.right)

    lisInclCurr = root.data 

    if root.left:
        lisInclCurr += largestIndependentSet(root.left.left) + largestIndependentSet(root.left.right)
    if root.right:
        lisInclCurr += largestIndependentSet(root.right.left) + largestIndependentSet(root.right.right)
    
    root.lis = max(lisInclCurr, lisExclCurr)

    return root.lis

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break 
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(largestIndependentSet(root))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(n)