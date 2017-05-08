---
layout: post
title: Tutorial of python with Standford 
subtitle: I will let you know the basics of python syntax with python tutorial of some stanford lecture.
category: Python
tags: [language, python]
permalink: /2017/04/01/Tutorial_Of_Python_In_Stanford/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---


# Tutorial of Python in Stanford university 

This is just arragement and rewritten for my python study, So If I have a problem in document, let me know about it

and then I will erase this later on. 

in order for me to be used to python, Just type the tutorial of stanford. 

So if you want to know more detail of python. just let you know you need to read [this paper(my tutorial with jump to python)](https://hyunyoung2.github.io/2017/03/30/Jump_to_python_tutorial/) that I wrote. 

In here, Just I will only arrange the tutorial of python, not numpy. 

I mean this is just the basic syntax of Python 

# Python
  
- Basic data types

- Containers 
  - Lists
  - Dictioinaries
  - Sets       
  - Tuple
      
- Functions
  
- Classes
  
  
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML">
\begin{bmatrix}
aaa & b\cr
c   & ddd
\end{bmatrix}
</script>
  
Python is a high-level, dynamically typed multiprogramming lauguage. Python code is readable and it's easy to express your ideas with few lines of code

As an example, here is an implementation of the classic quicksort algorithm in python:

This tutorial is implemented on python 3.6 of Windows 10 

```python
>>> def quicksort(arr) :
...     if len(arr)  <= 1 :
...             return arr
...     pivot = arr[len(arr) // 2]
...     left = [x for x in arr if x < pivot]
...     middle = [x for x in arr if x == pivot]
...     right = [x for x in arr if x > pivot]
...     return quicksort(left) + middle + quicksort(right)
...
>>> print (quicksort([3,6,8,10,1,2,1]))
[1, 1, 2, 3, 6, 8, 10]
```
  
## Basic data types

Python is similar to most languages. I mean Pythons has a number of basic types including integers, floats, booleans, and strings. These data types act in ways that are familiar from other lanuages. 


### Nubmers

Integers and floats work as you would expect form other languages :

```python
>>> x = 3
>>> print (type(x))     ## Prints "<class 'int'>"
>>> print (x)
3
>>> print (x + 1)
4
>>> print (x - 1)
2
>>> print (x * 2)
6
>>> print (x ** 2)
9
>>> x += 1
>>> print (x)
4
>>> x *= 2
>>> print (x)
8
>>> y = 2.5
>>> print (type(y))      ## Prints "<class 'float'>"
>>> print (y, y + 1, y * 2, y ** 2)
2.5 3.5 5.0 6.25
>>> complex(2,4)        ## complex number
(2+4j)
```

notice that unlike other languages, Python does not have unary increment(**x++**) or decrement(**x\-\-**) operators.

Python also has built-in types for long integers and complexx numbers; you can find all of the detail in [the documentation of python](https://docs.python.org/3.6/library/stdtypes.html#numeric-types-int-float-long-complex)


### Booleans

it is similar for python to implement for Boolean logic like other languages, BUT English words rather than sympbol(**&&, \|\|, etx**) :

```python
>>> t = True
>>> f = False
>>> print (type(t))     ## Prints "<class 'bool'>"
>>> print (type(f))     ## Prints "<class 'bool'>"
>>> print (t and f)     ## logical AND, &&
False
>>> print (t or f)      ## logical OR, ||
True
>>> print (not f)       ## logical NOT, ~
True
>>> print (not t)
False
>>> print (~t)          ## logical NOT, ~
-2
>>> print (~f)
-1
>>> print (t != f)      ## Logical XOR, ^ 
True
>>> print (t ^ f)
True
>>> print (True != True)
False
>>> print (False != False)
False
>>> print (True ^ True)
False
>>> print (False ^ False)
False
```

### Strings 

Python support the great strings :

```Python 
>>> hello = 'hello'           ## String literals can use single quotes
>>> world = "world"           ## or Double quotes; it doesn't matter
>>> print (hello)
hello
>>> print (world)
world
>>> print (len(hello))
5
>>> print (hw)
hello world
>>> hw12 = '%s %s %d' % (hello, world, 12)      ## how to use format of print function 
>>> print (hw12)
hello world 12
```

**String objects have a number of useful methods**

```python
>>> s = "hello"
>>> print (s.capitalize())    ## covert the first letter capitalized
Hello
>>> print (s.upper())         ## convert the letters into upper case 
HELLO
>>> print (s.lower())         ## convert the letters into lower case 
hello
>>> print (s.rjust(7))        ## Right-justify a string, padding with spaces: Prints "  hello"
  hello
>>> print (s.ljust(7))        ## Left-justify a string, padding with spaces: Prints "hello  "
hello
>>> print (s.center(7))       ## Center a string, padding with spaces: Prints " hello "
 hello
>>> print (s.replace('l', '(ell)'))     ## replace all instance of one substring with another
he(ell)(ell)o
>>> print ("    world ".strip())    ## Strip leadding and trail whitespaces: Print "world"
world
```

You can find more details in [the documentaion of python](https://docs.python.org/3.6/library/stdtypes.html#string-methods)

##  Containers

Python has several built-in container types which are Lists, Dictionary, Sets, and Tuples


### Lists

A List is the python equivalent of array, but is resizable and can contain elements of different types.

```python
>>> xs = [3,1,2]          ## a new List
>>> print (xs, xs[2])     
[3, 1, 2] 2   
>>> print (xs[-1])        ## negative indices mean the reverse direction of list
2
>>> xs[2] = "foo"         ## List can constains elements of different types. 
>>> print (xs)
[3, 1, 'foo']
>>> xs.append("bar")      ## Add a new element to the end of the list
>>> print (xs)
[3, 1, 'foo', 'bar']
>>> x = xs.pop()          ## Pop element at the end of List 
>>> print (x, xs)
bar [3, 1, 'foo']
>>> xs.append("bar")      ## Also, You can remove and return any element according to the number of pop(number)
>>> print (xs)
[3, 1, 'foo', 'bar']
>>> x = xs.pop(1)
>>> print (x, xs)
1 [3, 'foo', 'bar']
```

As usual, You can find all the detials in [the documentaion of python](https://docs.python.org/3.6/tutorial/datastructures.html#more-on-lists)

**Slicing**

In addition to accessing list elements one at a time. Python provides concise syntax to access sublists; this is know as _Slicing__

```python 
>>> nums = range(5)               ## Range is a built-in function that creates a range of integers. 
>>> print (nums)                  ## Range is range
range(0, 5) 
>>> print (nums[2:4])             ## Get a slice from idex 2 to 4 (exclusive)
range(2, 4)
>>> numsList = list(range(5))     ## this is different between python 2.7 and 3.6
>>> print (numsList)
[0, 1, 2, 3, 4]
>>> print (numsList[2:4])         ## Get a slice from idex 2 to 4 (exclusive)
[2, 3]
>>> print (numsList[2:])          ## Get a slice from idex 2 to the end
[2, 3, 4]
>>> print (numsList[:2])          ## Get a slice from the start to index 2 (exclusive)
[0, 1]
>>> print (numsList[:])           ## Get a slice of the whole List
[0, 1, 2, 3, 4]
>>> print (numsList[:-1])         ## Get a slice from the start to the end (exclusive)
[0, 1, 2, 3]                      ## And slice indices can be negative
>>> numsList[2:4] = [8,9]
>>> print (numsList)              ## asssign a new sublist to a slice
[0, 1, 8, 9, 4]
```

We will see slicing again in the context of numpy arrays.

**Loops**

You can Loop over the elements of a list like this : 

```python 
>>> animals = ['cat', 'dog', 'monkey']
>>> for temp in animals:
...     print (temp)
...
cat
dog
monkey
```

If you want to access to index of each element within the body of a loop, Use the built-in **enumerate** function. 

```python
>>> animals = ['cat', 'dog', 'monkey']
>>> for idx, animal in enumerate(animals) :
...     print ("#%d: %s" % (idx + 1, animal))
...
#1: cat
#2: dog
#3: monkey
```

**List comprehensions**

When programming, frequently we want to transform one type of data into another one. As an simple example, consider the following code that computes the number squared

```python
>>> nums = [0, 1, 2, 3, 4, 5]
>>> squares = []
>>> for x in nums :
...     squares.append(x ** 2)
...
>>> print (squares)
[0, 1, 4, 9, 16, 25]
```

let's make it more simple

```python 
>>> nums = [0, 1, 2, 3, 4, 5]
>>> squares = [x ** 2 for x in nums]
>>> print (squares)
[0, 1, 4, 9, 16, 25]
```

List comprehension also contains if statement liks conditions :

```python
>>> nums = [0, 1, 2, 3, 4, 5]
>>> even_squares = [x ** 2 for x in nums if x % 2 == 0]
>>> print (even_squares)
[0, 4, 16]
```

### Dictionary

A Dictionary stores (key, value) pairs, similar to a map in Java or an object in javasript.

```python 
>>> d = {'cat':'cute', 'dog':'furry'}           ## create a new dictionary with some data
>>> d['cat']                                    ## Get an entry form a Dictionary
'cute'
>>> print ('cat' in d)                          ## check if a dictionary has 'cat' as a given key
True
>>> print ('cute' in d)
False
>>> d['fish'] = 'wet'                           ## add a new element into a dictionary 
>>> print (d['fish'])                           ## print element one of a dictionary based on a given key    
wet
>>> print (d['monkey'])                         ## check if you don't have a given key. 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'monkey'
>>> print (d.get('monky', 'N/A'))               ## Get an element with a default(N/A)
N/A
>>> print (d.get('fish', 'N/A'))                ## Get an element with a default(N/A)
wet
>>> del d['fish']                               ## Remove an element form a dictionary
>>> print (d.get('fish', 'N/A'))                ## Get an element with a default(N/A)
N/A
```

You can figure out more details in [the documentation of python](https://docs.python.org/2/library/stdtypes.html#dict)

**Loops**

It is easy to iterate over the keys in a dictionary :

```python 
>>> d = {'person' : 2, 'cat' : 4, 'spider' : 8}
>>> for animal in d :
...     legs = d[animal]
...     print ("A %s has %d legs" % (animal, legs))
...
A person has 2 legs
A cat has 4 legs
A spider has 8 legs
```

If you want to access to keys and their corresponding values, use the **items** method :

on python 3.6 **iteritems = items**

```python 
>>> d = {'person' : 2, 'cat' : 4, 'spider' : 8}
>>> for animal, legs in d.items() :
...     print ("A %s has %d legs" % (animal, legs))
...
A person has 2 legs
A cat has 4 legs
A spider has 8 legs
```

**Dictionary Comprehension**

These are similar to list comprehension, But allow you to easily construct dictionaries.

```python
>>> nums = [0,1,2,3,4,5]
>>> even_num_to_squares = {x: x**2 for x in num if x % 2 == 0}
>>> print (even_num_to_squares)
{0: 0, 2: 4, 4: 16}
```

### Sets

A Set is an unordered collection of distinct elements. if you think of set as set of math. it is easy to understand set type of python 

```python 
>>> animals = {'cat',  'dog'}          ## Create a new set
>>> print ('cat' in animals)           ## Check whether an element is in a set
True
>>> print ('fish' in animals)          ## Check whether an element is in a set
False
>>> animals.add('fish')                ## Add new element into a set
>>> print ('fish' in animals)          ## Check whether an element is in a set or not
True
>>> print (len(animals))               ## Compute how many elements set has
3
>>> animals.add('cat')                 ## Add new element into a set
>>> print (len(animals))               ## Compute how many elements set has
3
>>> print (animals)                    ## print the total elements
{'dog', 'cat', 'fish'}
>>> animals.remove('cat')              ## Remove a particular element from a set
>>> print (len(animals))
2
>>> print (animals)                    ## Check whether or not a particular one is deleted
{'dog', 'fish'}
```

As usual, Everything  you want to know about sets can be found in [the doucmentation of python](https://docs.python.org/2/library/sets.html#set-objects)

**Loops**

Iterating over a set has the same syntax as iterating over a list, however since sets are unordered, you cannnot make assumptions about the order in which you visit the elements of the set

```python 
>>> animals = {"cat", "dog", "fish"}
>>> for idx, animals in enumerate(animals) :
...     print ("#%d: %s" % (idx +1, animals))
...
#1: dog
#2: cat
#3: fish
```

**Set Comprehension**

You can construct a set like list and dictionary, using the set comprehensions

sqrt() means square root of any number. 

```python 
>>> from math import sqrt
>>> sums = {int(sqrt(x)) for x in range(30)}
>>> print (sums)
{0, 1, 2, 3, 4, 5}
```

### Tuple

A Tuple is an (immutable) ordereed list of values. A tuple is in many ways similar to a list; one of the most important differences is that tuples can be used as keys in dictionaries and as elements of sets, whiles lists cannot.

```python 
>>> d = {(x, x+1): x for x in range(10)}
>>> t = (5, 6)           
>>> print (type(t))       ## Prints "<class 'tuple'>"
>>> print (type(d))       ## Prints "<class 'dict'>"
>>> d[t]
5
>>> d
{(0, 1): 0, (1, 2): 1, (2, 3): 2, (3, 4): 3, (4, 5): 4, (5, 6): 5, (6, 7): 6, (7, 8): 7, (8, 9): 8, (9, 10): 9}
>>> d[(1,2)]
1
```

[The documentation](https://docs.python.org/3.6/tutorial/datastructures.html#tuples-and-sequences) has more information about tuple


## Functions

python function is defined using **def** keyword

```python
>>> def sign(x):
...     if x > 0 :
...             return 'positive'
...     elif x < 0 :
...             return 'negative'
...     else :
...             return 'zero'
...
>>> for x in [-1, 0, 1] :
...     print (sign(x))
...
negative
zero
positive
```

you can also define functions to take optional keyword arguments this way. 

```python
>>> def hello(name, loud=False) :
...     if loud :
...             print ("HELLO: %s!" % name.upper())
...     else:
...             print ("Hello, %s" % name)
...
>>> hello('Bob')
Hello, Bob
>>> hello('Fred', loud=True)
HELLO: FRED!
>>> hello('Fred', True)
HELLO: FRED!
```

There is a lot more information about python functions in [the documentation of python](https://docs.python.org/2/tutorial/controlflow.html#defining-functions)

## Classes


the syntax for defining classes in python is straitforward

```python
>>> class Greeter(object) :
...     #Constructor
...     def __init__(self, name) :
...             self.name = name
...     #Instance method
...     def greet(self, loud=False) :
...             if loud :
...                     print ("HELLO, %s!" % self.name.upper())
...             else :
...                     print ("Hello, %s" % self.name)
...
>>> g = Greeter('Fred')
>>> g.greet()
Hello, Fred
>>> g.greet(loud=True)
HELLO, FRED!
>>> g.greet(True)
HELLO, FRED!
```

you can also read more information of Class in [the documentation of python](https://docs.python.org/3.6/tutorial/classes.html)

# Reference 

  - [Standford university's tutorial of python](http://cs231n.github.io/python-numpy-tutorial/) 
  
  - [github of CS288 python Tutorial of stanford](https://github.com/kuleshov/cs228-material/blob/master/tutorials/python/cs228-python-tutorial.ipynb)
  
  - [Numpy for Matlab Users](http://scipy.github.io/old-wiki/pages/NumPy_for_Matlab_Users)
  
  - [matplotlib for graph with python](https://matplotlib.org/index.html)
  
  if you continue to python more, I recommend you some library of python, numpy, scipy, matplolib

















