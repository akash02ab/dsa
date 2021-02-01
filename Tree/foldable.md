# Check weather binary tree is foldable or not

### A binary tree is said to be foldable if its left subtree structure is mirror image of right subtree structure (the node values need not be same).

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `boolean`: `True` if binary tree is foldable, <br> `False` otherwise |

<br>

> example :

```
input:
2 -1 H
1 2 L
3 2 R
8 1 R
9 3 L
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

2. pass *left subtree* and *right subtree* of root to a helper function

3. for every left node in *left subtree* there must be right node in *right subtree* at same level

4. and, also for every right node in *left subtree* there must be left node in *right* subtree at same level

5. return `True` or `Flase` based on above two condition

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

    def isFoldableUtil(self, node1, node2):
        if node1 is None and  node2 is None:
            return True 
        
        if node1 is None or node2 is None:
            return False 
        
        return self.isFoldableUtil(node1.left, node2.right) and self.isFoldableUtil(node1.right, node2.left)

    def isFoldable(self, root):
        if root is None: return True 

        return self.isFoldableUtil(root.left, root.right)

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.isFoldable(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)