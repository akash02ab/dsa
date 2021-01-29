# Build balanced binary search tree from sorted array

| input | output |
| --- | --- |
| `arr`: sorted array | `arr`: preorder traversal <br> of binary search tree |

<br>

> example :

```
input:
5 10 20 30 40 50 55

output:
30 10 5 20 50 40 55
```

<br>

> approach :

1. find the `middle` element of array

2. make the `middle` element `root` of **BST**

3. recursively build the *left subtree* and *right subtree* using the *left part of array* and *right part of array* respectively

4. find `middle` element of *left subarray* and form *left subtree* and do same for *right subtree*

5. return the `root`

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
    
    def sortedArrayToBalancedBST(self, arr, start, end):
        if start > end:
            return None 
        
        middle = (start + end) // 2
        root = Node(arr[middle])

        root.left = self.sortedArrayToBalancedBST(arr, start, middle - 1)
        root.right = self.sortedArrayToBalancedBST(arr, middle + 1, end)

        return root
    
    def preorderTraversal(self, root):
        if root:
            print(root.data, end = ' ')
            self.preorderTraversal(root.left)
            self.preorderTraversal(root.right)


arr = list(map(int, input().split())) 

tree = BST()

root = tree.sortedArrayToBalancedBST(arr, 0, len(arr) - 1)

tree.preorderTraversal(root)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)