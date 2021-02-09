# Minimum coin change

### Given n coins and amount, find number of way amount can be obtained using given coins.

<br>

| input | output |
| --- | --- |
| `arr[]`: coins <br> `n`: amount | `n`: number of ways |

<br>

> **example :**

```
input:
1 2 5
5

output:
4
```
```
number of ways are 4:
(1, 1, 1, 1, 1)
(1, 1, 1, 2)
(1, 2, 2)
(5)
```

<br>

> **implementation :**

```python 
def minimumCoinChange(coin, amount):
    size = len(coin)
    # no. of ways
    NOW = [[0 for i in range(size)] for j in range(amount + 1)]

    for i in range(size):
        NOW[0][i] = 1

    for i in range(1, amount + 1):
        for j in range(size):
            x, y = 0, 0

            if i - coin[j] >= 0:
                x = NOW[i - coin[j]][j]
            
            if j >= 1:
                y = NOW[i][j-1]
            
            NOW[i][j] = x + y
    
    return NOW[amount][size - 1]

coin = list(map(int, input().split()))

amount = int(input())

print(minimumCoinChange(coin, amount))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n<sup>2</sup>)