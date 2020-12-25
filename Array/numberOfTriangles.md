# Number of triangles

> Given an array of unsorted positive integers find the total numbers of triangle possible

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of size `n` | `n`: total number of triangle |

<br>

```
input:
7
8 12 7 14 50 6 10

output:
18
```

<br>

> approach :
1. sort the array in ascending order

2. choose three numbers `a`, `b` and `c` where, `a < b < c`

3. if `a + b > c` than triangle is possible

4. check for all <sup>n</sup>C<sub>3</sub> combination

<br>

> implementation :

```python
def numberOfTriangle(arr, n):
    arr.sort()

    count = 0
    for i in range(n - 3):
        for j in range(i + 1, n - 2):
            for k in range(j + 1, n):
                if arr[i] + arr[j] > arr[k]:
                    count += 1
                else:
                    break
    
    return count

n = int(input())

arr = list(map(int, input().split()))

print(numberOfTriangle(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>3</sup>)
<br>S(n) = O(1)
