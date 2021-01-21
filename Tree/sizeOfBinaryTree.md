# Size of binary tree

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree | `n`: size of binary tree |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 3 R
-1

output:
4
```

```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. recursively call the left and right subtree and `count` the nodes

3. return `0` if node has no child

4. return total `count` of nodes

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
        if root is None: return

        if root.data == key: return root

        temp1 = self.inorder(root.left, key)
        # if node is found on left side no need to look on right side
        if temp1: return temp1
        # look for node on right side
        temp2 = self.inorder(root.right, key)
        return temp2

    def insert(self, data):
        [value, parent, child] = data
        node = Node(int(value))
        # add first node to the binary tree
        if self.root is None:
            self.root = node
            return
        
        current = self.root

        # get the parent node from binary tree
        ptr = self.inorder(current, int(parent))

        if child is 'L':
            ptr.left = node
        else:
            ptr.right = node
    
    def getRootNode(self):
        return self.root
    
    # explore left and right child and increment the count
    def sizeOfTree(self, root):
        if root:
            return 1 + self.sizeOfTree(root.left) + self.sizeOfTree(root.right)
        else:
            return 0


arr = []

while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

tree = BinaryTree()

# build a binary tree
for item in arr:
    tree.insert(item)

# get root node of binary tree
root = tree.getRootNode()

print(tree.sizeOfTree(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)