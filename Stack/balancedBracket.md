# Check if sequence is balanced or not

| input | output |
| --- | --- |
| `string`: string of brackets | `boolean`: `True` is sequence is balanced<br>`False` otherwise |

<br>

> example :
```
input:
()([{}]{})

output:
True
```
```
input:
()[}

output:
False
```

```
input:
()[](({})

output:
False
```
<br>

> approach :
1. push for open bracket

2. for closed bracket perform pop
    * `open = pop()`
    * compare `open` and `closed` bracket
    * if they do not form pair return `False` else `continue`

3. at the end check if stack is empty
    * if stack is empty it means that brackets are balanced so, return `True`
    * else brackets are imbalanced so, return `False`

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def isEmpty(stack):
    return len(stack) is 0

def isOpen(bracket):
    open = ['(', '[', '{']
    return bracket in open

def match(open, close):
    pair = {'(': ')', '[': ']', '{': '}'}
    return pair[open] is close

def isBalanced(brackets):
    stack = []

    for bracket in brackets:
        if isOpen(bracket):
            push(stack, bracket)
        else:
            open = pop(stack)
            close = bracket
            if not match(open, close):
                return False
    
    if isEmpty(stack):
        return True
    else:
        return False
        

brackets = list(input())
print(isBalanced(brackets))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)