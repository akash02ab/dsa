# Rearrange array in-place such that `arr[i]` becomes `arr[arr[i]]`

> constraint : `0 <= arr[i] < n`

<br>

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of `n` natural numbers | `arr[n]`: rearranged array |

<br>

```
input:
5
1 0 2 4 3

output:
[0, 1, 2, 3, 4]
```

<br>

> approach :

    let a and b be two numbers
    let n be number greater than both a and b

    replace a with a + b * n

    from this expression value of both a and b can be retrieved

    a = a % n
    b = a / n

<br>

> implementation :

```python
def rearrange(arr, n):
    for i in range(n):
        arr[i] = arr[i] + (arr[arr[i]] % n) * n

    for i in range(n):
        arr[i] = arr[i] // n

    return arr

n = int(input())

arr = list(map(int, input().split()))

print(rearrange(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)