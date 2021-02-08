# k<sup>th</sup> ugly number

### A number is said to be ugly if it's prime factorization only contains 2, 3 or 5.

<br>

| input | output |
| --- | --- |
| `k`: positive integer | `n`: k<sup>th</sup> ugly number |

<br>

> **example :**

```
input:
10

output:
12
```

<br>

> **implementation :**

```python
def getKthUglyNumber(k):
    ugly = [1]
    i2 = i3 = i5 = 0
    next2x, next3x, next5x = 2, 3, 5

    for _ in range(1, k):
        nextUglyNum = min(next2x, next3x, next5x)
        ugly.append(nextUglyNum)

        if nextUglyNum == next2x:
            i2 += 1
            next2x = ugly[i2] * 2
        if nextUglyNum == next3x:
            i3 += 1
            next3x = ugly[i3] * 3
        if nextUglyNum == next5x:
            i5 += 1
            next5x = ugly[i5] * 5
    
    return ugly[-1]

k = int(input())

print(getKthUglyNumber(k))
```

<br>

> **time and space complexity :**
<br> T(n) = O(k)
<br> S(n) = O(k)