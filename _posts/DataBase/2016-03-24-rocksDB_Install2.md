---
layout: post
title: RockDB install2
subtitle: while I installed rocksDB, I found errors and fix it.  
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

## 간단한 rocksDB 예제

<a href = "http://www.guguncube.com/2925/rocksdb-installation-and-performance-tests">이 RocksDB performance test </a>

이 사이트는 페이스 북의 rocksDB와 python을 이용해서 간단하게 데이터 베이스 시스템의 성능을 측정하는 방식이다. 

만약 rocksDB를 처음 접한다면 한번쯤 보고 따라 해보는 것도 좋을 거 같다. 

순서는 대략 다음과 같이 진행된다. 

1. git clone rocksDB github

2. make  && make install 을 통한 rocksDB 설치

3. 그리고 python을 설치 한후, 간단한 데이터베이스 코딩을 한다. 

## rocksDB test process

<a href ="https://github.com/facebook/rocksdb/">facebook github</a>를 보면 rocksDB의 모든 것을 알 수 있다. 

아래는 기본적인 설치 과정을 따라하면 경험한 오류 들이다. 


자 이제 기본적인 설치 과정을 보려면 <a href = "https://github.com/facebook/rocksdb/blob/master/INSTALL.md">facebook rocksDB install.md</a> or <a href = "http://hyunyoung2.github.io/2016-03-22-RocksDBInstall">RocksDB install</a>

위의 두 링크는 같은 것이기 때문에 어느 것을 봐도된다. 

그리고 내가 진행한 방식은 두가지이다. 

하나는 release version, 다른 하나는 그냥 rocksDB 공식 github 자체를 이용했다. 

다른 말로는 rocksDB 4.3 & 4.6version이라는 말이다. 

만약 4.3의 release rocksDB를 원한면  <a href = "https://github.com/facebook/rocksdb">facebook git</a>을 참조하자.

아니라면, 아래처럼 하자.

Now I have downloaded on <a href = "https://github.com/facebook/rocksdb">facebook git</a> with git instruction, which is "git clone https://github.com/facebook/rocksdb.git". 

And I compile the rocksDB source with make. 

results are :

