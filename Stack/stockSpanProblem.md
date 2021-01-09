# Stock span problem

### Given a list of stock prices of `n` days, find the stock span for each day. Stock span is count of consecutive days before i<sup>th</sup> day having price less than equal to current day.

<br>

| input | output |
| --- | --- |
| `arr`: stock prices | `arr`: stock span |

<br>

> example :

```
input:
10 4 5 90 120 80

output:
[0, 0, 1, 3, 4, 0]
```

<br>

> approach :

1. for all the elements in array

2. compare the current elements with all the elements before it

3. if element is found which has value greater than current element value then calculate the `span`
    ```
    span[i] = indexOf(current) - indexOf(greater) - 1
    ```

4. the number of comparison with all the previous elements can be reduce using stack

5. push the element in stack only if its greater than current element

6. now compare the current element only with the top of stack element instead of every element before it

7. if top of stack is smaller than current element, keep poping the stack untill top of stack become greater or stack becomes empty

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def isEmpty(stack):
    return len(stack) is 0

def top(stack):
    return stack[len(stack) - 1]

def stockSpan(price):
    stack = []
    result = []
    
    for i in range(len(price)):
        while not isEmpty(stack) and price[top(stack)] <= price[i]:
            pop(stack)
        
        if isEmpty(stack):
            result.append(i)
        else:
            result.append(i - top(stack) - 1)

        push(stack, i)

    return result


arr = list(map(int, input().split()))

print(stockSpan(arr))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)
