# Perfect hill

### A perfect hill is sequence of length 2k+1 where the first k+1 integers are strictly increasing and last k+1 integers are strictly decreasing. Find the maximum length of perfect hill.

<br>

> **example :**

```
input:
10 15 16 9 4 3 11 1

output:
5
```

```
        16
      /    \
    15      9
   /         \
  10          4

(one of possible perfect hill for given input having length 5)
```

<br>

> **implementation :**

```python 
def getIncreasingSubsequenceLength(arr, size):
    seqLength = [1] * size 

    for i in range(size):
        for j in range(i):
            if arr[i] > arr[j] and seqLength[i] < seqLength[j] + 1:
                seqLength[i] = seqLength[j] + 1

    return seqLength 

def getDecreasingSubsequenceLength(arr, size):
    seqLength = [1] * size

    for i in range(size-1, -1, -1):
        for j in range(i, size):
            if arr[i] > arr[j] and seqLength[i] < seqLength[j] + 1:
                seqLength[i] = seqLength[j] + 1
    
    return seqLength

def perfectHill(arr, size):
    increasingSeq = getIncreasingSubsequenceLength(arr, size)
    decreasingSeq = getDecreasingSubsequenceLength(arr, size)

    maxLength = 0

    for i in range(size):
        leftHillLen = increasingSeq[i] - 1
        rightHillLen = decreasingSeq[i] - 1
        hillLength = 2 * min(leftHillLen, rightHillLen) + 1
        maxLength = max(hillLength, maxLength)
    
    return maxLength

arr = list(map(int, input().split()))

print(perfectHill(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n<sup>2</sup>)
<br> S(n) = O(n)