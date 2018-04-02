---
layout: post
title: How to remove a character like Carriage return character(\^M)?
subtitle: %s/^M//g
category: Natural Language Processing Labs
tags: [nlp, vim]
permalink: /2018/04/01/New_Line_Character_Problem/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

When you work with vim, you find out some character like **^M**.  

That is because Unix uses 0xA for a newline character. Windows uses a combination of two characters: 0xD 0xA. 

0xD is the carriage return character. ^M haapens to be the way vim displays 0xD(0x0D=13, M is the 13th letter in the English alphabet).

If you want to remove the character(^M) in vim. run the following in command mode:

> %s/^M//g

Where **^M** is entered by holding down **Ctrl** and typing **v** followed by **m**, i.e. pressing **Ctrl** and simultaneously pressing "v" and then "m".

after that, release **Ctrl**. 

This expression will replace all occurences of **^M** with the empty string(i.e. nothing). 

Normally It is used to get rid of **^M** in files copied from Windows to Unix such as Solaris, Linux, OSX)

# Reference 

  - Eng ver
   - [Stackoverflow](https://stackoverflow.com/questions/5843495/what-does-m-character-mean-in-vim)
   
  - Kor ver
   - [how to remove ^M character in vim or vi](http://mwultong.blogspot.com/2007/08/vim-vi-m-m.html)
