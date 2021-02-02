# Run length encoding 

| input | output |
| --- | --- |
| `string`: original string | `string`: encoded string |

<br>

> example :

```
input:
aaabbbbccc

output:
a3b4c3
```

<br>

> appraoch :

* for each character in string (start from index 1)
    * if current character is equal to previous character
        * increment character count
    * else add the character and character count to `result` string

* add the last character and charater count to the `result` string *(edge case)*

* return `result` string

<br>

> implementation :

```python
def runLengthEncoding(string):
    result = ''
    count = 1
    n = len(string)

    for i in range(1, n):
        if string[i] == string[i-1]:
            count += 1
        else:
            result += f'{string[i-1]}{count}'
            count = 1
    
    result += f'{string[n-1]}{count}'
    
    return result

string = input()

print(runLengthEncoding(string))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)