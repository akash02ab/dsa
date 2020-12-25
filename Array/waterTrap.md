# Water trap problem

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of `n` elements | `n`: amount of water stored |

<br>

```
input:
12
0 1 0 2 1 0 1 3 2 1 2 1

output:
6
```

<br>

> appraoch :
1. build an array `left` of size `n` where `left[i]` represent maximum height bar that is left to it including i<sup>th</sup> bar

2. build an array `right` of size `n` where `right[i]` represent maximum height bar that is right to it including i<sup>th</sup> bar

3. repeat for every bar and find the water trapped above that bar 
    ```
    water += min(left[i], right[i]) - height[i]
    ```

> implementation :

```python
def waterTrap(arr, n):
    left, right, count = [arr[0]], [arr[n - 1]], 0

    for i in range(1, n):
        left.append(max(left[i - 1], arr[i]))

    for i in range(n - 2, -1, -1):
        right.insert(0, max(right[0], arr[i]))

    for i in range(n):
        count += min(left[i], right[i]) - arr[i]

    return count

n = int(input())

arr = list(map(int, input().split()))

print(waterTrap(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)