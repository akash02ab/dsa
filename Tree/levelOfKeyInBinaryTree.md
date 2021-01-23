# Level of key in binary tree

### note :- level of root is `1`.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to build<br>binary tree <br> `k`: key | `n`: level of key,<br> `-1` if key is not present |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
-1
5

output:
3
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. bulid a **binary tree**

2. recursively look for `key` in left subtree and right subtree

3. if key is found return `+1` to calling function

4. return `-1` if key is not found in entire tree

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

    def level(self, root, key):
        if root is None: return 0

        if root.data == key:
            return 1
        
        temp1 = temp2 = 1

        temp1 += self.level(root.left, key)
        if temp1 > 1: return temp1
        temp2 += self.level(root.right, key)
        return temp2 if temp2 > 1 else -1

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break
    arr.append(temp)

key = int(input())

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.level(root, key))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)