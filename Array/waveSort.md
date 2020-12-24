# Sort the array in wave form

> constraint :
```
arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4] ....
```
<br>

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of `n` elements | `arr[n]`: sorted array in wave form |

<br>

```
input:
7
10 90 49 2 1 5 23

output:
[90, 10, 49, 1, 5, 2, 23]
```

<br>

> appraoch :

1. go through all the even position elements `(0, 2, 4 ...)`

2. if previous element is smaller than swap with current element

3. if next element is larger than swap with current element

<br>

> implementation :

```python
def waveSort(arr, n):
    for i in range(0, n, 2):
        if i > 0 and arr[i - 1] > arr[i]:
            [arr[i - 1], arr[i]] = [arr[i], arr[i - 1]]
        if i < n - 1 and arr[i] < arr[i + 1]:
            [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]]

    return arr

n = int(input())

arr = list(map(int, input().split()))

print(waveSort(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)