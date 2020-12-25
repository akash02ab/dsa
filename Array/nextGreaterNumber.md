# Next greater number with same set of digit

| input | output |
| --- | --- |
| `n`: positive integer | `m`: next integer greater than `n` |

<br>

```
input:
534976

output:
536479
```

<br>

> appraoch :

1. find the first place from right where left digit is less than the right digit i.e. ` numbers[i] > numbers[i - 1]`

2. find the smallest digit larger than `numbers[i - 1]` to the right let's call it `numbers[k]`

3. swap the two digit `numbers[i - 1]` and `numbers[k]`

4. sort all the numbers that are right to the `numbers[i - 1]` in non-decreasing order

<br>

> implementation :

```python
def findNext(number):
    arr = list(map(int, str(number)))

    n = len(arr)

    for i in range(n - 1, 0, -1):
        if arr[i] > arr[i - 1]:
            break

    if i == 0:
        return -1

    k = i
    for j in range(i + 1, n):
        if arr[j] < arr[k]:
            k = j
    
    [arr[k], arr[i - 1]] = [arr[i - 1], arr[k]]

    arr[i : n] = arr[i : n][::-1]

    return ''.join(map(str, arr))

number = int(input())

print(findNext(number))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1) `if input is in array format else O(n)`