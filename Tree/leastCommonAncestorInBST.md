# Least common ancestor of two nodes in binary search tree

| input | output |
| --- | --- |
| `arr[]`: binary search tree <br> `p, q`: value of two nodes | `n`: value of ancestor node of `p` & `q` |

<br>

> example :

```
input:
20 7 21 3 11 9 13
9 13

output:
11
```

<br>

> approach :

1. bulid **binary search tree**

2. get the `root` node of **BST**

3. while root:
    * if root `value` is greater than both `p` and `q` then move to left sub-tree
    * if root `value` is lower than both `p` and `q` then move to right sub-tree
    * `break` if first node `value` in between `p` and `q` is found

4. return root node

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
                    break
            else:
                if current.right:
                    current = current.right
                else:
                    current.right = node
                    break
        
    def getRootNode(self):
        return self.root

   def leastCommonAncestor(root, p, q):
       while(root):
           if root.data < p and root.data < q:
               root = root.right
           elif root.data > q and root.data > q:
               root = root.left
           else: 
               break

       return root.data

tree = BST()

arr = list(map(int, input().split()))

p, q = map(int, input().split())

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

print(tree.leastCommonAncestor(root, p, q))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)
