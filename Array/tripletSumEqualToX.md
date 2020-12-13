# Find a triplet in an array whose sum is equal to 'X'

| input | output |
| --- | --- |
| arr[]: array of integers <br> X: single integer | [a, b, c] |

```
input:
arr[] = [6, 9, 1, 4, 2, 7]
X = 7

output:
[1, 2, 4]
```

```python
def findTriplet(arr, X):
    arr.sort()

    for index in range(len(arr) - 2):
        l, r = index + 1, len(arr) - 1

        while l < r:
            tripletSum = arr[index] + arr[l] + arr[r]

            if tripletSum == X:
                return [arr[index], arr[l], arr[r]]
            elif(tripletSum < X):
                l += 1
            else:
                r -= 1
    
    return -1


arr = list(map(int, input().split()))

X = int(input())

result = findTriplet(arr, X)

print(result)
```


>Time and space complexity:
<br>T(n) = O(n<sup>2</sup>)
<br>S(n) = O(1)


