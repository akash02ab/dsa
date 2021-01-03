# Duplicate in `k`

### Check whether array contains duplicate element in next `k` index.

<br>

| input | output |
| --- | --- |
| `n, k` : length of array, window size<br> `arr` : array of `n` element | `string` : `Yes` if duplicate is present, <br> `No` otherwise |

<br>

```
input:
7 3
1 2 3 4 5 6 4

output:
'Yes'
```

```
input:
7 4
1 2 3 4 5 6 7

output:
'No'
```

<br>

> approach :

1. create hash table for first `k` elements

2. check if `i`<sup>th</sup> element is present in hash table, if present return `Yes`

3. slide the hash to next `k` element

4. repeat step 2 to 3 for all `array` elements

5. if no duplicate elements found return `No`

<br>

> implementation :

```python
def checkDuplicateInK(arr, n, k):
    hash = []

    for i in range(1, min(k + 1, n)):
        hash.append(arr[i])

    for i in range(n - 1):
        item = arr[i]
        
        if item in hash:
            return 'Yes'

        hash.pop(0)

        if i + k + 1 < n:
            hash.append(arr[i + k + 1])

    return 'No'

n, k = map(int, input().split())

arr = list(map(int, input().split()))

print(checkDuplicateInK(arr, n, k))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(k)
