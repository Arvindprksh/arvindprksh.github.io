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
   
  <script src="https://gist.github.com/hyunyoung2/63cfabdd6fb174fe69b621be8d48686d.js"></script>
   
  After making page(.html, .md) for this source, generate that page !
  
  And then, you can see as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tags example.png)

  let's split the above code.
 
  <script src="https://gist.github.com/hyunyoung2/47bf4e75c1ba154514b5db945ff146c8.js"></script>

  the above code is just a list of tags included in posts as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tag.png)
  
  And the rest of above code makes a tags-based list. 
  
  let's see code below. 
  
  <script src="https://gist.github.com/hyunyoung2/fca0b5126074a6dd342759c24b8c3a97.js"></script>
  
  The above code makes a list of each tags, of course. 
  
  In this code, if you change "site.tags" into "site.categories", that is a list based on category. 
  
  that code is as follows. 
  
  <script src="https://gist.github.com/hyunyoung2/015080b43418f91da09ff77bc1a16d87.js"></script>
  
  But In my case, I change the above code a little to fit my wegsite. 
  
  
  How to chang my code you can see another [another of my blog](/2016/12/17/Tag_Cloud/) explaing to you how to make cloud system of tags and categories.
  
  After I mend the above example code to fit situation that I want. the final look is like this : 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/in categories.png)
  
## information of terminology

### What is the category in jekyll ?

 - instead of placing posts inside of folders, you can specify one or more categories that the post belong to. when the site is generated the post will act as though it had been set with these categories normally. Categories can be specified as a YAML List(front matter) or a space-separated string. 

 I also use frot matter to express categories. 

### What is tags in jekyll ?

 - this similar to categories, one or multiple tags cans be added to a post. Also like categories, tags can be specified as a YAML List(front matter) or a space-separated string. 

 I also use frot matter to express tags. 

## Reference

  - [Jekyll's official site about category and tags](https://jekyllrb.com/docs/frontmatter/#predefined-variables-for-posts)
  
  - [brandonparsons's using tags in a jekyll bolg on github pages](https://blog.brandonparsons.me/2015-using-tags-in-a-jekyll-blog-on-github-pages)
  
  - [codinfox's aportion of using catergory and tags](https://codinfox.github.io/dev/2015/03/06/use-tags-and-categories-in-your-jekyll-based-github-pages/) : what I mainly refer to.
      
  - [mikeapted's Adding category and tag archive pages to Jekyll](https://www.mikeapted.com/jekyll/2015/12/30/category-and-tag-archives-in-jekyll-no-plugins/)
  
  - [melyanna's tags archive implemented](https://melyanna.github.io/2016-02-15-tags/)
  
  - [melyanna's archive table of contents](https://melyanna.github.io/toc/)
