# Find maximum difference between node and it's ancestor

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `n`: max difference b/w <br> node and it's ancestor |

<br>

> example :

```
input:
25 -1 H
32 25 L
45 25 R
3 32 L
50 32 R
2 45 L
15 45 R
4 50 L
-5 2 R
-1

output:
50
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perform *postorder traversal* on **binary tree**

3. if the node is `leaf node` return the node value

4. find the `minimum` node value from *left subtree* and *right subtree*

5. find the `difference` between the current node the its `minimum` node value recieved from its child

6. update the `maxDiff` if a difference larger than current difference is found

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
        self.INTMAX = float('inf')
        self.maxDiff = float('-inf')

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

    def isLeaf(self, node):
        return node.left is None and node.right is None 

    def maxDifference(self, root):
        if root is None: return self.INTMAX

        if self.isLeaf(root): return root.data

        left = self.maxDifference(root.left)
        right = self.maxDifference(root.right)

        minimum = min(left, right)

        self.maxDiff = max(self.maxDiff, root.data - minimum)

        return min(minimum, root.data)
    
    def maximumDifferenceBetweenNodeAndItsAncestor(self, root):
        self.maxDifference(root)
        return self.maxDiff

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.maximumDifferenceBetweenNodeAndItsAncestor(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)