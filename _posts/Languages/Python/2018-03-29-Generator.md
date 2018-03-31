---
layout: post
title: Generator
subtitle: What is the Generator on python?
category: Python
tags: [python, middle]
permalink: /2018/03/29/Generator/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

I referenced the sites below on Generator of python, and then I will cite it to summarize and to understand it. 

Above all, before you understand what the generator does and what is the yield keyword. 

Let's see iterable and iteration and iterator. 

# Iterable 

When you create a list, you can read its items one by one. Reading its items one by one is called iteration. 

{% highlight python linenos %}
my_list = [1,2,3]
for i in my_list:
    print(i)
'''
## The result of the code above ##
1
2
3
'''
{% endhighlight %}

As you can see above, my_list iterated once by reading its items one by one. here my_list is iterable. 

Another example with list comprehension. 

Below shows you can creat iterable with list comprehension.

{% highlight python linenos %}
my_list = [x*x for x in range(3)]
for i in my_list:
    print(i)
'''
## The result of the code above ##
0
1
4
'''
{% endhighlight %}

Everyting you can use for-in statement on is an iterable like lists, strings, files...

This kind of iterable is so hany, that is because you can read items as much as you want easily, But Whne you work with iterable, all iterables is in memory. 

So this is not efficient to manage memory, in particular when you use big data. 

The normal function is got rid of when the function hit return statement, after executing the last line in the function or hitting exception.

Also all memory the function has during executing is sustained until the functio is terminated. and then once again calling the function is the same from managing memory.

one day, programmer have wanted smart iterable. specifically speaking, after finishing the job, the programmer want that the function doesn't disapper. 

The function have to remember all of thing the function itself behaved, and then if caller calls once again, the function continuously do the job from the place the function remember.

on python, you can do it with yield keyword by create generator. 

Let's walk throuhg Generator 

# Generator

Generators are iterable, a kind of iterable you can only iterate over once. Generators do not store all the value in memory. They generate the vale on the fly as follows:

{% highlight python linenos %}
my_generator = (x*x for x in range(3))
print(my_generator)
for i in my_generator:
    print(i)
'''
## The result of the code above ##
<generator object <genexpr> at 0x7f488082e3b8>
0
1
4
'''
{% endhighlight %}

It is simple to create generator. because it similar to list comprehension. () is used instead of [].

In the code above, you cannot perform for-in statement with my_generator a second time since you can use generators once: they calculate 0, then forget about it and calculate 1 and at the end calculating 4, one by one.

Also you can make generator with yield keyword. 

## yield 

yield is a keyword that is used like return, except the function will return a generator. 

{% highlight python linenos %}
def createGenerator():
    my_list = range(3)
    for i in my_list:
        yield i*i

my_generator = createGenerator()
print(my_generator)
for i in my_generator:
    print(i)
    
for i in my_generator:
    print("2",i)
'''
## The result of the code above ##
<generator object createGenerator at 0x7f4880892620>
0
1
4
'''
{% endhighlight %}

When you perform my_generator with for-in statement a second time. it has nothing. 

To understand yield, you must understand that when you call the function, the code you have written in the function body does not run. the function only return the generator object. 

Then, you will run the generator each time the for statement uses the generator. 

In detail, the frist time the for calls the generator object created from your function, it will run the code in your function from the beginning until it hits yield, then it'll return the first value of the loop. Then each other call will run the loop you have written in the function one more time, and return the next value, until there is no value to return. 

The generator is considered empty once the function runs but does not hit yield anymore. that could be because the loop had come to an end. 

Let's go through another example of generator:

{% highlight python linenos %}
def square_numbers(nums):
    result = []
    for i in nums:
        result.append(i*i)
    return result

my_nums = square_numbers([1,2,3,4,5])

print(my_nums)
'''
## The result of the code above ##
[1, 4, 9, 16, 25]
'''
{% endhighlight %}

As you can see, the code above return a list


{% highlight python linenos %}
def square_numbers(nums):
    for i in nums:
        print("Befor yield")
        yield i * i
        print("After yield")
    print("really")
        
my_nums = square_numbers([1,2,3,4,5])

print("my_num:{}".format(my_nums))

print("next(my_nums):{}".format(next(my_nums)))

for i in my_nums:
    print(i)
    
print("After calling the end of generator once again")
print("next(my_nums):{}".format(next(my_nums))) # stopIteration
'''
## The result of the code above ##
my_num:<generator object square_numbers at 0x7f48808abf10>
Befor yield
next(my_nums):1
After yield
Befor yield
4
After yield
Befor yield
9
After yield
Befor yield
16
After yield
Befor yield
25
After yield
really
After calling the end of generator once again
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-58-d0890c329d66> in <module>()
     16 
     17 print("After calling the end of generator once again")
---> 18 print("next(my_nums):{}".format(next(my_nums)))

StopIteration: 
'''
{% endhighlight %}

the code above show you how the generator works. in particular, generator remembers what they did. 

So in the next call, they continuously proceed after the previous job. 

Also because generator is run once one by one, When there is nothing left in generator, if you call next item, Generator create exception, **stopIteration**.

The pro of generator is generator is fast and great at efficiency of managing memory than list.

# Reference 

 - Eng ver.
  - [Stackoverflow's generator and interator](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do/231855#231855)
  
 - Kor ver.
  - [To understanding python'keyword yield](https://tech.ssut.me/2017/03/24/what-does-the-yield-keyword-do-in-python/)
  - [School of web's generator](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%9C%EB%84%88%EB%A0%88%EC%9D%B4%ED%84%B0-generator/)
