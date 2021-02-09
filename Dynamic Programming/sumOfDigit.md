# Sum of digits from 1 to N

| input | output |
| --- | --- |
| `n`: natural number | `n`: sum of digits from 1 to n |

<br>

> **example :**

```
input:
12

output:
51
```
```
sum of all digits from 1 to 12 ->
1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + (1+0) + (1+1) + (1+2)
```

<br>

> **implementation :**

```python
import math

def digitSum(n, a):
    if (n < 10):
        return (n * (n + 1)) // 2
     
    d = int(math.log(n, 10))
    p = int(math.ceil(pow(10, d)))
    msd = n // p 

    return (msd * a[d] + (msd * (msd - 1) // 2) * p + msd * (1 + n % p) + digitSum(n % p, a)) 

def sumOfDigitsFrom1ToN(n):     
    d = int(math.log(n, 10))
    a = [0]*(d + 1)
    a[0] = 0
    a[1] = 45

    for i in range(2, d + 1):
        a[i] = a[i - 1] * 10 + 45 * int(math.ceil(pow(10, i - 1)))
         
    return digitSum(n, a)
  
  
n = int(input())

print(sumOfDigitsFrom1ToN(n))
```

<br>

> **time and space complexity :**
<br> T(n) = O(log<sub>10</sub>n)
<br> S(n) = O(log<sub>10</sub>n)