```shell
일단 처음으로 rocksDB를 설치를 하기 위아여 다운을 받고 있다. 
 
[hyunyoung.lee@localhost ~]$ git clone https://github.com/facebook/rocksdb.git

 
[hyunyoung.lee@localhost ~]$ ls
Desktop    Downloads  linux-4.5         Music     Public   Templates
Documents  leveldb    linux-4.5.tar.xz  Pictures  rocksdb  Videos
[hyunyoung.lee@localhost ~]$ cd rocksdb/
[hyunyoung.lee@localhost rocksdb]$ ls
appveyor.yml                hdfs                  ROCKSDB_LITE.md
arcanist_util               HISTORY.md            src.mk
AUTHORS                     include               table
build_tools                 INSTALL.md            third-party
CMakeLists.txt              java                  thirdparty.inc
CONTRIBUTING.md             LANGUAGE-BINDINGS.md  tools
coverage                    LICENSE               USERS.md
db                          Makefile              util
DEFAULT_OPTIONS_HISTORY.md  memtable              utilities
doc                         PATENTS               Vagrantfile
DUMP_FORMAT.md              port                  WINDOWS_PORT.md
examples                    README.md
[hyunyoung.lee@localhost rocksdb]$ make
Makefile:99: Warning: Compiling in debug mode. Don't use the resulting binary in production
  GEN      util/build_version.cc

 
 
 [hyunyoung.lee@localhost rocksdb]$ ls
appveyor.yml                        db_test2                      optimistic_transaction_test
arcanist_util                       db_universal_compaction_test  options_file_test
arena_test                          db_wal_test                   options_test
AUTHORS                             DEFAULT_OPTIONS_HISTORY.md    options_util_test
auto_roll_logger_test               deletefile_test               PATENTS
autovector_test                     delete_scheduler_test         perf_context_test
backupable_db_test                  doc                           plain_table_db_test
block_based_filter_block_test       document_db_test              port
block_hash_index_test               DUMP_FORMAT.md                prefix_test
block_test                          dynamic_bloom_test            rate_limiter_test
bloom_test                          env_test                      README.md
build_tools                         event_logger_test             redis_test
cache_bench                         examples                      reduce_levels_test
cache_test                          fault_injection_test          rocksdb_dump
checkpoint_test                     file_indexer_test             ROCKSDB_LITE.md
CMakeLists.txt                      filelock_test                 rocksdb_undump
coding_test                         filename_test                 skiplist_test
column_family_test                  file_reader_writer_test       slice_transform_test
compact_files_test                  flush_job_test                spatial_db_test
compaction_iterator_test            full_filter_block_test        src.mk
compaction_job_stats_test           geodb_test                    sst_dump
compaction_job_test                 hdfs                          sst_dump_test
compaction_picker_test              heap_test                     stringappend_test
compact_on_deletion_collector_test  histogram_test                table
comparator_db_test                  HISTORY.md                    table_properties_collector_test
CONTRIBUTING.md                     include                       table_reader_bench
corruption_test                     inlineskiplist_test           table_test
coverage                            INSTALL.md                    third-party
crc32c_test                         iostats_context_test          thirdparty.inc
c_test                              java                          thread_list_test
cuckoo_table_builder_test           json_document_test            thread_local_test
cuckoo_table_db_test                LANGUAGE-BINDINGS.md          tools
cuckoo_table_reader_test            ldb                           transaction_test
db                                  ldb_cmd_test                  ttl_test
db_bench                            librocksdb_debug.a            USERS.md
db_block_cache_test                 LICENSE                       util
db_compaction_filter_test           listener_test                 utilities
db_compaction_test                  log_test                      Vagrantfile
db_dynamic_level_test               make_config.mk                version_builder_test
dbformat_test                       Makefile                      version_edit_test
db_inplace_update_test              manual_compaction_test        version_set_test
db_iter_test                        memenv_test                   wal_manager_test
db_log_iter_test                    memory_test                   WINDOWS_PORT.md
db_properties_test                  memtable                      write_batch_test
db_repl_stress                      memtable_list_test            write_batch_with_index_test
db_sanity_test                      memtablerep_bench             write_callback_test
db_stress                           merge_helper_test             write_controller_test
db_table_properties_test            merger_test                   write_stress
db_tailing_iter_test                merge_test
db_test                             mock_env_test
[hyunyoung.lee@localhost rocksdb]$ ./db_bench
Please install gflags to run rocksdb tools.

위에서 본거와 같이 make을 하고 나면 각종 rocksDB와 관련되 실행 파일을 볼 수 있다. 

그리고 벤치 마킹을 위해 ./db_bench프로그램을 실행했지만 rocksDB는 gflags에 dependency가 있다. 

이를 설치해야한다. 
```
 
for a few days, I was looking for the way, which installs gflags. 

so I followed <a href = "https://github.com/facebook/rocksdb/blob/master/INSTALL.md"> the install.md file of the facebook github.

in the gflag installation of the install.md file, their tools of rocksDB has denpendency on <a href = "https://gflags.github.io/gflags/">glfags library.</a>

and I have stuided on the way to install gflags library.

First, direclty, I used <a href = "https://github.com/gflags/gflags">the google github.</a> 

but google github source code need a camke(version 2.8.12) which creates makefile.

I installed cmake utility with yum. but this tools is 2.8.10. 

So to fix it, I refers to  <a href = "https://xinyustudio.wordpress.com/2014/06/18/how-to-install-cmake-3-0-on-centos-6-centos-7/">this site</a>, where here is to manually install cmake-3.0.0 on centos 7.

but, when I recompiled the rocksDB, I couldn't run ./db_bench program. 

that is why a executable file couldn't open the .so file, ilbgflas.so.2.

if you have a question about the way to fix it, please refer to <a hfer = "https://lonesysadmin.net/2013/02/22/error-while-loading-shared-libraries-cannot-open-shared-object-file/">this.</a>

The following is my experience for isntall.

