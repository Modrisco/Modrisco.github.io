---
layout: post
title: An online judgement 2019.3.17
date: 2019-03-22 00:28:49.000000000 +10:00
---
### 1. Rotate upper letters and lower letters in a string
Difficulity: ✩
> Give a string s, rotate all lower letters (a-z) to upper letters (A-Z), and process the same way for upper letters.
 Input: 'uuuCCKsf(*.'
 Output: 'UUUcckSF(*.'

Use Python string library could provide a straightforward solution
````python
import string
def rotate_letter(s):
    l = list(s)
    for index, letter in enumerate(l):
        if letter.islower():
            l[index] = letter.upper()
        elif letter.isupper():
            l[index] = letter.lower()
    return ''.join(l)
if __name__ == '__main__':
    s = input()
    rotate_letter(s)
````

### 2. Statistic letter show times in a string
Difficulity: ✩✩
> Give a string s, make a statistic of letters and order by frequency, if several letters have the same frequency, order by natural order (a-z)
Input: hufosniuosfbyvgugbyuceca
Output: u:4; b:2; c:2; f:2; g:2; o:2; s:2; y:2; a:1; e:1; h:1; i:1; n:1; v:1;
 
 
 Firstly, for python, this is a hash problem, make a dict and a counter will help to make this statistic.
````python
>>>> input: 'hufosniuosfbyvgugbyuceca'
s = input()
c = Counter(s)
print(c)
>>>> ouput: Counter({'h': 1, 'u': 4, 'f': 2, 'o': 2, 's': 2, 'n': 1, 'i': 1, 'b': 2, 'y': 2, 'v': 1, 'g': 2, 'c': 2, 'e': 1, 'a': 1})
````
Secondly, let's do the sorting part. Sorting a list or dictionary with only one key could be easy.
````python
# sort the dict by value in desc
print(sorted(c.items(), key=lambda x: x[1], reverse=True))
>>>> output: [('u', 4), ('f', 2), ('o', 2), ('s', 2), ('b', 2), ('y', 2), ('g', 2), ('c', 2), ('h', 1), ('n', 1), ('i', 1), ('v', 1), ('e', 1), ('a', 1)]
````

We may notice that the the order of keys with same value are still inn their string's first show order `('f', 2), ('o', 2), ('s', 2), ('b', 2), ('y', 2), ('g', 2), ('c', 2)`. Then here comes the problem with ordering a list / dictionary with two keys. Plus, the second key is not numeric. 
To deal with this problem. We can use `ord()` to convert a letter into it's ascii number. Then, we use two keys in the sort part.
````python
sorted_c = sorted(c.items(), key=lambda x: (x[1],-ord(x[0])), reverse=True)
print(c)
>>>> output: [('u', 4), ('b', 2), ('c', 2), ('f', 2), ('g', 2), ('o', 2), ('s', 2), ('y', 2), ('a', 1), ('e', 1), ('h', 1), ('i', 1), ('n', 1), ('v', 1)]
````
Finally, decorate the output part as required.
````python
output = []
for item in sorted_c:
    output.append(str(item[0]) + ':' + str(item[1]) + ';')
print(output)
>>>> output: u:4; b:2; c:2; f:2; g:2; o:2; s:2; y:2; a:1; e:1; h:1; i:1; n:1; v:1;
````
Now, we are done~

### 3 Decimal to letter
Difficulity: ✩✩
Same as Leetcode 168 [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/).
> Given a list of positive integers, return a list of corresponding column titles as appear in an Excel sheet.
 Translate rule:
    1 -> A, 2 -> B, 3 -> C ... 26 -> Z, 27 -> AA, 28 -> AB .... 
Input: [1, 28, 701]
Output: ["A", "AB", "ZY"]

Let's see the relationship between the Excel sheet column title and the number:
```
A   1     AA    26+ 1     BA  2×26+ 1     ...     ZA  26×26+ 1     AAA  1×26²+1×26+ 1
B   2     AB    26+ 2     BB  2×26+ 2     ...     ZB  26×26+ 2     AAB  1×26²+1×26+ 2
.   .     ..    .....     ..  .......     ...     ..  ........     ...  .............   
.   .     ..    .....     ..  .......     ...     ..  ........     ...  .............
.   .     ..    .....     ..  .......     ...     ..  ........     ...  .............
Z  26     AZ    26+26     BZ  2×26+26     ...     ZZ  26×26+26     AAZ  1×26²+1×26+26
```
Now we can see that `ABCD＝A×26³＋B×26²＋C×26¹＋D＝1×26³＋2×26²＋3×26¹＋4`
But how to get the column title from the number? We can't simply use the n%26 method because:
`ZZZZ＝Z×26³＋Z×26²＋Z×26¹＋Z＝26×26³＋26×26²＋26×26¹＋26`
We can use (n-1)%26 instead, then we get a number range from 0 to 25.

Code:
``` python
def convertToTitle(n: int) -> str:
    import string
    letters = list(string.ascii_uppercase)
    result = []
    if n == 0:
        return ""
    while n > 0:
        result.append(letters[(n-1) % 26])
        n = (n - 1) // 26
    return ''.join(result[::-1])

if __name__ == "__main__":
    numbers = input()
    return [convertToTitle(number) for number in numbers]
```

Welcome to share any interview questions and discuss together~

