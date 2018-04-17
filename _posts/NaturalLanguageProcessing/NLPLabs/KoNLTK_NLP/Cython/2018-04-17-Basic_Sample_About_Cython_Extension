---
layout: post
title: Basic Sample about Cython Extension
subtitle: How to basically make extension module with Cython 
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/17/Basic_Sample_About_Cython_Extension/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Basic sample about Cython extension 

Let's see how to use Cythong for extension module from python 

First, Check out if your cython is installed. if not, do as follows:

> pip3 install cython

and then make **helloworld.pyx** to generate **\*.so** file. 

```python
# in hellowworld.pyx

print("Hello World")
```
Second, **setup.py** which is like a python Makefile. 

```python
from distutils.core import setup
from Cython.Build import cythonize

setup(
    ext_modules = cythonize("helloworld.pyx")
)

```

And the on prompt, type in as follows:

> python3 setup.py build_ext --inplace 

which will leave a file in your local directory called **helloworld.so** in linux or **helloworld.pyd** in windows, Now to use this fileL: start the python interpreter and simply import it as if it was a regular python module.

Let's chekck if it works 

```python3
 python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import helloworld
Hellow World
```

## Reference 

 - [Cython Tutorial's Cython Hellow World](http://cython.readthedocs.io/en/latest/src/tutorial/cython_tutorial.html#cython-hello-world)
 - [Cython Tutorial's Source Files and Compilation](http://cython.readthedocs.io/en/latest/src/userguide/source_files_and_compilation.html#compilation)
 - [Cython compilation](http://cython.readthedocs.io/en/latest/src/reference/compilation.html)
