# BST to max heap

| input | output |
| --- | --- |
| `arr`: BST | `arr`: max heap |

<br>

> example :

```
input:
3 2 4 1 5

output:
[5, 4, 3, 2, 1]
```

<br>

> approach :

1. build **BST** 

2. perform `reverse inorder` traversal and store element in `result` array during traversal

3. return `result` array

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BST:
    def __init__(self):
        self.root = None

    def insert(self, data):
        node = Node(data)

        if self.root is None:
            self.root = node
            return

        current = self.root

        while current:
            if current.data > data:
                if current.left:
                    current = current.left
                else:
                    current.left = node
                    current = None
            else:
                if current.right:
                    current = current.right
                else:
                    current.right = node
                    current = None

    def getRoot(self):
        return self.root

    def reverseInorder(self, root):
        result = []
        if root:
            result = self.reverseInorder(root.right)
            result.append(root.data)
            result += self.reverseInorder(root.left)
        
        return result

arr = list(map(int, input().split()))

tree = BST()

for item in arr:
    tree.insert(item)    

root = tree.getRoot()

print(tree.reverseInorder(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)