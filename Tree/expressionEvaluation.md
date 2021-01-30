# Evaluate the expression tree

### The expression tree only contains binary operators such as `+`, `-`, `*` and `\`. The operands are present only at leaf node.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build a binary tree | `n`: result of expression tree |

<br>

> example :

```
input:
+ -1 H
* + L
- + R
5 * L
4 * R
80 - L
30 - R
-1

output:
70
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build the **expression tree**

2. perform *postorder traversal* on expression tree

3. if node is a `leaf` node return the integer value of the node

4. collect result of *left subtree* and *right subtree* in variable `left` and `right` respectively

5. evaluate the expression according to the operators occurence

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
        node = Node(value)

        if self.root is None:
            self.root = node 
            return 
        
        ptr = self.findNode(self.root, parent)

        if child is 'L':
            ptr.left = node 
        else:
            ptr.right = node 
    
    def getRootNode(self):
        return self.root

    def isLeaf(self, root):
        return root.left is None and root.right is None

    def evaluate(self, root):
        if root is None: return 0

        if self.isLeaf(root):
            return int(root.data)
        
        left = self.evaluate(root.left)
        right = self.evaluate(root.right)

        if root.data == '+':
            return left + right
        elif root.data == '-':
            return left - right 
        elif root.data == '*':
            return left * right 
        elif root.data == '/':
            return left // right

tree = BinaryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break 
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.evaluate(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)