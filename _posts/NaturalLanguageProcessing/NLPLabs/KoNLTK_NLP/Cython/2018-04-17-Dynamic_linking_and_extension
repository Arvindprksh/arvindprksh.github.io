---
layout: post
title: dynamic linking and extension on cython
subtitle: dynamic linking and extension on cython for practice
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/17/Dynamic_linking_and_extension/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Dynamic linking

If you want to link dynamically, use as the followings on **extension()**

**libraries=["m"]**

{% highlight pythonlinenos %}
from distutils.core import setup
from distutils.extension import Extension
from Cython.Build import cythonize

ext_modules=[
    Extension("sin",
              sources=["sin.pyx"],
              libraries=["m"] # Unix-like specific
    )
]

setup(
  name = "sin",
  ext_modules = cythonize(ext_modules)
)
{% endhighlight %}

Let's another exmples. 

If you want access C code for which Cython does not porvide a ready to use declaration, you must declare them yourself.

Just define like this :

{% highlight pythonlinenos %}
# If cython does not provide, 
cdef extern from "math.h":
   double sin(double x)

def call_sin(double x):
   print("math.h")
   return sin(x)
{% endhighlight %}

This declares the **sin()** function in a way that makes it available to Cython code and instructs Cython to generate C code that includes the **math.h** header file. 

The C compiler will see the original declaration in **math.h** at compile time, but Cython does not parse "math.h" and requires a separate definition.

Just like the sin() function from the math library, it is possible to declare and call into any C library as long as the module that Cython generates is properly linked against the shared and static library. 

OR


Note taht you can easily export an external C function from your Cython module by declaring it as **cpdef**.

This generates a Python wrapper for it and adds it to the module dict. 

The following is a Cython module that provides direct access to the C **cos()** function for python code :

{% highlight pythonlinenos %}
cdef extern from "math.h":
   cpdef double cos(double x)
{% endhighlight %}

Also you would get the same result when This declaration appears in the **.pxd** file that belong to the Cython moduleand This allows the C declaration to be resued in other Cython modules. 


Let's import things above like this:

{% highlight pythonlinenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/8.Dynamic_liking on git:master x [15:16:47] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sin
>>> sin.
sin.__class__(         sin.__ge__(            sin.__name__           sin.__sizeof__(
sin.__delattr__(       sin.__getattribute__(  sin.__ne__(            sin.__spec__
sin.__dict__           sin.__gt__(            sin.__new__(           sin.__str__(
sin.__dir__(           sin.__hash__(          sin.__package__        sin.__subclasshook__(
sin.__doc__            sin.__init__(          sin.__reduce__(        sin.__test__
sin.__eq__(            sin.__le__(            sin.__reduce_ex__(     sin.call_f(
sin.__file__           sin.__loader__         sin.__repr__(          sin.call_sin(
sin.__format__(        sin.__lt__(            sin.__setattr__(       sin.cos(
>>> sin.cos(1)
0.5403023058681398
>>> sin.call_sin(1)
math.h
0.8414709848078965
{% endhighlight %}

# Reference 

 - [Calling C function on the official Cython](http://cython.readthedocs.io/en/latest/src/tutorial/external.html)
