# Reverse stack

| input | output |
| --- | --- |
| `arr`: all stack elements | `arr`: reversed stack |

<br>

> example :

```
input:
1 2 3 4

output:
[4, 3, 2, 1]
```

<br>

> approach :

1. `empty` the `stack` recursively

2. call `insertAtBottom` inside recursive call
    * `empty` the `stack` again recursively
    * `push` the new `item`
    * `push` the rest of `item` recursively

<br>

> implementation :

```python
def isEmpty(stack):
    return len(stack) == 0

def push(stack, item):
    stack.append(item)

def pop(stack):
    if isEmpty(stack):
        return 'underflow'

    return stack.pop()

def insertAtBottom(stack, item):
    if isEmpty(stack):
        push(stack, item)
    else:
        x = pop(stack)
        insertAtBottom(stack, item)
        push(stack, x) 

def reverse(stack):
    if not isEmpty(stack):
        x = pop(stack)
        reverse(stack)
        insertAtBottom(stack, x)

arr = list(map(int, input().split()))

stack = []

for item in arr:
    push(stack, item)

reverse(stack)

print(stack)
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(n)