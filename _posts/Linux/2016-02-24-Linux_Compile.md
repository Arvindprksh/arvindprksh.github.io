---
layout: post
title: How to compile Linux
subtitle: Linux compile at CentOS 7.1 from kernel 3.7 to 4.5
category: Linux
tags: [linux, compile]
permalink: /2016/02/24/Linux_Compile/
---

# Agenda

운영체제 중 리눅스계 운영체제는 다양한게 존재한다. 예를 들어 Ubuntu, CentOs, Mint 등 다양한 종류가 있다.
커널을 컴파일을 할때 자기의 운영체제가 어떤 운영체제인지 확인을 하는 것이 중요하다. 
그래야 내가 사용할 software management package를 어떤 것을 써야 하는지 알수가 있기 때문이다. 
즉, 커널을 컴파일하기전에 각 운영체제에 맞는 컴파일하는 필요한 도구가 있기 때문이다. 
난 이번에 Centos 7.1에서 리눅스를 컴파일 하기로 했다. 

Mainly I used **yum**

# Before compile, if you normal user, Just you have to get privilege

* add user in /etc/sudoers file for getting privilege.

```shell
$ su
Password: 
# chmod u+w /etc/sudoers
# vim /etc/suoers
---write "user ID  ALL=(ALL)  ALL" on the last line in /etc/sudoers or below "root ALL=(ALL) ALL"----   
# chmod u-w /etc/sudoers
# exit
```

above instruction is method to give user sudo privilege.

아래의 두개의 참조는 사용자에게 sudo권한을 주는 것이다. 즉 다시 말하면 커널을 root 유저가 privilege을 가지고 있는데 이것을 일반 유저가

저 privilege을 가지기 위한 설정을 하는 것이다. /etc/sudoers 파일을 수정해서 말이다.

In other words, the following is introduction which configures sudoers file.

<a href = "http://blueray21.tistory.com/15">reference1</a>

<a href = "https://www.centos.org/docs/5/html/5.2/Deployment_Guide/s3-wstation-privileges-limitroot-sudo.html">reference2</a>

if you know more sudores file, pleas link to <a href = "https://www.garron.me/en/linux/visudo-command-sudoers-file-sudo-default-editor.html">this site</a> 

이제부터 본격적인 이야기를 하기로

1. wget을 이용하여 컴파일 할 소스를 다운 로드 

2. make mrproper -> 각종의 연관성 (denpendcy) 을 지우는 작업 -> 굳이 안해도 됨

3. make menuconfig -> 컴파일시 어떻게 할 것인지에 대한 환경설정

4. make clean -> 이전에 했던 잔재이 .o(a compiled file) .ko(module file)를 제거하는 과정

5. make -> 이제 kernel 생성(make bzimage와 비슷)
 
6. make modules -> 각종 모듈을 생성  -> you don't have to do this process, just make is enough

7. make modules_install -> 생성한 모듈 설치 

8. make install -> 생성한 커널 설치 

**If you compile kerenl with old .config file, don't type make mrproper and before make menuconfig, just make oldconfig or make olddefconfig**

좀더 자세히 알고 싶다면 <a href = "http://net2free.tistory.com/230">이 사이트 참조</a>

이 사이트는 위의 커널 설치 과정을 좀더 자세하게 설명을 하고 있다. 

하지만 만약 커널 컴파일 과정을 정확히 알고 싶다면 <a href = "http://lxr.free-electrons.com/">kernel source browser.</a>을 보기 바란다.

아래의 참조 사이트 너가 만약 CENTO user라면 커널 컴파일 시 필요한 소프트웨어 package에 대한 이야기를 해분다.  

<a href = "https://wiki.centos.org/HowTos/Custom_Kernel">이 사이트 basic management software</a>

그리고 내가 centos 7.1에 커널 4.4/4.4.6/4.5을 설치하기 위해서 커널 빌드시 openssl 에 대한 오류가 발생을 했다. 

그때 해결이 된 사이트가 바로 아래의 사이트이다.

<a href = "http://unix.stackexchange.com/questions/105969/installing-openssl-shared-libraries-on-centos-6-5
">during compile, openssl error resolution</a>

그리고 우분투에서 커널을 디버깅 하는 법을 설명하는 아래 사이트도 참조하면 괜찮을 듯 

<a href = "http://www.cyberciti.biz/faq/debian-ubuntu-building-installing-a-custom-linux-kernel/">우분투 컴파일</a>

linux-4.4.tar.xz is uncompressed with " xz -cd linux-4.X.tar.xz \| tar xvf -".

