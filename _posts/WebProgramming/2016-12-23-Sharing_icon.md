---
layout: post
title: How to make sharing icon and error that when I make gitpage, I encountered
subtitle: How to make sharing icon,print and email and a error with nav-bar
category: Web Programming
tags: [jekyll]
permalink: /2016/12/23/Sharing_icon/
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---

## sharing icon

 In my case, Since I used someone's template, I have to understand this code structure someone made. 
 
 finally I found out where I have to put the code about sharing code. 
 
 Now, I wirte down the code that I newly make to share my gitpage with someone's email and printer
 
 <script src="https://gist.github.com/hyunyoung2/cf07b73aba9a7e1ce5482ea8df120538.js"></script>
 
 As you can see the code. key point of sharing code about email and printer is like this :
 
```
 email : 
  a tag's href="mailto:?subject=<title>&body=<contents of email>"
 
 printer
  a tag's href="javascript:;" onclick="window.print()"
``` 
  
  the above code is key, the rest is for design, 
  
  for example. it's like what butto I use for sharing incon
  
  The follwoing is sharing button of my gitpage
  
 ![](/img/Image/WebProgramming/2016-12-23-Sharing_icon/sharing icon.png)

  In the above code, about design, if  you have much better idea.
  
  please let me know about what you know. 
  
  I will appreciate seriously. 


## Error with nav-custom bar. 

  When I use someone's template. I encoutered a trouble. 
  
  for example. when I use a tag, after a tag, title of a list disappears in the back of navigation bar like this. 

 ![](/img/Image/WebProgramming/2016-12-23-Sharing_icon/error with nav-bar.png)
  
  But after using a tag, what I want is like this. 
  
 ![](/img/Image/WebProgramming/2016-12-23-Sharing_icon/error with nav-bar1.png)
  
  In order to do the above thing. when I develop website first, I take a little time to fix it. 
  
  So for another people, especially for newbies of web developing. I organized my experience of web developing. 
  
  way I resolve this problem is "padding" of css style.
  
  i.e nav-bar contain a series of space. so I have to expect how much space nav-bar need. and I consider it after using a tag
  
  when I made categories cloud system, the following is the code to resolve this problem 
  
```
  h2 tag's attribute :  id="{{ tag[0] | slugify }}" style="padding-top: 00px;"
```  
  
  for your information of css, I recommend a site of [w3schools](http://www.w3schools.com/css/css_padding.asp)
  
  In this site, you can experiment a concise code. 
  
  I wish this article helps newbies that will make website 
  
## Reference 

  - [css padding](http://www.w3schools.com/css/css_padding.asp)
  
