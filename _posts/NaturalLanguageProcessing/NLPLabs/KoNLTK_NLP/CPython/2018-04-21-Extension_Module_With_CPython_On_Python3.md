---
layout: post
title: Extension module with CPython on Python3
subtitle: How to make Extension module with CPython on Python3
category: Natural Language Processing Labs
tags: [nlp, konltk]
permalink: /2018/04/21/Extension_Module_With_CPython_On_Python3/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Python3's Building Python with C or C++

If you want make extension module with C or C++ above python 3.x, 

First You have to include **Python.h** on top of your c source file which gives you access to the internal Python API used to hook your module into interpreter. it is call CPython C-API.

Before including **python.h**, check if you have installed python3-dev with apt like **sudo apt install python3-dev**

Then You need to connect c source file to python. Normally The signature of the C implementation of your function always takes one of the following three times:

{% highlight c linenos %}
static PyObject *MyFunction( PyObject *self, PyObject *args );

static PyObject *MyFunctionWithKeywords(PyObject *self,
                                 PyObject *args,
                                 PyObject *kw);

static PyObject *MyFunctionWithNoArgs( PyObject *self );
{% endhighlight %}

i.e. You need to define python module function, its c function usually are named by combination the Python module and function names together like this :

{% highlight c linenos %}
static PyObject *module_func(PyObject *self, PyObject *args) {
   /* Do your stuff here. */
   Py_RETURN_NONE;
}
{% endhighlight %}

The following example :

{% highlight c linenos %}
static PyObject * spam_system(PyObject *self, PyObject *args)
{
    const char *command;
    int sts;

    if (!PyArg_ParseTuple(args, "s", &command))
        return NULL;
    sts = system(command);
    return PyLong_FromLong(sts);
}
{% endhighlight %}


Second, you need to define method structure like this :

{% highlight c linenos %}
struct PyMethodDef {
   char *ml_name;
   PyCFunction ml_meth;
   int ml_flags;
   char *ml_doc;
};
{% endhighlight %}

-  ml_name − This is the name of the function as the Python interpreter presents when it is used in Python programs.

-  ml_meth − This must be the address to a function that has any one of the signatures described in previous seection.

-  ml_flags − This tells the interpreter which of the three signatures ml_meth is using.

   -  This flag usually has a value of METH_VARARGS.

   -  This flag can be bitwise OR'ed with METH_KEYWORDS if you want to allow keyword arguments into your function.

   -  This can also have a value of METH_NOARGS that indicates you do not want to accept any arguments.

- ml_doc − This is the docstring for the function, which could be NULL if you do not feel like writing one.


The following is example.


{% highlight c linenos %}
static PyMethodDef SpamMethods[] = {
    ...
    {"system",  spam_system, METH_VARARGS,
     "Execute a shell command."},
    ...
    {NULL, NULL, 0, NULL}        /* Sentinel */
};
{% endhighlight %}

As you can see above thing, this method table needs to be terminated a sentinel that consists of NULL and 0 Value for the appropriate members.

Third, you need to define module table in python3 like this :

{% highlight c linenos %}
static struct PyModuleDef spammodule = {
   PyModuleDef_HEAD_INIT,
   "spam",   /* name of module */
   spam_doc, /* module documentation, may be NULL */
   -1,       /* size of per-interpreter state of the module,
                or -1 if the module keeps state in global variables. */
   SpamMethods
};
{% endhighlight %}


This struction must be passed to the interpreter in the module's initialization function. the initialization function must be named PyInit_name(), where name is the name of the module, and should be the only non-static item defined in the module file: 

Finally, You need to define PyInit function like this :

{% highlight c linenos %}
PyMODINIT_FUNC PyInit_spam(void)
{
    return PyModule_Create(&spammodule);
}
{% endhighlight %}


Be careful of the final function, PyInit_function have to use PyModule_Create(&module_table) in python3


But If you want to use multi-phase initialization as Python source distribution as **Modules/xxmodule.c** like this : 

{% highlight c linenos %}
static struct PyModuleDef xxmodule = {
    PyModuleDef_HEAD_INIT,
    "xx",
    module_doc,
    0,
    xx_methods,
    xx_slots,
    NULL,
    NULL,
    NULL
};

/* Export function for the module (*must* be called PyInit_xx) */

