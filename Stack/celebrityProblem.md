# Celebrity problem

### There are `n` person in total. A person is identified as celebrity if every other `n - 1` person knows him and he does not know anyone. Find the celebrity.

<br>

| input | output |
| --- | --- |
| `arr[][]`: adjacency matrix | `n`: id of celebrity if exists, <br> -1 otherwise |

<br>

> example :

```
input:
4
1 0 1 1
0 1 1 0
0 0 1 0
0 1 1 1

output:
2
```

> approach :

1. create a **stack** and `push` all the id’s in the **stack**

2. run a loop while there are more than 1 element in the **stack**

3. `pop` top two element from the **stack** (represent them as `A` and `B`)

4. check if `A` knows `B`, then `A` can’t be a celebrity and push `B` in **stack**. Check if `A` doesn’t know `B`, then `B` can’t be a celebrity push `A` in **stack**
Assign the remaining element in the **stack** as the celebrity

5. run a loop from `0 to n-1` and find the count of persons who knows the celebrity and the number of people whom the celebrity knows

6. if the count of persons who knows the celebrity is `n-1` and the count of people whom the celebrity knows is `0` then return the id of celebrity else return `-1`

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def isEmpty(stack):
    return len(stack) is 0

def knows(A, B):
    return acquaintance[A][B]

def findCelebrity(acquaintance, n):
    stack = []
    # push all the people to the stack for checking
    for i in range(n):
        push(stack, i)

    # start with two people
    A = pop(stack)
    B = pop(stack)

    # remove people if he knows other person
    while len(stack) > 1:
        if knows(A, B):
            A = pop(stack)
        else:
            B = pop(stack)

    # if only two people were initially then there is no celebrity
    if isEmpty(stack):
        return -1

    # let's assume that celebrity is C
    C = pop(stack)
    
    # check whether A is celebrity
    if knows(C, A):
        C = A
    # check whether B is celebrity
    if knows(C, B):
        C = B

    # check if C is actually a celebrity
    for i in range(n):
        # if C knows other person or other person does not know C then C is not a celebrity
        if i != C and (knows(C, i) or not knows(i, C)):
            return -1 

    return C
    

n = int(input())

acquaintance = []

for _ in range(n):
    temp = list(map(int, input().split()))
    acquaintance.append(temp)

print(findCelebrity(acquaintance, n))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)