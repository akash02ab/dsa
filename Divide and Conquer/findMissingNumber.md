# Find missing term in arithmatic progression

| input | output |
| --- | --- |
| `arr[]`: arithmatic series | `n`: missing number |

<br>

> **example :**

```
input:
-2 0 2 4 6 8 12 14 16 18 20

output:
10
```

<br>

> **approach :**

1. find the common difference of arithmatic progression
    
    * T<sub>n</sub> = a + (n - 1) * d
    * T<sub>n+1</sub> = a + n * d
    * d = (T<sub>n+1</sub> - a) / n

2. find the `middle` element and look for `left` and `right` element to it. If they follow the arithmatic progression

    * if `arr[right] - arr[middle] != difference` :
         * return `arr[middle] + difference`
    
    * if `arr[middle] - arr[left] != difference` :
        * return `arr[middle] - difference`

3. Check if `middle` element is at it's correct position or not
    
    * if `middle` element is in it's correct position then check for *left subarray*

    * if `middle` element is not in it's correct position then check for *right subarray*

<br>

> **implementation :**

```python
def findMissingElement(arr, start, end, difference):
    if end <= start: return -1
    
    middle = (start + end) // 2

    if arr[middle + 1] - arr[middle] != difference:
        return arr[middle] + difference
    
    if middle > 0 and arr[middle] - arr[middle - 1] != difference:
        return arr[middle] - difference

    if arr[middle] == (arr[0] + middle * difference):
        return findMissingElement(arr, middle + 1, end, difference)
    
    else:
        return findMissingElement(arr, start, middle - 1, difference)


arr = list(map(int, input().split()))

size = len(arr)

difference = (arr[size - 1] - arr[0]) // size

print(findMissingElement(arr, 0, size - 1, difference))
```

<br>

> **time and space complexity :**
<br>T(n) = O(log(n))
<br>S(n) = O(1)