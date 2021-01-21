# Level order traversal of binary tree

| input | output |
| --- | --- |
| `arr[][]`: instruction to build <br> a binary tree | `arr[]`: level order traversal <br> of binary tree |

<br>

> example :

```
input:
14 -1 H
9 14 R
12 14 L
6 9 R
5 12 R
1 12 L
-1

output:
[14, 12, 9, 1, 5, 6]
```

```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

> appraoch :

1. build a **binary tree**

2. `enqueue` the root of the **binary tree** to **queue**

3. while **queue** is not empty:
    * `dequeue` from queue
    * add the node to `result` array
    * `enqueue` the left and right child of node if any

4. return `result` array

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

def enqueue(arr, item):
    arr.append(item)

def dequeue(arr):
    return arr.pop(0)

def isEmpty(arr):
    return len(arr) == 0

def levelOrderTraversal(root):
    queue = []

    if root: enqueue(queue, root)
    
    result = []

    while not isEmpty(queue):
        node = dequeue(queue)
        
        result.append(node.data)
        
        if node.left: enqueue(queue, node.left)
        
        if node.right: enqueue(queue, node.right)
    
    return result

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(levelOrderTraversal(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)