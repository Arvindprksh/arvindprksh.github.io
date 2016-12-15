---
layout: post
title: Performance of F2FS(F2 filesystem)
subtitle: How did they measure the performance of F2FS ?
css:
category:
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
show-avatar: false
nav-short: true
---

I qoute paper of [F2FS : A New File system For Flash Storage](https://www.usenix.org/system/files/conference/fast15/fast15-paper-lee.pdf) from [USENIX](https://www.usenix.org/),

Because I want to know how they measured Filesystem with some factor.

# What is the F2FS ?

As of now, I understand F2FS is designed for SSD. 

![](/img/Image/SSD-Solid_State_Drives/2016-12-12-How_To_Check_Performance_Of_F2FS/On-Disk layout of F2FS.png)

As you can see the picture. F2FS makes Data area sequential to run SSD efficiently. 

ans F2FS uses log_structure's concept to make Data area sequential. 

In here, I want to know how they measured F2FS's performance. So I will summarize it in the current my gitpage. 

figure below is File structure of F2FS.

![](/img/Image/SSD-Solid_State_Drives/2016-12-12-How_To_Check_Performance_Of_F2FS/File structure of F2FS.png)

# Evaluation of F2FS 

## Specification of the platforms is evaluated with F2FS

![](/img/Image/SSD-Solid_State_Drives/2016-12-12-How_To_Check_Performance_Of_F2FS/Summary of Benchmarks in F2FS paper.png)

As you can see the above figure, Benchmark of F2FS is carried out in two broadly target systems. 

One is mobile system and the other one is server system. 

according to the paper(F2FS : A New File system For Flash Storage), Mobil system is Calaxy S4, and **Sever system is x86 platform**.

Moreover, In case of Server system. they use SATA SSD and PCIe SSD.

The workload of F2F2 benchmark splits into Several factors. the factors is :

 - **Sequantial read /write and Random Read / write bandwidth in MB/s**
 
 - In case of banwidth, using simple single thread application that triggers 512KB sequential I/Os and 4KB random I/O random write with O_DIRECT
    
     **my qeustion, What is the O_DIREDT ? I think that is option in filesystem.**
     
 F2FS compares with **EXT4, BTRFS, NILFS2**
 
  - EXT4 is a widely used file system
  
  - BTRS is a copy-on-write file system

  - NILFS2 is a LFS. 
  
 As you can see the above Summary of Benchmarks. Summary consists of characteristics in terms of :
 
  - generated I/O patterns
  
  - the number of touched files. 
  
  - the ratio of reads and writes(R/W)
  
  - Whether they contain fsync system calls
  
 For server benchmark, F2FS uses tools :
 
  - synthetic benchmark called Filebench with a different I/O pattern and fsync usage
  
 After reading this F2FS paper, The scenario is differenct depending on that type of Server. 
  
  - Videoserver issues mostly sequential reads and writes. 
  
  - Fileserver per-allocates 80,000 files with 128KB data and Subsequently starts 50 threads, each of which creats and delets files randomly as well as reads and appends small data to randomly chosen files. thus, This workload represents a scenario having many large files touched by buffered random wirtes and no **fsync**.
  
  - Varmail creates and deletes a number of small files with **fsync**. 
  
  - oltp pre-allocates ten large files and update their data randomly with fsync with 200 threads in parallel. 
  
  if you want to know result of the above benchmarks. I recommend you to read this paper, [F2FS : A New File system For Flash Storage](https://www.usenix.org/system/files/conference/fast15/fast15-paper-lee.pdf)

# Reference

  - [F2FS : A New File system For Flash Storage](https://www.usenix.org/system/files/conference/fast15/fast15-paper-lee.pdf)
  
  - [Wikipedia's SQL Lite](https://en.wikipedia.org/wiki/SQLite) - means a relational database management system contained in a c programming library.
 
