# Symmetric Difference

| input | output |
| --- | --- |
| arr[][]: multi-dimentional array | set: symmetric diffecrence 

```
arr[x][y]: [[1, 2, 3], [2, 3, 4, 4], [4, 5, 7]]

symmetric difference:

l: {1, 5, 7}

```

```python
def symmDiff(arr):
    l = set()
    
    for i in range(len(arr)):
        l = l ^ set(arr[i])
    
    return l

print(symmDiff([[1, 2, 3], [2, 3, 4, 4], [4, 5, 7]]))
```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(1)
```