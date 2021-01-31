# Serialization and deserialization of N-ary tree

### Serialization is to store a tree in linear way so that it can be later restored. Structure of tree must be maintianed.

### Deserialization is reading tree back from linear array that is maintained during serialization.

<br>

| input | output |
| --- | --- |
| `arr[][]`: instruction to <br> build N-ary tree | `arr[]`: linear representation <br> of N-ary tree <br> `arr[]`: preorder traversal <br> of rebuild N-ary tree |

<br>

> example :

```
input:
1 -1
2 1
3 1
4 1
5 2
6 3
7 3
-1

output:
[1, 2, 5, 'P', 'P', 3, 6, 'P', 7, 'P', 'P', 4, 'P', 'P']
1 2 5 3 6 7 4
```
```
each row contain [value, parent] pair
-1 at end represent end of input
```

<br>

> approach :

1. build a **N-ary tree**

2. store the **N-ary tree** in linear form
    * perform *traversal* on tree
    * store the node value if its visited for the first time
    * store `P` (pop) if its visited for the last time

3. reconstruct the **N-ary tree** using linear representation obtained from serialization
    * if item is `P`, `pop` the element from `stack`
    * else:
        * `peek` the top of `stack` which is `parent`
        * insert the node to its `parent`
        * `push` the node into `stack`

<br>

> implementation :

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.child = []

class N_aryTree:
    def __init__(self):
        self.root = None 
    
    def findNode(self, root, key):
        if root is None: return 

        if root.data == key:
            return root 
        
        for node in root.child:
            temp = self.findNode(node, key)
            if temp: return temp
    
    def insert(self, data):
        [value, parent] = data
        node = Node(int(value))

        if self.root is None:
            self.root = node
            return 
        
        ptr = self.findNode(self.root, int(parent))
        ptr.child.append(node)
    
    def getRootNode(self):
        return self.root 

    def serialization(self, root, result):
        result.append(root.data)
        
        for node in root.child:
            self.serialization(node, result)
        else:
            result.append('P')
    
    def push(self, stack, item):
        stack.append(item)

    def pop(self, stack):
        stack.pop()

    def peek(self, stack):
        if len(stack) == 0: return None
        return stack[len(stack) - 1]

    def deserialization(self, traversal):
        stack = []

        for item in traversal:
            if item is 'P':
                self.pop(stack)
            else:
                parent = self.peek(stack)
                self.insert([item, parent])
                self.push(stack, item)
    
    def traversal(self, root):
        print(root.data, end = ' ')

        for node in root.child:
            self.traversal(node)

tree = N_aryTree()

arr = []
while True:
    temp = list(map(str, input().split()))
    if temp[0] == '-1': break 
    arr.append(temp)

for item in arr:
    tree.insert(item)

root = tree.getRootNode()

serial = []

tree.serialization(root, serial)

print(serial)

tree1 = N_aryTree()

tree1.deserialization(serial)

root = tree1.getRootNode()

tree1.traversal(root)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)