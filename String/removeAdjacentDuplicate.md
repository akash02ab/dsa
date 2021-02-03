# Remove all duplicate adjacent characters from a string

| input | output |
| --- | --- |
| `string`: original string | `string`: filtered string |

<br>

> example :

```
input:
vieanna

output:
vie
```

<br>

> approach :

1. create a `stack` to remove the adjacent duplicate characters in `string`

2. traverse the `string` and check if the `stack` `is empty` or the `top` element of the `stack` not equal to the current character

    * if found to be true, `push` the current character into `stack`
    
    * otherwise, `pop` the element from the top of the `stack`

3. finally, return all the remaining elements of the `stack`

<br>

> implementation :

```python
def isEmpty(stack):
    return len(stack) == 0

def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def top(stack):
    return stack[-1]

def removeAdjacentDuplicate(string):
    stack = []

    index = 0

    while index < len(string):
        if isEmpty(stack) or string[index] != top(stack):
            push(stack, string[index])
        else:
            pop(stack)
        
        index += 1
    
    return ''.join(stack)


string = input()

print(removeAdjacentDuplicate(string))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)