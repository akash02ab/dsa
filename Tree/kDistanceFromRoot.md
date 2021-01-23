# k distance from root

### Print all the nodes that are k distance from the root. *(root is at level 0)*

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build binary tree <br> `k`: level of tree | `arr[]`: all the nodes in `k`<sup>th</sup> level |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
6 3 L
7 3 R
-1
2

output:
[4, 5, 6, 7]
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. move to left subtree and right subtree and decrease the level

3. if level is equal to `0`
    * add the node value to `result` array

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
    
    def getKdistanceNodes(self, root, k):
        result = []

        if root is None: return 

        if k == 0:
            result.append(root.data)
            return result
        else:
            temp = self.getKdistanceNodes(root.left, k - 1)
            if temp: result += temp
            temp = self.getKdistanceNodes(root.right, k - 1)
            if temp: result += temp
        
        return result

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

print(tree.getKdistanceNodes(root, k))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)