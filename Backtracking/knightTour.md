# Knight tour 

| input | output |
| --- | --- |
| `n`: size of chess board | `arr[][]`: board of size `n`x`n` <br> representing the tour |

<br>

> **example :**

```
input:
8

output:
[[0, 59, 38, 33, 30, 17, 8, 63], 
 [37, 34, 31, 60, 9, 62, 29, 16],
 [58, 1, 36, 39, 32, 27, 18, 7],
 [35, 48, 41, 26, 61, 10, 15, 28], 
 [42, 57, 2, 49, 40, 23, 6, 19], 
 [47, 50, 45, 54, 25, 20, 11, 14], 
 [56, 43, 52, 3, 22, 13, 24, 5], 
 [51, 46, 55, 44, 53, 4, 21, 12]]
```

<br>

> **implementation :**

```python 
def isSafe(x, y, size, board):
    return x >= 0 and x < size and y >= 0 and y < size and board[x][y] == -1

def knightTour(x, y, moveI, size, board, xMove, yMove):
    if moveI == size * size:
        return True 
    
    for k in range(size):
        nextX = x + xMove[k]
        nextY = y + yMove[k]

        if isSafe(nextX, nextY, size, board):
            board[nextX][nextY] = moveI 

            if knightTour(nextX, nextY, moveI + 1, size, board, xMove, yMove):
                return True 
            else:
                board[nextX][nextY] = -1
    
    return False 

def solveKnightTour(size):
    board = [[-1 for i in range(size)] for j in range(size)]

    xMove = [2, 1, -1, -2, -2, -1, 1, 2]
    yMove = [1, 2, 2, 1, -1, -2, -2, -1]

    board[0][0] = 0

    if knightTour(0, 0, 1, size, board, xMove, yMove):
        print(board)
    else:
        print(-1)

size = int(input())

solveKnightTour(size)
```

<br>

> **time and space complexity :**
<br> T(n) = O(8<sup>(n-1)</sup>)
<br> S(n) = O(n)
<br> *(n is total number of box in chess board)*