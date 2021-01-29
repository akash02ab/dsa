# Balance the given binary search tree

| input | output |
| --- | --- |
| `arr[]`: inorder traversal of BST | `arr[]`: preorder traversal of balanced BST |

<br>

> example :
```
input :
10 20 30 40 50

output:
30 10 20 40 50
```
<br>

> approach :

1. build a **BST**

2. store the nodes of **BST** in an `array` in sorted order of values *(for this perform inorder traversal of **BST**)*

3. perform balancing of **BST** using divide and conquer paradigm:  
    * find the `middle` of `array` and make it `root` of balanced **BST**
    * recursively build the *left subtree* and *right subtree* using same logic

4. return `root` node 

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
            if data < current.data:
                if current.left is None:
                    current.left = node
                    break 
                else:
                    current = current.left
            else:
                if current.right is None:
                    current.right = node 
                    break 
                else:
                    current = current.right 
    
    def getRootNode(self):
        return self.root

    def storeBSTNodes(self, root):
        arr = []

        if root:
            arr = self.storeBSTNodes(root.left)
            arr.append(root)
            arr += self.storeBSTNodes(root.right)

        return arr

    def arrayToBalancedBST(self, arr, start, end):
        if start > end:
            return None 
        
        middle = (start + end) // 2
        root = arr[middle]

        root.left = self.arrayToBalancedBST(arr, start, middle - 1)
        root.right = self.arrayToBalancedBST(arr, middle + 1, end)

        return root

    def preorderTraversal(self, root):
        if root:
            print(root.data, end = ' ')
            self.preorderTraversal(root.left)
            self.preorderTraversal(root.right)

tree = BST() 

arr = list(map(int, input().split()))

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

# inorder traveral of BST gives the sorted order
inorder = tree.storeBSTNodes(root)

root = tree.arrayToBalancedBST(inorder, 0, len(inorder) - 1)

tree.preorderTraversal(root)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)