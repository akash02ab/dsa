# Search an element in row wise and column wise 2D sorted array

| input | output |
| --- | --- |
| `n`: size of array <br> `arr[][]`: sorted array <br> `x`: target element | `(i, j)`: index of target element |

<br>

> **example :**

```
input:
4
10 20 30 40
15 25 35 45
27 29 37 48
32 33 39 50
29

output:
(2, 1)
```

<br>

> **implementation :**

```python
def search(arr, size, x):
    i, j = 0, size - 1

    while i < size and j >= 0:
        if(arr[i][j] == x):
            return (i, j)
        if arr[i][j] > x:
            j -= 1
        else:
            i += 1
    
    return -1

n = int(input())

arr = [] 
for _ in range(n):
    temp = list(map(int, input().split()))
    arr.append(temp)

x = int(input())

print(search(arr, n, x))
```

<br>

> **recurrence relation :**
<br> T(k) = 3 * T(k / 4) + 1
<br> *(k is number of element in array i.e k = n<sup>2</sup>)* 

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2 * (log<sub>4</sub>3)</sup>) = O(n<sup>2 * 0.792</sup>) = O(n<sup>1.5</sup>)
<br> S(n) = O(1)