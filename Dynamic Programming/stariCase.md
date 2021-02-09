# Stair case 

### Number of ways to reach top of n step stari case where one can either climb one step or two step at a time.

<br>

| input | output |
| --- | --- |
| `n`: number of steps | `m`: number of ways <br>  to climb `n` steps |

<br>

> **example :**

```
input:
5

output:
8
```

<br>

> **implementation :**

```python
def countSteps(size):
    fib = [0, 1, 2]

    if size < 0: return 0

    if size <= 2:
        return fib[size]

    for i in range(3, size + 1):
        fib.append(fib[i-1] + fib[i-2])
    
    return fib[-1]

size = int(input())

print(countSteps(size))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(n)