---
layout: post
title: Interfacing With External C Code2
subtitle: Let's practice more 
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/20/Interfacing_With_External_C_Code2/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Different way1

Let's only have **add.c** , **c_function.pxd** , **function.pyx** and **substraction.c**. 

So Let's see the **c_function.pxd** and **function.pyx**

{% highlight python linenos %}
## In function.pyx
from c_function cimport sum_function, substraction_function

def sum(int a, int b):
    print("sum function is called!")
    return sum_function(a, b)

def substraction(int a, int b):
    print("substraction function is called!")
    return substraction_function(a, b)

## In C_function.pxd
cdef extern from "add.c":
    int sum_function(int a, int b)

cdef extern from "substraction.c":
    int substraction_function(int a, int b)
{% endhighlight %}

As you can notice, the thing above don't use header file, They are including directly from **.c** file. 

be care of make **.so** file at the time. 

Let's see **setup.py**


{% highlight python linenos %}
from distutils.core import setup
from distutils.extension import Extension
from Cython.Build import cythonize

ext_modules = [Extension("operator", ["function.pyx"])]

setup(
    name="sum and substraction function",
    ext_modules = cythonize(ext_modules)
)
{% endhighlight %}

In here, the source part is only one, **function.pyx**

# Different way2

Let's only have **add.c** , **c_function.pxd** , **function.pyx** and **substraction.c**.

So Let's see the **c_function.pxd** and **function.pyx**

{% highlight python linenos %}
## In function.pyx

cdef extern from "add.c":
    int sum_function(int a, int b)

cdef extern from "substraction.c":
    int substraction_function(int a, int b)

def sum(int a, int b):
    print("sum function is called!")
    return sum_function(a, b)

def substraction(int a, int b):
    print("substraction function is called!")
    return substraction_function(a, b)
{% endhighlight %}

As you can notice, the thing above don't use header file, They are including directly from **.c** file. 

be care of make **.so** file at the time. 

Let's see **setup.py**

{% highlight python linenos %}
from distutils.core import setup
from distutils.extension import Extension
from Cython.Build import cythonize

ext_modules = [Extension("operator", ["function.pyx"])]

setup(
    name="sum and substraction function",
    ext_modules = cythonize(ext_modules)
)
{% endhighlight %}

In here, the source part is only one, **function.pyx**


