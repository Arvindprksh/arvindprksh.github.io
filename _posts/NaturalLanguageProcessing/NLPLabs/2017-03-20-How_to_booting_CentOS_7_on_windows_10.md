---
layout: post
title: How to do multi-booting CentOS 7 on Windows 10 
category: Natural Language Processing Labs
tags: [multibooting]
permalink: /2017/03/20/How_to_booting_CentOS_7_on_windows_10/
big-image:
   - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

I will show you what I experienced to acheive multi-booting CentOS 7 on Windows 10. 

First of all, I installed Window first than CentOS,

Just when I was searching for it, many of blogs show me I have to install windows first than linux. 

So, basically, You have to install windows, after that, you need to install Linux(CentOS 7)


1. install windows. 


2. check disk management to install linux. 

  2-1. you have to check if your computer have available space to install linux. 
  
      without it, You have to make it, available sapce to install linux. 
      
      It is easy to make it. 
      
      the method is : 
      
      first you click right button of mouse, after that, press "shrink volume"
      
      If you do as I said above. you can get window as below.
      
 ![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-03-20-How_to_booting_CentOS_7_on_windows_10/Shrink_volume.PNG)
 
   on the above image. You have to make available space to install linux. 
   
 
 3. you need to make booting image on USB or CD. But in my case, I recommend you make USB-booting table. That is easy. 
 
  
  You can get tool to make booting USB from [here(https://rufus.akeo.ie/downloads/rufus-2.8p.exe](https://rufus.akeo.ie/downloads/rufus-2.8p.exe)
  
  After downloading it, keep in mind, befor making booting USB, you have to download CentOS.iso file 
  
  If you want to download CentOS.iso file, visit [CentOS's download page](https://www.centos.org/download/)
  
  If you execute the tool to make booting USB. you will get the image below
  
  ![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-03-20-How_to_booting_CentOS_7_on_windows_10/booting_USB.PNG)
  
  **Keep in mind in here, maybe you have to configure disk form and booting system to GPT partition's UEFI**
  
  In my case, my computer's booting way was to use UEFI. So When I used MBR(master boot record), I couldn't get started after installation of Centos. 
  
 
 4. after Rufus,  You need to reboot to install Centos 7
 
 
 5. from now on, just install CentOS 7 in turn. If you cannot boot into USB. **You need to use BIOS to configure the order of booting.**
 
 the way to enter BIOS is different per manufacturers. normally, press ESC key or F11.
 
 
 IF you want to know why you make booting USB to UEFI mode. 
 
 
 **search for "What is the MBR and UEFI"**
  
  
# Reference 

 - [CentOS windows ](http://kde713.tistory.com/13)
    
 - [MBR and UEFI 1](http://cappleblog.co.kr/131)

 - [MBR and UEFI 2](http://blog.naver.com/PostView.nhn?blogId=leekh8412&logNo=100132406507)