```shell
아래를 보면 분명히 library는 존재하는데 찾을 수 없다는 메시지가 나온다. 
 - 이 경우는 올바른 라이브가 설치 되어도 나왔던메시지이다.
[hyunyoung.lee@localhost rocksdb]$ ./db_bench
./db_bench: error while loading shared libraries: libgflags.so.2: cannot open shared object file: No such file or directory


아래는 위의 에러를 수정한 후 다시 ./db_bench를 해봐도 같은 오류가 발생을 했다. 

확인을 해보니 아래와 같은 파일을 있고, 정작 libgflags.so.2는 없다. 

이를 확인 한 다음 나는 구글 github를 직접 이용을 한게 아니라 

아예 페이스북에서 설명하는 방식을 하기로 했다.
[hyunyoung.lee@localhost build]$ cd /usr/
[hyunyoung.lee@localhost usr]$ ls
bin  etc  games  include  lib  lib64  libexec  local  sbin  share  src  tmp
[hyunyoung.lee@localhost usr]$ cd local/
[hyunyoung.lee@localhost local]$ ls
bin  cmake-3.0.0  doc  etc  games  include  lib  lib64  libexec  sbin  share  src
[hyunyoung.lee@localhost local]$ cd lib
[hyunyoung.lee@localhost lib]$ ls
cmake  libgflags_nothreads.so  libgflags_nothreads.so.2.2  libgflags_nothreads.so.2.2.0  libgflags.so  libgflags.so.2.2  libgflags.so.2.2.0  pkgconfig


아래는 페이스북이 알려준 gflags를 설치  library 위치를 확인한 결과이다. 

[hyunyoung.lee@localhost ~]$ cd /usr/local/lib
[hyunyoung.lee@localhost lib]$ ls
libgflags.a   libgflags_nothreads.a   libgflags_nothreads.so    libgflags_nothreads.so.2.1.0  libgflags.so.2      pkgconfig
libgflags.la  libgflags_nothreads.la  libgflags_nothreads.so.2  libgflags.so                  libgflags.so.2.1.0
[hyunyoung.lee@localhost lib]$ 




위의 에러를 고치기 위해서는 일단 리눅스의 동적라이브러리와 라이브러니 경로 설정을 제대로 해야 한다. 

그 결과 정상적으로 설치가 가능했다. ./db_bench프로그램을 위한 정상적이 라이브러리 설치가 가능했다. 

그리고 아래는 이제 제대로 ./db_bench프로그램으로 ssd를 테스트 해본것이다.

[hyunyoung.lee@localhost rocksdb]$ ./db_bench
LevelDB:    version 4.6
Date:       Wed Apr  6 19:46:33 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Write rate: 0 bytes/second
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.716 micros/op 582671 ops/sec;   64.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       4.138 micros/op 241635 ops/sec;   26.7 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       4.358 micros/op 229486 ops/sec;   25.4 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       4.306 micros/op 232244 ops/sec;   25.7 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       5.271 micros/op 189712 ops/sec;   21.0 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.614 micros/op 1628417 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       0.677 micros/op 1476487 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.139 micros/op 98630 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      18.241 micros/op 54821 ops/sec; (795757 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called without an active exception
terminate called recursively
Received signal 6 (Aborted)
Aborted
[hyunyoung.lee@localhost rocksdb]$ vim ./bashrc
[hyunyoung.lee@localhost rocksdb]$ gedit ~/.bashrc
[hyunyoung.lee@localhost rocksdb]$ ./db_bench
LevelDB:    version 4.6
Date:       Thu Apr  7 09:53:27 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Write rate: 0 bytes/second
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.771 micros/op 564609 ops/sec;   62.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       3.994 micros/op 250388 ops/sec;   27.7 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       4.313 micros/op 231867 ops/sec;   25.7 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       4.379 micros/op 228341 ops/sec;   25.3 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       5.324 micros/op 187812 ops/sec;   20.8 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.607 micros/op 1648277 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       0.653 micros/op 1531684 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.463 micros/op 95577 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      19.673 micros/op 50829 ops/sec; (795962 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called without an active exception
terminate called recursively
Received signal 6 (Aborted)
Aborted
[hyunyoung.lee@localhost rocksdb]$ 
```

<!--
## simple test results of ./db_bench executable with CentOS Linux release 7.2.1511 (Core) and just cnetos7.1 kernel

