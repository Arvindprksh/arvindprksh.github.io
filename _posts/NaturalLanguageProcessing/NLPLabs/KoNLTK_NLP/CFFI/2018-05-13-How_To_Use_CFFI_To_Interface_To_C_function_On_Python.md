---
layout: post
title: CFFI to interface to C function on pyhon
subtitle: Let's see the syntax and macro in Makefile
category: Natural Language Processing Labs
tags: [nlp, konltk, python]
permalink: /2018/05/13/How_To_Use_CFFI_To_Interface_To_C_function_On_Python/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# CFFI tutorial 1

 CFFI is better environment than Ctypes. 
  
 CFFI is python module, so you have to install it with pip
 
 > pip3 install cffi  
  
 Let's see an example code explaining how to use CFFI to interface python with native library.
 
 The code is composed of a Point structure and functions using it.
 
{% highlight c linenos %}
/* Point.h */
/* Simple structure for CFFI example */
typedef struct {
    int x;
    int y;
} Point;

/* point.c */
/* display a Point value */
void show_point(Point point){
   printf("Point in C is (%d, %d)\n", point.x point.y);
}

/* Increment a Point which was passed by value */
void move_point(Point point){
    show_point(point);
    point.x++;
    point.y++;
    show_point(point);
}

/* increment a Point which was passed by reference */
void move_point_by_ref(Point *point){
    show_point(*point);
    point->x++;
    point->y++;
    show_point(*point);
}

/* Return by value */
Point get_default_point(void) {
    static int x_counter = 0; 
    static int y_counter = 0; 
    x_counter++;
    y_counter--;
    return get_point(x_counter, y_counter);
}

Point get_point(int x, int y) {
    Point point = {x, y};
    printf("Return Point   (%d, %d)\n", point.x, point.y);
    return point;
}
{% endhighlight %}

Normally, CFFI has four mode. "ABI"  versus "API" with in-line or out-line mode. 

But I would deal with "API-out-line" mode. Basically "API" is more fast than "ABI"

To cap, you would make c source file using python.h so you can use the shared object as module on python. 

In other words. after writing cpython code, and then you generate c source so creat shared object for python. 

the shared object behave like interface python with c function. 

CFFI automatically make c source file to wrap c functions to use on python code. 

Let's make the library to c interface. 

Basicall, When you use the CFFI, CFFI is used to generate the wrapped c source to be able to call in python with shared object. 

{% highlight python linenos %}
ffi = cffi.FFI()

with open(os.path.join(os.path.dirname(__file__), "point.h)) as f:
    ffi.cdef(f.read()) # here CFFI is using the cdef from cython.
 
ffi.set_source("_point",
    '#include "Point.h"', 
    libraries=["libpoint"], 
    library_dirs=[os.path.dirname(__file__),],
)

ffi.compile()
{% endhighlight %}

If you already have the Point.c and Point.h file. run build_point.py.

> python3 build_point.py  

After it, FFI module generate c source file with **#inlcude <Pythong.h>** like Cpython. 

On the code of CFFI, ffi's set_source function is set up to source information for you to generate with CFFI ffi module. 

first argument is the name of .c file you want to generate. Next is the custom C source you want to insert to C source generated with CFFI ffi module. 

Finally, You need to set up to the information about which libraries you want to link against. 

After running the file, build_point.py, The files generated is the following : 

> \_point.c    
> \_point.o and libpoint.so  
> \_point.cpython-35m-x86_64-linux-gnu.so   

The .so files is interface module you can access on python. 

Specifically speaking, libpoint.so would be accessed by \_point.cpython-35m-x86_64-linux-gnu.so. 

i.e. This way API mode in out-line system utilize two .so files.

one is normal .so from normal c source file, Point.c , like libpoint.so. 

the other is .so file from \_point.c files. 

So \_point.cpython-35m-x86_64-linux-gnu.so would play a role of interface on python. also, to call c function of Point.c, \_point.cpython-35m-x86_64-linux-gnu.so would access .so file from normal c source file in my case like libpoint.so.

From now on, Let's see the python file about how to call the naive c structure and function. 

{% highlight python linenos %}
class Point():
    def __init__(self, x=None, y=None):
        if x:
            self.p = _point.lib.get_point(x, y)
        else:
            self.p = _point.lib.get_default_point()
            
    def show_point(self):
        _point.lib.show_point(self.p)        
{% endhighlight %}

As you can see the code above, it is easy to call using \_point interface module. 

the way you call c function on pyhon is **\_point(interface module name).lib.c_function_name.**

That is it about how to call c function from python inteface module to c function.

## Let's run example code

If you visit [my repository](https://github.com/hyunyoung2/Hyunyoung2_Ctypes-CFFI-SWIG/tree/master/CFFI/tutorial1) for this article example code. 

**you want to use the .so file, you have to configure export LD_LIBRARY_PATH in the current directory which .so file is in like this: **

> export LD_LIBRARY_PATH=$(pwd)  

This is linux load library file like .so file in your current directory

so just type in for linux to search the current directory for shared library 

Then, change the file permission like this:

> chmod 755 build_point.py   
> chmod 755 test_point.py   

After it, you can run the following command : 

> make   

Then the result is : 

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/konltk/Hyunyoung2_Ctypes-CFFI-SWIG/CFFI/tutorial1 on git:master x [21:08:08] 
$ make
gcc -c -Wall -Werror -fpic Point.c
gcc -shared Point.o -o libpoint.so
./build_point.py
./test_point.py
Pass a struct into C
Returning Point    (1, 2)
Point in python is (1, 2)
Point in C      is (1, 2)

Pass by value
Returning Point    (5, 6)
Point in python is (5, 6)
Point in C      is (5, 6)
Point in C      is (6, 7)
Point in python is (5, 6)

Pass by reference
Returning Point    (5, 6)
Point in python is (5, 6)
Point in C      is (5, 6)
Point in C      is (6, 7)
Point in python is (6, 7)

Get Struct from C
Returning Point    (1, 99)
New Point in python (from C) is (1, 99)
Returning Point    (2, 98)
New Point in python (from C) is (2, 98)
Returning Point    (3, 97)
New Point in python (from C) is (3, 97)
Returning Point    (4, 96)
New Point in python (from C) is (4, 96)
{% endhighlight %}

This article is referenced by [Dan Bader's CFFI](https://dbader.org/blog/python-cffi) and [git repository of Dan Bader's CFFI](https://github.com/jima80525/ctypes_example/tree/master/cffi). 

# Reference 

 - [Python's CFFI module](https://cffi.readthedocs.io/en/latest/index.html)
 
 - [Dan Bader's CFFI](https://dbader.org/blog/python-cffi)
 
 - [How to use libffi](https://eli.thegreenplace.net/2013/03/04/flexible-runtime-interface-to-shared-libraries-with-libffi/)

 - [Example git repository about how to use CFFI](https://github.com/wolever/python-cffi-example)
