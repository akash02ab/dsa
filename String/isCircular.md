# Check if sequence of moves is circular is not

### Let's assume the path begins from co-ordinate (0, 0), if the path end at (0, 0) then it's circular.

<br>

| input | output |
| --- | --- |
| `string`: sequence of moves | `boolean`: `True` if path is circular, <br> `False` otherwise |

<br>

> example :

```
input:
GLGLGLG

output:
True
```

```
input only contains `L`, `R` and `G`
L: change direction to left
R: change direction to right
G: move one unit forward
```

<br>

> approach :

1. initial position is (0, 0) facing North direction

2. for each move in path:
    * if move is `L` or `R`, change the direction

    * if move is `G` then, update the cordinate

3. if final position is (0, 0), the path is circular

<br>

> implementation :

```python
def isCircular(path):
    [N, E, S, W] = [0, 1, 2, 3]

    # initial position
    x = y = 0
    # assume facing north initially
    direction = N

    for move in path:
        if move == 'R':
            direction = (direction + 1) % 4
        elif move == 'L':
            direction = (4 + direction - 1) % 4
        else:
            if direction == N:
                y += 1
            elif direction == E:
                x += 1
            elif direction == S:
                y -= 1
            else:
                x -= 1
    
    return x == 0 and y == 0

path = input()

print(isCircular(path))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)