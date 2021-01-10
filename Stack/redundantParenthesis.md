# Identify redundant parenthesis

### A expression is given in the from of string. Identify if there is any redundant parenthesis present in the expression.

<br>

| input | output |
| --- | --- |
| `string`: expression | `boolean`: `True` if redundant parethesis<br>is present, `False` otherwise |

<br>

> example :

```
input:
(a + b) * (c / d)

output:
False
```

```
input:
(3 * 2) - ((14 * 4))

output:
True
```

```
input:
(4 * 6)()

output:
True
```

<br>

> approach :

1. `push` the *expression* in **stack** if it is not `)`

2. if *expression* is `)`
    * `pop` out all the expression untill `top` of **stack** becomes `(`

3. if there is no item to `pop` from **stack** before `(`, then definately a *redundant parenthesis* is present in the *expression*

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def top(stack):
    return stack[len(stack) - 1]

def redundantParenthesis(expression):
    stack = []

    for input in expression:
        if input is ')':
            tp = top(stack)

            if tp is '(':
                return True
            else:
                while tp != '(':
                    tp = pop(stack)
        else:
            push(stack, input)

    return False

expression = list(input())

print(redundantParenthesis(expression))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)