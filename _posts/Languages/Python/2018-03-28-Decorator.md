---
layout: post
title: Decorator
subtitle: What is the Decorator on python?
category: Python
tags: [python, middle]
permalink: /2018/03/28/Decorator/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

In the context of design patterns, decorators dynamically alter the functionality of a function, method or even class without having to directly use subclasses.

The decorator is ideal when you need to extend the functionality of functions that you don't want to modify

i.e. Essentially, decorators work as wrappers, modifying the behviour of the code before and after a target function execution, without the need to modify the funtion itself, increase the original functionality of the function. 

So we can call it decorating function, method or class that you don't want to modify. 

Let's see function is object in python, ahead of proceeding to how I could decorate a function on syntax of python.

Because function is regarded as object, python's function is first class function.

The functions on python is moved to another function and is stored to another variable and is returned from functions.

Let's see an example about what I was sayging above. 

- Assign functions to variables 

{% highlight python linenos %}
def greet(name):
    return "hello " + name

greet_someone = greet

print(greet_someone("hyun"))
'''
## the result of the code above ##
hello hyun
'''
{% endhighlight %}

- Define functions insdies other functions. 

{% highlight python linenos %}
def greet(name):
    def get_message():
        return "Hello "
    result = get_message()+name
    return result
print(greet("hyun"))
'''
## the result of the code above ##
Hello hyun
'''
{% endhighlight %}

- Functions can be passed as parameters to other functions.

{% highlight python linenos %}
def greet(name):
    return "hello "+name

def call_func(func):
    other_name = "hyun"
    return func(other_name)

print(call_func(greet))
'''
## the result of the code above ##
hello hyun
'''
{% endhighlight %}

- Functions can return other functions 

To sum up, In this case, functions generates other functions.

{% highlight python linenos %}
def compose_greet_func():
    def get_message():
        return "Hello there!"
    return get_message

greet = compose_greet_func()
print(greet())

'''
## the result of the code above ##
Hello there!
'''
{% endhighlight %}

- Inner functions have access to the enclosing scope

i.e. this is call and knowns as closure. 

{% highlight python linenos %}
def compose_greet_func(name):
    def get_message():
        return "Hellow there "+name+"!"
    return get_message

greet = compose_greet_func("hyun")

print(greet())

'''
## the result of the code above ##
Hellow there hyun!
'''
{% endhighlight %}

From now on, let's go through decorators. 

# Decorator 

I wnat to add some functionality to get_text function without modifying the get_next function. 

At the time, I could do it with decorator like this:

{% highlight python linenos %}
def get_text(name):
    return "Hellow, {0} What are you doing?".format(name)

def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))
    
    return func_wrapper

my_get_text = p_decorate(get_text)

print(my_get_text("hyun"))

get_text = p_decorate(get_text)
print(get_text("hyun"))

'''
## the result of the code above ##
<p>Hellow, hyun What are you doing?</p>
<p>Hellow, hyun What are you doing?</p>
'''
{% endhighlight %}

as you can see, decorating is to adding a functionality before and after the function to wrap, In here, get_next is wrapped. 

p_decorate function decorate the get_next function by func_wrapper function. 

But you don't need to write the line, "get_text = p_decorate(get_text)". If you use syntax of python for decorator.

## Python's Decorator syntax

When you make decorator like **my_get_text = p_decorate(get_text)**, There is a neat shorcut for decorator. 

The way to express decorator is to use @ symbol as follows:

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))
    return func_wrapper

@p_decorate
def get_text(name):
    return "Hellow, {0} What are you doing?".format(name)

print(get_text("hyun"))

'''
## the result of the code above ##
<p>Hellow, hyun What are you doing?</p>
'''
{% endhighlight %}

If you also want to creat another decorator function similar to p tag function. I mean I want to extend p tag function with strong, div tag function.

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))
    return func_wrapper

def strong_decorate(func):
    def func_wrapper(name):
        return "<strong>{0}</strong>".format(func(name))
    return func_wrapper

def div_decorate(func):
    def func_wrapper(name):
        return "<div>{0}</div>".format(func(name))
    return func_wrapper

def get_text(name):
    return "lorem ipsum, {0} dolor sit amet".format(name)

get_text = div_decorate(p_decorate(strong_decorate(get_text)))

print(get_text("hyun"))

'''
## the result of the code above ##
<div><p><strong>lorem ipsum, hyun dolor sit amet</strong></p></div>
'''
{% endhighlight %}

The code above is simple way to make decorator. The above thing is recursive function, first is strong tag function, second is p tag function, and final one is div tag.

If you change the codes above with @ symbol, that is the same from below:

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(name):
        return "<p>{0}</p>".format(func(name))
    return func_wrapper

def strong_decorate(func):
    def func_wrapper(name):
        return "<strong>{0}</strong>".format(func(name))
    return func_wrapper

def div_decorate(func):
    def func_wrapper(name):
        return "<div>{0}</div>".format(func(name))
    return func_wrapper

@div_decorate
@p_decorate
@strong_decorate
def get_text(name):
    return "lorem ipsum, {0} dolor sit amet".format(name)

