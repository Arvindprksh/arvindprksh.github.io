---
layout: post
title: What is the difference between Unicode and UTF-8?
subtitle: UTF-8 is an encoding and Unicode is a character set
category: Natural Language Processing Labs
tags: [nlp, encoding]
permalink: /2018/04/02/What_Is_The_Difference_Between_Unicode_and_UTF8/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

In here, I am not going to explain in detail about How to translate the UTF-8 into another encoding ways like UTF-16 and UTF-32. 

Also I am not goint to explain about big-endian and little endian of UTF 16. 

Just what I am saying is What is the difference between Unicode and utf8. 

# Unicode is a character set and UTF-8 is an encoding. 

All the computer deals with data as binary code such as "0" and "1", so you need some way you change data into binary number which is call encoding. 

Let's think of it more, When you change some data into binary number, just number like decimal, octa, and hexa, is so easy to traslate to binary number. 

First of all, When making binary number, computer matches all of the data like number and text into number like decimal, octa and decimal.

Let's see the simple way number is translate into binary. 

If you have a sequence of 1,2,3,4, then computer translates it into binary number like this:

> 00000001 00000010 00000011 00000100

this binary can be saved on disk. 

as opposed to thing above. when binary is tranlsated to show the data to user, first is translating binary into number. 

As you notice, translating between number and binary is an encoding way such as UTF-8, UTF-16(BE, LE) and UTF-32. 

Let's say an application reads the following a seqeunce of binary from the disk. 

> 1101000 1100101 1101100 1101100 1101111

The app already knows What type of encoding used to translate number to binary. Let's say we used UTF-8 to encode. 

So the app would translate binary into number like this: 

> 104 101 108 108 111

At this time, The app use Unicode to show it as text to user.

In here, as you recognize What is the unicode, Unicode is character set used to numbers into characters. 

# Conclusion

UTF-8, UTF-16(BE, LE), and UTF-32 is an encoding used to translate binary data into numbers. Unicode is a character set used to translate numbers into characters


# Reference 

 - [Stackoverflow about "What is the difference between Unicode and UTF-8?"](https://stackoverflow.com/questions/3951722/whats-the-difference-between-unicode-and-utf-8)
 
 - [The Difference beween UTF-8 and Unicode](http://www.polylab.dk/utf8-vs-unicode.html)
 
 - Appendix
 
 - [Unicode space](http://jkorpela.fi/chars/spaces.html)

 - [Stackoverflow about encoding](https://stackoverflow.com/questions/6224052/what-is-the-difference-between-a-string-and-a-byte-string)
