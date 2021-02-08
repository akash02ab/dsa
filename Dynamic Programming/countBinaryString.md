# Find the numbers of n-bit integers which don't have consecutive 0's

| input | output |
| --- | --- |
| `n`: bits | `n`: count of numbers |

<br>

> **example :**

```
input:
3

output:
5
```

```
all 3 bits numbers:

000
001
010
011
100
101
110
111

out of 8 binary representation 5 numbers don't have consecutive 0's 
```

<br>

> **implementation :**

```python
def countBinaryString(n):
    # base condition
    fib = [0, 2, 3]

    for i in range(3, n + 1):
        fib.append(fib[i-1] + fib[i-2])

    return fib[-1]

bit = int(input())

print(countBinaryString(bit))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(n)