# Mirror image of binary tree

| input | output |
| --- | --- |
| `arr[][]`: information to <br> build binary tree | `arr[]`: inorder traversal of <br> mirror binary tree |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
-1

output:
[3, 1, 5, 2, 4]
```

<br>

> appraoch :

1. build a **binary tree**

2. perform preorder traversal on **binary tree**

3. swap the nodes

4. return the root of the sub-tree

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
        
        current = self.root

        ptr = self.findNode(current, int(parent))

        if child is 'L':
            ptr.left = node
        else:
            ptr.right = node

    def getRootNode(self):
        return self.root
    
    # perform inorder traversal
    def inorder(self, root):
        result = []
        if root:
            result = self.inorder(root.left)
            result.append(root.data)
            result += self.inorder(root.right)
        
        return result

    # visit the left sub-tree and right-subtree
    def mirrorBinaryTree(self, root):
        if root:
            self.mirrorBinaryTree(root.left)
            self.mirrorBinaryTree(root.right)
            root.left, root.right = root.right, root.left

# bulid a binary tree
tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

# get the root node of the binary tree
root = tree.getRootNode()

# get the mirror image of binary tree
tree.mirrorBinaryTree(root)

# print the inorder traversal of mirror binary tree
print(tree.inorder(root))
```

> **Time and space compleixty :**
<br>T(n) = O(n)
<br>S(n) = O(n)