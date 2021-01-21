# Is binary tree a max heap

| input | output |
| --- | --- |
| `n`: number of nodes <br> `arr[][]`: info to bulid binary tree | `boolean`: `True` if BT is max heap, <br> `False` otherwise |

<br>

> example :

```
input:
7
4 -1 H
2 4 L
6 4 R
1 2 L
3 2 R
5 6 L
7 6 R

output: 
False
```

```
input:
5
14 -1 H
7 14 L
3 14 R
4 7 L
2 7 R

output:
True
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childInfo]
```

<br>

> approach :

1. build **binary tree**

2. check for **max heap** property:
    * **binary tree** must be *complete*
    * `parent` node must be greater than `child` nodes

3. return `True` if its **max heap**, `False` otherwise

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

    def inorder(self, root, key):
        if root is None: return

        if root.data == key: return root

        temp1 = self.inorder(root.left, key)
        # if node is found on left side no need to look on right side
        if temp1: return temp1
        # look for node on right side
        temp2 = self.inorder(root.right, key)
        return temp2
    
    def insert(self, data):
        [value, parent, child] = data
        node = Node(int(value))

        # add first node(root) of the binary tree
        if self.root is None:
            self.root = node
            return
        
        current = self.root

        # get the parent node from the binary tree
        ptr = self.inorder(current, int(parent))

        # add either to left or right side according to instruction
        if child is 'L':
            ptr.left = node
        else:
            ptr.right = node
            
    # return the root node of binary tree
    def getRoot(self):
        return self.root


def isMaxHeap(root):
    # node has no right or left child
    if root.left is None and root.right is None:
        return True
    # node has only right child so, its not complete binary tree
    elif root.left is None and root.right:
        return False
    # there is chain of two left node with no right node so, not following heap property
    elif root.right is None and root.left.left:
        return False
    # check if parent node is greater than left child node
    elif root.right is None and root.left.left is None:
        return root.data >= root.left.data
    # check if parent node is greater than both left and right node
    elif root.data >= root.left.data and root.data >= root.right.data:
        return isMaxHeap(root.left) and isMaxHeap(root.right)
    
    return False

tree = BinaryTree()

n = int(input())

arr = []

for _ in range(n):
    temp = list(map(str, input().split()))
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRoot()

print(isMaxHeap(root))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)
<br>*(the size of recursion stack)*
