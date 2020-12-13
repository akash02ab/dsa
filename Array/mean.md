# Mean of range in array

| Input | Output |
| --- | --- |
| n: size of array <br> q: number of queries <br> arr[n]: array of size n <br> l, r: range within n | m: mean of given range |

```
input:
n, q = 5, 3
arr[] = [1, 2, 3, 4, 5]

(l, r) pair:
1 3
2 4
3 5

output:
2
3
4
```

```python
def mean(sum_, qs, qe):
    s = qe - qs + 1

    if qs > 1:
        return (sum[qe-1] - sum[qs-2]) // s
    else:
        return sum[qe-1] // s

n, q = map(int, input().split())

arr = list(map(int, input().split()))

sum_ = []
sum_.append(arr[0])

for i in range(1, n):
    sum_.append(arr[i] + sum[i-1])

for _ in range(q):
    l, r = map(int, input().split())

    m = mean(sum_, l, r)
    
    print(m)
```

```
Time and Space complexity:
T(n) = O(n)
S(n) = O(n)
```