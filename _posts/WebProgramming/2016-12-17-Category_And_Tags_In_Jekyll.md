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
   
  <script src="https://gist.github.com/hyunyoung2/226a95e1ea9c31fa86f561fba477a140.js"></script>
   
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
  
  <script src="https://gist.github.com/hyunyoung2/cebef17d97fe84d3ac4c12c81a5ce11b.js"></script>
  
  The above code makes title and the title-based list, of course. Currently,  title is tag in here. 
  
  In this code, if you change the tags into categories, that is a list based on category. 
  
  that code is as follows. 
  
  <script src="https://gist.github.com/hyunyoung2/cebef17d97fe84d3ac4c12c81a5ce11b.js"></script>
  
  I made my word cloud and a list based on catergories with the above code.
  
  of course, I made my word cloud and a list based on tags. **BUT** both of them is the same, 
  
  just those are different a little. And I added several into the code that make word cloud and a list. 
  
  let's see my word cloud and a list based on categries. 
  

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
