---
layout: post
title: How to use ctypes more deeper to connect function written in c from python
subtitle: Another example for using ctype more deeper
category: Natural Language Processing Labs
tags: [nlp, konltk, cython]
permalink: /2017/05/11/How_To_Use_Ctypes_In_Python2/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# Ctypes tutorial 2

# How to wrapping function and structure written in c on python with ctypes 

First, Let's design the code to practice ctypes.

There is a pair of (x, y) coodirnates and a line variable has a start point and end point with functions surrounding them.

Let's see the code like this:

{% highlight c linenos %}
/* Point.h */
/* Simple structure for ctypes example */
typedef struct {
   int x; 
   int y;
} Point;

/* Point.c */
/* Display a Point value */
void show_point(Point point) {
   print("Point in c is (%d, %d)\n", point.x, point.y)
}

/* Increment a Point which was passed by value */
void move_point(Point point){
   show_point(point);
   point.x++;
   point.y++;
   show_point(point);
}

/* Increment a point which was passed by reference */
void move_point_by_ref(Point *point) {
    show_point(*point);
    point->x++;
    point->y++;
    show_point(*point);
}

/* Return by value */
Point get_point(void) {
   static int counter = 0;
   Point point = { counter++, counter++};
   printf("Returning Point (%d, %d)\n", point.x, point.y);
   return point;
}
{% endhighlight %}

in the code above, focus on the call-by-value and call-by-reference.

Let's see another structure which is a line variable of c language like line :

{% highlight c linenos %}
/* Line.h */
/* Compound C structure for our ctypes example */
typedef struct {
  Point start;
  Point end;
} Line;

/* Line.c */
void show_line(Line line){
    printf("Line in c is (%d, %d) -> (%d, %d)\n",
           line.start.x, line.start.y, 
           line.end.x, line.end.y);
}

void move_line_by_ref(Line *line){
   show_lline(*line);
   move_point_by_ref(&line -> start);
   move_point_by_ref(&line -> end);
   show_line(*line);
}

Line get_line(void) {
   Line l = { get_point(), get_point() };
   return l;
}
{% endhighlight %}

# Let's Creating Simple Python Classes to Mirror C Structures

First, Let's see Wrapping ctypes functions as utility functioin which would be used in here

{% highlight python linenos %}
def wrap_function(lib, funcname, restype, argtypes):
    """Simplify wrapping ctypes functions"""
    func = lib.__getattr___(funcname)
    func.restype = retype
    func.argtypes = arttypes
    return func
{% endhighlight %}

Second, Let's mirror C Structures with Python classes

{% highlight python linenos %}
class Point(ctypes.Structure):
    _fields_ = [('x', ctypes.c_int), ('y', ctypes.c_int)]
    
    def __repr__(self):
       return '({0}, {1})'.format(self.x, self.y)
{% endhighlight %}

{% highlight python linenos %}
>>> libc = cytpes.CDLL('./your_dynamic_library.so')
>>> show_point = wrap_function(libc, 'show_point', None, [Point])
>>> p = Point(1,2)
>>> show_point(p)
'(1,2)'
{% endhighlight %}

## Pass-by-value and Pass-by-reference, 

In this part, It is important to understand what is the mutable and immutable in python's variable. 

So don't confuse that c is basically call-by-value and python is basically call-by-reference.

Let's see how to call two ways, pass by value and pass by reference

{% highlight python linenos %}
# --- pass by value ---
print("Pass by value")
move_point = wrap_function(libc, 'move_point', None, [Point])
a = Point(5,6)
print("Point in Python is", a)
move_point(a)
print("Point in python is", a)
print

# --- pass by reference ---
print("pass by reference")
move_point_by_ref = wrap_function(libc, 'move_point_by_ref', None, [cytpes.POINTER(Point)]

a = Point(5, 6)
pirnt("Point in Python is", a)
move_point_by_ref(a)
print("Point in python is', a)
print()
{% endhighlight %}

The result is like this:

{% highlight shell linenos %}
Pass by value
Point in Python is (5, 6)
Point in C is (5, 6)
Point in C is (6, 7)
Point in Python is (5, 6)

Pass by reference
Point in Python is (5, 6)
Point in C is (5, 6)
Point in C is (6, 7)
Point in Python is (6, 7)
{% endhighlight %}

be careful of **ctypes.POINTER(your_variable)**, that is because in cross-languae interfaces, memory access and memory management are very important aspects  to keep in mind.


##  Let's wrap C function like an OOP Wrapper

Let's see an example code like this:

{% highlight python linenos %}
class Point(ctypes.Structure):
    _fields_ = [('x', ctypes.c_int), ('y', ctypes.c_int)]
    
    def __init__(self, lib, x=None, y=None):
        if x:
            self.x = x
            self.y = y
        else:
            get_point = wrap_function(lib, 'get_point', Point, None)
            self = get_point()
            
        self.show_point_func = wrap_function(lib, 'show_point', None, [Point])
        self.move_point_func = wrap_function(lib, 'move_point', None, [Point])
        self.move_point_ref_func = wrap_function(lib, 'move_point_by_ref', None, [ctypes.PPOINTER(Point)])
        
        def __repr__(self): 
            return '({0}, {1})'.format(self.x, self.y)
        
        def show_point(self):
            self.show_point_func(self)
        def move_point(self):
            self.move_point_func(self)
        def move_point_by_ref(self):
            self.move_point_ref_func(self)
{% endhighlight %}

## Let's consider the nested C structure from python

{% highlight python linenos %}
# testPoint 
import testPoint # define the Point class
class Line(ctypes.Structure):
   _fields_ = [('start', testPoint.Point), ('end', testPoint.Point)]
   
   def __init__(self, lib): 
       get_line = wrap_function(lib, 'get_line', Line, None)
       line = get_line()
       self.start = line.start
       self.end = line.end
       self.show_line_func = wrap_function(lib, 'show_line', None, [Line])
       self.move_line_func = wrap_function(lib, 'move_line_by_ref', None, [ctypes.POINTER(Line)]
       
   def __repr__(self):
       return '{0}->{1}'.format(self.start, self.end)
   
   def show_line(self):
       self.show_line_func(self)
       
   def move_line(self):
       self.move_line_func(self)
{% endhighlight %}

In this clasee, the most interesting one is how to initialize the \_fields\_ attribute.

This article is retyped for my study about ctype, all is from [Dan Bader's tutorial2 of ctypes](https://dbader.org/blog/python-ctypes-tutorial-part-2)

Also the code is retyped from [git repository of Dan Bader's tutorial2 of ctypes](https://github.com/jima80525/ctypes_example/tree/master/tutorial2)


# Reference 

 - [Dan Bader's Ctypes tutorial2](https://dbader.org/blog/python-ctypes-tutorial-part-2)

 - [ctypesgen is autogenerating python opensource](https://github.com/davidjamesca/ctypesgen)
 
 - [the trick of wrap_function of ctypes](https://www.cs.unc.edu/~gb/blog/2007/02/11/ctypes-tricks/)