```c
1. after git cloen https://github.com/facebook/rocksdb.git, finally, ./db_bench executable' test result

[hyunyoung.lee@localhost rocksdb]$ ./db_bench
LevelDB:    version 4.6
Date:       Fri Apr  8 16:05:54 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz#
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Write rate: 0 bytes/second
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.504 micros/op 664742 ops/sec;   73.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       4.168 micros/op 239919 ops/sec;   26.5 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       4.323 micros/op 231311 ops/sec;   25.6 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       4.830 micros/op 207057 ops/sec;   22.9 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       5.789 micros/op 172729 ops/sec;   19.1 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.633 micros/op 1579474 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       0.685 micros/op 1459566 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.360 micros/op 96529 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      19.252 micros/op 51943 ops/sec; (815018 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called without an active exception
terminate called recursively
Received signal 6 (Aborted)
Received signal 6 (Aborted)
#0   #0   /lib64/libc.so.6(gsignal+0x37) [0x7f9b22d635f7] /lib64/libc.so.6(gsignal+0x37) [0x7f9b22d635f7] ??	??:0	??	??:0	

#1   /lib64/libc.so.6(abort+0x148) [0x7f9b22d64ce8] #1   /lib64/libc.so.6(abort+0x148) [0x7f9b22d64ce8] ??	??:0	
#2   /lib64/libstdc++.so.6(_ZN9__gnu_cxx27__verbose_terminate_handlerEv+0x165) [0x7f9b236679d5] ??	??:0	
#2   /lib64/libstdc++.so.6(_ZN9__gnu_cxx27__verbose_terminate_handlerEv+0xf5) [0x7f9b23667965] ??	??:0	
#3   /lib64/libstdc++.so.6(+0x5e946) [0x7f9b23665946] ??	??:0	
#3   /lib64/libstdc++.so.6(+0x5e946) [0x7f9b23665946] ??	??:0	
#4   /lib64/libstdc++.so.6(+0x5e973) [0x7f9b23665973] ??	??:0	
#4   /lib64/libstdc++.so.6(+0x5e973) [0x7f9b23665973] ??	??:0	
#5   /lib64/libstdc++.so.6(+0x5f4df) [0x7f9b236664df] ??	??:0	
#5   /lib64/libstdc++.so.6(+0x5f4df) [0x7f9b236664df] ??	??:0	
#6   ./db_bench() [0x49db4a] ??	??:0	
#6   ./db_bench() [0x4cb7b8] rocksdb::InternalKeyComparator::Compare(rocksdb::Slice const&, rocksdb::Slice const&) const	/home/hyunyoung.lee/rocksdb/db/dbformat.cc:74	rocksdb::Comparator::Equal(rocksdb::Slice const&, rocksdb::Slice const&) const	/home/hyunyoung.lee/rocksdb/./include/rocksdb/comparator.h:39	
#7   ./db_bench() [0x585b4f] 
#7   ./db_bench() [0x4b3354] rocksdb::BlockIter::BinarySeek(rocksdb::Slice const&, unsigned int, unsigned int, unsigned int*)	/home/hyunyoung.lee/rocksdb/table/block.cc:192	rocksdb::CompactionIterator::NextFromInput()	/home/hyunyoung.lee/rocksdb/db/compaction_iterator.cc:145	
#8   ./db_bench() [0x5861f2] 
#8   ./db_bench() [0x4b3e82] rocksdb::BlockIter::Seek(rocksdb::Slice const&)	/home/hyunyoung.lee/rocksdb/table/block.cc:96 (discriminator 2)	rocksdb::CompactionIterator::Next()	/home/hyunyoung.lee/rocksdb/db/compaction_iterator.cc:100	
#9   ./db_bench() [0x494f28] 
#9   ./db_bench() [0x5ab401] rocksdb::BuildTable(std::string const&, rocksdb::Env*, rocksdb::ImmutableCFOptions const&, rocksdb::EnvOptions const&, rocksdb::TableCache*, rocksdb::InternalIterator*, rocksdb::FileMetaData*, rocksdb::InternalKeyComparator const&, std::vector<std::uniqu	_ptr<rocksdb::IntTblPropCollectorFactory, std::default_delete<rocksdb::IntTblPropCollectorFactory> >, std::allocator<std::unique_ptr<rocksdb::IntTblPropCollectorFactory, std::default_delete<rocksdb::IntTblPropCollectorFactory> > > > const*, unsigned int,	std::string const&, std::vector<unsigned long, std::allocator<unsigned long> >, unsigned long, rocksdb::CompressionType, rocksdb::CompressionOptions const&, bool, rocksdb::InternalStats*, rocksdb::Env::IOPriority, rocksdb::TableProperties*, int)	/home/hyunyoung.lee/rocksdb/db/builder.cc:113	rocksdb::IteratorWrapper::Update()	/home/hyunyoung.lee/rocksdb/./table/iterator_wrapper.h:118	
#10  ./db_bench() [0x5155d8] 
#10  ./db_bench() [0x5ab42f] rocksdb::Status::operator=(rocksdb::Status&&)	/home/hyunyoung.lee/rocksdb/./include/rocksdb/status.h:252	rocksdb::IteratorWrapper::Update()	/home/hyunyoung.lee/rocksdb/./table/iterator_wrapper.h:118	
#11  ./db_bench() [0x5179fd] 
#11  ./db_bench() [0x5980d3] rocksdb::FlushJob::Run(rocksdb::FileMetaData*)	/home/hyunyoung.lee/rocksdb/db/flush_job.cc:148	
#12  ./db_bench() [0x4d8f44] rocksdb::IteratorWrapper::Update()	/home/hyunyoung.lee/rocksdb/./table/iterator_wrapper.h:118	
#12  ./db_bench() [0x509540] rocksdb::PerfStepTimer::Stop()	/home/hyunyoung.lee/rocksdb/./util/perf_step_timer.h:41 (discriminator 1)	
#13  ./db_bench() [0x48e06f] rocksdb::DBImpl::FlushMemTableToOutputFile(rocksdb::ColumnFamilyData*, rocksdb::MutableCFOptions const&, bool*, rocksdb::JobContext*, rocksdb::LogBuffer*)	/home/hyunyoung.lee/rocksdb/./include/rocksdb/status.h:159	
#13  ./db_bench() [0x4d9a9c] rocksdb::Benchmark::SeekRandom(rocksdb::ThreadState*)	/home/hyunyoung.lee/rocksdb/tools/db_bench_tool.cc:3161	
#14  ./db_bench() [0x480e28] rocksdb::Status::operator=(rocksdb::Status&&)	/home/hyunyoung.lee/rocksdb/./include/rocksdb/status.h:252	
#14  ./db_bench() [0x4efaf7] rocksdb::Stats::Stop()	/home/hyunyoung.lee/rocksdb/tools/db_bench_tool.cc:1266 (discriminator 3)	
#15  ./db_bench() [0x5b7842] StartThreadWrapper	/home/hyunyoung.lee/rocksdb/util/env_posix.cc:716	
#16  /lib64/libpthread.so.0(+0x7dc5) [0x7f9b2415adc5] ??	??:0	
#17  /lib64/libc.so.6(clone+0x6d) [0x7f9b22e2428d] rocksdb::DBImpl::BackgroundCallFlush()	/home/hyunyoung.lee/rocksdb/db/db_impl.cc:2750	??	??:0	
Aborted




2. ./db_bench executable' test result with RocksDB 4.3.1


[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench
LevelDB:    version 4.3
Date:       Fri Apr  8 16:01:31 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Writes per second: 0
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.493 micros/op 669708 ops/sec;   74.1 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       3.404 micros/op 293767 ops/sec;   32.5 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       3.827 micros/op 261307 ops/sec;   28.9 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       3.746 micros/op 266982 ops/sec;   29.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :      14.461 micros/op 69153 ops/sec;    7.7 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       1.620 micros/op 617243 ops/sec;  
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       3.185 micros/op 313968 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      19.230 micros/op 52001 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      58.851 micros/op 16992 ops/sec; (896449 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called recursively
terminate called without an active exception
Received signal 6 (Aborted)
Aborted
[hyunyoung.lee@localhost rocksdb-4.3.1]$ 
```


