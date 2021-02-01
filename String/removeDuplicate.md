# Remove duplicate from string

| input | output |
| --- | --- |
| `string`: original string | `string`: string w/o duplicate |

<br>

> example :

```
input:
christofernolan

output:
christofenla
```

<br>

> approach :

1. maintain two variables
    * `current` = 0
    * `final` = 0

2. goto each `character` of `string` and maintain `hash` table and increment `current` by 1 

3. if `character` is not present in `hash` table:
    * add it to `hash` table
    * replace `string[final]` with `string[current]`
    * increment `final` by 1

4. return `string` from index `0` to `final` 

<br>

> implementation :

```python
def removeDuplicate(string):
    hash = {}

    string = list(string)

    current = final = 0
    
    for char in string:
        if char not in hash:
            hash[char] = 1
            string[final] = string[current]
            final += 1
        
        current += 1
    
    return ''.join(string[0 : final])

string = input()

print(removeDuplicate(string))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)
<br>*(ascii are from range 0 to 255, thus constant space)*