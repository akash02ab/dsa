# Least common ancestor of nodes `p` and `q` in binary tree

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree <br> `p, q`: two nodes in binary tree | `n`: ancestor of `p` & `q` |

<br>

> example :

```
input:
1 -1 H
3 1 L
2 1 R
4 2 R
5 2 L
-1
3 4

output:
1
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> appraoch :

1. build a **binary tree**

2. get the root node of **binary tree**

3. look for either `p` or `q` in left sub-tree and right sub-tree

4. if either of the node if found return the node to its parent node

5. if a node is found in between the node `p` and `q` return the node

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
    
    def leastCommonAncestor(self, root, p, q):
        # return None if there is on left or right child
        if root is None: return 

        # if either p or q is found return that node
        if root.data == p or root.data == q:
            return root

        # look for p and q in left sub-tree and right sub-tree
        leftLCA = self.leastCommonAncestor(root.left, p, q)
        rightLCA = self.leastCommonAncestor(root.right, p, q)

        # if one element is found in left sub-tree and other in right sub-tree return that node
        if leftLCA and rightLCA:
            return root
        # return the left sub-tree
        elif leftLCA:
            return leftLCA
        # return the right sub-tree
        else:
            return rightLCA

# build a binary tree
tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

# two nodes whose least common ancestor is to be found
p, q = map(int, input().split())

# insert nodes into binary tree
for item in arr:
    tree.insert(item)

# get the root of binary tree
root = tree.getRootNode()

# find the node with least common ancestor of node p and q
print(tree.leastCommonAncestor(root, p, q).data)
```
 
> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)