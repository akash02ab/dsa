# Smallest sum impossible

> Given an array of positive integers. Find the smallest number that cannot be generated with sum of numbers by using the array.

<br>

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of `n` elements | `n`: smallest number that is<br>impossible to form by summing |

<br>

```
input:
7
2 4 7 5 6 9 1

output:
35
```

<br>

> approach :
1. sort the array in ascending order
    ```
    [1, 2, 4, 5, 6, 7, 9]
    ```
2. initialize sum to 1
    ```
    sum = 1
    ```
3. check if sum can be formed using only first element
    ```
    (1) 2 4 5 6 7 9
    ```
    in this case `sum = 1` can be formed by using `(1)`
    <br>so, `sum += 1`

4. now `sum = 2`, check if sum can be formed using first two elements
    ```
    (1 2) 4 5 6 7 9
    ```
    in this case `sum = 2` can be formed by using `(2)` alone, <br>and `sum = 3` can also be formed by using `(1 2)`
    <br>so, `sum += 2`

5. now `sum = 4`, check if sum can be formed using first three elements
    ```
    (1 2 4) 5 6 7 9
    ```
    in this case `sum = 4` can be formed by using `(4)` alone, <br>and `sum = 5` can be formed by using `(1 4)`, <br>and `sum = 6` can be formed by using `(2 4)`, <br>and `sum = 7` can be formed by using `(1 2 4)`
    <br>so, `sum += 4`

6. continue the above process untill sum cannot be fromed or last element of array is reached

<br>

> implementation :

```python
def smallestSumImpossible(arr, n):
    arr.sort()

    sum = 1

    for i in range(n):
        if sum < arr[i]:
            return sum
        
        sum += arr[i]

    return sum

n = int(input())

arr = list(map(int, input().split()))

print(smallestSumImpossible(arr, n))
```

> **Time and space complexity :**
<br>T(n) = O(n log(n))
<br>S(n) = O(1)
