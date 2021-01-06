# Implement stack using queue

### Implement `push` and `pop` operation using only `enqueue` and `dequeue` operations.

<br>

| input | output |
| --- | --- |
| `arr`: list of `stack` operations | `arr`: status of `stack` <br> after all operations |

<br>

> example :

```
input:
1 2 3 -1 4 5 -1 6
(-1 represent pop operation)

output:
3
5
[6, 4, 2, 1]
```

<br>

> approach :

1. `push` is implemented using two **queue**
    
    * `enqueue` new `item` in empty **queue**
    * `dequeue` all elements from other **queue** and `enqueue` to first **queue**

2. `pop` is implemented using simple `dequeue` operation

<br>

> implementaion :

```python
def enqueue(queue, item):
    queue.append(item)

def dequeue(queue):
    return queue.pop(0)

def push(stack, item):
    # temp queue
    temp = []
    # add new item to empty temp queue
    enqueue(temp, item)

    # append other item already in stack to temp queue
    while len(stack) > 0:
        x = dequeue(stack)
        enqueue(temp, x)

    # restore stack
    for item in temp:
        enqueue(stack, item)

    '''
    stack is maintained in reverse order of insertion
    this enable to perform pop from 0th position in O(1)
    '''

def pop(stack):
    return dequeue(stack)

stack = []

arr = list(map(int, input().split()))

for item in arr:
    if item is -1:
        print(pop(stack))
    else:
        push(stack, item)

print(stack)
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>*(push takes O(n) and pop takes O(1))*
<br>S(n) = O(n)
<br>*(temp queue is require to maintain stack operation)*