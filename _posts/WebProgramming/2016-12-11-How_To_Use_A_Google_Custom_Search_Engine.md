---
layout: post
title: How to use a google custom Search Engine
subtitle: How can I add a google custom search engine in my jekyll ?
category: WebProgramming
tags: [jekyll, google_custom_search_engine, beautiful-jekyll, static_website, gitpage]
permalink: /2016/12/11/How_To_Use_A_Google_Custom_Search_Engine/
comments: true
social-share: false
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---



# What is the google custom Search Enginge. 

  This is awesome, When I studied Natural Languge, I was thinking about search engine, How can I increase accuracy of searching engine. 
  
  At that time, I was thinking about itegrationg with machine learning, n-gram algrithm, tf-idf, vector-consine-similarity and so on, 
  
  But you can use the google search engine easily. 
  
  that is beacause google's giving you google custom search engine.
  
  ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/Google official site of custom search engine.png)
  
  if you want to see the movie that introduce google custom search. please Click this, [Google Custom Search Engine's YouTube](https://www.youtube.com/watch?v=Qd9z48Bo8ZA). 
  
  and If you want to go google's the official site of google custom engine. please click this, [Google Custom Search Engine](https://cse.google.com/cse/)
  
  
  i.e Google Custom Search Engine makes searching your site easy.
  
  Also, basic version is enough for me to make search engine in my jekyll 

  And If you want to use Google Custom Search Engine, first you have to sign in to Custom Search Engine.
  
  Well, Let's start how to make a Google Custom Search Engine.
 
# My Google Custom Search Engine

 ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/A Google Custom Search Engine.png)
  
 As you can see the above image. I made a Google Custom Search Enginge for my gitpage. it's awesome. 
 
 So it's easy, And i could search for what I want on My Gitpage. 
 
 From now on, I would like to share my experience and errors that I experienced.
 
## First, You have to make Search page. 

 I make a Search page using Markdown,
 
 ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/Seach page.png)

## Second, You have to copy and paste A Google Custom Search Engine Code from your Google account. 

  The code below you can get from your Google Custome Search Engine.
  
  You have to copy and paste that code in the Search page you made. 

{% highlight javascript linenos=table %}
<div id="google-custom-search">
<script>
  (function() {
    var cx = 'USER cx Number. ';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = '//www.google.com/cse/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:searchbox></gcse:searchbox>
</div>
{% endhighlight %} 

  i.e You have to put the above code between **\<body> and \<div> section** in the site where you're rendering Searching window. 
  
  **BUT** In my case of using template of jekyll, beautiful-jekyll.
  
  I cannot render window of Search Engine as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/Search engine without result.png)
  
  **So, Now I will explain to you how to fix it**
  
  **That is why** You have to be careful of the code of **<gcse:searchresults></gcse:searchresults>**

  As you can see **<gcse:searchresults></gcse:searchresults>** on the Google Custom Search Engine's official site. 
  
  The google's official Custome Engine site says that **<gcse:searchresults></gcse:searchresults>** makes your search page render the result that you looked for. 
  
  In my case, When I cannnot get a incomplete Google Custom Search Engine, I put **<gcse:searchresults></gcse:searchresults>** between **\<body> and \<div> section** in the site where you're rendering the result of Searching

  Specifically, I put **<gcse:searchresults></gcse:searchresults>** below **<gcse:searchbox></gcse:searchbox>**

{% highlight javascript linenos=table %}
<div id="google-custom-search">
<script>
  (function() {
    var cx = 'USER cx Number. ';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = '//www.google.com/cse/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:searchbox></gcse:searchbox>
<gcse:searchresults></gcse:searchresults>
</div>
{% endhighlight %} 

  After the above code, I can get a complet Google Custom Search Engine in my Gitpage like this. 
  
  ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/a complete google custom search engine.png)
  
  And then I can search for what I want in my Gitpage like this.
  
  ![](/img/Image/WebProgramming/2016-12-11-How_To_Use_A_Google_Custom_Search_Engine/A Google Custom Search Engine.png)

# Reference

 - [Justin James's adding google custom search engine](http://digitaldrummerj.me/blogging-on-github-part-7-adding-a-custom-google-search/)
 
 - [Google Custom Search Engine](https://cse.google.com/cse/)
 
 - [Google Custom Search Engine's YouTube](https://www.youtube.com/watch?v=Qd9z48Bo8ZA)
