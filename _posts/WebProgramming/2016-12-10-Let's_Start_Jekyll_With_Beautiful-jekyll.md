---
layout: post
title: Let's start jeklly with beautiful-jekyll
subtitle: What is the YAML front matter ?
category: Web Programming
tags: [jekyll]
permalink: /2016/12/10/Let's_Start_Jekyll_With_Beautiful-jekyll/
comments: true
social-share: false
bigimg: 
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

## Beautiful-jekyll

  this is so greate template of jekyll, it is so comportable and easy.
  
  I'm not worried about making my gitpage,blog because of jekyll, static site generator. 
  
  I appreciate jekyll again, whenever I develop and study, I cannot organization what I did well, 
  
  But from now on, I will be easier to organize what I did. 
  
  Now I will organize my using Jekyll and everything I update in beatiful-Jekyll.
  
- [x] First, How to use big Image, (2016.12.15) 
- [x] Second, How to use a Custom google Search engine. (2016.12.15) 
- [ ] Third, How to use Tags and categories. 
- [x] Fourth, What is the DISQUS ? (2016.12.15) 
- [x] Fifth, How can I do hightlither When I want to use codeblock in markdown. (2016.12.15) 
- [ ] Sixth, What is the permalink option ?
- [ ] Seventh, How to use markdown in githubpage.
    
## Jekyll with Beatiful-jekyll

  If you use beatiful-jekyll, It's so easy. 
  
  Jekyll can manage page, post and so on. 
  
  first, let's know what is the front matter
  
## [YAML front matter](http://jekyllrb.com/docs/frontmatter/)  ("parameters" for a page)
 
  I quote [Front Matter](http://jekyllrb.com/docs/frontmatter/) of the officail site of Jekyll.
  
  The front matter is where Jekyll starts to get really cool. Any file that contains **a YAML front matter block** will be processed by Jekyll as specail file. 
  
  **The front matter must be the first thing int the file and must take the from of valid YAML set between triple-dashed lines.**
  
  Here is a basic example. 
  
```
---
layout: post
title: Blogging Like a Hacker
---
```
  Between, these triple-dashed lines., you can set predefined variables(if you want to see that kind of variables, refer to [jekyll's official site](https://jekyllrb.com/docs/frontmatter/)) or even create custom ones of your own.
  
  These variables will then be available to you to access using Liquid tags.
  
  **i.e Whenever you make a page, You have to put a YAML front matter in top of a page with triple-dashed lines. I recommend you the minimum number of lines in a YAML fron matter is two like the above example**
  
  At least, I wish you make two things that is layout and title. 
  
  if you want to use another functionality. From now on, listen to what I will explain. 
  
```
---
layout: 
title: 
subtitle: 
css:
tags:
date:
bigimag(big-image):
share-image:
permalink:
comments:
social-share:
show-share:  -- exactly I don't know
meta-title:   -- exactly I don't know
meta-description:   -- exactly I don't know
show-avatar: 
nav-short:  
---
```
  As you can see the above example, YAML front matter has many types, So You have to look at [jekyll's official site](http://jekyllrb.com/docs/frontmatter/), if you want to sepcifically know about it. 
 
  But from now on, I will explain to you guys about that type of YAML front matter that I will use in my static website based on jekyll with [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll).
  
  What I explain to you about some of YAML front matter is :
  
  **tags, catergory, permanlink, comments, bigimage**
  
  Now, I will explain to you about **subtitle, css**. 
  
  that is so easy and simple 
  
  - subtitle : Short description of page or bolg post that goes under the title. 
  
  ![](/img/Image/WebProgramming/2016-12-10-Let-s_Start_Jekyll_With_Beautiful-jekyll/bigimg_title_subtitle_in_jekyll.png)
  
   i.e You can check up title and subtile in the above image.
  
  - css : List of CSS files to include in the page 
  
   i.e, You can make your own css in your git repository that has static website generator(jekyll).
 
  
## Reference 

  - [Jekyll Front Matter](http://jekyllrb.com/docs/frontmatter/)
  
  - [Beautiful-jekyll's git repository explaing the YAML front matter on README](https://github.com/daattali/beautiful-jekyll/blob/master/README.md#yaml-front-matter-parameters)
  
  - [Beautiful-jekyll's git](https://github.com/daattali/beautiful-jekyll)
  
  
