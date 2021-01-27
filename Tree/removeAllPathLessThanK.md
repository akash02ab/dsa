# Remove all the paths having lenght less than k from root

| input | output |
| `arr[][]`: instruction to bulid<br>binary tree<br>`k`: length of path | `arr`: inorder traversal of <br> modified binary tree |

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
9 8 R
-1
3

output:
1 2 3 5 7 8 9
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. recursively look for nodes having length `0` from root

3. if left subtree and right subtree of node is `None` and `k` is not `0`, it means path lenght from `root` is less than `k` so, set that node to `None`

4. return the `root` node

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

    def removePathLessThanK(self, root, k):
        if root is None:
            return None 
        
        if k == 0:
            return root

        root.left = self.removePathLessThanK(root.left, k - 1)
        root.right = self.removePathLessThanK(root.right, k - 1)

        if root.left is None and root.right is None:
            root = None
        
        return root

    def inorderTraversal(self, root):
        if root:
            self.inorderTraversal(root.left)
            print(root.data, end = ' ')
            self.inorderTraversal(root.right)

tree = BinaryTree()

arr = []
while True: 
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

k = int(input())

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

tree.removePathLessThanK(root, k)

tree.inorderTraversal(root)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)