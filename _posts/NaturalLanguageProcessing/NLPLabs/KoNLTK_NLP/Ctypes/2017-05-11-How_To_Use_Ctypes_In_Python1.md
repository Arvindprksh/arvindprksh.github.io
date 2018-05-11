---
layout: post
title: How to wrapping function written in another language with ctypes
subtitle: how to use ctypes
category: Natural Language Processing Labs
tags: [nlp, konltk, ctypes]
permalink: /2017/05/11/How_To_Use_Ctypes_In_Python1/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# How can I be available of ctypes to connect external library on python wrapping it. 

I would explain how to use ctypes to call the foreign library in python. 

That is the built-in ctypes module in python, allowing you to use existing libraries in other language byt writing simple wrapper in Python itself.

Let's simple example : 

First 

```c 
int simple_function(void) {
    static int couter = 0;
    counter++;
    return coutner;
}
```

The simple_function function simply returns counting numbers. Each time it called in increments counter and returns that value. 

```c
void add_one_to_string(char *input){
   int ii = 0;
    for (; ii < strinlen(input): ii++){
        input[ii]++;
    }
}
```

With the function above, we talk about python's immutable strings. 

```c 
char* alloc_C_string(voie){
   char* phrase = strdup("I was written in C");
   printf("C just allocated %p(%ld): %s\n", 
           phrase, (long int)phrase, phrase);
   return phrase;
}

void free_C_string(char* ptr) {
   printf("About to free %p(%ld): %s\n",
         ptr, (long int)ptr, ptr);
   free(ptr);
}
```

with the function above, I would talk about memory management. 


## Loading a C Library with python's built-in module, Ctypes

Ctypes allows you to  load a shared library("DLL" on Windows) and access methods directly from it, 

```python
import ctypes

# Load the shared library into c types.
libc = ctypes.CDLL("./dynamic_library.so")
```

If you want to call c funtion called simple_function() defined before. Ctypes makes it easier. 

```python
import ctypes

# Load the shared library into c types. 
libc = ctypes.CDLL("./your_dynamic_library")

# Call the C function from the Library
counter = libc.simple_function()
```

Basic types, ints, and floats generally get marshalled byt ctypes trivially, But in python string is immutable. 

So string cannot change in python. that is problem when you use string as arguement.

Let's see the exmaple 

```python
print("Calling C function which tries to modify Python string")
original_string = "starting string"
print("Before:", original_string)

# This call does not change value, even though it tries!
libc.add_one_to_string(original_string)

print("After:", original_strin)
```

the thing above results in this output

```shell
Calling C function which tries to modify Python string")
Before: starting string
After: straring string
```

As you know, after some testing, there is nothing of changes. So In this time. I need a little marshalling work.

i.e. We need to  convert the original string bytes using str.encode, and then pass this to the constructor for a ctypes.string_buffer.String_buffers are Mutable. 

and they are passed to C as a char * as you would expect.

```python
# The ctypes strings buffer is mutable, however. 
print("Calling C function with mutable buffer this time")

# Need to encode the orifinal to get bytes for string_buffer
mutable_string = cytpes.create_string_buffer(str.encode(original_string))

print("Before:", mutable_string.value)
libc.add_one_to_string(mutable_string) # Works!
print("After:", mutable_string.value)
```
The result is like this:

```shell
Calling C function with mutable buffer this time
Before: b'string string'
After: b'tubsujoh!tusjoh'
```

As you can check on the above, string_buffer is printed as a byte arrary on the Python side.

you can specify the return type of c function then this is necessary work, because each of the functions in the loaded library is actually a Python object which has its own properties. 

```python
alloc_func = libc.alloc_C_string
alloc_func.restype = ctypes.POINTER(ctypes.c_char)
```

Also you can specify the types of any argument passed into the C function by setting the argtypes property to a list of types like this:

```python
free_func = libc.free_C_string
free_func.argtypes = [ctypes.POINTER(ctypes.c_char),]
```

**One thing you need to keep in mind is when you allocate memory in c part, you have to free it in c passing in c language function.**

This content and tutorial is [Dan Bader's tutorial1](https://dbader.org/blog/python-ctypes-tutorial)

also the code is from [git repository in dan Bader](https://github.com/jima80525/ctypes_example/tree/master/tutorial1)

# Referenc

 - [Dan Bader's tutorial](https://dbader.org/blog/python-ctypes-tutorial)
 
 - [The tutorial Github repository](https://github.com/jima80525/ctypes_example)
