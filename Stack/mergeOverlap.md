# Merge overlapping intervals

| input | output |
| --- | --- |
| `n` : numbers of intervals <br> `start, end` : `n` instance of start and end time| `arr` : merged time intervals |

<br>

```
input:
4
1 3
2 4
5 7
5 8

output:
[(1, 4), (5, 8)]
```

<br>

> approach :

1. sort the interval in the increasing order of start time

2. initialize two empty stack `stackS` and `stackE` 

3. push the initial `start` time to `stackS` and `end` time to `stackE`

4. for rest of the time intervals
    * `start` = start time from top of `stackS`
    
    * `end` = end time from top of `stackE`
    
    * if `new-start` is greater than `end` then there is no overlap simply push the `new-start` and `new-end` to respective stacks

    * else update `end` if `new-end` is greater and push it to stack accordingly

5. at the end both the stack contains merged intervals

<br>

> implementation :

```python
def push(stack, item):
    stack.append(item)

def pop(stack):
    return stack.pop()

def top(stack):
    return stack[len(stack) - 1]

def mergeOverlap(intervals):
    intervals.sort()
    # stacks to store the overlaped start and end time
    stackS = []
    stackE = []
    # push the first time interval
    push(stackS, intervals[0][0])
    push(stackE, intervals[0][1])
    # for rest of the intervals
    for i in range(1, len(intervals)):
        start = top(stackS)
        end = top(stackE)

        '''
        push the new-start (intervals[i][0]) and new-end (intervals[i][1]) 
        to the stack if there is no overlaping
        '''
        if end < intervals[i][0]:
            push(stackS, intervals[i][0])
            push(stackE, intervals[i][1])    
        elif end < intervals[i][1]:
            # update end only if new-end is greater the end
            end = intervals[i][1]
            # pop the old start and end time
            pop(stackS)
            pop(stackE)
            # push the new overlaped start and end time
            push(stackS, start)
            push(stackE, end)
    
    return [(stackS[i], stackE[i]) for i in range(len(stackS))]

n = int(input())

intervals = []

for _ in range(n):
    start, end = map(int, input().split())
    intervals.append([start, end])

print(mergeOverlap(intervals))
```

> **Time and space complexity :**
<br>T(n) = O(n log(n))
<br>S(n) = O(n)