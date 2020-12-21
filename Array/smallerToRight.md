# Count smaller to right

### Count all the elements that are right to current element and also smaller than the current element

| input | output |
| --- | --- |
| n: size of array<br>arr[n]: array of n elements | arr[n]: count of elements smaller<br>than i<sup>th</sup> element from (i+1) to n |

```
input:
7
10 1 3 7 3 2 1

output:
[6, 0, 2, 3, 2, 1, 0]
```
>Naive approach

```python
def countSmaller(arr, n):
    result = []

    for i in range(n):
        count = 0
        for j in range(i+1, n):
            if(arr[i] < arr[j]):
                count += 1
        
        result.append(count)

    return result

n = int(input())
arr = list(map(int, input().split()))

print(countSmaller(arr, n))
```

> Time and space complexity:
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(1)

<br>

---

<br>

> Balanced Binary Tree approach

```python
```

> Time and space complexity:
<br>T(n) = O(n logn)
<br>S(n) = O(n)