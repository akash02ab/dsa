# Reverse the words within the sentence

| input | output |
| --- | --- |
| `string`: original sentence | `string`: sentence with <br> words in reverse order |

<br>

> example :

```
input:
hello this is sample

output:
sample is this hello
```

<br>

> approach :

1. reverse the each word in the sentence

2. reverse the whole sentence

3. return the sentence

<br>

> implementation :

```python
def reverseWords(sentence):
    # convert string to list of words
    sentence = sentence.split(' ')

    # reverse each word of the sentence
    for index in range(len(sentence)): 
        word = sentence[index]
        sentence[index] = word[::-1]

    # convert sentence back to string with space
    sentence =  ' '.join(sentence)
    # reverse the whole string
    sentence = sentence[::-1]

    return sentence

sentence = input()

print(reverseWords(sentence))
```

<br>

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(1)