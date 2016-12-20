---
layout: post
title: Big Image in Beautiful-jekyll for my gitpage
subtitle: How Can I deploy my picture in jekyll template of beautiful-jekyll ?
category: WebProgramming
tags: [jekyll, utility]
permalink: /2016/12/16/Big_Image_In_Beautiful_Jekyll/
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

## big image on my git page

  I want to deploy image on my git, Becuase In case of only letters, It makes me bored.
  
  Accidentally, When I saw my gitpage about algorithm. But that page only has text. So it's boring. 
  
  And then, I use the bigimage functionality of my jekyll from [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll)
  
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/big Image blog.png)
  
### How to add big image frame on my git page

  the way to introduce imgaes is so easy on my jekyll. 
  
  Just, Use YAML front matter like this, 
  
  **Frist,** Multiple bigimage. 

```
---
.......
bigimg: 
  - "/Your Image Path/filename of image" : "comment"
  - "/Your Image Path/filename of image" : "comment"
  - "/Your Image Path/filename of image" : "comment"
---  
```
  
  After the above YAML front matter, you get the result below. 
  
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/big Image blog.png)

  As you can see the above image, the bottom of left includes "your comment" of bigimg.
  
  i.e if you wrote your big Image like this.
  
  > bigimg:  
  >   - "/Your Image Path/filename of image" : "San Francisco, CA (2016)"

  like the above image, the bottom of left indicates that text,"San Francisco, CA (2016)".
  

  **Second,** Single bigimage with comment
  
```
---
.......
bigimg: 
  - "/Your Image Path/filename of image" : "comment"
---  
``` 
  if you want to post one image with comment. 
  
  Just type in YAML front matter like this :
  
  > bigimg:    
  >   - "/Your Image Path/filename of image" : "comment"  
 
  then, you can see as follows :
  
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/Single bigimage with comment.png)
  
  **Third,** Single bigimage. 
  
```
---
.......
bigimg: /Your Image Path/filename of image
---  
```
  The last one that I introduce to you is the above. 
  
  if you only want to post one image.
  
  Just type in YAML front matter like this :
  
   > bigimg: /Your Image Path/filename of image  
 
  then, you can see as follows :
  
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/Single bigimage.png)
  
## Error case

  If you find bigimage works like this, that is becuase you type the wrong path of image.  
  
  The following is the wrong path :
  
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/big image wrong path.png)
  
  In my case of the wrong path, after I fix the path, big image works well. 
  
  The following is after fixing it :
  ![](/img/Image/WebProgramming/2016-12-16-Big_Image_In_Beautiful_Jekyll/after fixing the wrong path.png)
  
## Summary of big image 

  If you want to use bigimage option in beautiful, I recommend you to use one of both below in YAML front matter.

  > mutilple big image

```
---
.......
bigimg: 
  - "/Your Image Path/filename of image" : "comment"
  - "/Your Image Path/filename of image" : "comment"
  - "/Your Image Path/filename of image" : "comment"
---  
``` 
  
  > OR single big image with comment

```
---
.......
bigimg: 
  - "/Your Image Path/filename of image" : "comment"
---  
``` 
  
 
## Reference

 - [Beautiful-jekyll's git](https://github.com/daattali/beautiful-jekyll)
