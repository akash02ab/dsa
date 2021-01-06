# Next closest greatest element

### Given array find the closest greater element which is present on the right side of the element.

<br>

| input | output |
| --- | --- |
| `arr`: list of positive numbers | `arr`: next greatest element <br> to the right |

<br>

> example :

```
input:
10 20 5 15 25 14

output:
[20, 25, 15, 25, None, None]

(None, if no element greater to its right is present)
```

<br>

> approach :

1. initialize `result` array with `None`

2. initialize `stack` with first element

3. for rest of the element say `next`
    * pop from stack and assign to `current`
    
    * if `current` element is smaller than `next` element than update the `result` array 
    
    * repeat the above step while `current` from **stack** come out as smaller than the `next`
    
    * if `next` is smaller than `current` than still a greater element is to be found  

<br>

> implementation :

```python
def isEmpty(stack):
    return len(stack) == 0

def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def nextGreaterElements(arr):
    stack = []
    # push index of first element to stack 
    push(stack, 0)
    
    n = len(arr)
    
    result = [None] * n
    
    # for rest of the elements
    for i in range(1, n):
        next = arr[i]

        if not isEmpty(stack):
            # if stack is not empty, then pop an element from stack
            j = pop(stack)
            current = arr[j]
            
            '''
            if the poped element is smaller than next, then
                * add it to result array
                * keep poping while element are smaller and stack is not empty
            '''
            while current < next:
                result[j] = next
                
                if not isEmpty(stack):
                    j = pop(stack)
                    current = arr[j]
                else:
                    break
            
            # if current greater than or equal to next then push it to stack
            if current >= next:
                push(stack, j)

            # push index of next to stack so that next greater can be found for it
            push(stack, i)
    
    return result


arr = list(map(int, input().split()))

print(nextGreaterElements(arr))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)