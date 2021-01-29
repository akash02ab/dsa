# Given two node, check wheather the nodes are cousin or not

### Two nodes are said to be cousin when they are on same level and are not siblings.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build <br> the binary tree <br> `a, b`: value of nodes | `boolean`: `True` if nodes are cousin, <br> `False` otherwise |

<br>

> example :

```
input :
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
6 3 R
-1
4 6

output:
True
```

```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. check if two node are in same `level`

3. if they are on same `level` check if they are `sibling` or not

4. if they are not `sibling` return `True`, else return `False`

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
        if temp2: return temp2 

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

    def sibling(self, root, a, b):
        if root is None: return False

        if root.left and root.right:
            return (root.left.data == a and root.right.data == b) or (root.left.data == b and root.right.data == a)
        
        return self.sibling(root.left, a, b) or self.sibling(root.right, a, b)

    def level(self, root, ptr, level):
        if root is None: return 0

        if root.data == ptr: return level

        temp1 = self.level(root.left, ptr, level + 1)
        if temp1: return temp1
        temp2 = self.level(root.right, ptr, level + 1)
        return temp2

    def cousin(self, root, a, b):
        if self.level(root, a, 1) == self.level(root, b, 1) and not self.sibling(root, a, b): 
            return True

        return False


tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break 
    arr.append(temp)

a, b = map(int, input().split())

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.cousin(root, a, b))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)