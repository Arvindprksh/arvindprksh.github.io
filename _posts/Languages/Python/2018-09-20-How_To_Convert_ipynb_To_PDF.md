---
layout: post
title: How to convert ipynb file to PDF
subtitle: jupyter nbconvert 
category: Python
tags: [python, tip]
permalink: /2018/09/20/How_To_Convert_ipynb_To_PDF/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This article is for my memorization about converting ipynb to PDF

I had to report [paper work](https://github.com/hyunyoung2/Hyunyoung2_graduate_school_assignment/blob/master/Selected_Topic_in_Computer_Science/Assignment1/Assignment1.ipynb) commited with python. 

then I used jupyter and I found out nbconvert function. 

If you have nbcovert and jupyter, it is easy to convert ipynb to PDF. 

the way to convert ipynb to PDF is the following :

> jupyter nbconvert --to pdf file_name.ipynb

Another way is using template like this:

> jupyter nbconvert --to pdf --template what_you_want_to_use file_name.ipynb

refert to the following of help message of **jupyter nbconvert**.

```
Both HTML and LaTeX support multiple output templates. LaTeX includes
    'base', 'article' and 'report'.  HTML includes 'basic' and 'full'. You
    can specify the flavor of the format used.
    
    > jupyter nbconvert --to html --template basic mynotebook.ipynb
```

as metioned, the process above is under where you installed nbconvert , pandoc and etc.

If not, install them below 

1. nbconvert 

> pip3 install nbcovert

2. Pandoc 

> sudo apt-get install pandoc

then run it to convert ipynb to PDF if you suceed! 

Congradulation! you are done. 

BUT if you get error message like me as follows:

![](/img/Image/Languages/Python/2018-09-20-How_To_Convert_ipynb_To_PDF/jupyter_notebook_nbconvert_pdf_error.png)

```
OSError: xelatex not found on PATH, if you have not installed xelatex you may need to do so. Find further instructions at https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex.
```
just visit the URL, https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex.

you will find out how to install TeX, if you are linux user, type in the following 

> sudo apt-get install texlive-xetex

![](/img/Image/Languages/Python/2018-09-20-How_To_Convert_ipynb_To_PDF/Install_TeX.png)

Then you could convert ipynb to PDF with prompt like two wasy below.

> jupyter nbconvert --to pdf file_name.ipynb

Another way is using template like this:

> jupyter nbconvert --to pdf --template what_you_want_to_use file_name.ipynb


you could convert ipynb to a lots of format in Jupyter on web browser, 

> File - Download as - PDF via LaTex or etc.

In my case, when I used PDF via I had another error, Korean language problem like this:

![](/img/Image/Languages/Python/2018-09-20-How_To_Convert_ipynb_To_PDF/Korean_language_problem.png)

The solution of the problem is fixing template, base.tplx like this: 

![](/img/Image/Languages/Python/2018-09-20-How_To_Convert_ipynb_To_PDF/basetplx.png)

>\\usepackage{kotex}  
>%\usepackage[T1]{fontenc}

After typing in  kotex like above, Korean Language problem would be resolved.

The location of base.tplx is under **lib/python3.5/site-packages/nbconvert/templates/latex**. 

depending on when you install python with root(sudo) or --user. The location of base.tplx is different

If root(suod), The python site-packages is under **/usr/lib**

If --user, The python site-packages is under **~/.local/lib**


# Reference

 - [Pandoc](http://pandoc.org/)
 
 - [nbconvert's user documentation about installation](https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex)

 - [Kotex error problem Kor ver.](http://hoze.tistory.com/1426)
