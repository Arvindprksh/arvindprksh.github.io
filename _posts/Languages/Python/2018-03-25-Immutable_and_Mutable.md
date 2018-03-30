---
layout: post
title: Immutable vs Mutable variable on python 
subtitle: how to work on handling the variable of Immutable and Mutable
category: Python
tags: [python, middle]
permalink: /2018/03/25/Immutable_and_Mutable/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


There are two types of variables on python, one is Mutable and the other is Immutable. 

On python, it is different to manage reference of variable depending on whether or not variable is mutable. 

So specifically, you want to check the state of variables's reference like whether the references is the same or not. 

Use **id** function and **is** operator or **deepcopy** of copy module 

above all, Keep in mind of everyone in python is object, even function is thought of as object.

So when you creat a object, the object will have object id number

Let's dive deeper int to the detail of what is the mutable and immutable. 

Immutable type : 

1. numbers : int(), float(), comlex()
2. Immutable sequences : str(), tuple(), frozenset(), byte()
3. True and False : bool()

In summary, Object of built-in types like **int, float, bool, str, tuple, unicode** are Immutable types. 

Mutable type : 

1. Mutable sequences : List(), bytearray()
2. set type : set()
3. mapping tyep : dictionary()
4. classes, class instances
5. etc. 

In summary, Object of built-in types like **list, set, dict** are mutable. 

Also **custom classes** are generally mutable. 

Ahead of divin into how to check if the variable I use in python programming is mutable or immutable. 

you have to understand id and type function and is operator 

# ID and TYPE function on python and IS operator

The built-in function **id()** return the identity of object as an integer. 

This integer usually corresponds to the object's location in memory.

You can compare two object with **is** operator. 

The built-in function **type()** returns the type of an object. Let's look at a simple example. 

{% highlight python linenos %}
'''Example 1'''
x = "test"
y = "test"
print("The Identity of x:{}".format(id(x)))
print("The Identity of y:{}".format(id(y)))

'''Comparing Object id'''
print("is x the same from y: {}".format(x is y))

'''Example 2'''
a = 50 
print("The type of a: {}".format(type(a)))
b = "test"
print("The type of b: {}".format(type(b)))

'''
##the output above##
The Identity of x:140440541230672
The Identity of y:140440541230672
is x the same from y: True
The type of a: <class 'int'>
The type of b: <class 'str'>

'''
{% endhighlight %}

We have now seen how to compare two simple varialbe on python to find out the types and id's. 

So using this two function and **is** operator, we can check to see how the variable references the identity of each variable on code of python.

# Mutable and Immutable Objects

as you can read earlier, a mutable object can change its state or contents and immutable object can't

Mutable Objects : list, dict, set, byte array 

Immutable Objects : int, float, complex, string, tuple, frozen set[note: immutable version of set], bytes.

Let's see how to work on immutable variable in python. 

{% highlight python linenos %}
'''Simple example of immutable variable'''
x = 10
y = x

print("id(x) == id(y): {}".format(id(x)==id(y)))

print("id(x) == id(10): {}".format(id(x)==id(10)))

'''After simple operation'''
x = x + 1

print("id(x) == id(y): {}".format(id(x)==id(y)))

print("id(x) == id(10): {}".format(id(x)==id(10)))

'''
## The result of the code above ##
id(x) == id(y): True
id(x) == id(10): True
id(x) == id(y): False
id(x) == id(10): False
'''
{% endhighlight %}

As you can see the code above, Immutable obects doesn't allow modification after creation.

Let's see how to work on mutable variable in python. 

{% highlight python linenos %}
'''Simple example of mutable variable'''
m = list([1,2,3])

n = m

print("id(m) == id(n): {}".format(id(m)==id(n)))

print("id(n) == id([1,2,3]]): {}".format(id(n)==id([1,2,3])))

'''After simple operation'''
m.pop()

print("id(m) == id(n): {}".format(id(m)==id(n)))

print("id(n) == id([1,2,3]]): {}".format(id(n)==id([1,2,3])))


'''
## the result of the code above ##
id(m) == id(n): True
id(n) == id([1,2,3]]): False
id(m) == id(n): True
id(n) == id([1,2,3]]): False
'''
{% endhighlight %}

As you can see, the behaviour of mutable is opposite to Immutable. i.e. 

# How to be treated on Immutable variable and Mutable variable when you passe them onto a function

{% highlight python linenos %}
'''How to deal with function call on Immutable and Mutable Variable'''

