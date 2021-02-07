# Find the minimum number of platform required such that there is no collision

| input | output |
| --- | --- |
| `n`: number of trains <br> `arr[][]`: arrival and departure time of trains| `n`: minimum number of platform need |

<br>

> **example :**

```
input:
5
7:12 7:25
8:00 8:20
7:30 7:45
6:50 7:10
7:15 7:30

output:
2
```

<br>

> **implementation :**

```python
def countPlatform(timeTable, n):
    arrival = []
    departure = []

    for [arr, dep] in timeTable:
        arrival.append(arr)
        departure.append(dep)
    
    arrival.sort()
    departure.sort()
    
    platform = train = 1

    i, j = 1, 0

    while i < n and j < n:
        if arrival[i] < departure[j]:
            train += 1
            i += 1
        else:
            train -= 1
            j += 1

        if train > platform:
            platform = train
    
    return platform

n = int(input())

timeTable = []

for _ in range(n):
    arrival, departure = map(str, input().split())
    timeTable.append([arrival, departure])

print(countPlatform(timeTable, n))
```

<br>

> **time and space complexity :**
<br> T(n) = O(nlog(n))
<br> S(n) = O(1)