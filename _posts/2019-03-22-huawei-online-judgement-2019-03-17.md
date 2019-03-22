---
layout: post
title: HUAWEI online judgement 2019.3.17
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
Output: 
 
 
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


