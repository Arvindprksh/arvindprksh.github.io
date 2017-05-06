---
layout: post
title: Tutorial of python with jump to python,open-book.
subtitle: I will let you know the basics of python syntax.
category: Python
tags: [language, python]
permalink: /2017/03/30/Jump_to_python_tutorial/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---


ahead of reading this article. If you have a little of experience about programming. you don't need to read this aticle.

**Just go to [standford's tutorial]()**

this article that I will introduce you is for newbie of python

I made this tutorial of python based on ["Jump to Python", open-book](https://wikidocs.net/book/1).

Note that I wrote this article based on what I understand about python, comparing it with what I understand on C++/C language. 

---

**Before you read this article, You have to keep in mind about several things.**

**In Python, everything is object, instance of class. especially above Python 3.x.**

In other words, even integer is object above Python 3.x.

---

**BUT,** If you are beginner of Python, You don't need to consider this concept. however, If you want to be intermediate.

Keep in mind, "Everything of Python is Object, instance of Class"

Indirectly, You can check it up about what I wrote above. 

**use getrefcount() function in sys module**

**If you can know whether I write what I understand on Python or not, Please let me know what's wrong as tutorial of Python.**

And then, I will fix it as you know me after I check it up. 

If you know me, I really appreciate it!!

---

# Tutorial Of python With [Jump to python,Open-book](https://wikidocs.net/book/1)

Python has effective approach to object-oriented Programming. 

And the features of the Python are dynamically typed language and multi-paradigm programming language. 

So you can code source like many ways for Object-oriented Programming, strucural programming, and functional Programming.  

**remember ! Basically in jump to python, the version of Python is above 3.0. basically they use 3.0 version python.**

what kind of data type do python have?

**But this tutorial will be made on Python 2.7.5 that I have On my CentOS, Or on python 3.6 at Windows 10**

  - [Basic data types](#Basic-data-types)
      - numberic
      - string
      - Boolean
      
  - Containers 
      - Lists
      - Dictioinaries
      - Sets
      - Tuple
      
  - Functions
  
  - Classes


&nbsp;&nbsp;
## Basic data types

### Numberic : This data type is similar to primitive type of C, C++ language or JAVA. i.e,BUT one is different from those languages, that is when you want to change primitive type to object type. Normally, you use the **wrapper class** in java. just think of this type in python like it. i.e numeric is also object in python.

Let's see the sampe code, be careful, my python is 2.7

```python
>>> a = 123     # integer
>>> b = -178    # negative integer 
>>> c = 0 
>>> print a, b, c
123 -178 0
>>> print type(a), type(b), (c)   # in python 3.0 type -> class
<type 'int'> <type 'int'> 0
>>> a = 1.2     # float-point
>>> b = -3.45
>>> c = 4.24E10
>>> d = 4.24e-10
>>> print a, b, c, d
1.2 -3.45 42400000000.0 4.24e-10
>>> print type(a), type(b), type(c), tyep(d)
<type 'float'> <type 'float'> <type 'float'>
>>> print type(a), type(b), type(c), type(d)
<type 'float'> <type 'float'> <type 'float'> <type 'float'>
>>> a = 0o177    # octal numeric
>>> a
127
>>> b = 0x8ff    # hexa numeric
>>> b
2303
>>> a = 3       # calculation with '+, -, *, /, // %'
>>> b = 4
>>> a + b
7
>>> a - c
-42399999997.0
>>> a - b
-1
>>> a * b
12
>>> a / b     # in python 3.0, 0 -> 0.75 
0
>>> a // b    # '//' operator is similar to floor function of math
0
>>> a ** b
81
>>> a % b
3
```

### String : this is just string when you use string in Java and C++ language. here, when you create string type in python. whatever mark between 'string' and "string"you use doesn't matter. 

```python
>>> str = "Life is too short, you need to learn python"
>>> print str
Life is too short, you need to learn python
>>> print type(str)                                   # in python 3.0, type -> class
<type 'str'>
>>> str = 'Life is too short, you need to learn python'
>>> print str
Life is too short, you need to learn python
>>> print type(str)
<type 'str'>
>>> str = """                             # for multilines with '''string''', 'string \n string', another way is with """string""" and "string \n string"
... Life is too short, 
... you need to learn Python
... """
>>> print str

Life is too short, 
you need to learn Python

>>> print type(str)
<type 'str'>
>>> say = '"Python is very easy to learn" I said'           # how to use ' and " together
>>> print say
"Python is very easy to learn" I said
>>> print type(say)
<type 'str'>
>>> say = "'Python is very easy to learn' I said"
>>> print say
'Python is very easy to learn' I said
>>> print type(say)
<type 'str'>
>>> say = "\"Python is very easy to learn\" I said"
>>> print say
"Python is very easy to learn" I said
>>> print type(say)
<type 'str'>


>>> head = "python "                      # extension of string
>>> tail = "looks like fun"
>>> head + tail
'python looks like fun'
>>> head * 3
'python python python '
>>> str = "Life is too short, you need to learn python"           # indexing and slicing of string
>>> str[3]
'e'
>>> str[:3]
'Lif'
>>> str[3:]
'e is too short, you need to learn python'
>>> str[-1]
'n'
>>> str[8:-1]
'too short, you need to learn pytho'
>>> str1 = "20170405sunny"
>>> year = str1[0:4]
>>> date = str1[4:8]
>>> weather = str1[8:]
>>> year
'2017'
>>> date
'0405'
>>> weather
'sunny'
>>> test =  "pithon"                    # string is immutable, So you have to create new string when you fix string, wrong letter.
>>> test[1] = y
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> test = test[0] + "y" + test[2:]
>>> test
'python'

>>> number = 10                         # string formatting 
>>> day = "three"
>>> "After I ate %d apples, I was sick for %s days" % (number, day)
'After I ate 10 apples, I was sick for three days'

>>> "Error is %d%%" % 10                # %%
'Error is 10%'
>>> "%10s" % "hi"
'        hi'
>>> "%-10s" % "hi"
'hi        '
>>> "%-10s Let's study python" % "hi"
"hi         Let's study python"
>>> "%0.4f" % 3.124567
'3.1246'
>>> "%10.4f" % 3.124567
'    3.1246'
>>> "%-10.4f" % 3.124567
'3.1246    '

>>> str = "python is the best language in the world to learn fast"   # string object method
>>> str.count('i')
2
>>> str.find('i')
7
>>> str.find('0')
-1
>>> str.index('0')                                  # error happens when you search for something out of the original string. taht is how different between find() and index()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found
>>> str.index('i')
7
>>> str1 = "."
>>> str1.join("ASAP")
'A.S.A.P'
>>> str.upper()                                               # upper case and lower case
'PYTHON IS THE BEST LANGUAGE IN THE WORLD TO LEARN FAST'
>>> str.lower()
'python is the best language in the world to learn fast'
>>> str2 = " test "
>>> str2.lstrip                                             # strip function, how to eliminate the blank of the string
<built-in method lstrip of str object at 0x141bf00>
>>> str2.lstrip()
'test '
>>> str2.rstrip()
' test'
>>> str2.strip()
'test'
>>> str2.replace("test", "python")                      # How to replace the old one with the new one
' python '
>>> str.split()                                         # how to split string into list
['python', 'is', 'the', 'best', 'language', 'in', 'the', 'world', 'to', 'learn', 'fast']
>>> str3 = "A.S.A.P"
>>> str3.split(".")
['A', 'S', 'A', 'P']

>>> "After I ate {0} apples. I was sick for {days} days".format(10,days=7)        # in here, further advance of formatting with format function 
'After I ate 10 apples. I was sick for 7 days'
>>> "{0:>10}".format("hi")
'        hi'
>>> "{0:<10}".format("hi")
'hi        '
>>> "{0:^10}".format("hi")
'    hi    '
>>> "{0:=^10}".format("hi")
'====hi===='
>>> "{0:=>10}".format("hi")
'========hi'
>>> "{0:=<10}".format("hi")
'hi========'
>>> y=3.1245497
>>> "{0:0.4f}".format(y)
'3.1245'
>>> "{0:10.4f}".format(y)
'    3.1245'
>>> "{{ and }}".format()
'{ and }'
```

### Boolean : python has also boolean type .

| value  | true and false |
|========|================|
|"string"| True           |
|""      | False          |
|[1,2,3] | True           |
|[]      | False          |
|(1,2)   | True           |
|()      | False          |
|{"2":2} | True           |
|{}      | False          |
|1       | True           |
|0       | False          |
|None    | False          |

## Containners

**The type below is resizable. this feature is very adorable, If you use C language once, you will know what I mean.**

**the below is handled in python 3.6**

Especially, The difference between python 2.7 and 3.* is print whithin me making this tutorial. 

```python
python 2.7 - print "stirng"
python 3.6 - print ("String")
```

one more thing, it's type function 

if you enter print (type(a-data type)), 

the result is **class 'data type'** like this

```python 
>>> print (type(a))
<class 'list'>
>>> print (type(3))
<class 'int'>
```

### List  

**The features of List** : I think you shoud think of the list as the list you learned in Data structure class. this data type is that you can change factor in the list, it is ordered. The very important thing is dynamically resized and type.

```python
>>> "let's do python tutorial"
"let's do python tutorial"
>>> a = []
>>> b = [1,2,3]
>>> c = ['Life', 'is', 'too', 'fun']
>>> d = [1, 2, 'Life', 'fun', 'is']
>>> e = [1, 2, ['Life', 'is']]
>>> e = [[1, 2], ['Life', 'is']]
>>> e = [1, 2, ['Life', 'is']]
>>> f = [[1, 2], ['Life', 'is']]               # idexing of list
>>> e[0]
1
>>> e[1]
2
>>> e[2]
['Life', 'is']
>>> e[2][1]
'is'
>>> f[0][1]
2
>>> f[1]
['Life', 'is']
>>> f[-1][1]
'is'
>>> b + c
[1, 2, 3, 'Life', 'is', 'too', 'fun']
>>> a + b + c + d + e + f
[1, 2, 3, 'Life', 'is', 'too', 'fun', 1, 2, 'Life', 'fun', 'is', 1, 2, ['Life', 'is'], [1, 2], ['Life', 'is']]
>>> a = [1, 2, ['a', 'b', ['Life', 'is']]]
>>> a[2][2][0]
'Life'
>>> a = [1,2,3,4,5]      # the span to slice list - is the same from string. 
>>> b = "12345"
>>> a[:3]
[1, 2, 3]
>>> b[:3]
'123'
>>> a = [1, 2, ['a', 'b', ['Life', 'is']]]
>>> a[2][:2]
['a', 'b']
```

**Operator and  Function of List**

```python
>>> a = [1, 2, 3]
>>> b = [4, 5, 6]
>>> a + b
[1, 2, 3, 4, 5, 6]
>>> a * 3
[1, 2, 3, 1, 2, 3, 1, 2, 3]
>>> a ** 3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for ** or pow(): 'list' and 'int'
>>> a + "hi"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate list (not "str") to list
>>> a  =  [1, 2, 3]
>>> a[2] = 4
>>> a
[1, 2, 4]
>>> a[1:2]
[2]
>>> a[1:2] = ['a', 'b', 'c']
>>> a
[1, 'a', 'b', 'c', 4]
>>> b = [1, 2, 3]
>>> b[2] = ['a', 'b', 'c']
>>> b
[1, 2, ['a', 'b', 'c']]
>>> a[1:3] = []        ## how to erase list with none object !
>>> a
[1, 'c', 4]
>>> del a[1]           ## python del function, this fucntio usage is 'del object'!!
>>> a
[1, 4]
>>> del a[0:]
>>> a
[]
>>> a = [1, 4, 2]
>>> a.sort()
>>> a
[1, 2, 4]
>>> a.append(2)         ## just literally, append a factor in last location. BUT, insert is you can make where you want to place factor in the list
>>> a
[1, 2, 4, 2]
>>> a = ['c', 'a', 'e']
>>> a.sort()            ## sorting fucntion alphabetically, numerically like increment way BUT, 
>>> a = [1, 4, 2, 'a', 'o', 'e']
>>> a.sort()            ## keep in mind, you need to compare the same type.
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<' not supported between instances of 'str' and 'int'
>>> a
['a', 'c', 'e']
>>> a.reverse()         ## In case you want to reverse the list 
>>> a
['e', 'c', 'a']
>>> a.index('c')         ## When you want to look up the index number of factor that you'r looking for  
1
>>> a.index(0)           ## when you search for no factor in list  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 0 is not in list
>>> a.insert(1, 3)        ## When you want to insert the particular factor into list, BUT, you will have to declare loction to inser. 
>>> a
['e', 3, 'c', 'a']
>>> a.remove(3)           ## if you want to remove the particular factor in list
>>> a
['e', 'c', 'a']
>>> a.remove(3)           ## if you remove fator is no there
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: list.remove(x): x not in list
>>> a = [1, 2, 3]
>>> a.pop()               ## To pop the last factor of list like Stack function of pop ()
3
>>> a
[1, 2]
>>> a.extend([4,5,6,7])   ## To extend a list with [4, 5, 6, 7] it's like **a += [4, 5, 6, 7]** and **a = a + [4, 5, 6, 7] **
>>> a
[1, 2, 4, 5, 6, 7]
>>> a.pop(2)              ## To pop the particular location's factor of list like Stack function of pop ()
4
>>> a
[1, 2, 5, 6, 7]
>>> a.append(2)
>>> a
[1, 2, 5, 6, 7, 2]        ## how many factors of the particular factor like '2' is in list ? 
>>> a.count(2)
2
```

### Tuple

**The feature of Tuple** : this is not greatly different from list's features. however, you can plus the new factor, you cannot change and remove the factor's value in Tuple  

```python
>>> t1 = ()
>>> t2 = (1,)                ## you need char '(' and ')' when you make Tuple. 
>>> t2
(1,)
>>> print (type(t2))
<class 'tuple'>
>>> t2 = (1)
>>> t2
1
>>> print (type(t2))         
<class 'int'>
>>> t2 = (1,)               ## i.e, If you tuple with one factor, you have to use '(' and ')'
>>> t2 = (1, 2, 3)
>>> t3 = 1, 2, 3
>>> t4 = ('a', 'b', ('ab', 'cd'))
>>> t5 = (1, (2,3), ('a', 'b'), 'c')
>>> t5
(1, (2, 3), ('a', 'b'), 'c')
>>> t5 = (1, (2,3), ('a', 'b'), 'c',1)
>>> t5
(1, (2, 3), ('a', 'b'), 'c', 1)
>>> t2
(1, 2, 3)
>>> t2[1]
2
>>> del t2[1]                ## when you remove factor from  tuple, error happens
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object doesn't support item deletion
>>> t2[1]  = 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> t2[1:2]  = 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>>
```

**Opaerator and Function of Tuple** 

you know I can't reomve and change any value in tuple. So Opearation and function that we'll see below is simple.

So, Apart from these, **I think you need to use tuple when you need static constant data.**

to sum up, this type is immutable. 

```python
>>> t1 = (1, 2, 'a', 'b')
>>> t1[0]
1
>>> t1[0:]
(1, 2, 'a', 'b')
>>> t1[0:3]
(1, 2, 'a')
>>> t2 = (3, 4)
>>> t1 + t2
(1, 2, 'a', 'b', 3, 4)
>>> t2 * 3
(3, 4, 3, 4, 3, 4)
>>> t1 * 2
(1, 2, 'a', 'b', 1, 2, 'a', 'b')
```

### Dictionary

** The feature of Dictionary **: this type is similar to map data type on other programming lauguages, more Basically, this is associative array with hash.

Basic form : {key1:value1, key2:value2 ...}

normally, you need to use a immutable varialbe as key, and value doesn't matter whatever you use.

key is not necessarily immutable. you can use key with integer. 

```python
>>> dic = {'name': 'hyunyoung2', 'phone':'00011112222', 'birth':'1111' }   ## how to make dictionary
>>> dic
{'name': 'hyunyoung2', 'phone': '00011112222', 'birth': '1111'}
>>> print (type(dic))
<class 'dict'>
>>> a = {1: 'hello world'}
>>> a[1]
'hello world'
>>> a = {'a': [1,2,3]}
>>> a['a']
[1, 2, 3]
```

**Operator and Function of dicationary**

```python
>>> a = {1: 'a'}            ## from now on, How to insert factor into Dictionary
>>> a[2] = 'b'
>>> a
{1: 'a', 2: 'b'}
>>> a = {1: 'a'}
>>> a
{1: 'a'}
>>> a[2] = 'b'
>>> a
{1: 'a', 2: 'b'}
>>> a['name'] = 3
>>> a[(1,2)] = [1,2,3]
>>> a[[1,2]] = [1,2,3]      ## you can use tuple, integer, string as look-up, but cannot use set, list Because unhashed type. 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> a[[1,2]] = 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> a[{1,2}] = 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'set'
>>> del a[1]
>>> a
{2: 'b', 'name': 3, (1, 2): [1, 2, 3]}
>>> del a['name']
>>> a
{2: 'b', (1, 2): [1, 2, 3]}
```

**Operator and Fucntion of Dictionary**


```python 
>>> a = {"name": "hyunyoung2", "Object":"To Study python", "Chapter":"Dictionary"}
>>> a
{'name': 'hyunyoung2', 'Object': 'To Study python', 'Chapter': 'Dictionary'}
>>> a.keys()                                    ## only to extract key value
dict_keys(['name', 'Object', 'Chapter'])
>>> for i in a.keys() :
...     print  (i)
...
name
Object
Chapter
>>> for i in a.values() :                       ## onle to extract value
...     print (i)
...
hyunyoung2
To Study python
Dictionary
>>> list(a.keys())
['name', 'Object', 'Chapter']
>>> list(a.values())
['hyunyoung2', 'To Study python', 'Dictionary']
>>> a.items()                                  ## a pair of key and value, it's similar to enumerate fucntion of list 
dict_items([('name', 'hyunyoung2'), ('Object', 'To Study python'), ('Chapter', 'Dictionary')])
>>> list(a.items())             
[('name', 'hyunyoung2'), ('Object', 'To Study python'), ('Chapter', 'Dictionary')]
>>> a.clear()
>>> a
{}
>>> a = {"name": "hyunyoung2", "Object":"To Study python", "Chapter":"Dictionary"}
>>> a.get('name')                               ## not indexing, just get function is used. 
'hyunyoung2'
>>> a.get('Object')
'To Study python'
>>> a.get('test')
>>> a.get('test', 'by default')
'by default'
>>> 'name' in a                                 ## "in" operator, a has 'name' in a Dictionary, this returns True(boolean value)
True
>>> 'test' in a                                 ## the opposite of the above situation
False
```

### Set

**Set is literally used to represent set.**

First of all, all you need to know is set has some features unlike the other data type. 

 1. there is no duplication of the same. 
 
 2. it's unordered. 
 
 let's check it! (be careful, now I'm typing with python 3.6 in here)
 
```python
>>> a = set([1,2,3])          ## you can see how to intialize set, from now on. 
>>> a
{1, 2, 3}
>>> print (type(a))
<class 'set'>
>>> b = set("hellow")         ## over here, You can verify the features of the set of python's data type.  
>>> b                         ## First, There is no duplication,  one of two "l" letters disappear. 
{'w', 'l', 'o', 'e', 'h'}     ## Second, it's unodered.
>>> print (type(b))
<class 'set'>
>>> c = {1,2,3,4, "hello"}    ## if you initialize a set this way, then "hello" is dealt with like one data. 
>>> c
{1, 2, 3, 4, 'hello'}
>>> print (type(c))
<class 'set'>
>>> a[1]                      ## As you can see, you cannot index in the set. 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
```

As you can see above. when I make a set initialized with "hello" of string. one out of two "l" letters disappear in the set. 

and then the order of "hellow" is unordered. 

**So with the feature above, Sometimes you can use the set as filter. But you have something careful.**

**That is you cannot index any component in the set. So if you want to index some component in the set**

Let's check it 


```python
>>> a = set([1,2,3])
>>> a
{1, 2, 3}
>>> print (type(a))
<class 'set'>
>>> a[1]                               ## As you can see in here, you cannot index anyone in the set. 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
>>> a[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
>>> l1 = list(a)                       ## another way to use list
>>> l1
[1, 2, 3]
>>> print (type(l1))
<class 'list'>
>>> l1[0]
1
>>> l1[2]
3
>>> t1 = tuple(a)                      ## the other way to use tuple
>>> t1
(1, 2, 3)
>>> print (type(t1))
<class 'tuple'>
>>> t1[1]
2
>>> t1[2]
3
```

After you change set into list and tuple. you can index, the reason why list and tuple are ordered. 

**Operator and Fucntion of Set**

In here, you can use this data type usefully, when you need intersection , sume, difference of sets. 

Let's see some example.

```python 
>>> s1 = set ([1,2,3,4,5,6])
>>> s1
{1, 2, 3, 4, 5, 6}
>>> s2 = set ([4,5,6,7,8,9])
>>> s2
{4, 5, 6, 7, 8, 9}
>>> s1 & s2                     ## intersection of sets. 
{4, 5, 6}
>>> s1.intersection(s2)
{4, 5, 6}
>>> s1 | s2                     ## sum of sets. 
{1, 2, 3, 4, 5, 6, 7, 8, 9}
>>> s1.union(s2)
{1, 2, 3, 4, 5, 6, 7, 8, 9}
>>> s1 - s2                     ## Difference of sets. 
{1, 2, 3}
>>> s2 - s1
{8, 9, 7}
>>> s1.difference(s2)
{1, 2, 3}
>>> s2.difference(s1)
{8, 9, 7}
```

Another Operation and Funtion of Set

```python 
>>> s1 = set([1,2,3])
>>> s1
{1, 2, 3}
>>> print (type(s1))
<class 'set'>
>>> s1.add(4)                               ## just to add one factor
>>> s1
{1, 2, 3, 4}
>>> s1.add([5,6,7])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> s1.update([4,5,6])                      ## just to add a bunch of factors
>>> s1
{1, 2, 3, 4, 5, 6}
>>> s1.remove(2)
>>> s1
{1, 3, 4, 5, 6}
```

## Statement

In here, You see the statements of Python. But I'm going to deal with the total statement in detail. 

Just I'm going to deal with representative statement that you normally use when you make programming.  

**be carefule, when you use python, indentation is very important, the role of this indent is bracket({}) of another language, in particular c Languagae.**

i.e python recognize the local area of the python's area. 

(be careful, now I'm typing with python 3.6 in here)

### If
 
 this is the exact same from another language's statement in terms of functionality.
 
 Let's see you simple code. 
  
```python 
>>> pocket = ['paper', 'cell phone', 'money']
>>> card  = 1
>>> if '100 dollar' in pocket :                       ## If statement of python cosists of if ~ elif ~ else. 
...     print ("I'm rich")                            ## you need to be careful, don't forget ":(colone)", 
... elif card :
...     print ("I have a money a little bit")
... else :
...     print ("I have others, paper and cell phone")
...
I have a money a little bit                           ## what is the pass ? this just literally means the meaning of pass 
>>> if '100 dollar' in pocket :                       ## this is useful in If or class 
...     print ("I'm rich")
... elif card:
...     pass
... else :
...     print ("I have others, paper and cell phone")
...
>>> if '100 dollar' in pocket : pass                  ## in here, this show you how to represent statement in a line 
... else : print ("I have a others, paper and cell phone")    ## when if has one statement 
...
I have a others, paper and cell phone
 ```
 
### While

This while statement is also the exact same from another language's while in terms of functionality. 

Let's see simple code of  while statement. 

```python 
>>> coffee = 0                                        ##  you can see the basic operation of while statement of python
>>> while coffee < 10 :
...     coffee += 1
...     print ("today you have drunk %d cups of coffee" % coffee)
...     if coffee == 10 :
...             print ("we don't have coffee at all")
...
today you have drunk 1 cups of coffee
today you have drunk 2 cups of coffee
today you have drunk 3 cups of coffee
today you have drunk 4 cups of coffee
today you have drunk 5 cups of coffee
today you have drunk 6 cups of coffee
today you have drunk 7 cups of coffee
today you have drunk 8 cups of coffee
today you have drunk 9 cups of coffee
today you have drunk 10 cups of coffee
we don't have coffee at all

>>> coffee = 0                                        ## one is differenct from the above, just In here, I used "break" keyword
>>> while coffee < 10 :
...     coffee = coffee + 1
...     print ("Today, you have drunk % cups of coffee" % coffee)
...     if coffee == 2 :
...             print ("Sorry, we made a mistake of counting coffee!")
...             print ("So you cannot sell it")
...             break
...     if coffee == 10 :
...             print ("our coffee sold out")
...
Today, you have drunk 1 cups of coffee
Today, you have drunk 2 cups of coffee
Sorry, we made a mistake of counting coffee!
So you cannot sell it

>>> coffee = 0                                        ## this's also different, just one, in here I used "continue" keyword
>>> while coffee < 10 :
...     coffee = coffee + 1
...     print ("Today, you have drunk %d cups of coffee" % coffee)
...     if coffee == 2 :
...             continue
...             print ("Sorry, you made a mistake of counting coffee")
...             print ("So, you cannot sell it")
...     if coffee == 10 :
...             print ("our coffee sold out")
...
Today, you have drunk 1 cups of coffee
Today, you have drunk 2 cups of coffee
Today, you have drunk 3 cups of coffee
Today, you have drunk 4 cups of coffee
Today, you have drunk 5 cups of coffee
Today, you have drunk 6 cups of coffee
Today, you have drunk 7 cups of coffee
Today, you have drunk 8 cups of coffee
Today, you have drunk 9 cups of coffee
Today, you have drunk 10 cups of coffee
our coffee sold out
```

If you do programming once, you can understand the above situation.  

### for

this's also the exact same from another language's for statement in terms of functionality. 

needless to say, Let's see example code. 

```python 
>>> score = [90, 25, 67, 45, 80]                         ## The basic for statement
>>> number = 0
>>> for test in score :
...     number += 1
...     if test > 60 :
...             print ("%d-th student pass, becuase the score is %d" % (number, test))
...     else :
...             print ("%d-th student fail, becuase the score is %d" % (number, test))
...
2-th student pass, becuase the score is 90
3-th student fail, becuase the score is 25
4-th student pass, becuase the score is 67
5-th student fail, becuase the score is 45
6-th student pass, becuase the score is 80

>>> score = [90, 25, 67, 45, 80]                         ## for statement with continue keyword
>>> number = 0
>>> for test in score :
...     number += 1
...     if test < 60 : continue
...     print ("%d-th student pass, because the score is %d" % (number , test))
...
1-th student pass, because the score is 90
3-th student pass, because the score is 67
5-th student pass, because the score is 80

>>> score = [90, 25, 67, 45, 80]                         ## for statement with pass keyword
>>> number = 0
>>> for test in score :
...     number += 1
...     if test < 60 : pass                              ## without else keyword
...     print ("%d-th student pass, because the score is %d" % (number, test))
...
1-th student pass, because the score is 90
2-th student pass, because the score is 25
3-th student pass, because the score is 67
4-th student pass, because the score is 45
5-th student pass, because the score is 80

>>> score = [90, 25, 67, 45, 80]
>>> number  = 0
>>> for test in score :
...     number += 1
...     if test < 60 : pass                              ## including else keyword
...     else : print("%d-th student pass, because the score is %d" % (number, test))
...
1-th student pass, because the score is 90
3-th student pass, because the score is 67
5-th student pass, because the score is 80

>>> score = [90, 25, 67, 45, 80]                         ## for statement with break keyword
>>> number = 0
>>> for test in score :
...     number += 1
...     if test < 60 : break
...     print ("%d-th student pass, because the score is %d" % (number, test))
...
1-th student pass, because the score is 90


>>> sum = 0
>>> for i in range(0, 10) :                             ## what kind of role is range function
...     sum += i
...     print ("sum : %d" % sum)
...
sum : 0
sum : 1
sum : 3
sum : 6
sum : 10
sum : 15
sum : 21
sum : 28
sum : 36
sum : 45

>>> sum = 0
>>> range(10)
range(0, 10)
>>> for i in range(10) :
...     sum += i
...     print ("sum: %d" % sum)
...
sum: 0
sum: 1
sum: 3
sum: 6
sum: 10
sum: 15
sum: 21
sum: 28
sum: 36
sum: 45

>>> for i in range(2, 10) :                             ## with two for statements
...     for j in range (1, 10) :
...             print ("%d*%d : %d " % ( i, j , i*j), end = " " )
...     print ("")
...
2*1 : 2  2*2 : 4  2*3 : 6  2*4 : 8  2*5 : 10  2*6 : 12  2*7 : 14  2*8 : 16  2*9 : 18
3*1 : 3  3*2 : 6  3*3 : 9  3*4 : 12  3*5 : 15  3*6 : 18  3*7 : 21  3*8 : 24  3*9 : 27
4*1 : 4  4*2 : 8  4*3 : 12  4*4 : 16  4*5 : 20  4*6 : 24  4*7 : 28  4*8 : 32  4*9 : 36
5*1 : 5  5*2 : 10  5*3 : 15  5*4 : 20  5*5 : 25  5*6 : 30  5*7 : 35  5*8 : 40  5*9 : 45
6*1 : 6  6*2 : 12  6*3 : 18  6*4 : 24  6*5 : 30  6*6 : 36  6*7 : 42  6*8 : 48  6*9 : 54
7*1 : 7  7*2 : 14  7*3 : 21  7*4 : 28  7*5 : 35  7*6 : 42  7*7 : 49  7*8 : 56  7*9 : 63
8*1 : 8  8*2 : 16  8*3 : 24  8*4 : 32  8*5 : 40  8*6 : 48  8*7 : 56  8*8 : 64  8*9 : 72
9*1 : 9  9*2 : 18  9*3 : 27  9*4 : 36  9*5 : 45  9*6 : 54  9*7 : 63  9*8 : 72  9*9 : 81
```

the following is useful when you type code with python 

that is called **List comprehension of python.**


**without if statement in List Comprehension**

**[**statement **for** item **in** iterable object**]**


**[**statemetn which include above two variable. **for** item1 **in** iterable object1 
                                             **for** item2 **in** iterable object2
                                             .....                                                  
                                             **for** itemN **in** interable ojectN]

If you want to contain if statement in List Comprehension

**[**statement **for** item **in** iterable object **if** condition**]**

**[**statemetn which include above two variable. **for** item1 **in** iterable object1 **if** condition1
                                             **for** item2 **in** iterable object2 **if** condition2
                                             .....                                                  
                                             **for** itemN **in** interable ojectN **if** conditionN**]**

Let's see example of List Comprhension

```python 
>>> a = [1,2,3,4]                           ## everyone of a List time 3 using for statement 
>>> result = []                             ## to insert the itme into result variable of list
>>> for num in a :
...     result.append(num*3)
...
>>> result
[3, 6, 9, 12]
>>> result = [num * 3 for num in a]         ## BUT, if you use List comprehension, 
>>> result                                  ## your task is so easy to make new list with some other List
[3, 6, 9, 12]
>>> result = [num * 3 for num in a if num % 2 == 0]     ## with List Comprehension and if statement in List comprehension
>>> result
[6, 12]

>>> result = [x*y for x in range(2,10)
...               for y in range(1,10)]
>>> result                                        ## in order to show you easily how to use two variable in List comprehension
[2, 4, 6, 8, 10, 12, 14, 16, 18, 
3, 6, 9, 12, 15, 18, 21, 24, 27, 
4, 8, 12, 16, 20, 24, 28, 32, 36, 
5, 10, 15, 20, 25, 30, 35, 40, 45, 
6, 12, 18, 24, 30, 36, 42, 48, 54, 
7, 14, 21, 28, 35, 42, 49, 56, 63, 
8, 16, 24, 32, 40, 48, 56, 64, 72, 
9, 18, 27, 36, 45, 54, 63, 72, 81]
```

## Function

(be careful, now I'm typing with python 3.6 in here)

**Function : this is exactly the same from meaning of function in otherprogramming language. However, the keyword of function in python is def keyword.**

Let me know how to use function in python with some example. 

before making code of function, function has argument and return value.

depending on the two value, the total type of function is some 4. 


```python 
>>> def sum(a,b) :                 ## with arguments and return value
...     return a+b
...
>>> sum(1,3)
4

>>> def say():                     ## with no arguments and return value
...     return  "Hi"
...
>>> say()
'Hi'

>>> def sum(a, b):                 ## with arguments and no return value
...     print ("%d + %d = %d" % (a, b, a+b))
...
>>> sum( 3, 7)
3 + 7 = 10

>>> def say() :                    ## with no arguments and no return value
...     print ("hello!")
...
>>> say()
hello!

>>> def sum(*args) :              ## In order to get arguments randomly. 
...     sum = 0                   ## * is used to do that   
...     for i in args :
...             sum = sum + i
...     return sum
...
>>> sum(1,2,3,4,5)
15
>>> sum(1,2,3,4,5,6,7)
28
>>> sum(1,2,3,4,5,6,7,8,9)
45
>>> a, b = sum_and_mul(3, 7)
>>> a
10
>>> b
21
>>> type(a)
<class 'int'>
>>> type(b)
<class 'int'>

>>> def say_nickname(nick) :       ## you don't have to use return keyword with value that you'r goind to return. 
...     if nick == "stupid" :
...             return
...     print ("my nickname is %s " % nick)
...
>>> say_nickname("stupid")
>>> say_nickname("stupid!")
my nickname is stupid!

>>> def let_me_introduce_myself(name, old, gender = True) :           ## with arguments initialized. 
...     print ("my name is %s" % name)
...     print ("my age is %s" % old)
...     if gender == True :
...             print ("my gender is male")
...     else :
...             print ("my gender is female")
...
>>> let_me_introduce_myself("hyunyoung2", "20")
my name is hyunyoung2
my age is 20
my gender is male
>>> let_me_introduce_myself("hyunyoung2", "20", False)
my name is hyunyoung2
my age is 20
my gender is female

>>> def let_me_introduce_myself(name, gender = True, old) :
...     print ("my name is %s" % name)
...     print ("my age is %s" % old)
...     if gender == True :
...             print ("my gender is male")
...     else :
...             print ("my gender is female")
...
  File "<stdin>", line 1
SyntaxError: non-default argument follows default argument


>>> def sum(a, b):            ## only in the case of python as you can see, 
...     return a+b, a-b       ## python returns a couple of variables, the type of retun values is tuple. 
...
>>> return_value = sum(5, 5)
>>> return_value
(10, 0)
>>> type(return_value)
<class 'tuple'>
```

## class

(be careful, now I'm typing with python 3.6 in here)

**class : this is frame to make object that is the same from class. and Class has member function and member variable of class**

So, you need to understand inheritance, overloading and overriding and so on. for example, polymorphism. 

If you feel difficult from the above things. for now, You don't have to try to understand the above concepts. 

Later on, you would understand those concepts. if you have experience about programming, in particular 

if you have experience of C or C++ Languages, You must know about the concept.


**according to Jump to python, they represent overloading and constructor, So in here, I will explain to you about both of them a little**

Let's see example of code. 

class name[(the name of inheritance of class)] : 
    <class variable1>
    <class variable1>
    ...
    def class_function1(self,[, argument1, argument2,,,]):
        <statement1 that this function have to deal with>
        <statement2 that this function have to deal with>
        ...
    def class_function2(self,[, argument1, argument2,,,]):
        <statement1 that this function have to deal with>
        <statement2 that this function have to deal with>
        ...
        
***Let's see example of the class code!*        

```python
>>> class HouseLee :                      ## parent class
...     lastname = "Lee"
...     def __init__(self, name):         ## constructor
...             self.fullname = self.lastname + name
...     def travel(self, where) :
...             print ("%s goes to %s" % (self.fullname, where))
...     def love(self, other) :
...             print ("%s falls in love with %s" % (self.fullname, other.fullname))
...     def fight(self, other) :
...             print ("%s fought %s" % (self.fullname, other.fullname))
...     def __add__(self, other) :        ## class overloading
...             print ("%s was married with %s" % (self.fullname, other.fullname))
...     def __sub__(self, other) :        ## class overloading
...             print ("%s was divorced from %s" % (self.fullname, other.fullname))
...
>>> class HouseNa (HouseLee) :            ## Inheritance of class
...     lastname = "Na"
...     def travel(self, where, day) :    ## overriding function of class 
...             print ("%s, to %s for %d days" % (self.fullname, where, day))
...

>>> romio = HouseLee(" HY")               ## create class 1
>>> juliet = HouseNa(" YJ")               ## create class 2
>>> romio.travel("Busan")                 ## function call of class 1
Lee HY goes to Busan
>>> juliet.travel("Busan", 3)             ## function call of class 2 overriding
Na YJ, to Busan for 3 days
>>> juliet.travel("Busan")
Traceback (most recent call last):        ## error in the number of arguments of function of class 2
  File "<stdin>", line 1, in <module>
TypeError: travel() missing 1 required positional argument: 'day'
>>> romio.love(juliet)
Lee HY falls in love with Na YJ
>>> romio + juliet                        ## overloading of + operator
Lee HY was married with Na YJ
>>> romio.fight(juliet)
Lee HY fought Na YJ     
>>> romio - juliet                        ## overloading of - operator
Lee HY was divorced from Na YJ
```


## Module

(be careful, now I'm typing with python 3.6 in here)

In python, module is just file cotaining code, function, variable, class and so on. 

```python
# mod1.py
def sum(a, b) :
    return a+b
```

The above code is just another file that is made of python code. 

when you want to import this module. 

you have to enter module name this way 

**form MODULE import FUNCTION (as nickname)**

OR

**import MODULE (as nickname)**

```python 
>>> import mod1
>>> mod1.sum(1,2)
3
>>> from mod1 import sum
>>> sum(1,2)
3
>>> import mod1 as test
>>> test.sum(1,2)
3
>>> from mod1 import sum as t
>>> t(1,2)
3
```

## Package

**When you make complecated modules, I need you to make hierarchy of a couple of module files.** 

below is an example of package 

```python
game/
    __init__.py
    sound/
        __init__.py
        echo.py
        wav.py
    graphic/
        __init__.py
        screen.py
        render.py
    play/
        __init__.py
        run.py
        test.py
```

If you have the virtaul package. how do I call the function of module in the above package. 

You have to be careful of (.)dot letter. 

only if you use package, you can use this mark(.).  

```python
import game.sound.echo
game.sound.echo.echo_test()  ## function call 


from game.sound import echo
echo.echo_test()             ## function call from moudle 

from game.sound.echo import echo_test
echo_test()                  ## function call directly as function name
```

## Exception

(be careful, now I'm typing with python 3.6 in here)

Exception is similar with another programming lanuage exception 

let's look at an example of exception handling 

```python 
try : 
  f = open ("file.txt", "r")
except FileNotFoundError as e :
  print (str(e))
else :
  data = f.read()
  f.close()
finally :
  print ("this is executed if error happens or not")
```

## Inner Function & Outer Function

(be careful, now I'm typing with python 3.6 in here)

there are built-in and built-out functions. 

BUT I will introduce a couple of functions a bit. 

**lambda : keyword the I used when you create function**

lambda variable1, variable2, ... :  expression with those variables(variable1, variable2, ...)

```python 
>>> sum = lambda a, b : a+b
>>> sum(3,4)
7

>>> myList = [lambda a, b : a+b, lambda a,b :a*b]
>>> myList
[<function <lambda> at 0x032F6660>, <function <lambda> at 0x032F6618>]
>>> myList[0]
<function <lambda> at 0x032F6660>
>>> myList[0](3,4)
7
>>> myList[1](3,4)
12
```

**map : map returns value that adapted each of iterable data into that f(function)**

**map(f, iterable) : this means, f is function, iterable is data type that can be iterable.**

let's see a code of map

```python
>>> def two_times(numberList):                   ## before using map function 
...     result = []
...     for number in numberList :
...             result.append(number*2)
...     return result
...
>>> return_value = two_times([1,2,3,4,5])
>>> type(return_value)
<class 'list'>
>>> return_value
[2, 4, 6, 8, 10]

>>> def twoTimes(x): return x*2                  ## function definition to start off with map function 
...
>>> map(twoTimes, [1,2,3,4,5])                   ##  What is the map ? just object 
<map object at 0x032F4BD0>
>>> list(map(twoTimes, [1,2,3,4,5]))             ## to make  return value of map list
[2, 4, 6, 8, 10]
>>> list(map(lambda a: a*2, [1,2,3,4]))          ## if you use lambda instead of map function. 
[2, 4, 6, 8]
```

**If you are avaiable for study of python, I recommend you to look for reduce function of python**

I think map function is associated with map-reduce file system a little

in distribution system, How to use multi-core. then I think map function and reduce function is useful


# Reference 

  1. [Jump to the Python - Open book](https://wikidocs.net/book/1)
  
  2. [learning Python from example](http://pythonstudy.xyz/)
   
       - This site is actually I'm not refer to it When I wrote this article, tutorial of Jump to python. just later on, I think this will be useful site. So in order to remember this site. 
       
       - I wrote here as Reference. 
       
  - Also, the two sites above is in Korean, So If you want to know python, I won't recommend this site.
  
  - Strongly to you, I recommend this site, [tutorial of Python in Officail python site](https://docs.python.org/3/tutorial/),
  
  - In spite of Korean languages. If you want to read the site, Jump to Python. Just recommend you use the google translator.
