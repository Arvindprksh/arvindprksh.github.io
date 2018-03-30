---
layout: post
title: First class function on python 
subtitle: function is object, so you can use it like variable
category: Python
tags: [python, middle]
permalink: /2018/03/26/Python_First_Class_function/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

{% highlight python linenos %}
{% endhighlight %}

I referenced [the site](https://dbader.org/blog/python-first-class-functions) which explainged about Python's function is first class.

It makes me undestand a little how to do programming functional programming techniques.

So in order to share some peoplen which is interested in this content. I cite the site which helps me understand what is the first class function.

# Function is object

Python's function is first-class objects. i.e. functions is assigned to variable, stored in data structure, passed as arguments to other functions, and even returned as a values from other functions. 

All data in a python program is object or relation by objects. the object can be strings, lists, module, and function.

So in python there is nothing special about function. 

Let's see a simple handling a fucntion to a varialbe by assigning it to a variable. 

{% highlight python linenos %}
def yell(text):
    return text.upper() + '!'

print("=== yell function ===")
print(yell("hello"))

bark = yell

print("=== bark function ===")
print(bark("hello"))

'''
## the result of the code above ##
=== yell function ===
HELLO!
=== bark function ===
HELLO!
'''
{% endhighlight %}

As you can see the code above, yell was assigned to bark varialbe, so yell function has second name to call it. 

Here, after I delet the function yell, I call bark function, at the time, what happens?

{% highlight python linenos %}
def yell(text):
    return text.upper() + '!'

print("=== yell function ===")
print(yell("hello"))

bark = yell

print("=== bark function ===")
print(bark("hello"))

del yell

print("=== bark function after del yell function ===")
print(bark("hello"))

'''
## the result of the code above ##
=== yell function ===
HELLO!
=== bark function ===
HELLO!
=== bark function after del yell function ===
HELLO!
'''
{% endhighlight %}

As you can see, After deletion of yell function, you can call the function using bark function having the underlying function.

Let's check some attribute python provide in built-in

{% highlight python linenos %}
def yell(text):
    return text.upper() + '!'

print("=== yell function ===")
print(yell("hello"))

bark = yell

print("=== bark function ===")
print(bark("hello"))

del yell

print("=== bark function after del yell function ===")
print(bark("hello"))

print("The attribute of name of bark function: {}".format(bark.__name__) )

'''
## the reuslt of the code above ##
=== yell function ===
HELLO!
=== bark function ===
HELLO!
=== bark function after del yell function ===
HELLO!
The attribute of name of bark function: yell
'''
{% endhighlight %}

From the result above, you can notice the function name variable and function itself is separate. 

# Function can be stored in data structure

You can also store the function in data structure like another objects. 

Let's add functions to a list

{% highlight python linenos %}
funcs = [bark, str.lower, str.capitalize]
print(funcs)

'''
## The result to execute the code above ##
[<function yell at 0x7f7564663268>, 
<method 'lower' of 'str' objects>, 
<method 'capitalize' of 'str' objects>]
'''
{% endhighlight %}

Also the list with functions work like another objects:

{% highlight python linenos %}
for function_name in funcs:
        print(function_name, function_name("hey hello"))
'''
## The result to execute the code above ##
<function yell at 0x7f7564663268> HEY HELLO!
<method 'lower' of 'str' objects> hey hello
<method 'capitalize' of 'str' objects> Hey hello
'''

''' call function using the list with functions '''
funcs[0]("hey whant is going on?")

'''
## The result to execute the code above ##
'HEY WHANT IS GOING ON?!'
'''

# Function can be passed to Other fucntion

Let's make greeting function getting function as argument like :

{% highlight python linenos %}
def greet(func):
    greeting = func("Hi, I am a ptyhon")
    print(greeting)
    
print("=== yell function ===")
greet(yell)

def whisper(text):
    return text.lower() + "......"

print("=== whisper function ===")
greet(whisper)

'''
## the result of python executable above ##
=== yell function ===
HI, I AM A PTYHON!
=== whisper function ===
hi, i am a ptyhon......
'''
{% endhighlight %}

The code above ara saying you can influence the output of greet function by passing in differenct functions. 

In the case of functional programming, it is a neccesity. 

Functions that can accept other functions as arguments are also called higher-order functions.

Let's see classical exmaple with map built-in function. 

{% highlight python linenos %}
print(list(map(yell, ['hello', 'hey', 'hi'])))

'''
## the result of python executable above ##
['HELLO!', 'HEY!', 'HI!']
'''
{% endhighlight %}

This higher-order function is needed when you make **call back**.

i.e. if you want to execute some event in a system, when you reach the point to execute the event in other function. 

using function as argument in other function is a neccesity. 

# Function can Be nested

This means you can make funtions inside another functions, These are often called nested functions or inner functions.

let's see an example :

{% highlight python linenos %}
def speak(text):
    def whisper(t):
        return t.lower() + "....."
    return whisper(text)

speak("Hellow World")

'''
## the result of python executable above ##
'hellow world.....'
'''

# error checking 

whisper("yo") # name 'whisper' is not defined

speak.whisper #'function' object has no attribute 'whisper'
{% endhighlight %}

As you can see the code above, whisper function is nested in speak function, and speak function return the valuer of executing whisper function.

i.e. when you call speak function, the function(speak) make new inner-function(whisper) and then calls it. 

You cannot call the whisper function outside speak function. that is because the speak function is not defined outside speak function.

What if you really want to access the inner function whisper from outside speak? you could, When you call speak function, you return whisper function.

Let's see an example return one of inner functions.

{% highlight python linenos %}
def get_speak_function(volume):
    def whisper(text):
        return text.lower() + "......"
    def yell(text):
        return text.upper() + "!"
    if volume > 0.5:
        return yell
    else:
        return whisper
    
print(get_speak_function(0.3))

print(get_speak_function(0.5))

print(get_speak_function(0.3)("Hello"))

speak_func = get_speak_function(0.7)

print(speak_func("Hello"))

'''
<function get_speak_function.<locals>.whisper at 0x7f36345c7598>
<function get_speak_function.<locals>.whisper at 0x7f36345c7598>
hello......
HELLO!
'''
{% endhighlight %}

In here, you can notice function can not only accept behaviour through arguments but also they can also return behaviour.




# Reference 
 
 - Eng ver
  - [Python's Functions Are First-class](https://dbader.org/blog/python-first-class-functions)


 - Korean ver.
  - [School of Web's First class function](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%ED%8D%BC%EC%8A%A4%ED%8A%B8%ED%81%B4%EB%9E%98%EC%8A%A4-%ED%95%A8%EC%88%98-first-class-function/)
  - [notice the most great python's Function](https://tech.ssut.me/2017/03/24/python-functions-are-first-class/)
  - [Basic call back function's concept](https://blog.naver.com/w_river/220332756031)
