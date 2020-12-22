# Subarray with sum exactly k

## Is there exists any subarray with sum k

| Input | Output |
| --- | --- |
| arr[], k | True or Fasle|

```
arr[] = [4, 3, 7, -4, 4, 9, -2]
k = 7

subarrays with sum 7:
[4, 3], [7], [7, -4, 4], [-4, 4, 9, -2], [9, -2]

so, there are 5 subarray with sum 7
return True
```

```python
def isSubarrayExists(arr, k):
    n = len(arr)
    currentSum = 0
    prefixSum = []

    for i in range(n):
        currentSum += arr[i]

        if currentSum == k:
            return True

        if (currentSum - k) in prefixSum:
            return True

        prefixSum.append(currentSum)

    return False

arr = list(map(int, input().split()))

k = int(input())

print(isSubarrayExists(arr, k))
```
```
Time and space complexity:
T(n) = O(n)
S(n) = O(n)
```
<br>

---

<br>

## Number of subarray with sum k

| Input | Output |
| --- | --- |
| arr[], k | x : count of subarray<br>with sum k 

```python
from collections import defaultdict

def numberofSubarray(arr, k):
    n = len(arr)
    currentSum = count = 0
    prefixSum = defaultdict(int)

    for i in range(n):
        currentSum += arr[i]

        if currentSum == k:
            count += 1

        if (currentSum - k) in prefixSum:
            count += prefixSum[currentSum - k]

        prefixSum[currentSum] += 1

    return count

arr = list(map(int, input().split()))

k = int(input())

print(numberofSubarray(arr, k))
```

```
Time and space complexity:
T(n) = O(n)
S(n) = O(n)
```

<br>

---

<br>

## Maximum subarray sum divisible by k

| Input | Output |
| --- | --- |
| arr[], k | x : sum of maximum <br>subarray divisible by k 

```python
def subArraySumDivbyK(arr, k):
    n = len(arr)
    currentSum = sum_ = 0
    moduloSum = [-1 for i in range(k)]
    moduloSum[0] = 0
    

    for i in range(n):
        currentSum += arr[i]
        index = currentSum % k
        
        if moduloSum[index] == -1:
            moduloSum[index] = currentSum
        else:
            sum_ = max(sum_, currentSum - moduloSum[index]) 
    
    return sum_

arr = list(map(int, input().split()))

k = int(input())

print(subArraySumDivbyK(arr, k))
```
```
Time and space complexity:
T(n) = O(n)
S(n) = O(n)
```
