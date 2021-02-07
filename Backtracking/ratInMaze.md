# Rat in maze problem 

| input | output |
| --- | --- |
| `n`: size of maze <br> `arr[][]`: the maze | `arr[][]`: path from (0, 0) to (n, n) |

<br>

> **example :**

```
input:
4
1 1 0 0
1 1 1 1
0 0 1 0
1 1 1 1

output:
[[1, 0, 0, 0], 
 [1, 1, 1, 0], 
 [0, 0, 1, 0], 
 [0, 0, 1, 1]]
```

<br>

> **implementation :**

```python
def isSafe(maze, x, y, size):
    return x >= 0 and x < size and y >= 0 and y < size and maze[x][y] == 1

def solveMaze(maze, x, y, size, solution):
    if x == size - 1 and y == size - 1:
        solution[x][y] = 1
        return True 
    
    if isSafe(maze, x, y, size):
        solution[x][y] = 1

        if solveMaze(maze, x + 1, y, size, solution) or solveMaze(maze, x, y + 1, size, solution):
            return True 

        return False 
    
    return False 

def solveRatInMaze(maze, size):
    solution = [[0 for j in range(n)] for i in range(n)]

    if solveMaze(maze, 0, 0, size, solution):
        print(solution)
    else:
        print(-1)

n = int(input())

maze = []
for _ in range(n):
    row = list(map(int, input().split()))
    maze.append(row)

solveRatInMaze(maze, n)
```

<br>

> **time and space complexity :**
<br> T(n) = O(2<sup>n<sup>2</sup></sup>)
<br> S(n) = O(n<sup>2</sup>)