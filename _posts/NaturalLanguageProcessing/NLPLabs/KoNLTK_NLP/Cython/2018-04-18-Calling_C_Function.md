---
layout: post
title: How to call C function on cython
subtitle: Let's utilize The c standard function on Cython
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/18/Calling_C_Function/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Using C Function

This tutorial describes shortly what you need to know in order to call C library functions from Cython code. 

In here, We will consider a function on Cython with the standard C library. This does not add any dependencies to your code, and it has the additional advantage that Cython already define many such functions for you. So you can easily cimport and use them. 

Let's see an example about how to **cimport**, But before that, we need to know the extension of \*.pyx and \*.pxd. 

## pxd files and pyx files 

**.pyx** is the source the Cython uses as **.c** files. 

In addition to the **.pyx** source files, Cython uses **.pxd** files which work like C header file. i.e. They contain Cython declarations (and sometimes code section) which are only meant for inclusion by Cython modules. 

When you import a **pxd** into a **pyx** module by using the **cimport** keyword. 

- **pxd** files have many use-cases:
 
  - They can be used for sharing external C declarations. 

  - They can contain functions which are well suited for inlining by the C compiler. Such functions should be marked **inline** 

  - When accompanying an equally **pyx** file, they provide a Cython  interface to the Cython module so that other Cython modules can communicate with it using a more efficient protocol than the Python one. 

## atoi example with standar C library

As you already know, Cython defined the library to easily use C standard library on Cython.


{% highlight python linenos %}
# in catoi.pyx 
from libc.stdlib cimport atoi

cdef parse_charptr_to_py_int(char* s):
    assert s is not NULL, "byte string value is NULL"
    return atoi(s)   # note: atoi() has no error detection!
{% endhighlight %}

If you only declare code like thing above, you want to use the c standar library in Python using shared library. You can't 

even when you cythonize the pyx file to generate **.so** file

