# Check if two binary tree are identical

| input | output |
| --- | --- |
| `arr[][]`: instruction to build <br> binary tree | `boolean`: `True` if two trees are identical, <br>`False` otherwise |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 3 R
5 2 R
-1
1 -1 H
2 1 L
3 1 R
4 3 R
-1

output:
False
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build two **binary trees**

2. check if `root` are identical

3. recursively check if `left-subtree` and `right-subtree` are identical

4. return `True` if identical, `False` otherwise

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

    def inorder(self, root, key):
        # return None if end of node is reached
        if root is None: return
        # return node if key if found
        if root.data == key: return root
        # check for key in left subtree
        temp1 = self.inorder(root.left, key)
        # no need to check further if node is found on left part itself
        if temp1: return temp1
        # check for key in right subtree
        temp2 = self.inorder(root.right, key)
        return temp2
        
    def insert(self, data):
        [value, parent, child] = data
        node = Node(int(value))
        # add first node to the tree
        if self.root is None:
            self.root = node
            return

        current = self.root
        # get the parent node from the tree
        ptr = self.inorder(current, int(parent))
        # insert the child as per the instruction
        if child is 'L':
            ptr.left = node
        else:
            ptr.right = node
    
    def getRootNode(self):
        return self.root

def isIdentical(root1, root2):
    # if both node has no left or right child
    if not root1 and not root2:
        return True
    # check the value, and goto left subtree and right subtree
    if root1 and root2:
        return root1.data == root2.data and isIdentical(root1.left, root2.left) and isIdentical(root1.right, root2.right)
    
    return False

# build first binary tree
tree1 = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree1.insert(item)

# build second binary tree
tree2 = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree2.insert(item)

# get root node of both the binary trees
root1 = tree1.getRootNode()
root2 = tree2.getRootNode()

# check if both the trees are identical
print(isIdentical(root1, root2))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)
