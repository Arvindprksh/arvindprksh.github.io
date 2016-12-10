---
layout: post
title: Mounting Filesystem
subtitle: how to mount filesystem, For example F2FS
css:
tags:
date:
big-image:
share-image:
permalink:
comments:
show-share:
big-image:
meta-title:
meta-description:
---

# f2fs 
  
  This filesystem is friendly-flash file system, maybe if you know this more, click [this site(googlesource)](https://android.googlesource.com/kernel/common/+/22f837981514e157f8f9737b25ac6d7d90a14006/Documentation/filesystems/f2fs.txt)


```
기본 : 바이트 주소

LBA  : 섹터주소,  (섹터주소 X 512 = 바이트 주소)

BLK Addr : 블록 주소, (블록주소 x 4096 = 바이트 주소)

Seg Addr : 세그먼트 주소( 세그먼트 주소 x 2MB = 바이트 주소)
```

## Basic concept

if you want mount, basically, you have to read [this site(cray)](http://docs.cray.com/books/S-2377-22/html-S-2377-22/z1029459193.html) which explains mount process. 
  
just, [the site(cray)](http://docs.cray.com/books/S-2377-22/html-S-2377-22/z1029459193.html) shows you mount, in other words, if you test new device which doesn't have file system. after mkfs instruction. maybe it's better to see [the site(cray)](http://docs.cray.com/books/S-2377-22/html-S-2377-22/z1029459193.html).
  
## Install   

  basically, to install file system on linux [this site(thegeekstuff)](http://www.thegeekstuff.com/2013/01/mke2fs-examples/) explains what you have to know.
  
  First, you refer to [this site(googlesource's README)](https://kernel.googlesource.com/pub/scm/linux/kernel/git/jaegeuk/f2fs-tools/+/v1.6.1/README) and this install is version 1.6.1.
  
  The install above explains how to partition to use f2fs filesystem, 

  f2fs have dependency on _libuuid-devel or uuid-dev, pkg-config, autoconf, libtool_
  
  when I install the packages, my environment is the following 
 
```shell 
  [hyunyoung.lee@localhost Downloads]$ cat /etc/centos-release
  CentOS Linux release 7.2.1511 (Core) 
```  
  on Centos, in case of libuuid-devel or uuid-dev
  
  - libuuid-devel :  the following command in linux :
  sudo yum install libuuid-devel 
  
```shell
  [hyunyoung.lee@localhost Downloads]$ sudo yum install libuuid-devel  
  [sudo] password for hyunyoung.lee:   
  Loaded plugins: fastestmirror, langpacks  
  base                                                     | 3.6 kB     00:00       
  extras                                                   | 3.4 kB     00:00     
  updates                                                  | 3.4 kB     00:00     
  Loading mirror speeds from cached hostfile
  * base: mirror-centos.hostingswift.com
  * extras: centos-distro.cavecreek.net
  * updates: centos.mirrors.hoobly.com
  Package libuuid-devel-2.23.2-26.el7_2.2.x86_64 already installed and latest version
  Nothing to do
```
  - uuid-dev : The following command in linux :
  sudo yum install uuid-dev 
  
```shell 
 [hyunyoung.lee@localhost Downloads]$ sudo yum install uuid-dev  
 Loaded plugins: fastestmirror, langpacks  
 Loading mirror speeds from cached hostfile  
 * base: mirror-centos.hostingswift.com  
 * extras: centos-distro.cavecreek.net  
 * updates: centos.mirrors.hoobly.com  
 No package uuid-dev available.  
 Error: Nothing to do  
```

  but if you change the commad, it is :  
  sudo yum install uuid-devel  

```shell  
  [hyunyoung.lee@localhost Downloads]$ sudo yum install uuid-devel  
  Loaded plugins: fastestmirror, langpacks  
  Loading mirror speeds from cached hostfile  
  * base: mirror-centos.hostingswift.com  
  * extras: centos-distro.cavecreek.net  
  * updates: centos.mirrors.hoobly.com  
  Package uuid-devel-1.6.2-26.el7.x86_64 already installed and latest version  
  Nothing to do
```  
  - pkg-config  
  
  sudo yum install pkg-config

```shell
  [hyunyoung.lee@localhost Downloads]$ sudo yum install pkg-config  
  Loaded plugins: fastestmirror, langpacks  
  Loading mirror speeds from cached hostfile  
  * base: centos.chicago.waneq.com  
  * extras: centos-distro.cavecreek.net  
  * updates: mirror.spro.net  
  No package pkg-config available.  
  Error: Nothing to do  
```
  
  because of the text above. I would use rpm of software managment tool.   
  If you know more about rpm, click to [this site(s1-rpm-using)](https://www.centos.org/docs/5/html/Deployment_Guide-en-US/s1-rpm-using.html)
  
  the place where I download is [this site(pkgconfig-0.27.1-4.el7.x86_64)](https://rpmfind.net/linux/RPM/centos/7.2.1511/x86_64/Packages/pkgconfig-0.27.1-4.el7.x86_64.html).  
  
  The following is process of using rpm.  

```shell
  [root@localhost Downloads]# rpm -Uvh pkgconfig-0.27.1-4.el7.src.rpm   
  Updating / installing...    
  1:pkgconfig-1:0.27.1-4.el7         ################################# [100%]    
  warning: user mockbuild does not exist - using root    
  warning: group mockbuild does not exist - using root    
  warning: user mockbuild does not exist - using root    
  warning: group mockbuild does not exist - using root    
  warning: user mockbuild does not exist - using root    
  warning: group mockbuild does not exist - using root    
```
  
  So I solve the problem above, I installed mock,"sudo yum install mock"  

```shell  
  [hyunyoung.lee@localhost ~]$ sudo useradd -s /sbin/nologin mockbuild  
  [hyunyoung.lee@localhost Downloads]$ sudo rpm -ivh pkgconfig-0.27.1-4.el7.src.rpm   
  Updating / installing...  
    
  1:pkgconfig-1:0.27.1-4.el7         ################################# [100%]  
```
  - autoconf : the command is sudo yum install autoconf  
  
```shell
  [hyunyoung.lee@localhost Downloads]$ sudo yum install autoconf  
  [sudo] password for hyunyoung.lee:   
  Loaded plugins: fastestmirror, langpacks  
  Loading mirror speeds from cached hostfile  
  * base: centos.chi.host-engine.com  
  * extras: centos-distro.cavecreek.net    
  * updates: centos.mirrors.hoobly.com  
  Package autoconf-2.69-11.el7.noarch already installed and latest version  
  Nothing to do  
```

  - libtool : the command is sudo yum install libtool  

```shell   
  [hyunyoung.lee@localhost Downloads]$ sudo yum install libtool  
  Loaded plugins: fastestmirror, langpacks  
  Loading mirror speeds from cached hostfile  
  * base: mirror-centos.hostingswift.com  
  * extras: centos-distro.cavecreek.net  
  * updates: centos.mirrors.hoobly.com  
  Package libtool-2.4.2-21.el7_2.x86_64 already installed and latest version  
  Nothing to do  
```

  then the following in command line is :  
  
```shell
   autoreconf --install     
   ./configure    
   make    
```

  after that, just you get in the folder,mkfs. and you type instruction,sudo sudo ./mkfs.f2fs -l f2fs /dev/nvme0n1.  
  
  and ssd is formatted to f2fs.  

```shell   
  [hyunyoung.lee@localhost mkfs]$ sudo ./mkfs.f2fs -l f2fs /dev/nvme0n1

	>F2FS-tools: mkfs.f2fs Ver: 1.6.1 (2016-03-22)

  Info: Debug level = 0  
  Info: Label = f2fs  
  Info: Segments per section = 1  
  Info: Sections per zone = 1  
  Info: Trim is enabled  
  Info: sector size = 512  
  Info: total sectors = 1875385008 (915715 MB)  
  Info: zone aligned segment0 blkaddr: 512  
  Info: format version with  
  "Linux version 4.5.0 (hyunyoung.lee@localhost.localdomain) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-4) (GCC) ) #6 SMP Fri   >Apr 29 19:51:20 PDT 2016"  
  Info: Discarding device  
  Info: Discarded 1875385008 sectors  
  Info: Overprovision ratio = 0.210%    
  Info: Overprovision segments = 1917 (GC reserved = 960)  
  Info: format successful   
```

  when The mkfs instruction is impelemented, trim instruction is implemented to ssd. 
  
  <!--
  USB -> URAT(using console prog tera term Baoud Rate 38400

  trim
  
  trim
  -->

  next time, I will mount f2fs to my computer directory

  sudo mount -t f2fs /dev/block_device /home/hyunyoung.lee/mnt/f2fs

  [hyunyoung.lee@localhost f2fs]$ sudo insmod f2fs.ko

```shell
 [hyunyoung.lee@localhost mkfs]$ lsblk  
 NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT  
 sda           8:0    0 119.2G  0 disk   
 ├─sda1        8:1    0   500M  0 part /boot  
 └─sda2        8:2    0 118.8G  0 part   
 ├─cl-root 253:0    0    50G  0 lvm  /  
 ├─cl-swap 253:1    0   7.8G  0 lvm  [SWAP]  
 └─cl-home 253:2    0    61G  0 lvm  /home  
 nvme0n1     259:0    0 894.3G  0 disk /home/hyunyoung.lee/mnt/f2fs  
```
 
 Now I will analyze the kernel f2fs source file for whether metadata is suqeuntial or not.


 a sequential part of six areas is main area and metadata areas are ramdom write.
 
 For tatal information, see in [this site(klf2012_j_kim)](http://events.linuxfoundation.org/images/stories/pdf/klf2012_j_kim.pdf).


### What is the yum different fom rpm

  if you know more, just refer to [this site(difference-between-yum-and-rpm)](www.differencebetween.net/technology/difference-between-yum-and-rpm/).
  
  first. resultally, rpm and yum is software package management. but yum is much easier than rpm.
  
### file system
	
   파일 시스템은 논리적으로 데이터를 어떻게 관리를 할 지를 나타내는 것이다.
   논리적인 구조를 블럭디바이스에 mounting을 하고 난 후에 FTL은 논리적인 주소를 물리적인 주소로 맵핑을 해준다. 그런데 낸드플래시 메모리에 프로그래밍을 할 수 있는 단위로 최대한 맞추어서 프로그래밍을 하도록 FTL은 그런 역활을 하고 그리고 가비지 콜렉션이 골고루 되게 하기 위해서 wear-leveling을 한다. 이 두개가 FTL의 대표적인 기능이다. 
 
   if you want to know more about dentry, inode, click to [this site(vfs)](http://www.fieldses.org/~bfields/kernel/vfs.txt) and [site2(what-is-a-superblock-inode-dentry-and-a-file)](http://unix.stackexchange.com/questions/4402/what-is-a-superblock-inode-dentry-and-a-file)
 
### structure of f2fs metat data 

  if you want to know this, click to [this site(f2fs-checkpoint-data-structure)](http://esos.hanyang.ac.kr/tc/david/entry/f2fs-checkpoint-data-structure) 
  
  The following is fixing mount table
  
  /etc/fstab file is managing mount table
	
  the content below is my adding

  /dev/nvme0n1        /home/hyunyoung.lee/mnt/f2fs   f2fs    defaults   0 0

 if you want to know more, please click [this site(tistory)](http://naito.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4fstab-%EB%B6%80%ED%8C%85%EC%8B%9C-%EC%9E%90%EB%8F%99-%EB%A7%88%EC%9A%B4%ED%8A%B8)

### statr part of checking sequence of metadata

   in /fs/f2fs/super.c

```shell  
   function int f2fs_sync_fs(struct super_block sb*, int sync)
   	-> write_checkpoint fucntion checking

Linux kernel version(4.5) / fs / f2fs / super.c  
int f2fs_sync_fs()

		-> write_checkpoint()
			-> flush_nat_entries() & flush_sit_entries() 
				-> for example(in flush_nat_entries()), __flush_nat_entry_set
					-> raw_reset_form_node_info , here is raw write. 
  
				-> for example(int flush_sit_enrites()), here is raw wirte.
```

if you search about SSA, take care of npages_for set_summary function. 

my environment is centos 7.2 linux version 4.5
