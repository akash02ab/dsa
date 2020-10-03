# Maximum AND value pair in an array

| input | output |
| --- | --- |
| n: size of array <br> arr[n]: n distinct integers | m: max AND value of two integer

```
n = 4
arr = [13, 12, 18, 19]

binary representation of each number:
bit: 4 3 2 1 0
13:  0 1 1 0 1
12:  0 1 1 0 0
18:  1 0 0 1 0
19:  1 0 0 1 1

maxVal = 0

4th bit: two elements has bit set to 1
         thus, eligible to form pair
         maxVal = maxVal | (1 << 4)
         maxVal = 0 | 16
         maxVal = 16

3rd bit: two elements has bit set to 1
         but, not eligible to form pair because previous bit is 0
         this condition can be checked using checkPair()

2nd bit: similar to 3rd bit

1st bit: two elements has bit set to 1
         and, also satisfy the checkPair()
         maxVal = maxVal | (1 << 1)
         maxVal = 16 | 2
         maxVal = 18

0th bit: two elements has bit set to 1
         but, does not satisfy checkPair() condition

Return the maxVal
```

```python
def checkPair(currVal, arr, n):
    count = 0

    for i in range(n):
        if (currVal & arr[i]) == currVal:
            count += 1
    
    return count

def maxANDpair(arr, n):
    maxVal = 0

    for bit in range(31, -1, -1):
        count = checkPair(maxVal | (1 << bit), arr, n)

        if count >= 2:
            maxVal = maxVal | (1 << bit)
    
    return maxVal

n = int(input())

arr = list(map(int, input().split()))

m = maxANDpair(arr, n)

print(m)
```

```
Time and space complexity:
T(n) = O(n log(k))   where k is maximum bit
S(n) = O(1)
```

