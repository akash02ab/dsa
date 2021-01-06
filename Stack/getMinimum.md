# Get minimum in stack

### Get the minimum value present in stack in constant time.

<br>

| input | output |
| --- | --- |
| `arr`: list of all elements in `stack` | `arr`: minimum value after every pop operation |

<br>

> example :

```
input:
10 20 5 15 3 6 2 1

output:
1 2 3 3 5 5 10 10

1 is minimum when all elements are present
now, pop(1)
2 is current minimum 
now, pop(2)
3 is current minimum
pop(6)
again, 3 is current minimum
and, so on ...
```

<br>

> approach :

1. `push` all elements in **stack**

2. while pushing maintain `currentMin` in another stack

3. `pop` element from **stack** one by one and print the `currentMin`

<br>

> implementaion :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def getMin(stack, minimum):
    x = pop(stack)
    y = pop(minimum)

    if x > y:
        push(minimum, y)

    return y

stack = []
minimum = []

arr = list(map(int, input().split()))

for item in arr:
    # maintain the original stack
    push(stack, item)
    
    # maintain minimum so far using another stack `minimum`
    if(len(minimum) is 0):
        push(minimum, item)
    else:
        x = pop(minimum)
        # if new item is less than minimum so far push that on top of current minimum
        if item <= x:
            push(minimum, x)
            push(minimum, item)
        else:
            push(minimum, x)

# for every pop operation find the current minimum present in stack
while len(stack):
    # print the current minimum present in stack
    print(getMin(stack, minimum), end = ' ')
```

> **Time and space complexity :**
<br>T(n) = O(1) 
<br>*(push, pop and getMin is imlemented in constant time)*
<br>S(n) = O(n)
<br>*(maintaing minimum stack require extra space)*

<br>

> approach :

1. `push` elements in **stack**

2. maintain `currentMin` while pushing elements

3. if new `item` is less than `currentMin` than
    * `push` the difference `item - currentMin`

4. while `pop`
    * if poped `item` is less than `currentMin`
    * retrieve the previous `currentMin` by finding difference again
    * `currentMin -= item`

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

stack = []

arr = list(map(int, input().split()))

currentMin = 0
for item in arr:
    '''
    stack is empty push first element to stack
    initialize currentMin with first element
    '''
    if len(stack) is 0:
        push(stack, item)
        currentMin = item
        continue
    
    '''
    if item is less than currentMin then push difference of currentMin and item into stack
    this difference is always less than currentMin and help in identifying the next min element in stack
    when some of elements are poped from the stack
    '''
    if item < currentMin:
        # push (item - currentMin) instead of item
        push(stack, item - currentMin)
        currentMin = item
    else:
        # push item as it is, if item is greter than currentMin
        push(stack, item)

while len(stack):
    item = pop(stack)
    
    print(currentMin, end = ' ')
    
    # restore previous minimum value
    if item < currentMin:
        currentMin -= item
```
> **Time and space complexity :**
<br>T(n) = O(1) 
<br>*(push, pop and getMin is imlemented in constant time)*
<br>S(n) = O(1)
<br>*(no extra space)*