# Minimum bracket reversal

### Minimum number of bracket reversal required so that the brackets are balanced.

<br>

| input | output |
| --- | --- |
| `string`: bracket sequence | `n`: min reversal count |

<br>

> example :

```
input:
}{

output:
2
```

```
input:
}}{}

output:
1
```

```
input:
{}{{}

output:
-1
```

<br>

> approach :
1. if length of bracket sequence is odd then balancing is not possible

2. for all elements in the array

    * push the brackets into stack that are not already balanced

3. count the number of open brackets from the top of stack, call it `n`

4. minimum number of reversal required 
    ```
    len(stack) / 2 + n % 2
    ```

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def top(stack):
    return stack[len(stack) - 1]

def isEmpty(stack):
    return len(stack) is 0

def minBracketReversal(brackets):
    if len(brackets) % 2:
        return -1

    stack = []

    for bracket in brackets:
        if bracket is '}' and not isEmpty(stack):
            if top(stack) is '{':
                pop(stack)
            else:
                push(stack, bracket)
        else:
            push(stack, bracket)
    
    unbalancedLength = len(stack)
    n = 0

    while not isEmpty(stack) and top(stack) is '{':
        pop(stack)
        n += 1

    return unbalancedLength // 2 + n % 2

brackets = list(input())

print(minBracketReversal(brackets))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)
