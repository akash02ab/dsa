# Print all nodes that are k distance from any leaf

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build a binary tree <br> `k`: distance from leaf | `arr[]`: all the node that are <br> `k` distance from any leaf |

<br>

> example :

```
input:
1 -1 H
2 1 L
7 1 R
3 2 L
6 2 R
8 7 L
10 7 R
4 3 L
5 3 R
9 8 L
11 8 R
-1
2

output:
{1, 2, 7}
```

```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perform *preorder traversal* on **binary tree** having root at `level 0`

3. add the node values to `levelAt` array at index which is equal to `level` of **binary tree**

4. if current node `isLeaf`:
    * check if `level - k >= 0`:
        * add (`level - k`)<sup>th</sup> index of `levelAt` to `result` array

5. recursively traverse the *left subtree* and *right subtree*

6. return `result` array


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

    def isLeaf(self, root):
        return root.left is None and root.right is None

    def kDistanceFromLeaf(self, root, k, level, nodeAt):
        if root is None: return 
        
        result = []

        nodeAt[level] = root.data

        if self.isLeaf(root) and level - k >= 0:
            item = nodeAt[level - k]
            result.append(item)
        
        temp = self.kDistanceFromLeaf(root.left, k, level + 1, nodeAt)
        if temp: result += temp
        temp = self.kDistanceFromLeaf(root.right, k, level + 1, nodeAt)
        if temp: result += temp

        return set(result) 

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

nodeAtLv = [0] * len(arr) 

print(tree.kDistanceFromLeaf(root, k, 0, nodeAtLv))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)