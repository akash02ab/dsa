# Create a custom power function 

| input | output |
| --- | --- |
| `n, m`: base, exponent | `n`: pow(base, exponent) |

<br>

> **example :**

```
input:
2 10

output:
1024
```

<br>

> **approach :**

* divide the problem into two halves
    
    * if exponent is `n` first compute the exponent `(n / 2)`
    
    * then, compute the original exponent `n` by multiplying the result obtained by `(n / 2)`
    
    * if exponent is `even`:
        * x<sup>n</sup> = x<sup>n/2</sup> * x<sup>n/2</sup>

    * if exponent is `odd`:
        * x<sup>n</sup> = x<sup>n/2</sup> * x<sup>n/2</sup> * x

<br>

> **implementation :**

```python
def power(x, n):
    if n == 0: return 1

    temp = power(x, n // 2)

    if n % 2 == 0:
        return temp * temp
    else:
        return x * temp * temp

base, exponent = map(int, input().split())

print(power(base, exponent))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(log(n))