print(get_text("hyun"))


@p_decorate
@strong_decorate
@div_decorate
def get_text(name):
    return "lorem ipsum, {0} dolor sit amet".format(name)

print(get_text("hyun"))

@p_decorate
@div_decorate
@div_decorate
def get_text(name):
    return "lorem ipsum, {0} dolor sit amet".format(name)

print(get_text("hyun"))

'''
## the result of the code above ##
<div><p><strong>lorem ipsum, hyun dolor sit amet</strong></p></div>
<p><strong><div>lorem ipsum, hyun dolor sit amet</div></strong></p>
<p><div><div>lorem ipsum, hyun dolor sit amet</div></div></p>
'''
{% endhighlight %}

one important thing is, when you use several @ symbol to decorate several times, it decorate from bottom to top. 

So keep in mind the order when you want to decorate multiple times. 

## when you want to decorate method in a class

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(self):
        return "<p>{0}<p>".format(func(self))
    return func_wrapper

class Person(object):
    def __init__(self):
        self.name = "hyun"
        self.family = "Lee"
    @p_decorate
    def get_fullname(self):
        return self.name + " " + self.family

my_person = Person()
print(my_person.get_fullname())

'''
## the result of the code above ##
<p>hyun Lee<p>
'''
{% endhighlight %}

When you want to decorate the method in a class, it all is the same from normally decorating functions.

i.e. after defining decorator function outside a class, use @ symbol.

## advanced decorator

you don't want to care about how much parameter the wrapped function has, use some **args and kwargs** like this:

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(*args, **kwargs):        
        return "<p>{0}<p>".format(func(*args, **kwargs))
    return func_wrapper

class Person(object):
    def __init__(self):
        self.name = "hyun"
        self.family = "Lee"
        
    @p_decorate
    def get_fullname(self):
        return self.name + " " + self.family

my_person = Person()

print(my_person.get_fullname())

'''
## the result of the code above ##
<p>hyun Lee<p>
'''
{% endhighlight %}

In the example above, \*args means tuple, \*\*kwargs means dictionary. 

## When you want to pass arguments to decorator

When you want to pass arguments to decorator, add another function encloing the decorator function like this:

{% highlight python linenos %}
def p_decorate(func):
    def func_wrapper(*args, **kwargs):        
        return "<p>{0}<p>".format(func(*args, **kwargs))
    return func_wrapper
    
def tags(tag_name):
    def tags_decorator(func):
        def func_wrapper(name):
            return "<{0}>{1}<{0}>".format(tag_name, func(name))
        return func_wrapper
    return tags_decorator

@tags("p")
def get_text(name):
    return "Hello "+name

print(get_text("hyun"))

print(get_text.__name__)
print(get_text.__module__)
print(get_text.__doc__)

'''
## the result of the code above ##
<p>Hello hyun<p>
func_wrapper
__main__
None
'''
{% endhighlight %}

As you can see the result above, When you make decorator, decorator expect to receive a function as argument, that is why we have to build a function more to take extra arguments and generate the decorator.

In the example above, tags function is decorator generator. 

## Debugging the decorated functions

you just wraped a funtion to be decorated, the wrapper function does not carry any information of the function to be enclosed by wrapper function. 

the information like __name__ , __module__, and __doc__ is not carried from the function to be wrapped by wrapper function.

So in order to resolve this problem, python provide some library such as **functool.wraps**.

Let's go through how to use **functool.wraps** to carry the information such as __doc__, __name__, and __module__.

{% highlight python linenos %}
from functools import wraps

def tags(tag_name):
    def tags_decorator(func):
        @wraps(func)
        def func_wrapper(name):
            return "<{0}>{1}<{0}>".format(tag_name, func(name))
        return func_wrapper
    return tags_decorator

@tags("p")
def get_text(name):
    """returns some text"""
    return "Hello "+name

print(get_text("hyun"))

print(get_text.__name__)
print(get_text.__module__)
print(get_text.__doc__)

'''
## the result of the code above ##
<p>Hello hyun<p>
get_text
__main__
returns some text
'''
{% endhighlight %}

As you can check, when you use funtools.wraps on the func_wrapper function.

The informaion of **get_text** is carried to func_wrapper function.

# Let's see more about decorator

## decorator class

{% highlight python linenos %}
class DecoratorClass:
    def __init__(self, original_function):
        self.original_function = original_function
    def __call__(self, *args, **kwargs):
        print("{} is not called".format(self.original_function.__name__))
        return self.original_function(*args, **kwargs)

@DecoratorClass
def display():
    print("display function is done!")
@DecoratorClass
def display_info(name, age):
    print("display_info({}, {}) is done!".format(name, age))


display()
print(type(display))
print()
display_info("John", 25)
print(type(display_info))

'''
## the result of the code above ##
display is not called
display function is done!
<class '__main__.DecoratorClass'>

display_info is not called
display_info(John, 25) is done!
<class '__main__.DecoratorClass'>
'''
{% endhighlight %}

If you want to use decorator class, do it like the code above, but normally decorator function is used. 

## Let's go through loggin system with decorator

