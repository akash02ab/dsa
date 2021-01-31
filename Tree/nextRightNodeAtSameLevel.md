# Find the next right node at the same level

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build a binary tree <br> `key`: target element | `n`: value of next right node |

<br>

> example :

```
input:
10 -1 H
2 10 L
6 10 R
5 2 L
8 2 R
4 6 L
-1
2

output:
6
```
```
note :- H: head, L: left child, R: right child
each row conatins: [value, parentNode, childPosition]
-1 at end represent end of input
```

<br>

> approach :

1. build a **binary tree**

2. perform *level order traversal* on **binary tree**

3. maintain a `queue` for node element and `level` of nodes

4. look for `key` element in queue
    * if `key` is not found keep adding nodes element to `queue` level by level
    
    * if `key` is found then look for the next element in `queue` and check if it belongs to same level

5. return `None` if next right element is not found

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

    def enqueue(self, arr, item):
        arr.append(item)

    def dequeue(self, arr):
        return arr.pop(0)

    def isEmpty(self, arr):
        return len(arr) == 0

    def nextRight(self, root, key):
        if root is None: return None 
        
        queue = []
        level = [0]

        if root: self.enqueue(queue, root)

        while not self.isEmpty(queue):
            node = self.dequeue(queue)
            lv = self.dequeue(level)
            
            if node.data == key:
                if self.isEmpty(queue) or level[0] != lv:
                    return None

                return queue[0].data

            if node.left: 
                self.enqueue(queue, node.left)
                self.enqueue(level, lv + 1)

            if node.right: 
                self.enqueue(queue, node.right)
                self.enqueue(level, lv + 1)

        return None

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

print(tree.nextRight(root, key))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)