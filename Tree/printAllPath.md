# Print all path from root to leaf

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `arr[][]`: all path from root to leaf |

<br>

> example :

```
input:
5 -1 H
3 5 L
7 5 R
1 3 L
4 3 R
6 7 L
8 7 R
2 1 R
4 8 R
-1

output:
[5, 3, 1, 2]
[5, 3, 4]
[5, 7, 6]
[5, 7, 8, 4]
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perform *preorder traversal* on **binary tree** from root at `level` `0`

3. add the node item in `arr` at current `level`

4. if the node `isLeaf` print the `arr` from index `0 to level`

5. recursively traverse the *left subtree* and *right subtree*

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
        return root.left == None and root.right == None

    def printAllPath(self, root, level, arr):
        if root is None: return 

        arr[level] = root.data
        
        if self.isLeaf(root):
            print(arr[0 : level + 1])
        
        self.printAllPath(root.left, level + 1, arr)
        self.printAllPath(root.right, level + 1, arr)

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break 
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

result = [0] * len(arr)

tree.printAllPath(root, 0, result)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)