---
layout: post
title: How to use SWIG to wrap the function written in c for using the function on python
subtitle: Let's practice more 
category: Natural Language Processing Labs
tags: [nlp, konltk, swig]
permalink: /2018/05/11/How_To_Use_SWIG_To_Wrap_Function_Written_In_C_With_SWIG/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# SWIG

In this time I will wrap c function with [SWIG](http://www.swig.org/). 

SWIG is a software development tool that connects programs written in C and C++ with a variety of high-level programming languages.

Frist of all, install SWIG on ubuntu:

> sudo apt install SWIG  

When you use SWIG, you need to a interface file called pyflags.i, i.e. the extension is normally **i**. which will be used by [SWIG](http://www.swig.org/)

{% highlight c linenos %}
/* flags.c - Source file */
# include <stdio.h>
# inlcude "flags.h"

int gFlag = 0;

void welcome_msg(char *msg){
    printf("%s\n", msg);
    return;
}

int get_flag(){
    return flag;
}

void set_flag(int flag){
    gFlag = flag;
    return;
}

/* flags.h - Header file */
void welcome_msg(char *msg);
int get_flag();
void set_flag(int flag);
{% endhighlight %}

From now on, you have to write a interface file as shown below for the above c library. 

{% highlight linenos %}
/* pyflags.i - interface file*/
% module flags_wrap
%{
#include "flags.h"
%}

%include "flags.h"
{% endhighlight %}

Let's type in commands to make output files \_flags\_wrap.so with input file pyflags.i. 

{% highlight shell linenos %}
# Step to build python wrapper - build-python-wrapper-so.sh

swig -python pyflags.i
gcc -fPIC -c flags.c pyflags_wrap.c -l/usr/include/python3
ld -shared flags.o pyflags_wrap.o -o _flags_wrap.so
{% endhighlight %}

i.e. Let's see normally how to use SWIG.

{% highlight shell linenos %}
$ cd <path-to-source>
$ swig -<wrap-language> <module-name>.i
$ gcc -c <module-name>.c <module-name>_wrap.c -I<path-to-wrap-language-headers>
$ ld -shared <module-name>.o <module-name>_wrap.o -o _<module-name>.so
{% endhighlight %}

After running "make all", 

the following files is created. 

> flags.o flags_wrap.py _flags_wrap.so pyflags_wrap.c pyflags_wrap.o

Let's execute it on python interpreter.

{% highlight python linenos %}
# In example.py
# from flags_wrap.py 
import flags_wrap
print(flags_wrap.welcome_msg("Hi C, I am from Python"))

flags_wrap.set_flag(1)
print(flags_wrap.get_flag())
{% endhighlight %}

OR You can improt so file.

{% highlight python linenos %}
# In example2.py
# from _flags_wrap.so
import _flags_wrap
print(_flags_wrap.welcome_msg("Hi C, I am from Python"))

_flags_wrap.set_flag(1)
print(_flags_wrap.get_flag())
{% endhighlight %}
In here, I used pytho3, so if implement the python codes above with python2.7, it doesn't work. 

Let's see the result of running the above python files.

{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/konltk/Hyunyoung2_Ctypes-CFFI-SWIG/SWIG/tutorial1 on git:master x [22:42:06] 
$ python3 example2.py  # this _flag_wrap.so
Hi C, I am from Python
None
1

# hyunyoung2 @ hyunyoung2-desktop in ~/konltk/Hyunyoung2_Ctypes-CFFI-SWIG/SWIG/tutorial1 on git:master x [22:43:22] 
$ python3 example.py  # this flag_wrap.py
Hi C, I am from Python
None
1
{% endhighlight %}

If you want to know about this article, vist [my repository](https://github.com/hyunyoung2/Hyunyoung2_Ctypes-CFFI-SWIG/tree/master/SWIG/tutorial1)


# Reference 

 - [SWIG](http://www.swig.org/)
 
 - [SWIG's tutorial](http://www.swig.org/tutorial.html)
 
 - [Another SWIG's reference](http://www.ittc.ku.edu/kusp/kusp_docs/kusp_swig_guide/index.html)
