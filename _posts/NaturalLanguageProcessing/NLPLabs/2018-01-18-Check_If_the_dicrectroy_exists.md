---
layout: post
title: How to check whether or not the direcotry exists
subtitle: if statement to check if file exists.
category: Natural Language Processing Labs
tags: [linux, shell script]
permalink: /2018/01/18/Check_If_the_dicrectroy_exists/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

When I wrote shell script to downlowd corpus, I need to chekc if the directory I want to make exists.

I found it, for practice of shell script I will organize it in here. 

{% highlight lineos %}
if [ -d $LINK_OF_DIR ]; then 
    if [ -L $LINK_OF_DIR ]; then
    fi
fi
{% endhighlight %}

The above code checks whether or not $LINK_OF_DIR exists and is symbolic link.

the below is to check if $LINK_OF_DIR is directory. 

So if a directory with the name exists, if statement returns **false**

{% highlight lineos %}
if [ -d $LINK_OF_DIR ]; then 
......
fi
{% endhighlight %}


The follow is to check if $LINK_OF_DIR is symbolic link.

{% highlight lineos %}
...
    if [ -L $LINK_OF_DIR ]; then
    fi
...
{% endhighlight %}


# Reference

 - [stackoverflow](https://stackoverflow.com/questions/59838/check-if-a-directory-exists-in-a-shell-script)
