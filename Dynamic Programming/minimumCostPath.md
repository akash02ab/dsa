# Minimum cost path 

### Given cost matrix of size n x m, find the minimum cost to reach (n-1, m-1) from (0, 0), when only movement allowed is right, down and diagonally down.

<br>

|input | output |
| --- | --- |
| `m, n`: row and column of matrix <br> `arr[][]`: cost matrix | `n`: minimum cost path |

<br>

> **example :**

```
input:
4 4
1 2 3 4
4 5 8 3
1 5 9 2
6 2 4 3

output:
14
```

<br>

> **implementation :**

```python
def minCostPath(cost, n, m):
    CP = [[0 for i in range(m)] for j in range(n)]

    CP[0][0] = cost[0][0]

    for i in range(1, n):
        CP[i][0] = CP[i-1][0] + cost[i][0]

    for j in range(1, m):
        CP[0][j] = CP[0][j-1] + cost[0][j]

    for i in range(1, n):
        for j in range(1, m):
            CP[i][j] = min(CP[i-1][j], CP[i][j-1], CP[i-1][j-1]) + cost[i][j]
    
    return CP[n - 1][m - 1]

n, m = map(int, input().split())

cost = []
for _ in range(n):
    row = list(map(int, input().split()))
    cost.append(row)

print(minCostPath(cost, m, n))
```

<br>

>  **time and space complexity :**
<br> T(n) = O(n * m)
<br> S(n) = O(n * m)