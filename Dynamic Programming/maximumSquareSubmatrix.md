# Maximum size squre sub-matrix with all 1's 

| input | output |
| --- | --- |
| `arr[][]`: binary matrix | `n`: size of maxtrix with all 1's |

<br>

> **example :**

```
input:
4
1 0 1 1
1 1 1 1
0 1 1 1
1 1 0 1

output:
2
```

<br>

> **implementation :**

```python
def findMaxSquareSubMatrix(matrix, size):
    maxSize = [[0 for i in range(size)] for j in range(size)]

    # fill the row
    for i in range(size):
        maxSize[0][i] = matrix[0][i]

    # fill the column
    for i in range(size):
        maxSize[i][0] = matrix[i][0]

    for i in range(1, size):
        for j in range(1, size):
            temp = min(maxSize[i-1][j], maxSize[i][j-1], maxSize[i-1][j-1])
            maxSize[i][j] = matrix[i][j] + temp
    
    return maxSize[size-1][size-1]

n = int(input())

matrix = []
for _ in range(n):
    row = list(map(int, input().split()))
    matrix.append(row)

print(findMaxSquareSubMatrix(matrix, n))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)