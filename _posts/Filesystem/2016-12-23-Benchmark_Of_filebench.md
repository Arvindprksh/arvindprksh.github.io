---
layout: post
title: Benchmark tool of filesystem - filebench
subtitle: How can I test filesystem with filebench
category: SSD (Solid State Drives)
tags: [filesystem, benchmark]
permalink: /2016/12/23/Benchmark_Of_filebench/
---

 As you can read [my blog](/2016/12/12/How_To_Check_Performance_Of_F2FS/), F2FS filesystem use filebench tool to verify filesystem.
 
 **So I need to this tool to verify the new f2fs filesystem.**
 
 this new f2fs is sequential about meta data and inode data. 
 
## What is the FileBench ?

 Filebench is a filesystem and storage benchmark that can generate a large variety of workloads. Unlike typical benchmarks it is extremely flexible and allows to specify application's I/O behavior using its extensive Workload Model Language(WML). Users can either describe desired workloads from scratch or use (with or without modifications) workload personalities shipped with filebench (e.g., mail-, web-, file- and database-server workloads). Filebench is equally good for micro- and macro-benchmarking, quick to set up, and relatively easy to use.  
 
## After Installing filebench

 If you use the filebench benchmark. you have to create the description of the workload(so-called workload personality) in WML Language.
 
 Typically, workload personalites are stored in files with .f extension. 
 
 let's see simple workload desrption from filebench git repository 
 
``` 
define fileset name="testF",entries=10000,filesize=16k,prealloc,path="/home/hyunyoung.lee/tmp"

define process name="readerP",instances=2 {
  thread name="readerT",instances=3 {
    flowop openfile name="openOP",filesetname="testF"
    flowop readwholefile name="readOP",filesetname="testF"
    flowop closefile name="closeOP"
  }
}

run 60
``` 
 
  in the above desription, you have to change path="/tmp" to mount postion(so-called location of folder) or device that mounted f2fs or another filesyste. 
  
  and then you store it with .f extension. let's say filename of the above description is "test.f"
  
  execution command 
 
```shell
filebench -f test.f
```

 the following is example of execution of filebench with the above description.

```shell
$ filebench -f test.f
Filebench Version 1.5-alpha3
WARNING: Could not open /proc/sys/kernel/shmmax file!  --> this error happened whe you execute filebench with USER MODE
It means that you probably ran Filebench not as a root. Filebench will not increase shared
region limits in this case, which can lead to the failures on certain workloads.
0.000: Allocated 173MB of shared memory
0.001: Fileset has no directory width around line 4
0.001: Populating and pre-allocating filesets
0.016: testF populated: 10000 files, avg. dir. width = 0, avg. dir. depth = -0.0, 0 leafdirs, 156.250MB total size
0.016: Removing testF tree (if exists)
0.019: Pre-allocating directories in testF tree
0.221: Pre-allocating files in testF tree
0.537: Waiting for pre-allocation to finish (in case of a parallel pre-allocation)
0.537: Population and pre-allocation of filesets completed
0.537: Starting 2 readerP instances
1.539: Running...
61.544: Run took 60 seconds...
61.544: Per-Operation Breakdown
closeOP              14241044ops   237331ops/s   0.0mb/s      0.0ms/op [0.00ms - 27.61ms]
readOP               14241048ops   237331ops/s 3708.3mb/s      0.0ms/op [0.00ms - 24.88ms]
openOP               14241048ops   237331ops/s   0.0mb/s      0.0ms/op [0.00ms - 16.31ms]
61.544: IO Summary: 42723139 ops 711991.797 ops/s 237331/0 rd/wr 3708.3mb/s   0.0ms/op
61.544: Shutting down processes
```

 but if you change to root mode with su 
 
```shell
$ su                                         
Password: 
[root@localhost hyunyoung.lee]# filebench -f test.f
Filebench Version 1.5-alpha3
0.000: Allocated 173MB of shared memory
0.002: Fileset has no directory width around line 4
0.002: Populating and pre-allocating filesets
0.015: testF populated: 10000 files, avg. dir. width = 0, avg. dir. depth = -0.0, 0 leafdirs, 156.250MB total size
0.015: Removing testF tree (if exists)
0.569: Pre-allocating directories in testF tree
0.892: Pre-allocating files in testF tree
1.189: Waiting for pre-allocation to finish (in case of a parallel pre-allocation)
1.189: Population and pre-allocation of filesets completed
1.189: Starting 2 readerP instances
2.191: Running...
62.195: Run took 60 seconds...
62.195: Per-Operation Breakdown
closeOP              14213026ops   236868ops/s   0.0mb/s      0.0ms/op [0.00ms - 17.44ms]
readOP               14213027ops   236868ops/s 3701.1mb/s      0.0ms/op [0.00ms - 20.84ms]
openOP               14213029ops   236868ops/s   0.0mb/s      0.0ms/op [0.00ms - 23.21ms]
62.195: IO Summary: 42639082 ops 710602.726 ops/s 236868/0 rd/wr 3701.1mb/s   0.0ms/op
62.195: Shutting down processes
```
  As you can see the log, that warning disappear. 


 
## Summary of command to build filebench.
 
 Way to build filebench from officail site
 
 Because [filebench's repository](https://github.com/filebench/filebench) doesn't have configure file. 
 
 You have to generate the configure file. 
 
 filebench repository has dependency on libtoolize and automake tools to generate Makefile.in and configure files. 
 
```
Step 1. Generating autotill scripts

$ libtoolize
$ aclocal
$ autoheader
$ automake --add-missing
$ autoconf


Step 2 compilation and installation
$ ./configure
$ make
$ sudo make install

Step 3. make description for filebench with WML
vim test.f
#filebench -f test.f
```
 
 After installation of filebench. 
 
 If you enter "$ filebench" in shell prompt, you can get result below.

```
$ filebench
Usage error: No runtime options specified

Usage: filebench {-f <wmlscript> | -h | -c [cvartype]}

  Filebench version 1.5-alpha3

  Filebench is a file system and storage benchmark that interprets a script
  written in its Workload Model Language (WML), and procees to generate the
  specified workload. Refer to the README for more details.

  Visit github.com/filebench/filebench for WML definition and tutorials.

Options:
   -f <wmlscript> generate workload from the specified file
   -h             display this help message
   -c             display supported cvar types
   -c [cvartype]  display options of the specific cvar type
```
---

this version is another way. But I don't recommend you the following version to build and compile filebench. 

```shell 
$ git clone https://github.com/zfsonlinux/filebench.git
$ cd filebench
$ ./configure    -- run shell
$ make
$ sudo make install -- with sudo
$ filebench
$ set $dir=<dir>  -- in here, <dir> is formatted filesystem.
$ run 10
```
--- 
 
 ## Reference
 
  - [filebench git repository](https://github.com/filebench/filebench)
 
  - [Way to build filebench](https://github.com/filebench/filebench/wiki)
 
  - [Way to compile filebench](https://github.com/zfsonlinux/filebench)
