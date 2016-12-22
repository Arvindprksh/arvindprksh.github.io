---
layout: post
title: How to generate a list of category and tags in jekyll
subtitle: How can I automatically make a table of content using Category and Tags ?
category: Web Programming
tags: [jekyll]
permalink: /2016/12/17/Category_And_Tags_In_Jekyll/
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---

## a list using tags and categories
  
```markdown
---
layout: post
category: ~~~
tags: ~~~
---
```

   When you make a post in jekyll with fornt matter. You have to write that information if you want tag and category. 
   
   And then, you can make a list based on tags and category. 
   
   At first, based on tags, I will make what I want. 
   
   let's see example of code from [codeinfox](http://codinfox.github.io/blog/tags/)
   
<pre><code>
<div class="tags-expo">
  <div class="tags-expo-list">
    {% for tag in site.tags %}
    <a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a>
    {% endfor %}
  </div>
  <hr/>
  <div class="tags-expo-section">
    {% for tag in site.tags %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag | first }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
      <li>
        {{ post.title }}
      <small class="post-date">{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div></code></pre>
   
  After making page(.html, .md) for this source, generate that page !
  
  And then, you can see as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tags example.png)

  let's split the above code.
 
```markdown
    {% for tag in site.tags %}
    <a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a>
    {% endfor %}
```
   the above code is just a list of tags as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tag.png)
  
  And the rest of above code makes a tags-based list. 
  
  let's see code below. 
  
```markdown
  {% for tag in site.tags %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag | first }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
      <li>
        {{ post.title }}
      <small class="post-date">{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
  {% endfor %}
```
  
  The above code makes title and the title-based list, of course. Currently,  title is tag in here. 
  
  In this code, if you change the tags into categories, that is a list based on category. 
  
  that code is as follows. 
  
```markdown
<div class="tags-expo">
  <div class="tags-expo-list">
    {% for tag in site.categories %}
    <a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a>
    {% endfor %}
  </div>
  <hr/>
  <div class="tags-expo-section">
    {% for tag in site.categories %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
      <li>
        {{ post.title }}
      <small class="post-date">{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div>
```
  

## information of terminology

### What is the category in jekyll ?



### What is tags in jekyll ?




## Reference

  - [Jekyll's official site about category and tags](https://jekyllrb.com/docs/frontmatter/#predefined-variables-for-posts)
  
  - [brandonparsons's using tags in a jekyll bolg on github pages](https://blog.brandonparsons.me/2015-using-tags-in-a-jekyll-blog-on-github-pages)
  
  - [codinfox's aportion of using catergory and tags](https://codinfox.github.io/dev/2015/03/06/use-tags-and-categories-in-your-jekyll-based-github-pages/) : what I mainly refer to.
      
  - [mikeapted's Adding category and tag archive pages to Jekyll](https://www.mikeapted.com/jekyll/2015/12/30/category-and-tag-archives-in-jekyll-no-plugins/)
  
  - [melyanna's tags archive implemented](https://melyanna.github.io/2016-02-15-tags/)
  
  - [melyanna's archive table of contents](https://melyanna.github.io/toc/)
