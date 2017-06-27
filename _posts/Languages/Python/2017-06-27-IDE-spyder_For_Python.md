---
layout: post
title: IDE for python, Spyder 
subtitle: What is the Spyder
category: Python
tags: [python, tool]
permalink: /2017/06/27/IDE-spyder_For_Python/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

Spyder is IDE for python, I think this tool is very useful for anyone who want to use python. 

So I want to show you installation and running it. 

before doing that, my evironment setting is : 

> hyunyoung2@hyunyoung2-desktop:~$ uname -a     
> Linux hyunyoung2-desktop 4.8.0-36-generic #36~16.04.1-Ubuntu SMP Sun Feb 5 09:39:57 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

First If you want to install spyder or spyder3.

type in as following. 

> sudo apt-get install spyder3   
> sudo apt-get install spyder    

spyder3 for python3.n.

spyder for python2.7.

But if you cannot install like this :

```bash
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get install spyder
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package spyder
```

you have to update your package list and upgrade all software to the latest version.

> sudo apt-get update  
> sudo apt-get -y upgrade

```bash
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get update
Get:1 http://us.archive.ubuntu.com/ubuntu xenial InRelease [247 kB]
Get:2 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]
Get:3 http://us.archive.ubuntu.com/ubuntu xenial-updates InRelease [102 kB]       
......
```

```bash 
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get -y  upgrade
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
The following packages have been kept back:
  gnome-software gnome-software-common libmirclient9 linux-generic-hwe-16.04
  linux-headers-generic-hwe-16.04 linux-image-generic-hwe-16.04 python3-software-properties
  software-properties-common software-properties-gtk ubu
.....
```


From now on, let's install spyder or spyder3.

type in after upgrade and update is complete.  

> sudo apt-get install spyder3   
> sudo apt-get install spyder    

finally, you can run it  like this 

![](/img/Image/Languages/Python/2017-06-27-IDE-spyder_For_Python/spyder3.png)

from now on, You can code it with spyder like this. 

in temp.py, type in "print("hellow World)"

![](/img/Image/Languages/Python/2017-06-27-IDE-spyder_For_Python/hellowworld.png)

after that, you can check excutable like this :

![](/img/Image/Languages/Python/2017-06-27-IDE-spyder_For_Python/console.png)


# Reference 

 - [how to install pip](http://idroot.net/linux/install-pip-ubuntu-16-04/)
 
 - [spyder3 document](https://pythonhosted.org/spyder/installation.html)




