# Breadth first search

## BFS using adjacency matrix

| input | output |
| --- | --- |
| n: number of nodes<br>arr[][]: adj matrix | arr[]: node traversal order |

```
input:
5
1 1 0 0 1
1 1 1 1 1
0 1 1 1 0
0 1 1 1 1
1 1 0 1 1

output:
[0, 1, 4, 2, 3]
```

```python
def bfs(graph):
    n = len(graph)
    visited = [False] * n
    traversal = []

    firstNode = 0
    queue = [firstNode]
    visited[firstNode] = True

    while len(queue):
        i = queue.pop(0)
        traversal.append(i)

        for j in range(n):
            if(graph[i][j] == 1 and not visited[j]):
                queue.append(j)
                visited[j] = True

    return traversal

n = int(input())

graph = []
for _ in range(n):
    row = list(map(int, input().split()))
    graph.append(row)

print(bfs(graph))
```

> Time and space complexity:
<br>T(n) = O(V<sup>2</sup>)
<br>S(n) = O(V)
<br>where, V = number of vertex

<br>

---

<br>

## BFS using adjacency list

| input | output |
| --- | --- |
| n: number of nodes<br>arr[][]: adj list | arr[]: node traversal order |
```
input:
5
1 4
0 2 3 4
1 3
1 4
0 1 3

output:
[0, 1, 4, 2, 3]
```

```python
def bfs(graph):
    n = len(graph)
    visited = [False] * n
    traversal = []

    firstNode = 0
    queue = [firstNode]
    visited[firstNode] = True

    while len(queue):
        i = queue.pop(0)
        traversal.append(i)

        for j in graph[i]:
            if(not visited[j]):
                queue.append(j)
                visited[j] = True

    return traversal

n = int(input())

graph = []
for _ in range(n):
    row = list(map(int, input().split()))
    graph.append(row)

print(bfs(graph))
```

>Time and space complexity:
<br>T(n) = O(V + E)
<br>S(n) = O(V)
<br> where V = number of vertex, E = number of edge