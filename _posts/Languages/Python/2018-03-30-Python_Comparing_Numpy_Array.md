---
layout: post
title: How to compare two arrary on numpy module
subtitle: np.all() vs np.any()
category: Python
tags: [python, tip, numpy]
permalink: /2018/03/30/Python_Comparing_Numpy_Array/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


# How to compare two array of numpy to get which one is greater than another one


When you compare a array to another array with numpy module. You would meet a error like this:

> ValueError: The truth value of an array with more than one element is ambiguous. Use a.any() or a.all()

In order to solve this problem. Use np.all() as follows :


{% highlight python linenos %}
>>> import numpy as np
>>> a = np.array([1,2,3,4,5])
>>> b = np.array([6,7,8,9,10])
>>> c = np.array([1,2,3,9,5])
>>> if np.all(a > b):
...     print("test")
... else:
...     print("what")
... 
what
>>> if np.any(c > a):
...     print("any")
... 
any
{% endhighlight %}

# Reference 

 - [Stackoverflow](https://stackoverflow.com/questions/25760183/comparing-values-in-two-numpy-arrays-with-if)
