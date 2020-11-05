# Prime Number and Prime Factorization

## Prime factorization using sieve for multiple queries

| input | output |
| --- | --- |
| x: single<br>integer | arr[]: factors of x

```
x = 12246

factors of 12246:

arr = [2, 3, 13, 157]
```

```python
from math import sqrt, ceil

MAX = 1000001

SPF = [i for i in range(MAX)]

isPrime = [True for i in range(MAX)]

def sieve():
    for i in range(2, ceil(sqrt(MAX))):
        if isPrime[i]:
            for j in range(i * i, MAX, i):
                isPrime[j] = False
                if SPF[j] == j:
                    SPF[j] = i

def factorization(x):
    arr = []
    
    while x != 1:
        arr.append(SPF[x])
        x = x // SPF[x]

    return arr

x = int(input())

sieve()

print(factorization(x))
```
```
Time and space complexity:
T(n) = O(nloglogn)
S(n) = O(n)
```