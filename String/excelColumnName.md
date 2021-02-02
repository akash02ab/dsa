# Excel column name

| input | output |
| --- | --- |
| `n`: column number | `string`: column name |

<br>

> example :

```
input:
28

output:
AB
```

<br>

> appraoch :

* use the number system representation with base 26

* number = 28 = 26<sup>1</sup> * 1 + 26<sup>0</sup> * 2

* start converting number to string from right side

    * remainder = 28 % 26 = 2

    * colname += B *(B is represented by 2)*

    * number = number / 26 = 28 / 26 = 1

    * reaminder = 1 % 26 = 1

    * colname += A *(A is represented by 1)*

    * number = number / 26 = 1 / 26 = 0

* return colname *(AB)*

<br>

> implementation :

```python
def excelColumnName(number):
    colname = ''
    
    while number > 0:
        remainder = number % 26

        if remainder == 0:
            colname = 'Z' + colname
            number //= 26 - 1
        else:
            colname = chr(ord('A') - 1 + remainder) + colname
            number //= 26

    return colname

number = int(input())

print(excelColumnName(number))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(log<sub>26</sub>(n))
<br>S(n) = O(1)