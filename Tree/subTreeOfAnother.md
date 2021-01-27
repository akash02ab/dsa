# Check wheather a binary tree is a subtree of another

| input | output |
| --- | --- |
| `arr[][]`: insturction to build<br>first binary tree <br> `arr[][]`: instruction to build <br> second binary tree | `boolean`: `True` if tree2 is subtree <br> of tree1, `False` otherwise |

<br>

> example :

```
input:
26 -1 H
10 26 L
3 26 R
4 10 L
6 10 R
2 3 R
30 4 R
-1
10 -1 H
4 10 L
6 10 R
30 4 R
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

1. build a **binary tree**

2. find the `root` node of smaller tree in larger tree

3. if found perform parallel traversal of both the trees

4. if both trees are `identical` (the values and position of nodes) return `True`, else return `False`

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

    def identical(self, root1, root2):
        if root1 is None and root2 is None:
            return True

        if root1 is None or root2 is None:
            return False
        
        return root1.data == root2.data and self.identical(root1.left, root2.left) and self.identical(root1.right, root2.right)


    def subTree(self, root1, root2):
        if root1 is None:
            return False

        if root2 is None:
            return True
        
        if self.identical(root1, root2):
            return True
        
        return self.subTree(root1.left, root2) or self.subTree(root1.right, root2)

tree1 = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree1.insert(item)

root1 = tree1.getRootNode()

tree2 = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree2.insert(item)

root2 = tree2.getRootNode()

# is tree2 is a subTree of tree1
print(tree1.subTree(root1, root2))
```

> **Time and space complexity :**
<br>T(n) = O(m * n)
<br>S(n) = O(n)