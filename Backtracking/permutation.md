# Permutation of string 

| input | output |
| --- | --- |
| `string`: original string | `arr[]`: all permutation of string |

<br>

> **example :**

```
input:
ABC

output:
['ABC', 'ACB', 'BAC', 'BCA', 'CBA', 'CAB']
```

<br>

> **implementation :**

```python
def permutate(data, i, length):
    if i == length:
        l.append(''.join(data))
    else:
        for j in range(i, length):
            data[i], data[j] = data[j], data[i]
            permutate(data, i+1, length)
            data[i], data[j] = data[j], data[i]

string = input()
l = []
permutate(list(string), 0, len(string))
print(l)
```

<br>

> **time and space complexity :**
<br> T(n) = O(n * n!)
<br> S(n) = O(n)