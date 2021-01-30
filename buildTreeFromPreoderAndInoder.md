# Build a binary tree from inorder and preorder

| input | output |
| --- | --- |
| `arr[]`: preorder traversal <br> `arr[]`: inorder traversal | `arr[]`: postorder traversal after <br> binary tree is build completely |

<br>

> example:

```
input:
1 2 4 6 5 7 8 3
6 4 2 7 5 8 1 3

output:
6 4 7 8 5 2 3 1
```

<br>

> approach :

1. traverse the `preoder` array in linear form

2. find the position of i<sup>th</sup> element of `preorder` array in `inorder` array

3. make that element as root of **binary tree**

4. recursively build the *left subtree* and *right subtree* in similar fashion

5. return `root` of binary tree

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
        self.preIndex = 0

    def search(self, inorder, start, end, key):
        for i in range(start, end + 1):
            if inorder[i] == key:
                return i

    def buildTree(self, preorder, inorder, start, end):
        if start > end: return None 

        node = Node(preorder[self.preIndex])
        self.preIndex += 1

        if start == end:
            return node 
        
        inIndex = self.search(inorder, start, end, node.data)
        node.left = self.buildTree(preorder, inorder, start, inIndex - 1)
        node.right = self.buildTree(preorder, inorder, inIndex + 1, end)
        
        return node
    
    def postorder(self, root):
        if root:
            self.postorder(root.left)
            self.postorder(root.right)
            print(root.data, end = ' ')


preorder = list(map(int, input().split()))

inorder = list(map(int, input().split()))

tree = BinaryTree()

root = tree.buildTree(preorder, inorder, 0, len(preorder) - 1)

tree.postorder(root)
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n)