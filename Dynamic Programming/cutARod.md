# Cut a rod 

### Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces.

<br>

| input | output |
| --- | --- |
| `arr[]`: price | `n`: maximum cost |

<br>

> **example :**

```
input:
1 5 8 9 10 17 17 20

output:
22
```

<br>

> **implementation :**

```python 
def cutARod(price, size):
   cost = [0 for i in range(size + 1)]
   maxCost = 0 
   
   for i in range(1, size + 1):
       for j in range(i):
           maxCost = max(maxCost, price[j] + cost[i-j-1])
    
       cost[i] = maxCost
    
   return cost[-1]

arr = list(map(int, input().split()))

print(cutARod(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n)