you got warning compiling like this:

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [11:48:32] 
$ ./run.sh 
Compiling catoi.pyx because it changed.
[1/1] Cythonizing catoi.pyx
running build_ext
building 'catoi' extension
creating build
creating build/temp.linux-x86_64-3.5
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c catoi.c -o build/temp.linux-x86_64-3.5/catoi.o
catoi.c:980:18: warning: ‘__pyx_f_5catoi_parse_charptr_to_py_int’ defined but not used [-Wunused-function]
 static PyObject *__pyx_f_5catoi_parse_charptr_to_py_int(char *__pyx_v_s) {
                  ^
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-Bsymbolic-functions -Wl,-z,relro -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY(e(env(env) 
{% endhighlight %}

then the **.so** files is created like this:

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [11:51:18] C:148
$ ll
total 148K
drwxrwxr-x 3 hyunyoung2 hyunyoung2 4.0K  4월 18 11:48 build
-rw-rw-r-- 1 hyunyoung2 hyunyoung2  92K  4월 18 11:48 catoi.c
-rwxrwxr-x 1 hyunyoung2 hyunyoung2  37K  4월 18 11:48 catoi.cpython-35m-x86_64-linux-gnu.so
-rw-rw-r-- 1 hyunyoung2 hyunyoung2  344  4월 18 11:48 catoi.pyx
-rwxr-xr-x 1 hyunyoung2 hyunyoung2   59  4월 18 11:44 run.sh
-rw-rw-r-- 1 hyunyoung2 hyunyoung2  244  4월 18 11:45 setup.py
{% endhighlight %}

When you use **.so** file on python using **import** keyword. 

you can't use the **cdef parse_charptr_to_py_int(char* s)** function on python. 

Let's check it

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [11:48:40] 
$ python3 
Python 3.5.2 (default, Nov 23 2017, 16:37:01)
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import catoi
>>>
>>> catoi.__
catoi.__class__(         catoi.__ge__(            catoi.__name__           catoi.__sizeof__(
catoi.__delattr__(       catoi.__getattribute__(  catoi.__ne__(            catoi.__spec__
catoi.__dict__           catoi.__gt__(            catoi.__new__(           catoi.__str__(
catoi.__dir__(           catoi.__hash__(          catoi.__package__        catoi.__subclasshook__(
catoi.__doc__            catoi.__init__(          catoi.__reduce__(        catoi.__test__
catoi.__eq__(            catoi.__le__(            catoi.__reduce_ex__(
catoi.__file__           catoi.__loader__         catoi.__repr__(
catoi.__format__(        catoi.__lt__(            catoi.__setattr__(
{% endhighlight %}

As you can see thing above, **catoi** module doesn't have **parse_charptr_to_py_int** function. 

If you want to use the function above on python using **.so** file. 

there is two ways you have to wrap parse_charptr_to_py_int with python function,**def**. or cpdef keyword. 

First, Let's see wrapping the function with python keyword, **def**.

{% highlight python linenos %}
#In catoi.pyx

from libc.stdlib cimport atoi

cdef parse_charptr_to_py_int(char* s):
    assert s is not NULL, "byte string value is NULL"
    print(s)
    return  atoi(s)   # note: atoi() has no error detection!

def atoi_cython(char* s):
    print("parse_charptr_to_py_int fucntion called!")
    return parse_charptr_to_py_int(s)
{% endhighlight %}

As you can see the code above, recomplie the code with cythonize like 

> python3 setup.py build_ext --inplace  

you would get the messages like this : 

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [12:53:55] 
$ ./run.sh 
Compiling catoi.pyx because it changed.
[1/1] Cythonizing catoi.pyx
running build_ext
building 'catoi' extension
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c catoi.c -o build/temp.linux-x86_64-3.5/catoi.o
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-Bsymbolic-functions -Wl,-z,relro -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 build/temp.linux-x86_64-3.5/catoi.o -o /home/hyunyoung2/Labs/Konltk/Cython/6.Calling_C_Function/atoi/catoi.cpython-35m-x86_64-linux-gnu.so
(env) 
{% endhighlight %}

After that, run the python interpreter. 

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [12:54:01] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import catoi
>>> catoi.
catoi.__class__(         catoi.__ge__(            catoi.__name__           catoi.__sizeof__(
catoi.__delattr__(       catoi.__getattribute__(  catoi.__ne__(            catoi.__spec__
catoi.__dict__           catoi.__gt__(            catoi.__new__(           catoi.__str__(
catoi.__dir__(           catoi.__hash__(          catoi.__package__        catoi.__subclasshook__(
catoi.__doc__            catoi.__init__(          catoi.__reduce__(        catoi.__test__
catoi.__eq__(            catoi.__le__(            catoi.__reduce_ex__(     catoi.atoi_cython(
catoi.__file__           catoi.__loader__         catoi.__repr__(          
catoi.__format__(        catoi.__lt__(            catoi.__setattr__(   
>>> catoi.atoi_cython("123".encode("UTF-8"))
parse_charptr_to_py_int fucntion called!
123
{% endhighlight %}

You can check the function, catoi.ato_cython() function. 

Aslo, if you don't want to use **def** keyword,  use cpdef like this: 


{% highlight python linenos %}
## in catoi.pyx

from libc.stdlib cimport atoi

cpdef parse_charptr_to_py_int(char* s):
    assert s is not NULL, "byte string value is NULL"
    print(s)
    return  atoi(s)   # note: atoi() has no error detection!
{% endhighlight %}

Let's see the result if you use **cpdef** keyword.

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/atoi on git:master x [14:31:27] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import catoi
>>> catoi.
catoi.__class__(                catoi.__gt__(                   catoi.__reduce__(
catoi.__delattr__(              catoi.__hash__(                 catoi.__reduce_ex__(
catoi.__dict__                  catoi.__init__(                 catoi.__repr__(
catoi.__dir__(                  catoi.__le__(                   catoi.__setattr__(
catoi.__doc__                   catoi.__loader__                catoi.__sizeof__(
catoi.__eq__(                   catoi.__lt__(                   catoi.__spec__
catoi.__file__                  catoi.__name__                  catoi.__str__(
catoi.__format__(               catoi.__ne__(                   catoi.__subclasshook__(
catoi.__ge__(                   catoi.__new__(                  catoi.__test__
catoi.__getattribute__(         catoi.__package__               catoi.parse_charptr_to_py_int(
>>> catoi.parse_charptr_to_py_int("123".encode("UTF8"))
123
{% endhighlight %}

As you can see the result, you check the name to call function with :

That is **catoi.parse_charptr_to_py_int**.

from now on, I will deal with several examples. 

## CPython 

If you want to use CPython C-API on Cython, You can.

Let's test some cython file about CPython version your code is be complied with. 


{% highlight python linenos %}
from cpython.version cimport PY_VERSION_HEX

# print version >= 3.2 final ?
print(PY_VERSION_HEX >= 0x030200F0)
{% endhighlight %}

> python3 setup.py build_ext --inplace

The resulting import is : 

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/PY_version on git:master x [14:41:08] C:127
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import Cpython_version
True
{% endhighlight %}

## sin function from the C standard library

In sin.pyx file 

{% highlight python linenos %}
from libc.math cimport sin

cdef double f(double x):
    return sin(x*x)

# For the function above, cdef double f(double x):
def sin_f(double x):
    print("f function called!")
    return f(x)

cpdef double f1(double x):
    return sin(x*x)
{% endhighlight %}

import it : 


{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/6.Calling_C_Function/sin on git:master x [14:49:37] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sin
>>> sin.
sin.__class__(         sin.__format__(        sin.__loader__         sin.__reduce_ex__(     sin.__test__
sin.__delattr__(       sin.__ge__(            sin.__lt__(            sin.__repr__(          sin.f1(
sin.__dict__           sin.__getattribute__(  sin.__name__           sin.__setattr__(       sin.sin_f(
sin.__dir__(           sin.__gt__(            sin.__ne__(            sin.__sizeof__(        
sin.__doc__            sin.__hash__(          sin.__new__(           sin.__spec__           
sin.__eq__(            sin.__init__(          sin.__package__        sin.__str__(           
sin.__file__           sin.__le__(            sin.__reduce__(        sin.__subclasshook__(  
>>> type(sin.sin_f(1))
f function called!
<class 'float'>
>>> sin.sin_f(1)
f function called!
0.8414709848078965
>>> type(sin.f1(1))
<class 'float'>
>>> sin.f1(1)
0.8414709848078965
{% endhighlight %}

If you want to see all in here, visit [hyunyoung2_Cpython_and_Cython/Cython/6.Calling_C_Function/](https://github.com/hyunyoung2/hyunyoung2_Cpython_and_Cython/tree/master/Cython/6.Calling_C_Function)

There are several files, demo.pxd, demo.pyx. 

Run the shell script, run.sh

> ./run.sh

# Reference
 
 - [Calling c function](http://docs.cython.org/en/latest/src/tutorial/external.html)

 - [How to make extension module with Cython](https://www.artemisconsultinginc.com/writing-c-extension-python-using-cython)

 - [pxd files](http://cython.readthedocs.io/en/latest/src/tutorial/pxd_files.html)