def updateList(list1):
    list1 += [10]
    
n = [5, 6]

print("About list")
print("id(n): {}".format(id(n)))

updateList(n)
print("n: {}".format(n))
print("id(n): {}".format(id(n)))

def updateTuple(tuple1):
    print("id(tuple1): {}".format(id(tuple1)))
    tuple1 += (10,)
    return tuple1
    
n1 = (5, 6)

print("About Tuple")
print("id(n1): {}".format(id(n1)))

r = updateTuple(n1)
print("n: {}".format(n1))
print("id(n1): {}".format(id(n1)))

print("r: {}".format(r))
print("id(r): {}".format(id(r)))
'''
## The result of the code above ##
About list
id(n): 140440402287240
n: [5, 6, 10]
id(n): 140440402287240
About Tuple
id(n1): 140440402925448
id(tuple1): 140440402925448
n: (5, 6)
id(n1): 140440402925448
r: (5, 6, 10)
id(r): 140440403209672
'''
{% endhighlight %}


If you pass argument into function on python. the variable is immutable or not is important. 

All you need to focuse is whether or not the variable is mutable. 

If the variable is mutable, the call is **call by reference**

if the variable is Immutable, the call is **call by value**

In the case above, List is **call by reference** and tuple is **call by value**

Let's see the more detail about **call by vlaue** with integer variable and a function.

{% highlight python linenos %}
''' Immutable variable calls function in detail '''

def updateNumber(n1):
    print("id(n1): {}".format(id(n1)))
    n1 +=10
    return n1

b = 5
print("id(b): {}".format(id(b)))
t = updateNumber(b)
print("id(b): {}".format(id(b)))
print("id(t): {}".format(id(t)))
print("b: {}".format(b))
print("t: {}".format(t))
{% endhighlight %}


Let's see how to call by reference with some fucntion(copy.deepcopy)

{% highlight python linenos %}
# copy module
import copy 
# reference of x variable
x = [1,2]
# assign the reference of x into y variable
y = x 
# z and x don't share the reference. i.e. the reference between z and x is different. 
z = x[:]

# Also, using deepcopy, it makes x and deepcp not share the reference like the location of variable stored. 
deepcp = copy.deepcopy(X)

print(id(x))
print(id(y))
print(id(z))
print(id(deepcp))

```
## The results of print functions above ##
x:140297386131144
y:140297386131144
z:140297388728008
deepcp:140297386129032
```
{% endhighlight %}

To sum up, Not all python objects handle the change the same way, there are two ways, some objects are mutable meaning they can be altered.

Others are immutable; They cannot be altered but rather return new objects when attempting to update.


Let's see another additional emxample with mutability of variable on python

When you use default value parameter in a function as follows:

{% highlight python linenos %}
def my_function(param=[]):
    param.append("thing")
    return param

a = my_function()
print("id(my_function()): {0} {1}".format(id(a), a))
b = my_function()
print("id(my_function()): {0} {1}".format(id(b), b))

'''
## the result of the code above ##
id(my_function()): 140440402272776 ['thing']
id(my_function()): 140440402272776 ['thing', 'thing']
'''
{% endhighlight %}

As you can see the code above, Whenever you call the function which uses default list. The function will be using the same list. 

This is because 1. python only evaluates functions definition once, 2. python evaluates default arguments as part of the function definition, 3 finally, python allocates one mutable list for every call of that function.

So keep in mind don't pus a mutable object as the default value of a function parameter. 

Immutable types are perfectly safe.  But you have to use mutable variable on the code above, just do programming for safety.

{% highlight python linenos %}
def my_function2(param=None):
    if param is None:
        param = []
    param.append("thing")
    return param

a = my_function2()
print("id(my_function()): {0} {1}".format(id(a), a))
b = my_function2()
print("id(my_function()): {0} {1}".format(id(b), b))
'''
## the result of the code above ##
id(my_function()): 140142232306184 ['thing']
id(my_function()): 140142232307272 ['thing']
'''
{% endhighlight %}


# Reference 
  
  - Eng ver. 
   - [Stackoverflow](https://stackoverflow.com/questions/8056130/immutable-vs-mutable-types)
   - [Mutable vs Immutable Objects in Python](https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747)
   - [Python Objects: Mutable vs. Immutable](https://codehabitude.com/2013/12/24/python-objects-mutable-vs-immutable/)
   - []

 - Kor ver. 
  - [The difference of Mutable and Immutable on python](http://ledgku.tistory.com/54)