{% highlight python linenos %}
# -*- coding: utf-8 -*-

import datetime
import time

def my_logger(original_function):
    import logging
    logging.basicConfig(filename="{}.log".format(original_function.__name__), level=logging.INFO)
    
    def wrapper(*args, **kwargs):
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        logging.info( '[{}] the result args - {}, kwargs - {}'.format(timestamp, args, kwargs))
        return original_function(*args, **kwargs)
    return wrapper

@my_logger
def display_info(name, age):
    time.sleep(1)
    print('display_info({}, {}) function is executed.'.format(name, age))
    
display_info('Hyun', 27)

'''
## the result of the code above ##
display_info(Hyun, 27) function is executed.
'''
{% endhighlight %}

The code above generates the display_info.log file after executing the code above.

Let's look at another timer decorator.

{% highlight python linenos %}
def my_timer(original_function):
    import time
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = original_function(*args, **kwargs)
        t2 = time.time() - t1
        print ('{}\'s total time executed: {} ???'.format(original_function.__name__, t2))
        return result
    
    return wrapper

@my_timer 
def display_info(name,age):
    time.sleep(1)
    print('display_info({}, {}) function is executed.'.format(name, age))
    
display_info('Hyun', 25)

'''
## the result of the code above ##
display_info(Hyun, 25) function is executed.
display_info's total time executed: 1.001187801361084 ???
'''
{% endhighlight %}

Let's turn two functions above into one. 

{% highlight python linenos %}
import datetime
import time

def my_logger(original_function):
    import logging
    logging.basicConfig(filename="{}.log".format(original_function.__name__), level=logging.INFO)
    
    def wrapper(*args, **kwargs):
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        logging.info( '[{}] the result args - {}, kwargs - {}'.format(timestamp, args, kwargs))
        return original_function(*args, **kwargs)
    return wrapper

def my_timer(original_function):
    import time
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = original_function(*args, **kwargs)
        t2 = time.time() - t1
        print ('{}\'s total of time executed: {} ???'.format(original_function.__name__, t2))
        return result
    
    return wrapper

@my_logger
@my_timer 
def display_info(name,age):
    time.sleep(1)
    print('display_info({}, {}) function is executed.'.format(name, age))
    
display_info('Hyun', 25)

'''
## the result of the code above ##
display_info(Hyun, 25) function is executed.
display_info's total of time executed: 1.0012180805206299 ???
'''
{% endhighlight %}

on the code above, If I change the order of decorators. i.e. @my_timer -> @my_logger into @my_logger -> @my_timer

{% highlight python linenos %}
import datetime
import time

def my_logger(original_function):
    import logging
    logging.basicConfig(filename="{}.log".format(original_function.__name__), level=logging.INFO)
    
    def wrapper(*args, **kwargs):
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        logging.info( '[{}] the result args - {}, kwargs - {}'.format(timestamp, args, kwargs))
        return original_function(*args, **kwargs)
    return wrapper

def my_timer(original_function):
    import time
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = original_function(*args, **kwargs)
        t2 = time.time() - t1
        print ('{}\'s total time executed: {} ???'.format(original_function.__name__, t2))
        return result
    
    return wrapper

@my_timer 
@my_logger
def display_info(name,age):
    time.sleep(1)
    print('display_info({}, {}) function is executed.'.format(name, age))
    
display_info('Hyun', 25)

'''
## the result of the code above ##
display_info(Hyun, 25) function is executed.
wrapper's total time executed: 1.0014979839324951 ???
'''
{% endhighlight %}

One thing is chagned after change the order of decorator, that is the printed result of name variable. 

first order(@my_time -> @my_logger) printed **display_info**, but second order(@my_logger -> @my_time) printed **wrapper**. 

So If you want to fix it, the name variable printed, use **funtools.wraps** like before.


{% highlight python linenos %}
from functools import wraps
import datetime
import time

def my_logger(original_function):
    import logging
    logging.basicConfig(filename="{}.log".format(original_function.__name__), level=logging.INFO)
    @wraps(original_function)
    def wrapper(*args, **kwargs):
        timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        logging.info( '[{}] the result args - {}, kwargs - {}'.format(timestamp, args, kwargs))
        return original_function(*args, **kwargs)
    return wrapper

def my_timer(original_function):
    import time
    @wraps(original_function)
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = original_function(*args, **kwargs)
        t2 = time.time() - t1
        print ('{}\'s total time executed: {} ???'.format(original_function.__name__, t2))
        return result
    
    return wrapper

@my_timer 
@my_logger
def display_info(name,age):
    time.sleep(1)
    print('display_info({}, {}) function is executed.'.format(name, age))
    
display_info('Hyun', 25)

'''
## the result of the code above ##
display_info(Hyun, 25) function is executed.
display_info's total time executed: 1.0014572143554688 ???
'''
{% endhighlight %}

# Reference

 - Eng ver.
  - [A guide to Python's function decorators](https://www.thecodeship.com/patterns/guide-to-python-function-decorators/)
  
 - Kor ver.
  - [School of web's decorator](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0-decorator/)
