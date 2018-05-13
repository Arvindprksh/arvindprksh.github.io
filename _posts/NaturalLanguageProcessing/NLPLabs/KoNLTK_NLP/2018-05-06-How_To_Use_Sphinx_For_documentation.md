---
layout: post
title: How to use sphinx
subtitle: Let's start documentation with sphinx
category: Natural Language Processing Labs
tags: [nlp, konltk, python]
permalink: /2018/05/06/How_To_Use_Sphinx_For_documentation/
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

[![Documentation Status](https://readthedocs.org/projects/hyunyoung2s-sphinx-practice/badge/?version=latest)](http://hyunyoung2s-sphinx-practice.readthedocs.io/ko/latest/?badge=latest)

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

The last thing you have to do is add an empty file called **\.nojekyll** in your repository. This tells github's default software to ignore the sphinx-generated pages. Make sure you commit, too:

> cd /path/to/\_build/html  
> touch .nojekyll  
> git add .nojekyll   
> git commit =m "added .nojekyll"   
> git push   

![](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_sphinx_practice/master/imgs/nojekll_file.png)


### Readthedocs 

If you want to use Readthedocs flatform, it is easy than explaining to you by now with github page and sphinx. 

If you have git repository written in python, import it in readthedocs. 

After that, run the following command: 

> $ sphinx-quickstart  

That makes some file to be needed when you make webpage with sphinx like : 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Konltk_NLP/2018-05-06-How_TO_Use_Sphinx_For_documentation/sphinx_basic_files.png)

In the files, conf.py is important because sphinx create html based on the file option, conf.py.

So enter the Advanced Setting then notify to readthedocs where the conf.py is. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Konltk_NLP/2018-05-06-How_TO_Use_Sphinx_For_documentation/conf_readthedocs.png)

After recognizing the location of conf.py, readthedocs would render the website based on the option of the file. 

the following is my web site for practice of sphix. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Konltk_NLP/2018-05-06-How_TO_Use_Sphinx_For_documentation/sphinx_website_for_my_practice.png)

Tip : When you have Korean language, if building the Latexpdf fail. Keep in main of the latex option on conf.py.

In my case, after the option changed, web site was rendered well like thing above. 

the option I used is like :

{% highlight python linenos %}
latex_elements = {
    # The paper size ('letterpaper' or 'a4paper').
    #
    # 'papersize': 'letterpaper',

    # For konlp
    'papersize': 'a4paper',

    # The font size ('10pt', '11pt' or '12pt').
    #
    # 'pointsize': '10pt',

    # Additional stuff for the LaTeX preamble.
    #
    # 'preamble': '',

    # For konlp
    'preamble': '\\usepackage{kotex}',

    # Latex figure (float) alignment
    #
    # 'figure_align': 'htbp',
}
{% endhighlight %}

# Reference 

 - [Readthedocs's getting started](https://docs.readthedocs.io/en/latest/getting_started.html) 
 - [my git repository, hyunyoung2's sphinx practice](https://github.com/hyunyoung2/hyunyoung2_sphinx_practice)
 - [Sphinx-doc quickstart](http://www.sphinx-doc.org/en/master/usage/quickstart.html)
 - [How to use google doc style with sphinx extension](http://www.sphinx-doc.org/en/master/ext/napoleon.html)
