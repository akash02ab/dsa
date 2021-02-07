# N-Queen problem

| input | output |
| --- | --- |
| `n`: size of board | `arr[][]`: board with queen placed <br> in non-attacking position |

<br>

> **example :**

```
input:
4

output:
[[0, 0, 1, 0], [1, 0, 0, 0], [0, 0, 0, 1], [0, 1, 0, 0]]
```

<br>

> **implementation :**

```python
def isSafe(board, row, col, size):
    # check column
    i, j = row, 0
    while j < col:
        if board[i][j]: 
            return False
        j += 1
    
    # diagonal check
    i, j = row, col
    # upper left diagonal
    while i >= 0 and j >= 0:
        if board[i][j]:
            return False
        i -= 1
        j -= 1

    i, j = row, col 
    # upper right diagonal
    while i < size and j >= 0:
        if board[i][j]:
            return False 
        i += 1
        j -= 1
    
    return True

def solveNQueen(board, col, size):
    if col >= size: return True
    
    for row in range(size):
        if isSafe(board, row, col, size):
            board[row][col] = 1
            
            if solveNQueen(board, col + 1, size):
                return True
            
            board[row][col] = 0
    
    return False


n = int(input())

board = [[0 for i in range(n)] for j in range(n)]

if solveNQueen(board, 0, n):
    print(board)
else:
    print(-1)
```

<br>

> **time and space complexity :**
<br> T(n) <= O(n<sup>2</sup> * n!)
<br> S(n) = O(n)