## ./bench executable test result wiht CentOS Linux release 7.2.1511 (Core) and kerenl 4.5

Now, this enviroment is to complie rocksDB in CentOS Linux release 7.2.1511 (Core) and Centos7.1 kerenel

```shell
1. after git cloen https://github.com/facebook/rocksdb.git, finally, ./db_bench executable' test result


[hyunyoung.lee@localhost rocksdb]$ uname -a
Linux localhost.localdomain 4.5.0 #1 SMP Fri Apr 8 15:38:13 PDT 2016 x86_64 x86_64 x86_64 GNU/Linux
[hyunyoung.lee@localhost rocksdb]$ ./db_bench
LevelDB:    version 4.6
Date:       Fri Apr  8 16:27:48 2016
CPU:        <!--4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Write rate: 0 bytes/second
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.395 micros/op 716919 ops/sec;   79.3 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       4.406 micros/op 226984 ops/sec;   25.1 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       4.408 micros/op 226874 ops/sec;   25.1 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       4.249 micros/op 235327 ops/sec;   26.0 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       5.427 micros/op 184268 ops/sec;   20.4 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.615 micros/op 1624896 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       0.630 micros/op 1587105 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.001 micros/op 99985 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      23.273 micros/op 42967 ops/sec; (816316 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called                        
terminate called without an active exception
Received signal 6 (Aborted)
#0   /lib64/libc.so.6(gsignal+0x37) [0x7ff6b69a45f7] ??	??:0	
#1   /lib64/libc.so.6(abort+0x148) [0x7ff6b69a5ce8] ??	??:0	
#2   /lib64/libstdc++.so.6(_ZN9__gnu_cxx27__verbose_terminate_handlerEv+0x165) [0x7ff6b72a89d5] ??	??:0	
#3   /lib64/libstdc++.so.6(+0x5e946) [0x7ff6b72a6946] ??	??:0	
#4   /lib64/libstdc++.so.6(+0x5e973) [0x7ff6b72a6973] ??	??:0	
#5   /lib64/libstdc++.so.6(+0x5f4df) [0x7ff6b72a74df] ??	??:0	
#6   ./db_bench() [0x4cb7b8] rocksdb::InternalKeyComparator::Compare(rocksdb::Slice const&, rocksdb::Slice const&) const	/home/hyunyoung.lee/rocksdb/db/dbformat.cc:74	
#7   ./db_bench() [0x59826b] rocksdb::BinaryHeap<rocksdb::IteratorWrapper*, rocksdb::MinIteratorComparator>::upheap(unsigned long)	/home/hyunyoung.lee/rocksdb/./util/heap.h:104	
#8   ./db_bench() [0x509540] rocksdb::PerfStepTimer::Stop()	/home/hyunyoung.lee/rocksdb/./util/perf_step_timer.h:41 (discriminator 1)	
#9   ./db_bench() [0x48e06f] rocksdb::Benchmark::SeekRandom(rocksdb::ThreadState*)	/home/hyunyoung.lee/rocksdb/tools/db_bench_tool.cc:3161	
#10  ./db_bench() [0x480e28] rocksdb::Stats::Stop()	/home/hyunyoung.lee/rocksdb/tools/db_bench_tool.cc:1266 (discriminator 3)	
#11  ./db_bench() [0x5b7842] StartThreadWrapper	/home/hyunyoung.lee/rocksdb/util/env_posix.cc:716	
#12  /lib64/libpthread.so.0(+0x7dc5) [0x7ff6b7d9bdc5] ??	??:0	
#13  /lib64/libc.so.6(clone+0x6d) [0x7ff6b6a6528d] ??	??:0	
Aborted


2. ./db_bench executable' test result with RocksDB 4.3.1

[hyunyoung.lee@localhost ~]$ cd rocksdb-4.3.1/
[hyunyoung.lee@localhost rocksdb-4.3.1]$ uname -a
Linux localhost.localdomain 4.5.0 #1 SMP Fri Apr 8 15:38:13 PDT 2016 x86_64 x86_64 x86_64 GNU/Linux
[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench 
LevelDB:    version 4.3
Date:       Fri Apr  8 16:28:09 2016
CPU:        <!--4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Writes per second: 0
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
open error: IO error: lock /tmp/rocksdbtest-1000/dbbench/LOCK: Resource temporarily unavailable

the result above show up error because then, I had already tested rocskDB. 

[hyunyoung.lee@localhost rocksdb-4.3.1]$ uname -a
Linux localhost.localdomain 4.5.0 #1 SMP Fri Apr 8 15:38:13 PDT 2016 x86_64 x86_64 x86_64 GNU/Linux
[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench 
LevelDB:    version 4.3
Date:       Fri Apr  8 16:28:49 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Writes per second: 0
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.233 micros/op 810727 ops/sec;   89.7 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       2.819 micros/op 354756 ops/sec;   39.2 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       3.021 micros/op 330994 ops/sec;   36.6 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       3.287 micros/op 304199 ops/sec;   33.7 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       7.168 micros/op 139506 ops/sec;   15.4 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.571 micros/op 1752123 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       3.091 micros/op 323488 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      13.906 micros/op 71910 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      46.001 micros/op 21738 ops/sec; (915378 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called without an active exception
terminate called recursively
Received signal 6 (Aborted)
Received signal 6 (Aborted)
#0   #0   /lib64/libc.so.6(gsignal+0x37) [0x7f69726a25f7] /lib64/libc.so.6(gsignal+0x37) [0x7f69726a25f7] ??	??:0	??	??:0	

#1   /lib64/libc.so.6(abort+0x148) [0x7f69726a3ce8] #1   /lib64/libc.so.6(abort+0x148) [0x7f69726a3ce8] ??	??:0	
#2   /lib64/libstdc++.so.6(_ZN9__gnu_cxx27__verbose_terminate_handlerEv+0x165) [0x7f6972fa69d5] ??	??:0	
#2   /lib64/libstdc++.so.6(_ZN9__gnu_cxx27__verbose_terminate_handlerEv+0xf5) [0x7f6972fa6965] ??	??:0	
#3   /lib64/libstdc++.so.6(+0x5e946) [0x7f6972fa4946] ??	??:0	
#3   /lib64/libstdc++.so.6(+0x5e946) [0x7f6972fa4946] ??	??:0	??	??:0	
#4   /lib64/libstdc++.so.6(+0x5e973) [0x7f6972fa4973] 
#4   /lib64/libstdc++.so.6(+0x5e973) [0x7f6972fa4973] ??	??:0	??	??:0	
#5   /lib64/libstdc++.so.6(+0x5f4df) [0x7f6972fa54df] 
#5   /lib64/libstdc++.so.6(+0x5f4df) [0x7f6972fa54df] ??	??:0	??	??:0	
#6   ./db_bench() [0x4bb3b8] 
#6   ./db_bench() [0x4bb3b8] rocksdb::InternalKeyComparator::Compare(rocksdb::Slice const&, rocksdb::Slice const&) const	/home/hyunyoung.lee/rocksdb-4.3.1/db/dbformat.cc:74	rocksdb::InternalKeyComparator::Compare(rocksdb::Slice const&, rocksdb::Slice const&) const	/home/hyunyoung.lee/rocksdb-4.3.1/db/dbformat.cc:74	
#7   ./db_bench() [0x569aaf] 
#7   ./db_bench() [0x57ae5c] rocksdb::BlockIter::BinarySeek(rocksdb::Slice const&, unsigned int, unsigned int, unsigned int*)	/home/hyunyoung.lee/rocksdb-4.3.1/table/block.cc:185	rocksdb::BinaryHeap<rocksdb::IteratorWrapper*, rocksdb::MinIteratorComparator>::downheap(unsigned long)	/home/hyunyoung.lee/rocksdb-4.3.1/./util/heap.h:123	
#8   ./db_bench() [0x56a14d] 
#8   ./db_bench() [0x4a4df2] rocksdb::BlockIter::Seek(rocksdb::Slice const&)	/home/hyunyoung.lee/rocksdb-4.3.1/table/block.cc:96 (discriminator 2)	
#9   ./db_bench() [0x58ce28] rocksdb::CompactionIterator::Next()	/home/hyunyoung.lee/rocksdb-4.3.1/db/compaction_iterator.cc:87	
#9   ./db_bench() [0x4a8908] rocksdb::IteratorWrapper::Update()	/home/hyunyoung.lee/rocksdb-4.3.1/./table/iterator_wrapper.h:63	
#10  ./db_bench() [0x579cbc] rocksdb::CompactionJob::ProcessKeyValueCompaction(rocksdb::CompactionJob::SubcompactionState*)	/home/hyunyoung.lee/rocksdb-4.3.1/db/compaction_job.cc:699	
#10  ./db_bench() [0x4a9bf5] rocksdb::IteratorWrapper::Update()	/home/hyunyoung.lee/rocksdb-4.3.1/./table/iterator_wrapper.h:63	
#11  ./db_bench() [0x4f3bff] __normal_iterator	/usr/include/c++/4.8.2/bits/stl_iterator.h:726	
#11  ./db_bench() [0x4cdc7b] rocksdb::PerfStepTimer::Stop()	/home/hyunyoung.lee/rocksdb-4.3.1/./util/perf_step_timer.h:41 (discriminator 1)	
#12  ./db_bench() [0x4830aa] rocksdb::Benchmark::SeekRandom(rocksdb::ThreadState*)	/home/hyunyoung.lee/rocksdb-4.3.1/db/db_bench.cc:3072	
#13  ./db_bench() [0x4707a0] ~Status	/home/hyunyoung.lee/rocksdb-4.3.1/./include/rocksdb/status.h:29	
#12  ./db_bench() [0x4ddeea] rocksdb::Stats::Stop()	/home/hyunyoung.lee/rocksdb-4.3.1/db/db_bench.cc:1223 (discriminator 3)	
#14  ./db_bench() [0x59b382] rocksdb::DBImpl::BackgroundCallCompaction()	/home/hyunyoung.lee/rocksdb-4.3.1/db/db_impl.cc:2606	
#13  ./db_bench() [0x4de469] StartThreadWrapper	/home/hyunyoung.lee/rocksdb-4.3.1/util/env_posix.cc:1011	
#15  /lib64/libpthread.so.0(+0x7dc5) [0x7f6973a99dc5] ??	??:0	
#16  /lib64/libc.so.6(clone+0x6d) [0x7f697276328d] ??	??:0	
Aborted
[hyunyoung.lee@localhost rocksdb-4.3.1]$ cat /etc/c
centos-release           cron.d/                  cron.weekly/
centos-release-upstream  cron.daily/              crypttab
chkconfig.d/             cron.deny                csh.cshrc
chrony.conf              cron.hourly/             csh.login
chrony.keys              cron.monthly/            
cifs-utils/              crontab                  
[hyunyoung.lee@localhost rocksdb-4.3.1]$ cat /etc/centos-release
CentOS Linux release 7.2.1511 (Core) 
```

