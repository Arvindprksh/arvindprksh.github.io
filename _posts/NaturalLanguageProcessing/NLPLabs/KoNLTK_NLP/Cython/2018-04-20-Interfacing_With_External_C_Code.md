---
layout: post
title: Interfacing with External C code
subtitle: Let's practice
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2018/04/20/Interfacing_With_External_C_Code/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Interfacing with External C code 

Cython module can be used as a bridge to allow Python code to call C code, it can also be used to allow C code to call python code. 

{% highlight python linenos %}
cdef extern from "spam.h":
    int spam_counter
    void order_spam(int tons)
{% endhighlight %}

The **cdef extern from clause** does three things: 

  - It directs Cython to place a **#include** statement for the named header file in the generated C code.
  - It prevents Cython from generating any C code for the declarations found in the associated block
  - It treats all declarations within the block as though they started with cdef extern 

## Implementing function in C

When you want to call c code from a Cython module, usually that code will be in some external library that you link your extension against. However, you can also directly complie C(or C++) as part of your Cython module. In the **.pyx** file, you can put something like:

{% highlight python linenos %}
cdef extern from "spam.c":
   void order_spam(init tons)
{% endhighlight %}

Cython will assume that the function **order_spam()** is defined in the **spam.c**. If you also want to cimport this function from another module, it must be declared(not extern) in the **.pxd** file like this:

{% highlight python linenos %}
 cdef void order_spam(int tons)
{% endhighlight %}

For this to work, The signature of **order_spam()** in spam.c must match the signature that Cython uses, in particular the function must be static:

{% highlight python linenos %}
static void order_spam(int tons)
{
   printf("Ordered %i tons of spam!\n", tons);
}
{% endhighlight %}

From now on, Let's see some example with multiple **.c** files and **.h** file to make extension module on Cython 

I have **add.c**, **add.h**, **main.c**, **substraction.c** and **substraction.h** as C files.


{% highlight c linenos %}
## In the add.c 
int sum_function(int a, int b){
     return a + b;
}

## In the add.h
int sum_function(int a, int b);

## In the substraction.c
int substraction_function(int a, int b){

    if (a > b) {
        return a - b;
    }
    else {
        return b - a;
    }
}

## In the substraction.h
int substraction_function(int a, int b);
 
## In the main.c
#include <stdio.h>
#include "add.h"
#include "substraction.h"


int main(){
   int test_a = 2;
   int test_b = 3;
   int result = 0;


   result = sum_function(test_a, test_b);
   printf("the result of sum_function : %d\n", result);

   result = substraction_function(test_a, test_b);
   printf("the result of substraction : %d\n", result);
   return 0:
}
{% endhighlight %}

As you can know, **main.c** show you printf statement of the result using **sum.c** and **substractioin.c**. 

If you want to compile the main.c, run **one_shot_compiling.sh**. 

> ./one_shot_compiling.sh

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/7.Calling_external_C_function on git:master x [19:33:24] 
$ ./one_shot_compiling.sh 
the result of sum_function : 5
the result of substraction : 1
{% endhighlight %}

Let's make extension module with these external c file and Cython. 

First, you make the header file like **.pxd** file to include c code using into Cython module. 

{% highlight python linenos %}
## In the c_function.pxd

cdef extern from "add.h":
    int sum_function(int a, int b)

cdef extern from "substraction.h":
    int substraction_function(int a, int b)
{% endhighlight %}


And Cython's source file is **.pyx** file to wrap the c code to use from python. 

{% highlight python linenos %}
## In the function.pyx
from c_function cimport sum_function, substraction_function
cimport cython

def sum(int a, int b):
    print("sum function is called!")
    return sum_function(a, b)

def substraction(int a, int b):
    print("substraction function is called!")
    return substraction_function(a, b)
{% endhighlight %}


For now, You can make **.so** file with **.c** and **.pyx** files. 

Let's see how to make it with **setup.py**

{% highlight python linenos %}
## In the setup.py

from distutils.core import setup
from distutils.extension import Extension
from Cython.Build import cythonize

ext_modules = [Extension("operator",sources =["function.pyx", "add.c", "substraction.c"])]

setup(
    name="sum and substraction function",
    ext_modules = cythonize(ext_modules)
)
{% endhighlight %}

If you run the command like this:

> python3 setup.py build_ext \-\-inplace

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/7.Calling_external_C_function on git:master x [20:23:32] 
$ ./run.sh 
Compiling function.pyx because it changed.
[1/1] Cythonizing function.pyx
running build_ext
building 'operator' extension
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I. -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c function.c -o build/temp.linux-x86_64-3.5/function.o
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I. -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c add.c -o build/temp.linux-x86_64-3.5/add.o
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I. -I/home/hyunyoung2/Labs/Konltk/Cython/env/include -I/usr/include/python3.5m -c substraction.c -o build/temp.linux-x86_64-3.5/substraction.o
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-Bsymbolic-functions -Wl,-z,relro -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 build/temp.linux-x86_64-3.5/function.o build/temp.linux-x86_64-3.5/add.o build/temp.linux-x86_64-3.5/substraction.o -o /home/hyunyoung2/Labs/Konltk/Cython/7.Calling_external_C_function/operator.cpython-35m-x86_64-linux-gnu.so
(env) 
{% endhighlight %}

And then run the python interpreter

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/Cython/7.Calling_external_C_function on git:master x [20:23:34] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import operator
>>> operator.
operator.__class__(         operator.__file__           operator.__init__(          operator.__new__(           operator.__sizeof__(        operator.sum(
operator.__delattr__(       operator.__format__(        operator.__le__(            operator.__package__        operator.__spec__           
operator.__dict__           operator.__ge__(            operator.__loader__         operator.__reduce__(        operator.__str__(           
operator.__dir__(           operator.__getattribute__(  operator.__lt__(            operator.__reduce_ex__(     operator.__subclasshook__(  
operator.__doc__            operator.__gt__(            operator.__name__           operator.__repr__(          operator.__test__           
operator.__eq__(            operator.__hash__(          operator.__ne__(            operator.__setattr__(       operator.substraction(      
>>> operator.sum(1,2)
sum function is called!
3
>>> operator.substraction(2,3)
substraction function is called!
1
{% endhighlight %}


# Reference 

 - [external c code](http://cython.readthedocs.io/en/latest/src/userguide/external_C_code.html)

 - [compilation](http://cython.readthedocs.io/en/latest/src/reference/compilation.html)

