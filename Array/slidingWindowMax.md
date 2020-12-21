# Maximum at each Sliding Window

## Find the maximum element for each and every contiguous sub-array of size k.

| input | output |
| --- | --- |
| n: size of array<br>arr[]: array of n elements<br>k: size of sub-array | arr[]: maximum element of each sub-array <br>(the size of output array = n - k + 1)|

```
input:
16
15 9 4 17 18 12 6 26 27 16 1 12 14 21 35 29
4
output:
[17 18 18 18 26 27 27 27 27 16 21 35 35]
```
> cheap trick
```python
def slidingWindowMax(n, arr, k):
    result = []

    for i in range(n - k + 1):
        result.append(max(arr[i : i+k]))

    return result    

n = int(input())
arr = list(map(int, input().split()))
k = int(input())

output = slidingWindowMax(n, arr, k)

print(output)
```
> array implementation
```python
def slidingWindowMax(n, arr, k):
    result = []
    '''
    1. sliding window contains the index of sub-array of size k
    2. 0th index of window contains the index of maximum element in current sub-array
    3. window is updated each time it slides
    4. maximum size of window can not exceed k
    ''' 
    window = [0]

    
    # initialize window for first sub-array of size k
    for i in range(k):
        '''
        1. if value of current element is greater than other elements,
        there is no point in keeping the other elements
        2. remove index of other elements while value of current element is greater than value of elements in window
        3. if value of current element is less than last element at window, the current value can be maximum element at some point when window slides so, append it to window
        '''
        while len(window) and arr[i] >= arr[window[-1]]:
            window.pop()
        window.append(i)

    for i in range(k, n):
        # append maximum value of previous window
        result.append(arr[window[0]])

        # pop first element when windows slides
        if window[0] == i - k:
            window.pop(0)

        while len(window) and arr[i] >= arr[window[-1]]:
            window.pop()

        window.append(i)
    
    # append maximum value of last window
    result.append(arr[window[0]])

    return result    

n = int(input())
arr = list(map(int, input().split()))
k = int(input())

output = slidingWindowMax(n, arr, k)

print(output)
```

> Time and space complexity:
<br>T(n) = O(nk)
<br>S(n) = O(k)
