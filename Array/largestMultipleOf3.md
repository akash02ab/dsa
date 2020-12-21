# Largest multiple of 3

### Given an array of non-negative integers. Find the largest multiple of 3 that can be formed from array elements

<br>

| input | output |
| --- | --- |
| arr[]: array of elements | n: maximum number divisible by 3<br>if no such number exits than return -1 |

<br>

> Example :

```
input: 
8 1 9
output:
981

input:
8 1 7 6 0
output:
8760
```

```python
def maximumMultipleOf3(arr):
    arr.sort()
    queue1, queue2 = [], []
    sum = 0

    for i in range(len(arr)):
        sum += arr[i]
        
        if arr[i] % 3 == 1:
            queue1.append(arr[i])
        elif arr[i] % 3 == 2:
            queue2.append(arr[i])
    
    if sum % 3 == 1:
        if len(queue1):
            e = queue1.pop(0)
            arr.remove(e)
        elif len(queue2) >= 2:
            e = queue2.pop(0)
            arr.remove(e)
            e = queue2.pop(0)
            arr.remove(e)
        else:
            return -1

    elif sum % 3 == 2:
        if len(queue2):
            e = queue2.pop(0)
            arr.remove(e)
        elif len(queue1) >= 2:
            e = queue1.pop(0)
            arr.remove(e)
            e = queue1.pop(0)
            arr.remove(e)
        else:
            return -1

    arr.sort(reverse = True)
    return ''.join(map(str, arr))

arr = list(map(int, input().split()))

print(maximumMultipleOf3(arr))
```

> Time and space complexity:
<br>T(n) = O(n logn)
<br>S(n) = O(n)