[this site](http://www.cyberciti.biz/faq/debian-ubuntu-building-installing-a-custom-linux-kernel/) explains also you kernel compile 

----------------------------------------------------------------------------------------------------------------------------

the following is what I realize while I testing Ane 

below is final summary of compiling kernel

## 1  Round : yum groupinstall "Development Tools"

as soon as you install the host OS(in my case CentOs 7)    

you have to install utility for this procedure.   
 
```shell
----------------- Utility installation on CentOs for development--------------
$ sudo yum groupinstall "Development Tools"
-----------------------------------------End----------------------------------
```
      
If you cannot do the above thing. focus on the following.       
      
**BUT,** If you cannot use sudo privilege, You need to get privilege of sudo. As follows.   

```shell
--------------------how to get sudo privilege of userID-------------------------- 
$ su
# chmod u+w /etc/sudoers
# vim /etc/suoers
---write "user ID  ALL=(ALL)  ALL" on the last line in /etc/sudoers or below "root ALL=(ALL) ALL"----   
# chmod u-w /etc/sudoers
# exit
-----------------------------------------End----------------------------------------
$ reboot OR shutdown -r now  --> command for rebooting 
```
     
Now, you can use "yum groupinstall "Development Tools"

But you need a little tools for kernel compiling

**BUT**, you can get lock of yum, then reboot system or <strong>reboot yum. 

But I have not tried to reboot yum yet. So this is just my assumption</strong>

So I test it you can release the lock, after rebooting. 

another way is there, but In my case, this is easiest. 

In CentOS, Tool is needed for kernel compile, Please reference [this CentOS site](https://wiki.centos.org/HowTos/Custom_Kernel)

```shell
-------------------Tools is needed for kernel compile----------------------------------
$ yum groupinstall "Development Tools" OR $ yum groupinstall -y "Development Tools"
$ yum install ncurses-devel OR $ $ yum install -y ncurses-devel
$ yum install qt-devel OR $ yum install -y qt-devel
------------------------------------------------------------------------------------
```

The above is minimum Tools. depending on your enviroments, you might need more. 

**Now** I start the kernel compile. 

**Be careful, if you are developer of kernel, You have to refer to [document of linux github](https://github.com/torvalds/linux).**

if you refer to that site, you can get more information.

kernel compile explanation site,[free-electros](http://lxr.free-electrons.com/)

kernel source download site, [kernel.org](https://www.kernel.org/)

if you want to know make, visit two site. 

one is [stackoverflow](http://stackoverflow.com/questions/4178526/what-does-make-oldconfig-do-exactly-in-the-linux-kernel-makefile)

another one is [linux's document(kconfig.txt) of kbuild](https://github.com/torvalds/linux/tree/master/Documentation/kbuild)

Another [stackoverflow](http://serverfault.com/questions/116299/automatically-answer-defaults-when-doing-make-oldconfig-on-a-kernel-tree)

```shell
---------------------------------procedure of kernel compile--------------------------------
- download kernel source from [kernel.org](https://www.kernel.org/)
- OR if you develop the specific case kernel, download from the specific site that give you the kernel source.
$ git clone https://github.com/OpenChannelSSD/linux.git --> this is my case for opensource analysis
$ cd linux
- If you use old config 
$ cp /usr/src/kernels/3.10.0-327.36.1.el7.x86_64/.config /linux-4.8/.config
- OR you do not need to 
$ make defconfig
- But if you use the old .config, the following is what I recommend you for kernel compile. 
$ make oldconfig OR $ make olddefconfig
$ make menuconfig
$ make -j8 
- if you encouter errore. install the next one
$ sudo yum install openssl-devel

$ sudo make modules_install
$ sudo make install

- But If you have to make again, 
$ make clean
$ make menuconfig
$ make -j8
$ sudo make modules_install
$ sudo make install
--------------------------------------------------------------------------------------------
```

In case of make error, solution is [StackExchage](http://unix.stackexchange.com/questions/105969/installing-openssl-shared-libraries-on-centos-6-5) 

so far, Just this is about using opensource kernel.

below is using kernel that redhat or CentOS 7 manage 

And the following introduce another way of kernel compile. 

## 2 Round : Install kernel on CentOS 7 

### 2 - 1. Round : Basically If you want to install kernel(linux) that Centos7 manage

In other words, Just you need one command. In order to change kernel from CentOS Linux releas 7.1(Core) to 7.2 (Core)
  
```shell
----------------- kernel upgrade with the most simplest way--------------------
$ sudo yum update
 **This is just to update the whole thing involved in system of the Current system. **
---------------------------End----------------------------------------
```
     
I just found out [another way, liquidweb](https://www.liquidweb.com/kb/how-to-update-the-kernel-in-centos-red-hat/)   
      
```shell
--------------------------- The another way in [the URL,liquidweb.](https://www.liquidweb.com/kb/how-to-update-the-kernel-in-centos-red-hat/)--------------------------------------------------------------
$ sudo yum -y update kernel
-----------------------------End--------------------------------
```

In above case, I'm not sure it works. 
   
**BUT,** If you want to update to the latest stable kernel.
You have to use [ELREPO site](http://elrepo.org/tiki/tiki-index.php) of The Community Enterprise Linux Repository   
  
And in order to get started with installation of ELREPO. You need pre-requisite. 

**In my case of CentOS 7**  
  
  
----------[Get started with Pre-Requisite in elrepo.org](http://elrepo.org/tiki/tiki-index.php) to Add ELREO repository-------------------   
   
// **Import the Public Key**  
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org (external link)  
  
**For example in command line**  
  
```shell
$ sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
     
// **to install ELRepo for RHEL-7, SL-7 or CentOs-7**  
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm (external link)   
       
**For example, in command line**    
    
```shell
$ sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
Retrieving http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
Preparing...                          ################################# [100%]
Updating / installing...
    1:elrepo-release-7.0-2.el7.elrepo  ################################# [100%]
```
      
** If you want know more, I recommend [this site of Install Lastes Stable kernel On CentOS 6 and 7](https://www.unixmen.com/install-latest-stable-kernel-centos-6-7/)**

------------------------------End--------------------------------

**Now** You can start installing of the latest kernel

**In my case of kernel 4.8.0**

```shell
----------------------[kernel upgrade with ELRepo](http://elrepo.org/tiki/kernel-ml)---------
$ sudo yum --enablerepo=elrepo-kernel install kernel-ml
   
- (option) to update
$ sudo yum --enablerepo=elrepo-kernel update
--------------------------------------------End---------------------------------
```
   
#### 2 - 2. Round : Only after compiling kernel source from [Kernel.org(Linux kernel Archives)](https://www.kernel.org/), Way to install the kernel on The CentOS 7     

Before just reading this following article. I recommed you [a site for kernelnewbies](https://kernelnewbies.org/KernelBuild), on the site, You can check up kernel build process. If you understand contents of the kernel newbies. 

I think you don't have to read this following article. **but** if your setting is CentOS 7, I recommed you to read this following article.

First, if you want know about kernel compiling right away, I recommend you to see [this site](http://linoxide.com/how-tos/install-linux-kernel-4-0-elrepo-source/) written on April 14, 2015

[another explanation of compile linux](http://jensd.be/589/linux/complile-and-use-a-realtime-kernel-on-centos-7-or-rhel-7)

Just This method is that you have download kernel source from [Linux kernel Archives](https://www.kernel.org/)  
  
Basically, If you know about compiling kernel, I recommend you [Linux Cross Reference site](http://lxr.free-electrons.com/)  
  
**In my case, I used the linux-4.8.tar.xz on CentOS 7**  
    
First of all, You need depedency required to compile the linux kernel. 

Before the following, the above is summary of next thing that I explain.

```shell
------------------------------------Installing the Dependencies-----------------------------------------
$ sudo yum groupinstall 'Development Tools'

**If you need more dependencies after the above command, Do not worry, Just install what you need.**
yum install ~~~~

**In my case. I installed more besides "Development Tools"  as follows **
$ sudo yum insatll -y openssl-devel
$ sudo yum install ncurses-devel
$ sudo yum install qt-devel
     
- Minimum condition of compiling linux without "$ sudo yum groupinstall "Development Tools"

$ yum install -y gcc bc openssl-devel ncurses-devel pciutils libudev-devel
-----------------------------------------------End--------------------------------------------------------
```

**Now** let's install. 

```shell
------------------------Installation precedure------------------------------
// First, get kernel source from [Linux Kernel Archive](https://www.kernel.org/pub/linux/kernel/v4.x/)
$ wget https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.8.tar.xz
   
// Second, decompress the above linux-4.8.tar.xz file
the decompressed method is divided into two ways.
first of all, decompress under the current location.

$ xz -cd linux-4.X.tar.xz | tar xvf -

second of all, extract under /usr/src

$ tar -xf linux-4.8.tar.xz -C /usr/src/

// Now, move into the decompressed folder.
$ cd linux-4.8   OR   cd /usr/src/linux-4.8/
 
// the below is option // this command erase the file of .config file on linux-4.8
// so unless it is first time. I do not recommand this command. 
make mrproper

$ make mrproper
CLEAN .config 

after issuing "ls -alt" on the linux directory. .config file disappears. 
So you have to try to copy or remake .config again.
   
// configure a .config file 
**In my case, I used the /usr/src/kernels/3.10.0-327.36.1.el7.x86_64/.config**
$ cp /usr/src/kernels/3.10.0-327.36.1.el7.x86_64/.config /linux-4.8/.config

$ make oldconfig OR $ make menuconfig
$ make 
OR if you want to use more cores.
$ make -j<4 - this is the number of cores>
 
// this below is option 
$ make modules 
// even though the above command is not implemented, you can install the whole thing,
//In other words, "make" command means build .o and .ko file, compiling source files and making modules.

sudo make modules_install install

after reboot, If you want to check if installation is done well
$ uname -a OR uname -r
-------------------------------------End----------------------------------------------
```
when you boot kernel, If you want to change order of default booting 

just do it as follows. 

```  
when you boot the linux, if you want to configure order of booting. 
you have to pay attention the following command 
$ grep ^menuentry /boot/grub2/grub.cfg | cut –d\’ –f2
$ grub2-editenv list
$ grub2-set-default 0
```
but I'm not sure the above commnd(grep, grub2-*), Becuse I didn't do it. 

I think I don't need it

** you cannot use yum due to lock **

just click [this site](http://www.ehowstuff.com/how-to-resolve-another-app-is-currently-holding-the-yum-lock-waiting-for-it-to-exit/) 
