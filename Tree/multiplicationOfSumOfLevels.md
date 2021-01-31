# Find multiplication of sum of data of nodes at same level

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build binary tree | `n`: product of level sums |

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

output:
121680
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

```
nodes at each level:
[0: [26], 1: [10, 3], 2: [4, 6, 2], 3: [30]]

sum of levels:
[0: 26, 1: 13, 2: 12, 3: 30]

product of sums:
26 * 13 * 12 * 30 = 121680
```
<br>

> approach :

1. build a **binary tree**

2. perform *level order traversal*

3. at each *level* find `sum` of all the nodes

4. multiply all the `level sum`

5. return the `product` of `levelSum`

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

def size(arr):
    return len(arr)

def sumAndMultiplyLevel(root):
    queue = []

    if root: enqueue(queue, root)
    
    product = 1

    while not isEmpty(queue):
        levelSum = 0
        nodeCount = size(queue)

        while nodeCount > 0:
            node = dequeue(queue)

            levelSum += node.data
            
            if node.left: enqueue(queue, node.left)
            
            if node.right: enqueue(queue, node.right)

            nodeCount -= 1
        
        product *= levelSum
    
    return product

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(sumAndMultiplyLevel(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)