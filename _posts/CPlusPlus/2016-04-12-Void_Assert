---
layout: post
title: void assert (int expression) function
subtitle:
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


the content below refers to <a href = "http://www.cplusplus.com/reference/cassert/assert/">cplusplus.com</a> & <a href = "http://en.cppreference.com/w/cpp/error/assert">cppreferenc.com</a>

* assert macro

  - defined in header file <cassert>
<pre>
<code>
#ifdef NDEBUG
#define assert(condition) ((void)0)
#else
#define assert(condition) /*implementation defined*/
#endif
</code>
</pre>

* Parameters

condition - expression of scalar type

* Return value

(none)

```c++
# include <iostream>
//  uncomment to disable assert()
// #define NDEBUG -> this disable assert();
# include <cassert>

int main()
{
  assert(2+2==4)
  std::cout << "Execution contiues past the first assert\n";
  assert(2+2==5)
  std::cout << "Execution contiues past the second assert\n";
}

Possible output :
 when #define NDEBUG is comment :
  a.out: main.cpp:10: int main(): Assertion `2+2==5' failed.
  Execution continues past the first assert
 when #define NDEBUG is not comment: 
  Execution continues past the first assert
  Execution continues past the second assert
```
