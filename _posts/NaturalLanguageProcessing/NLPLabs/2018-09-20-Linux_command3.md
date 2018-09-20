---
layout: post
title: What kind of Linux command is useful?
subtitle: During researching natural lanuage with Ubuntu, organizing Linux command that I have used. 
category: Natural Language Processing Labs
tags: [linux, command, nlp]
permalink: /2018/09/20/Linux_Command2/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# wget utility and curl

The **wget utility** allows you to download we pages, files and images from the web using Linux command line.

 > wget -c URL_or_IP_Address_of_what_you_want_to_download

The **curl ** is a tool to transfer data from or to a server, using one of the supported protocoals.

 > curl -O URL_or_IP_Address_of_what_you_want_to_download
 
In more detailed, Let's say, If you want to Fetch the file **index.html** from a certain URL using HTTP protocol.
and display it to standard output. it is similar to view the source of the webpage, I mean the following will display the raw HTML

> curl a_certain_URL/index.html

After fetching the same file as above, but If you want to redirect the output to a file, index_file, in the current directory.

type in like this:

> curl a_certain_URL/index.html > index_file

If you want to output a file with the same name(index.html) in the current directory, this time use curl command with **-O** option like this:

> curl -O curl a_certain_URL/index.html


# Reference 

 - [Wget utility](https://www.lifewire.com/uses-of-command-wget-2201085)
 
 - [curl 1](https://www.lifewire.com/curl-definition-2184508)
 
 - [curl 2](https://www.computerhope.com/unix/curl.htm)
