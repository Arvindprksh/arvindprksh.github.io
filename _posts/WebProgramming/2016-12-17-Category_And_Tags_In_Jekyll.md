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

   When you make a post in jekyll with front matter. You have to write that information if you want tag and category. 
   
   And then, you can make a list based on tags and category. 
   
   At first, I will make tags-based list that I want. 
   
   let's see example of code from [codeinfox](http://codinfox.github.io/blog/tags/)
   
  <script src="https://gist.github.com/hyunyoung2/63cfabdd6fb174fe69b621be8d48686d.js"></script>
   
  So If you want to make tags-based list that you want. make page(.html, .md) for this source !
  
  And then, if You did,  you can see as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tags example.png)

  let's split the above code for understaing the code.
 
  <script src="https://gist.github.com/hyunyoung2/47bf4e75c1ba154514b5db945ff146c8.js"></script>

  the above code is just extracting tags included in posts as follows. 
  
  ![](/img/Image/WebProgramming/2016-12-17-Category_And_Tags_In_Jekyll/a list of tag.png)
  
  And the rest of above code makes a tags-based list like this :
  
  Then let's see the rest of the code
