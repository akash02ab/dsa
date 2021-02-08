# Longest consecutive sub-sequence

| input | output |
| --- | --- |
| `arr[]`: array of integers | `arr[]`: longest consecutive subsequence |

<br>

> **example :**

```
input:
10 4 3 11 13 5 6 12 7

output:
[4, 3, 5, 6, 7]
```

<br>

> **implementation :**

```python 
def findLongestConsecutiveSubsequence(arr, n):
    hash = {}

    for item in arr:
        hash[item] = 'unprocessed'
    
    maxLen = 0
    result = []
    for item in arr:
        if hash[item] == 'unprocessed':
            sequence = [item]
            hash[item] = 'processed'

            previous = item - 1
            while (previous in hash):
                sequence.append(previous)
                hash[previous] = 'processed'
                previous -= 1
            
            next = item + 1
            while (next in hash):
                sequence.append(next)
                hash[next] = 'processed'
                next += 1

            if maxLen < len(sequence):
                maxLen = len(sequence)
                result = sequence.copy()
    
    return result

arr = list(map(int, input().split()))

print(findLongestConsecutiveSubsequence(arr, len(arr)))
```

<br>

> **time and space complexity :**
<br> T(n) = O(n)
<br> S(n) = O(n)