PyMODINIT_FUNC
PyInit_xx(void)
{
    return PyModuleDef_Init(&xxmodule);
}
{% endhighlight %}

This is using **PyModuleDef_Init(&xxmodule)** and look at module table, xxmodule,above.


From now on, just see an example. 

{% highlight c linenos %}
## In Example_of_Python_C_API.c

#include <Python.h>

static PyObject *
spam_system(PyObject *self, PyObject *args)
{
    const char *command;
    int sts;

    if (!PyArg_ParseTuple(args, "s", &command))
        return NULL;
    sts = system(command);
    return PyLong_FromLong(sts);
}


static PyMethodDef SpamMethods[] = {
    {"system",  spam_system, METH_VARARGS,
     "Execute a shell command."},

    {NULL, NULL, 0, NULL}        /* Sentinel */
};

static char spam_doc [] =
   "helloworld( ): Any message you want to put here!!\n";

static struct PyModuleDef spammodule = {
   PyModuleDef_HEAD_INIT,
   "spam",   /* name of module */
   spam_doc, /* module documentation, may be NULL */
   -1,       /* size of per-interpreter state of the module,
                or -1 if the module keeps state in global variables. */
   SpamMethods
};

PyMODINIT_FUNC
PyInit_spam(void)
{
    return PyModule_Create(&spammodule);
}
{% endhighlight %}

> python3 setup.py build_ext \-\-inplace

The following is the result of the command above 

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/CPython/Python3 on git:master x [21:55:36] 
$ ./run.sh 
running build_ext
building 'spam' extension
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/usr/include/python3.5m -c Example_of_Python_C_API.c -o build/temp.linux-x86_64-3.5/Example_of_Python_C_API.o
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-Bsymbolic-functions -Wl,-z,relro -g -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 build/temp.linux-x86_64-3.5/Example_of_Python_C_API.o -o /home/hyunyoung2/Labs/Konltk/CPython/Python3/spam.cpython-35m-x86_64-linux-gnu.so
{% endhighlight %}

Let's see setup.py 

{% highlight python linenos %}
from distutils.core import setup, Extension

setup(name="test",  version="1.0",\
     ext_modules=[Extension("spam", ["Example_of_Python_C_API.c"])])
{% endhighlight %}

The following is the result using **spam.so** file to import like this:

{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/CPython/Python3 on git:master x [21:59:41] 
$ python3
Python 3.5.2 (default, Nov 23 2017, 16:37:01) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import spam
>>> spam.
spam.__class__(         spam.__file__           spam.__init__(          spam.__new__(           spam.__sizeof__(
spam.__delattr__(       spam.__format__(        spam.__le__(            spam.__package__        spam.__spec__
spam.__dict__           spam.__ge__(            spam.__loader__         spam.__reduce__(        spam.__str__(
spam.__dir__(           spam.__getattribute__(  spam.__lt__(            spam.__reduce_ex__(     spam.__subclasshook__(
spam.__doc__            spam.__gt__(            spam.__name__           spam.__repr__(          spam.system(
spam.__eq__(            spam.__hash__(          spam.__ne__(            spam.__setattr__(       
>>> spam.system("ls -l")
total 36
drwxrwxr-x 3 hyunyoung2 hyunyoung2  4096  4월 18 21:54 build
-rw-rw-r-- 1 hyunyoung2 hyunyoung2   898  4월 18 21:55 Example_of_Python_C_API.c
-rwxr-xr-x 1 hyunyoung2 hyunyoung2    59  4월 18 21:53 run.sh
-rw-rw-r-- 1 hyunyoung2 hyunyoung2   150  4월 18 21:59 setup.py
-rwxrwxr-x 1 hyunyoung2 hyunyoung2 17816  4월 18 21:55 spam.cpython-35m-x86_64-linux-gnu.so
0
{% endhighlight %}

# Reference 

 - [Tutorial](https://www.tutorialspoint.com/python/python_further_extensions.htm)
 - [python 3.5 building python with c or c++](https://docs.python.org/3.5/extending/extending.html)
 - [An example for python extension module](https://github.com/python/cpython/blob/master/Modules/xxmodule.c)
 - [Youtube](https://www.youtube.com/watch?v=bfmslcTKriw)
