# Largest subarray having equal 0's and 1's

| input | output |
| --- | --- |
| n: size of array<br>arr[n]: array contianing only 0's and 1's | i: start index of subarray, <br>j: end index of subarray |

```
input:
7
0 0 0 1 1 0 1

output:
1, 6
```
> appraoch


1. replace all 0's with -1
   ```
   [-1, -1, -1, 1, 1, -1, 1]
   ```
2. find prefix sum
    ```
    [-1, -2, -3, -2, -1, -2, -1]
    ```
3. prepare hash table to store prefix sum and their index
   ```
   hash = {
       -1: 0,
       -2: 1,
       -3: 2
   }
   ```
   (the hash table only contains the `smallest index` of `prefix sum`)

4. if prefix sum is not in hash table, add it

5. if prefix sum is already in hash table
   <br>(it means a subarray is found with equal number of 0's and 1's,
   <br>`start index` of subarray is present in hash table and `last index` is current index)
   <br>5.1 find the size of subarray
   ```
   size = end - start
   ```
   5.2 update maxSize if size is greater than maxSize

<br>

> implementation

```python
def largestSubArray(arr, n):
    prefixSum = [1 if arr[0] else -1]

    for i in range(1, n):
        if arr[i] == 1:
            prefixSum.append(prefixSum[i - 1] + 1)
        else:
            prefixSum.append(prefixSum[i - 1] - 1)

    hash = {}
    start = end = maxSize = 0
    
    for i in range(n):
        if prefixSum[i] == 0:
            maxSize = i
            start = 0
            end = i
        elif prefixSum[i] in hash:
            size = i - hash[prefixSum[i]]
            
            if size  > maxSize:
                maxSize = size
                start = hash[prefixSum[i]]
                end = i
        else:
            hash[prefixSum[i]] = i

    return start, end

n = int(input())

arr = list(map(int, input().split()))

print(largestSubArray(arr, n))
```
> Time and space complexity:
<br>T(n) = O(n)
<br>S(n) = O(n)