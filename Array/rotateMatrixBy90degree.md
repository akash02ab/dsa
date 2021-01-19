# Rotate matrix by 90<sup>o</sup> anti-clockwise

| input | output |
| --- | --- |
| `n`: size of square matrix<br>`arr[n][n]`: matrix of size `n x n` | `arr[n][n]`: matrix rotated by 90<sup>o</sup> |

<br>

```
input:
4
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16

output:
[[4, 8, 12, 16],
 [3, 7, 11, 15],
 [2, 6, 10, 14],
 [1, 5, 9, 13]]
```

<br>

> approach :
1. reverse each row

2. find transpose of matrix

<br>

> implementation :

```python
def swap(matrix, i, j):
    matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
def rotate(matrix, n):
    #reverse each row
    for i in range(n):
        matrix[i] = matrix[i][::-1]
    
    #transpose of matrix
    for i in range(n):
        for j in range(i, n):
            swap(matrix, i, j)

    return matrix

n = int(input())

matrix = []

for _ in range(n):
    row = list(map(int, input().split()))
    matrix.append(row)

print(rotate(matrix, n))
```

> **Time and space complexity :**
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(1)
