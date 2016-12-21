---
layout: post
title: Blue_DBM driver open source analysis
subtitle: code analysis of open Source with linux module command
category: SSD (Solid State Drives)
tags: [lightnvm, block device driver]
permalink: /2016/09/06/Ananlysis_Of_OpenSource_Blue_DBM/
---

The previous analysis is brief outline and process of device driver installation and removal.  

From now on, I will analyze Blue_DBM in this article. 

Let's start into code of blueDBM driver.

### Insmod and rmmod

  The **Insmod** command allows the installation of the module in the kernel. 
  
  # insmod nvme.ko
  
  The **lsmod** command allows you to verify if the module is installed correctly. 
  
  # lsmod
  
  # lsmod | grep nvme
  
  The **rmmod** command allow you to remove the module that you want 
  
  # rmmod nvme
  
  If you want to check whether module is removed, Just once again, use **lsmod** command
  
  
## Source tree of mounting Blue_DBM driver.

<!--- ef6b86e92aeb0feb87f3800e9547698e5d63ac4a is commit number, that is basic source to understading this source, Blue_DBM driver -->

  When you insert module with kernel, You issue **insmod**, At this time, kernel execute **module_init("name of function for initailization")** 
  
  So you have to always look for **module_init("name of function for initailization")**, So you can understand to register module. 
  
  On the other hand, when you use **rmmod** command, you have to search for **module_exit("name of function for exit of module")**
  
  At this time you would find flow of exit function of module. 
  
  This [URL](https://www.mindmup.com/#m:h1hyunyoung2/hyunyoung2.github.io:master:/img/Image/SSD-Solid_State_Drives/2016-09-06-Ananlysis_Of_OpenSource_Blue_DBM/
/Flow_of_module_init_and_exit.mup) is arrangement of bdbm_drv about module_init( ) and module_exit( )
 
  ![](/img/Image/SSD-Solid_State_Drives/2016-09-06-Ananlysis_Of_OpenSource_Blue_DBM/Flow_of_module_init_and_exit.png)
 
### register of Blue_DBM.ko 


<!-- this source base on git commit version number of beebb6152b803f213df6ed80c1c3ff1f72f4125a, be careful. -->

  [URL](https://www.mindmup.com/#m:h1hyunyoung2/hyunyoung2.github.io:master:/img/Image/SSD-Solid_State_Drives/2016-09-06-Ananlysis_Of_OpenSource_Blue_DBM/
/Register%20of%20Blue_DBM.ko.mup)
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-09-06-Ananlysis_Of_OpenSource_Blue_DBM/blue_DBM flow of register function.png)
