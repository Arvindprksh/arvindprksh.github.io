---
layout: post
title: Fibonacci funtion for practice with cython 
subtitle: How to tweak the performance with cython 
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/18/Fibonacci_function/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Fibonacci Fun 

This is for practice for Cython extension 

Firts, Let's make **fib.pyx** For Extension module 

{% highlight python linenos %}
from __future__ import print_function

def fib(n):
    """Print the Fibonacci series up to n."""
    a, b = 0, 1
    while b < n:
        print(b, end=' ')
        a, b = b, a + b

    print()
{% endhighlight %}

After it, In this case, we have to make **setup.py** like this: 

{% highlight python linenos %}
from distutils.core import setup
from Cython.Build import cythonize

setup(
    ext_modules=cythonize("fib.pyx"),
)
{% endhighlight %}

Run the following command on prompt: 

> python setup.py build_ext --inplace

The following is the result of running the command above 

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/Fibonacci_fun on git:master x [20:01:00] 
$ ./run.sh 
running build_ext
building 'fib' extension
creating build
creating build/temp.linux-x86_64-3.5
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c fib.c -o build/temp.linux-x86_64-3.5/fib.o
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-Bsymbolic-functions -Wl,-z,relro -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 build/temp.linux-x86_64-3.5/fib.o -o /home/hyunyoung2/Labs/Konltk/Cython/Fibonacci_fun/fib.cpython-35m-x86_64-linux-gnu.so
{% endhighlight %}



Finally, check if it works as python extension module 

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/Fibonacci_fun [18:20:30] 
$ python3 
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fib
>>> fib.fib(200)
1 1 2 3 5 8 13 21 34 55 89 144 
{% endhighlight %}

## Reference 

 - [Cython's Tutorial about Fibonacci fun for Extension module](http://cython.readthedocs.io/en/latest/src/tutorial/cython_tutorial.html)
