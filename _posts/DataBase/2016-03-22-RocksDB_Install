---
layout: post
title: RocksDB Install
subtitle:
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

정확한 사항은 페이스북에서 관리하는 github에 가서 해보면 좋을 거 같다. 

이 <a href = "https://github.com/facebook/rocksdb/blob/master/INSTALL.md"> facebook rocksDB</a>를 참조 했다. 

 - 위의 사이트를 보면 각각의 운영체제에서 rocksDB를 설치를 해야 할때 어떻게 해야 하는 지 잘보여 주고 있다. 
 
 난 그 중에서 현재 내가 사용중인 centos 7.1에 rocksDB를 설치 하기 위해 아래와 같은 과정을 따라 했다. 
 
 ## one of Supported platforms
 
 * **Linux - CentOS**
    * Upgrade your gcc to version at least 4.7 to get C++11 support:
      `yum install gcc47-c++`
    * Install gflags:

              wget https://gflags.googlecode.com/files/gflags-2.0-no-svn-files.tar.gz
              tar -xzvf gflags-2.0-no-svn-files.tar.gz
              cd gflags-2.0
              ./configure && make && sudo make install

    * Install snappy:

              wget https://snappy.googlecode.com/files/snappy-1.1.1.tar.gz
              tar -xzvf snappy-1.1.1.tar.gz
              cd snappy-1.1.1
              ./configure && make && sudo make install

    * Install zlib:

              sudo yum install zlib
              sudo yum install zlib-devel

    * Install bzip2:

              sudo yum install bzip2
              sudo yum install bzip2-devel


그리고 한 가지 더 rocksDB는 의존적인 프로그램이 있는데 목록은 다음과 같다. 

## Dependencies

* You can link RocksDB with following compression libraries:
  - [zlib](http://www.zlib.net/) - a library for data compression.
  - [bzip2](http://www.bzip.org/) - a library for data compression.
  - [snappy](https://code.google.com/p/snappy/) - a library for fast
      data compression.

* All our tools depend on:
  - [gflags](https://gflags.github.io/gflags/) - a library that handles
      command line flags processing. You can compile rocksdb library even
      if you don't have gflags installed.
  
  
그리고 rockDB를 사용하기 위해 컴파일을 할 시 주의 사항은 다음과 같다. 


## Compilation

**Important**: If you plan to run RocksDB in production, don't compile using default 
`make` or `make all`. That will compile RocksDB in debug mode, which is much slower
than release mode.

RocksDB's library should be able to compile without any dependency installed,
although we recommend installing some compression libraries (see below).
We do depend on newer gcc/clang with C++11 support.

There are few options when compiling RocksDB:

* [recommended] `make static_lib` will compile librocksdb.a, RocksDB static library. Compiles static library in release mode.

* `make shared_lib` will compile librocksdb.so, RocksDB shared library. Compiles shared library in release mode.

* `make check` will compile and run all the unit tests. `make check` will compile RocksDB in debug mode.

* `make all` will compile our static library, and all our tools and unit tests. Our tools
depend on gflags. You will need to have gflags installed to run `make all`. This will compile RocksDB in debug mode. Don't
use binaries compiled by `make all` in production.

* By default the binary we produce is optimized for the platform you're compiling on
(-march=native or the equivalent). If you want to build a portable binary, add 'PORTABLE=1' before
your make commands, like this: `PORTABLE=1 make static_lib`

페이스북의 설치 정규적인 설치 방법이다.
