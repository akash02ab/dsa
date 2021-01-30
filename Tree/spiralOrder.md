# Print the binary tree in spiral order

| input | output |
| --- | --- |
| `arr[][]`: instruction to build a binary tree | `arr[]`: binary tree in spiral order |

<br>

> example :

```
input:
1 -1 H
2 1 L
3 1 R
4 2 L
5 2 R
6 4 L
7 5 L
8 5 R
-1

output:
[1, 2, 3, 5, 4, 6, 7, 8]
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. initialize two stacks
    * `stack1` = `[root]` *(contains root of binary tree)*
    * `stack2` = `[]` *(an empty stack)*

3. while both the `stacks` are not empty:
    * while `stack1` is not empty:
        * `pop` from `stack1`
        * insert poped item to `result` array 
        * `push` *right* and *left* node to `stack2` in that order
    
    * while `stack2` is not empty:
        * `pop` from `stack2`
        * insert poped item to `result` array
        * `push` *left* and *right* node to `stack1` in that order

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

    def isEmpty(self, stack):
        return len(stack) == 0

    def push(self, stack, item):
        stack.append(item)
    
    def pop(self, stack):
        return stack.pop()

    def spiralOrder(self, root):
        if root is None: return 
    
        result = []
        stack1 = []
        stack2 = []

        self.push(stack1, root)

        while not self.isEmpty(stack1) or not self.isEmpty(stack2):
            while not self.isEmpty(stack1):
                node = self.pop(stack1)
                
                result.append(node.data)
                
                if node.right:
                    self.push(stack2, node.right)
                
                if node.left:
                    self.push(stack2, node.left)
        
            while not self.isEmpty(stack2):
                node = self.pop(stack2)

                result.append(node.data)

                if node.left:
                    self.push(stack1, node.left)

                if node.right:
                    self.push(stack1, node.right)
        
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

print(tree.spiralOrder(root)) 
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)