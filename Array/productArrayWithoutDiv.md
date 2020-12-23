# Product array without division

### Find product array such that product[i] is equal to product of all elements except product[i] without using division operator

<br>

| input | output |
| --- | --- |
| n: size of array<br>arr[n]: array of n elements | arr[n]: product array of n elements | 

```
input: 
5
1 2 3 4 5

output:
[120, 60, 40, 30, 24]
```
<br>

> approach :

1. find the left product of given array
  ```
    [1, 1, 2, 6, 24]
  ```
2. find the right product of given array
```
    [120, 60, 20, 5, 1]
```
3. combine left product and right product
```
    [120, 60, 40, 30, 24]
```

<br>

> implementation

```python
def productArrayWithoutDivision(arr, n):
    product = []
    temp = 1

    for i in range(n):
        product.append(temp)
        temp *= arr[i]

    temp = 1

    for i in range(n - 1, -1, -1):
        product[i] *= temp
        temp *= arr[i]

    return product


n = int(input())

arr = list(map(int, input().split()))

print(productArrayWithoutDivision(arr, n))
```

> Time and space complexity:
<br>T(n) = O(n)
<br>S(n) = O(n)