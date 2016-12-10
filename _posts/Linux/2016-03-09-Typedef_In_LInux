---
layout: post
title: typedef In kernel
subtitle: what is the typedef in kernel
css:
tags:
date:
big-image:
share-image:
permalink:
comments:
show-share:
big-image:
meta-title:
meta-description:
---

while seeing kernel source, I wonder Statement like "typedef int function (int * , int);" 

so, I find out that mean.

```c
typedef int F(void); // type F is "function with no parameters
                     // returning int"
F f, g; // f and g both have type compatible with F
F f { /* ... */ } // WRONG: syntax/constraint error
F g() { /* ... */ } // WRONG: declares that g returns a function
int f(void) { /* ... */ } // RIGHT: f has type compatible with F
int g() { /* ... */ } // RIGHT: g has type compatible with F
F *e(void) { /* ... */ } // e returns a pointer to a function
F *((e))(void) { /* ... */ } // same: parentheses irrelevant
int (*fp)(void); // fp points to a function that has type F
F *Fp; //Fp points to a function that has type F\
```

more identify above <a href = "http://stackoverflow.com/questions/4574985/typedef-a-functions-prototype"> this site </a>

I refer to <a href = "http://stackoverflow.com/questions/4574985/typedef-a-functions-prototype"> the site </a>
