---
layout: post
title: Extension module on Python2 
subtitle: How to make extension module with CPython
category: Natural Language Processing Labs
tags: [nlp, konltk, cpython]
permalink: /2018/04/21/Extension_Module_With_CPython_On_Python2/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Python2's Building Python with C or C++

If you want make extension module with C or C++ above python 2.7 

First You have to include **Python.h** on top of your c source file which gives you access to the internal Python API used to hook your module into interpreter. it is call CPython C-API.

Before including **Python.h**, install python2.7-dev wit apt on ubuntu like "sudo apt install python2.7-dev"

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
    return Py_BuildValue("i", sts);
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

Finally, You need to define initname function like this :

{% highlight c linenos %}
PyMODINIT_FUNC initspam(void)
{
    (void) Py_InitModule("spam", SpamMethods);
}
{% endhighlight %}

Be careful of the final function, initname have to use method table in python3

When the python program imports module **spam** for first time, initspam() is called.

Let's sum up the previous process :


{% highlight c linenos %}
#include <Python.h>

static PyObject *module_func(PyObject *self, PyObject *args) {
   /* Do your stuff here. */
   Py_RETURN_NONE;
}

static PyMethodDef module_methods[] = {
   { "func", (PyCFunction)module_func, METH_NOARGS, NULL },
   { NULL, NULL, 0, NULL }
};

PyMODINIT_FUNC initModule(void) {
   (void)Py_InitModule(func, module_methods);
}
{% endhighlight %}

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
    return Py_BuildValue("i", sts);
}


static PyMethodDef SpamMethods[] = {
    {"system",  spam_system, METH_VARARGS,
     "Execute a shell command."},

    {NULL, NULL, 0, NULL}        /* Sentinel */
};

PyMODINIT_FUNC
initspam(void)
{
   (void) Py_InitModule("spam", SpamMethods);
}
{% endhighlight %}

> python3 setup.py build_ext \-\-inplace

The following is the result of the command above 

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/CPython/Python2/Normal on git:master x [22:38:25] 
$ ./run.sh 
running build_ext
building 'spam' extension
x86_64-linux-gnu-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -fno-strict-aliasing -Wdate-time -D_FORTIFY_SOURCE=2 -g -fstack-protector-strong -Wformat -Werror=format-security -fPIC -I/usr/include/python2.7 -c Example_of_Python_C_API.c -o build/temp.linux-x86_64-2.7/Example_of_Python_C_API.o
x86_64-linux-gnu-gcc -pthread -shared -Wl,-O1 -Wl,-Bsymbolic-functions -Wl,-Bsymbolic-functions -Wl,-z,relro -fno-strict-aliasing -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -Wdate-time -D_FORTIFY_SOURCE=2 -g -fstack-protector-strong -Wformat -Werror=format-security -Wl,-Bsymbolic-functions -Wl,-z,relro -Wdate-time -D_FORTIFY_SOURCE=2 -g -fstack-protector-strong -Wformat -Werror=format-security build/temp.linux-x86_64-2.7/Example_of_Python_C_API.o -o /home/hyunyoung2/Labs/Konltk/CPython/Python2/Normal/spam.so
{% endhighlight %}

Let's see setup.py 

{% highlight python linenos %}
from distutils.core import setup, Extension

setup(name="test",  version="1.0",\
     ext_modules=[Extension("spam", ["Example_of_Python_C_API.c"])])
{% endhighlight %}

The following is the result using **spam.so** file to import like this:


{% highlight python linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Labs/Konltk/CPython/Python2/Normal on git:master x [22:38:28] 
$ python
Python 2.7.12 (default, Dec  4 2017, 14:50:18) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import spam
>>> spam.system("ls -l")
total 64
drwxrwxr-x 4 hyunyoung2 hyunyoung2  4096  4월 18 22:38 build
-rw-rw-r-- 1 hyunyoung2 hyunyoung2   513  4월 18 22:38 Example_of_Python_C_API.c
-rw-rw-r-- 1 hyunyoung2 hyunyoung2  4665  4월 18 22:34 README.md
-rwxr-xr-x 1 hyunyoung2 hyunyoung2    58  4월 18 22:37 run.sh
-rw-rw-r-- 1 hyunyoung2 hyunyoung2   150  4월 18 22:19 setup.py
-rwxrwxr-x 1 hyunyoung2 hyunyoung2 17120  4월 18 22:36 spam.cpython-35m-x86_64-linux-gnu.so
-rwxrwxr-x 1 hyunyoung2 hyunyoung2 17464  4월 18 22:38 spam.so
0
{% endhighlight %}

# Reference 

 - [Tutorial](https://www.tutorialspoint.com/python/python_further_extensions.htm)
 - [python 2.7 building python with c or c++](https://docs.python.org/2.7/extending/extending.html)
 - [An example for python extension module](https://github.com/python/cpython/blob/master/Modules/xxmodule.c)
