# Left rotate an array of size n by d elements

| input | output |
| --- | --- |
| `n`: size of array<br>`arr[n]`: array of `n` elements<br>`d`: rotation factor | `arr[n]`: rotated array

<br>

```
input:
6
1 2 3 4 5 6
2

output:
[3, 4, 5, 6, 1, 2]
```
## jugling alogrithm

<br>

> approach :

<br>

1. find gcd of `n` and `d`
    ```
    gcd(4, 2) = 2
    ```
2. divide array in groups of size equivalent to gcd
    ```
    (1 2)   (3 4)   (5 6)    i.e groups of 2
    ```
3. swap first element of first group with first element of second group, after that swap first element of second group with first element of third group and so on
    ```
    (3 2)  (5 4)  (1 6)
    ```
4. repeat previous step for second element for each group upto last element of each group
    ```
    (3 4)  (5 6)  (1 2)
    ```
5. the array is rotated by d-elements
    ```
    [3, 4, 5, 6, 1, 2]
    ```
<br>

> implementation :

<br>

```python
def gcd(a, b):
    if b == 0:
        return a

    return gcd(b, a % b)

def rotateLeft(arr, n, d):
    for i in range(gcd(n, d)):
        j = i
        k = (j + d) % n
        temp = arr[j]
        
        while i != k:
            arr[j] = arr[k]
            j = (j + d) % n
            k = (k + d) % n
        
        arr[j] = temp

    return arr


n = int(input())

arr = list(map(int, input().split()))

d = int(input())

print(rotateLeft(arr, n, d))
```

> Time and space complexity :
<br>T(n) = O(n)
<br>S(n) = O(1)

<br>

## reverse 3 time

<br>

> approach :

<br>

1. reverse the list from `0` to `d`

2. reverse the list from `d` to `n`

3. reverse the whole list from `0` to `n`

<br>

> implementation :

<br>

```python
def leftRotate(arr, n, d):
    arr[0: d] = arr[0: d][::-1]
    
    arr[d: n] = arr[d: n][::-1]
    
    arr.reverse()

    return arr

n = int(input())

arr = list(map(int, input().split()))

d = int(input())

print(leftRotate(arr, n, d))
```

> Time and space complexity :
<br>T(n) = O(n)
<br>S(n) = O(1)