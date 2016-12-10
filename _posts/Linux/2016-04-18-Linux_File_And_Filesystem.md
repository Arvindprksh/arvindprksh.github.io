---
layout: post
title: Linux File and Filesystem
subtitle: Basic information of Linux File and Filesystem, and f2fs is familiar to SSD 
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

these contents refers to this **_[web site(tldp's sect_03_01)](http://tldp.org/LDP/intro-linux/html/sect_03_01.html)_ and _[another site1(tldp's filesystems)](http://www.tldp.org/LDP/sag/html/filesystems.html)_, _[site 2(filesystem)](http://www.tldp.org/LDP/tlk/fs/filesystem.html)_**

maybe if you don't understand the article, pleas click to [this site(Searchstroage's partition)](http://searchstorage.techtarget.com/definition/partition) and search for partition & mount

# 1. General overview of the linux file system.

## 1-1. Files

### 1-1-1. General

 A simple desription of the UNIX system, also applicable to Linux, is this :
  
 >"On a UNIX system, everything is a file: if something is not a file, it is a process."
 
 this statement is true because there are special files that are more than just files(named pipes and sockets, for instance), but to keep things simple, saying that everything is a file is an acceptable generlization. A Linux systme, just like UNIX, makes no difference between a file and a directory, since a directory is just a file containing names of other file. Programs, service, texts, images, and so forth, are all files. Input and output devices, and generally all devices, are considered to be files, according to the system. 
 
 In order to manage all those files in an orderly fashion, man likes to think of them in an ordered tree-like structure on the hard disk, as we know from MS-DOS(Disk operationg System) for instance. The large branches contain more branches, and the branches at the end contain the tree's leaves or normal files. For now, we will use this image of the tree, but we will find out later why this is not a fully accurate image.
 
### 1-1-1. Sorts of files

 Most files are just files, called regular files; they contain normal data, for example text files, executable files or programs, input for or output from a program and so on. 
 
 while it is reasonably safe to suppose that everything you encounter on a Linux system is a file, there are some exception.
 
  * Directories : files that are lists of other files. 
  * Special files : the mechanism used for input and output. Most special files are in /dev  
  * Links : a system to make a file or directory visible in mutiple parts of system's file tree.
  * (Domain) sockets : a special file type, similar to TCP/IP sockets, providing interprocess networking protected by the file system's access control.
  * Nameped pipes : act more or less like sockets and form a way for processes to communicatt with ecah other, without using network socket semantics.
 
 
## 1-2. About Partitioning

### 1-2-1. Why Partition?

 Most people have a vague knowledge of what partitions are, since every operationg system has the ability to create or remove them. It may seem stange that Linux uses more than one partition on the same disk, even when using the standard installation procedure, so some explanation is called for.
 
 One of the goals of having different partition is to achieve higher data security in case of disaster. By dividing the hard disk in partitions, data can be grouped and separated. When an accident occurs, only the data in the partition that got the hit will be damaged, while the data on the other partitions will most likely survive.
 
 This principle dates from the days when Linux didn't have journaled file systems and power failures might have lead to disaster. **The use of partitions reamins for security and robustness reasons, so a breach on one part of the system doesn't automatically mean that the whole computer is in danger. This is currently the most important reason for partitioning. A simple example : a user creates a script, a program or a web application that starts filling up the disk. If the disk contains only one big partition, the entire system will stop functioning if the disk is full. If the user stores the data on a separate on the separate partition, then only that partition will be affected, while the system partitions and possible other data partitions keep functioning.
 
 Mind that having a journaled file system only provides data security in case of power failur and sudden disconnection of storage dvices. This does not protect your data against bad blocks and logical errors in the file system. In those cases, you should use RAID(Redundant Array of Inexpensive Disks) solution.
 
 the article below refers to **_[http://www.linfo.org/journaling_filesystem.html](this)_ and [IBM description](http://www.ibm.com/developerworks/library/l-journaling-filesystems/) **
 > A journaling filesystem is a filesystem that maintains a special file called a journal that is used to repair any inconsistencies that occur as the result of an improper shutdown of a computer. Such shutowns are usually due to an interruption of the power supply or to a software problem that cannot be resolved without a rebooting.
 
### 1-2-2. Partition layout and types

 There are two kinds of major partition on a Linux system :
  
  * data partition : normal Linux system data, including the root partition containing all the data to start up and run the system; and 
  * swap partition : expansion of the computer's physical memory, extra memory on hard disk.
  
  the article below refers to **_[this site(linux's all-about-linux-swap-space)](https://www.linux.com/news/all-about-linux-swap-space)_** 
  > Linux has two forms of swap space : the swap partition and the swap file. The swap partition is an independent section of the hard disk used solely for swapping. No other files can reside there. The swap file is a specail file in the filessystem that resides amongst your system and data files.
  
Most systems contain a root partition, one or more data partitions and one or more swap partitions. Systems in mixed environments may contains partitions for other system data, such a partition with a FAT, or vFAT file system for MS Windows data. 

### 1-2-3. filesystems (using Disk and other storage media)

 > this contents refers to **[this website(tldp's filesystems)](http://www.tldp.org/LDP/sag/html/filesystems.html)** 
 >A filesystem is the methods and data strcutures that an operating system uses to keep track of files on a disk or partition; 

# 2. f2fs (f2 file system is flash-friendly file system)
 
## 2-1. An f2fs teardown

 This content refers to **[this website(lwn)](https://lwn.net/Articles/518988/)**
 
 This filesysem is targeted to flash storage with FTL(flash translation layer) already built in. this is based on **[the log-structured filesystem(LFS) design](http://blog.notdot.net/2009/12/Damn-Cool-Algorithms-Log-structured-storage)**. 
 
### 2-1-1. [Log-structured file system](https://en.wikipedia.org/wiki/Log-structured_file_system)
 
 briefly, A log-structured filesystem is a filesystem in which data and metadata are written sequentially to a circular buffer, called a log.
 
  > this content refers to **[this site(cubrid)](http://www.cubrid.org/blog/dev-platform/how-ssd-changing-software-architecture/) and [naverD2](http://d2.naver.com/helloworld/162498)**
 > Wear Leveling - Uses blocks equally for lifetime extension. Counts the number of writes per block, and selects and uses the bloks with the fewest counts.

 if you know more about ssd, please click to _[this site](http://www.extremetech.com/extreme/210492-extremetech-explains-how-do-ssds-work)._

## 2-2. [F2Fs : A NEw File System for Flash Storage ](https://www.usenix.org/system/files/conference/fast15/fast15-paper-lee.pdf)

 - segment is used to determine the initial file system metadata layout. 
 - a unit of F2FS consists fo segment, section, zone, the size is segment < section < zone.
 - In cleaning, F2Fs adopts greedy policy, besides F2FS reserves a small unused capacity because to using cleaning room.

 If you see summary of F2FS, please click to [this site(haifux)](http://haifux.org/lectures/293/f2fs.pdf)

the Following is application-managed Flash.  
[Application-Managed Flash Paper](https://www.usenix.org/system/files/conference/fast16/fast16-papers-lee.pdf)

 The paper above expains ALFS(AMF Log-structured File System).
 To Sum up, ALFS maintains an inode map, It is stored in inode-map  seegments. Check Point is written periodically or When a flush command is implemented. Logical segments reserved for check-points are called _check-point segments_.
 If you see figure 5 and 6, you can understand relationship of LFS with FTL.
 
 and if you know more about f2fs, here is a [brief site(f2fs)](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) about f2fs. and If you want more colorful text that is the same of the above, click [this site(googlesource)](https://android.googlesource.com/kernel/common/+/22f837981514e157f8f9737b25ac6d7d90a14006/Documentation/filesystems/f2fs.txt)
 

# 3. SSD 

## 3-1. Read, Writes, and erasure

 In read, writes, ssd can commit it with page unit. but In the erasure, SSD can commit it with block unit

 Trim is command in linux, and the operating system sends it to tell SSD which blocks are free in the file system index. 
 
 Without TRIM the disk is unable to know which blocks are in use by a file or which ones are marked as free space. This is because when a file is deleted, the only thing the OS does is to mark the blocks that were used by the file as free inside the file system index. But the OS won’t tell the disk about this. This means that over time the performance of the SSD disk will degrade more and more, and it don’t matters how much space you free, because the SSD won’t know about it.

 What is TRIM? TRIM was invented for solving this problem. TRIM is the name of a command that the operating system can send to tell the SSD which blocks are free in the filesystem. The SSD uses this information to internally defragment the blocks and keep free pages available to be written quickly and efficiently.

 you want to know about Trim more. It is like The following :
 
 you simply add the option "discard" in the mounting options at /etc/fstab. In other words, this means that whenever you delete a file, The OS will be reporting in real-time to the SSD which blocks were occupied by that file and are not longer in use.
 Then, The SSD shoud perform defragmentation and deletion of those internally blocks.
 
 eventually, Trim is performing garbage collection and then SSD prepares for taking new data into blcoks.

 If you know more about ssd, please click to [this site(neutrino)](http://blog.neutrino.es/2013/howto-properly-activate-trim-for-your-ssd-on-linux-fstrim-lvm-and-dmcrypt/)