## ./bench executable test result wiht CentOS Linux release 7.2.1511 (Core) and kerenl 4.5, after newly compling the rocksDB.

after the rockDB above implement "make clean", each rockdDB folder,"rocksDB, rocksDB-4.3.1" remade again.

```shell
1. after git cloen https://github.com/facebook/rocksdb.git, finally, ./db_bench executable' test result

[hyunyoung.lee@localhost rocksdb]$ ./db_bench
LevelDB:    version 4.6
Date:       Fri Apr  8 17:17:10 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Write rate: 0 bytes/second
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.364 micros/op 732961 ops/sec;   81.1 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       3.505 micros/op 285274 ops/sec;   31.6 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       3.716 micros/op 269113 ops/sec;   29.8 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       3.840 micros/op 260433 ops/sec;   28.8 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       5.583 micros/op 179124 ops/sec;   19.8 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.617 micros/op 1620152 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       0.714 micros/op 1400356 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.603 micros/op 94311 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      21.391 micros/op 46749 ops/sec; (802460 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called                        
terminate called without an active exception
Received signal 6 (Aborted)
pure virtual method called
terminate called recursively
Aborted


2. ./db_bench executable' test result with RocksDB 4.3.1
[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench 
LevelDB:    version 4.3
Date:       Fri Apr  8 17:15:42 2016
CPU:        4 * Intel(R) Core(TM) i3-0000 CPU @ 3.40GHz
CPUCache:   3072 KB
Keys:       16 bytes each
Values:     100 bytes each (50 bytes after compression)
Entries:    1000000
Prefix:    0 bytes
Keys per prefix:    0
RawSize:    110.6 MB (estimated)
FileSize:   62.9 MB (estimated)
Writes per second: 0
Compression: Snappy
Memtablerep: skip_list
Perf Level: 0
WARNING: Assertions are enabled; benchmarks unnecessarily slow
------------------------------------------------
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillseq      :       1.221 micros/op 819029 ops/sec;   90.6 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       2.847 micros/op 351198 ops/sec;   38.9 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       3.130 micros/op 319489 ops/sec;   35.3 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       2.809 micros/op 356022 ops/sec;   39.4 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       8.356 micros/op 119676 ops/sec;   13.2 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.847 micros/op 1180877 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       1.990 micros/op 502608 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.191 micros/op 98128 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      43.993 micros/op 22730 ops/sec; (930993 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
pure virtual method called
terminate called recursively
terminate called recursively
Received signal 6 (Aborted)
Received signal 6 (Aborted)
terminate called without an active exception
Aborted

rocksDB 4.6 verions unstable but   4.3 release verion stable in centos 7.2 , linux 4.5 

when I implemented instruction, "make static". it will show below

[hyunyoung.lee@localhost rocksdb]$ make static_lib


[hyunyoung.lee@localhost rocksdb]$ ls
appveyor.yml   build_tools      coverage                    doc             hdfs        INSTALL.md            librocksdb.a    Makefile  port             src.mk       thirdparty.inc  util         WINDOWS_PORT.md
arcanist_util  CMakeLists.txt   db                          DUMP_FORMAT.md  HISTORY.md  java                  LICENSE         memtable  README.md        table        tools           utilities
AUTHORS        CONTRIBUTING.md  DEFAULT_OPTIONS_HISTORY.md  examples        include     LANGUAGE-BINDINGS.md  make_config.mk  PATENTS   ROCKSDB_LITE.md  third-party  USERS.md        Vagrantfile
```
-->
