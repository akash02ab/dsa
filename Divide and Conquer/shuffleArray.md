# Given array of 2n integers in following format a1, a2, ..., an, b1, b2, ..., bn. Shuffle it to format a1, b1, a2, b2, ...., an, bn

<br>

| input | output |
| --- | --- |
| `arr[]`: original array | `arr[]`: shuffled array |

<br>

> **example :**

```
input:
1 2 3 4 5 6 7 8

output:
[1, 5, 2, 6, 3, 7, 4, 8]
```

<br>

> **approach :**

1. if array of size `2` if found, return the array

2. find the `middle` element of array
    * find the middle of *left subarray*
        * `left = (start + middle) / 2`
    * find the first index of *right subarray*
        * `right = middle + 1`
    * while `left` `<` `middle`:
        * swap `array[left++]` and `arr[right++]`

3. recursively do the same with *left subarray* and *right subarray*

4. return the `array`

<br>

> **implementation :**

```python
def swap(arr, i, j):
    arr[i], arr[j] = arr[j], arr[i]

def shuffleArray(arr, start, end):
    if end - start == 1:
        return arr
    
    middle = (start + end) // 2

    right = middle + 1

    left = (start + middle) // 2 + 1

    for i in range(left, middle + 1):
        swap(arr, i, right)
        right += 1
    
    shuffleArray(arr, start, middle)
    shuffleArray(arr, middle + 1, end)
    return arr

arr = list(map(int, input().split()))

print(shuffleArray(arr, 0, len(arr) - 1))
```

<br>

> **time and space complexity :**
<br>T(n) = O(nlog(n))
<br>S(n) = O(log(n))