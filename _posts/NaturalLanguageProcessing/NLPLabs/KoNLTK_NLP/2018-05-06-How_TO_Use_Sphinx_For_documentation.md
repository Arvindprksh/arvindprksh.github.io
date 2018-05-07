---
layout: post
title: How to use sphinx
subtitle: Let's start documentation with sphinx
category: Natural Language Processing Labs
tags: [nlp, konltk, python]
permalink: /2018/04/24/PyPI_Practice/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


# sphinx practice for konlp of Konltk

[![Documentation Status](https://readthedocs.org/projects/hyunyoung2s-sphinx-practice/badge/?version=latest)](http://hyunyoung2s-sphinx-practice.readthedocs.io/en/latest/?badge=latest)

Above all, let's make virtual environment 

> sudo apt install -y python3-venv  
> pyvenv env  
> source env/bin/activate

After it, follow things below.

First, in order to run sphinx, install them below:

> pip install sphinx

Then, Create a directory inside your project to hold your docs: 

> cd /path/to/project
> mdkir docs

So, Run **sphinx-quickstart**

> sphinx-quickstart

This quick start will walk you through creating the basic configuration; When it's done, you'll have **index.rst**, **conf.py** and some other files. 

build your project like this:

> make html

Then check 

> open /path/to/\_build/index.html

After that if you want to host on the html files with github page. 

There ars wo simple way like this:

> mv /path/to/\_build/html/* /path/to/your_git_repository/  

Then push your local repository to your remote repository. 

**Keep in mind, you should add \.nojekyll in remote repository for github page to render your html generated on python code.**

The following is screencast of how to utilize sphinx : 

[![](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_sphinx_practice/master/imgs/sphinx_image.png)](https://www.youtube.com/embed/oJsUvBQyHBs)

### add a \.nojekyll file



# Reference 

 - [Readthedocs's getting started](https://docs.readthedocs.io/en/latest/getting_started.html) 
 - [my git repository, hyunyoung2's sphinx practice](https://github.com/hyunyoung2/hyunyoung2_sphinx_practice)
