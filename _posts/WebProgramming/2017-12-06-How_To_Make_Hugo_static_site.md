---
layout: post
title: How to make hugo static site
subtitle: What is the hugo flatform for static site 
category: Web Programming
tags: [hugo]
permalink: /2017/12/06/How_To_Make_Hugo_static_site/
css :  /css/ForYouTubeByHyun.css
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---


# What is the hugo?

 Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility,

 on my experience about hugo static site, It is fast to generate site. 
 
# How to install hugo website 

  as you could see how to install hugo site below youtube.
  
  From now on, I will explain on ubuntu 16.04
  
  First, download hugo 
  
  use snap package, when you installl hugo with apt-get, at that time, hugo's version is old. 
  
  > $ snap install hugo
  
  Sencond, Now generate directory for hugo website 
  
  > $ hugo new site "the name you want for hugo website"
  
  In your directory you named what you want for hugo website, if you type ls. 
  
{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~/Practice_Project/sample-hugo-site [18:25:11] 
$ ls -a  
.  ..  archetypes  config.toml  content  data  layouts  static  themes 
{% endhighlight %}
  
  as you can see above, there are some folders you need when you generate hugo website. 
  
  in particular, you will use config.toml  file much times 
  
  Third, let's type "hugo server"
  
  This mean hugo is run on localhost. and port number is already selected.
  
  As you could see there is nothing on website. 
  
  From now on, I will utilize a certain theme someone already made.
  
  In my case, I used [docdock](https://themes.gohugo.io/theme/docdock/credits)
  
  to use theme of hugo, you have to use "git" tool
 
  > $ git init
  
  > $ git submodule add "git repository you want to download" "the location you want"
  
  In my case
  
{% highlight shell linenos %}
# hyunyoung2 @ hyunyoung2-desktop in ~ [18:37:44] 
$ git submodule add https://github.com/vjeantet/hugo-theme-docdock.git themes/dockdock   
{% endhighlight %}
  
  And then, If you want the latest version of the theme you download, 
  
  > $ git submodule init   
  
  > $ git submodule update
  
  finally, you have to change the **config.toml** file like this :
  
{% highlight shell linenos %}
baseURL = "http://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"

theme = "dockdock; the name of the directory you downloaded in themes directory"
themeDir = "themes; the themes directory name"
{% endhighlight %}
 
  Now, you can see hugo website of the themes you adopted. 
  
# How to upload hugo website on github  
  
  But If you want to upload github. 
  
  First, generate github repository and configure remote repository. 
  
  > git remote add origin "you remote git repository"   
  
  > hugo 

  > git add --all(or some file)   
  
  > git commit -m "first commit"   
  
  > git push -u origin master
  
  Keep in mind, you change config.toml file like this:
  
  on my case, I used doc directory of master branch to render website on github 
  
{% highlight shell linenos %}
baseURL = "youre github website address like https://your repository name.github.io"
languageCode = "en-us"
title = "My New Hugo Site"

theme = "dockdock; the name of the directory you downloaded in themes directory"
themeDir = "themes; the themes directory name"
  
publishDir = "docs"
{% endhighlight %}
  
  I mean you have to add a line on config.toml,**publishDir= "docs"**  
  
  if you change the config.tmol file, you have to delete the directory, **publish.**
  
  After that, type like this:
  
  > hugo  
  
  > git add --all  
  
  > git commit -m "generate web files"
  
  > git push origin master
  
# How To Make Hugo Static Site with theme from [https://gohugo.io](https://gohugo.io/)

  Let's play youtube

  <div id="tutorial-section">

  <div id="tutorial-title">Installling & using Themes on hugo</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">How to make a hugo website and put in online</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">Installing & Using Themes</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://youtu.be/3wkR8GyDODs" frameborder="0" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://youtu.be/L34JL_3Jkyc" frameborder="0" allowfullscreen></iframe> </div>
  </div>
</div>


# Reference 

  [- the official hugo site](https://gohugo.io/)  
  
  [- themes of hugo](https://themes.gohugo.io/)  
  
  [- docdock](https://themes.gohugo.io/theme/docdock/)
  
  
