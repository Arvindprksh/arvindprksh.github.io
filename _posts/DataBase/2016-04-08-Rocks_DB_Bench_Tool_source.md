---
layout: post
title: Analysis of RocsksDB code
subtitle: about benchmark tool's source code
category: DataBase
tags: [rocksdb, facebook]
permalink: /2016/04/08/Rocks_DB_Bench_Tool_source/
---

rocksDB/tools/db_bench_too.cc is file to analyze "./db_bench" utility code.

facebook tests performance of rocksdb as configured by default.

now, I will test rocksDB in centos 7.2 , linux basic version(of cetnos 7.1), and rocksDB 4.3.1 release version

the following is set up environment of facebook's rocksDB test to compare levelDB to rocksDB performance, and XFS filesystem is important for me to think.

    Operating System Linux 2.6.38.4

    total database size is 800GB, stored on XFS filesystem with TRIM support
    
from now on, I will start source analyzation of rocksDB for rocksDB bench market tool.

above all, the following is the summarization of db_bench_tool terms & way to test rocksDB.

```c++
DEFINE_string(benchmarks,
              "fillseq,"
              "fillsync,"
              "fillrandom,"
              "overwrite,"
              "readrandom,"
              "newiterator,"
              "newiteratorwhilewriting,"
              "seekrandom,"
              "seekrandomwhilewriting,"
              "seekrandomwhilemerging,"
              "readseq,"
              "readreverse,"
              "compact,"
              "readrandom,"
              "multireadrandom,"
              "readseq,"
              "readtocache,"
              "readreverse,"
              "readwhilewriting,"
              "readwhilemerging,"
              "readrandomwriterandom,"
              "updaterandom,"
              "randomwithverify,"
              "fill100K,"
              "crc32c,"
              "xxhash,"
              "compress,"
              "uncompress,"
              "acquireload,"
              "fillseekseq,"
              "randomtransaction,"
              "randomreplacekeys",

              "Comma-separated list of operations to run in the specified"
              " order. Available benchmarks:\n"
              "\tfillseq       -- write N values in sequential key"
              " order in async mode\n"
              "\tfillrandom    -- write N values in random key order in async"
              " mode\n"
              "\toverwrite     -- overwrite N values in random key order in"
              " async mode\n"
              "\tfillsync      -- write N/100 values in random key order in "
              "sync mode\n"
              "\tfill100K      -- write N/1000 100K values in random order in"
              " async mode\n"
              "\tdeleteseq     -- delete N keys in sequential order\n"
              "\tdeleterandom  -- delete N keys in random order\n"
              "\treadseq       -- read N times sequentially\n"
              "\treadtocache   -- 1 thread reading database sequentially\n"
              "\treadreverse   -- read N times in reverse order\n"
              "\treadrandom    -- read N times in random order\n"
              "\treadmissing   -- read N missing keys in random order\n"
              "\treadwhilewriting      -- 1 writer, N threads doing random "
              "reads\n"
              "\treadwhilemerging      -- 1 merger, N threads doing random "
              "reads\n"
              "\treadrandomwriterandom -- N threads doing random-read, "
              "random-write\n"
              "\tprefixscanrandom      -- prefix scan N times in random order\n"
              "\tupdaterandom  -- N threads doing read-modify-write for random "
              "keys\n"
              "\tappendrandom  -- N threads doing read-modify-write with "
              "growing values\n"
              "\tmergerandom   -- same as updaterandom/appendrandom using merge"
              " operator. "
              "Must be used with merge_operator\n"
              "\treadrandommergerandom -- perform N random read-or-merge "
              "operations. Must be used with merge_operator\n"
              "\tnewiterator   -- repeated iterator creation\n"
              "\tseekrandom    -- N random seeks, call Next seek_nexts times "
              "per seek\n"
              "\tseekrandomwhilewriting -- seekrandom and 1 thread doing "
              "overwrite\n"
              "\tseekrandomwhilemerging -- seekrandom and 1 thread doing "
              "merge\n"
              "\tcrc32c        -- repeated crc32c of 4K of data\n"
              "\txxhash        -- repeated xxHash of 4K of data\n"
              "\tacquireload   -- load N*1000 times\n"
              "\tfillseekseq   -- write N values in sequential key, then read "
              "them by seeking to each key\n"
              "\trandomtransaction     -- execute N random transactions and "
              "verify correctness\n"
              "\trandomreplacekeys     -- randomly replaces N keys by deleting "
              "the old version and putting the new version\n\n"
              "Meta operations:\n"
              "\tcompact     -- Compact the entire DB\n"
              "\tstats       -- Print DB stats\n"
              "\tlevelstats  -- Print the number of files and bytes per level\n"
              "\tsstables    -- Print sstable info\n"
              "\theapprofile -- Dump a heap profile (if supported by this"
              " port)\n");

the texts above is way to benchmark rocksDB.

the following is the way to configure variable for benchmark. 

DEFINE_int64(num, 1000000, "Number of key/values to place in database");

DEFINE_int64(numdistinct, 1000,
             "Number of distinct keys to use. Used in RandomWithVerify to "
             "read/write on fewer keys so that gets are more likely to find the"
             " key and puts are more likely to update the same key");

```


## while analyzing source code, I committed to rocksdb open source.

![](/)


## get started (based on rocksdb 4.6 version source, I looked into the source)

**First, source analyzation get started in directory (/rocksDB/tools/db_benc.cc file)**

    - keywords : rocksdb::db_bench_tool(argc, argv);

```c++
#ifndef __STDC_FORMAT_MACROS
#define __STDC_FORMAT_MACROS
#endif

#ifndef GFLAGS
#include <cstdio>
int main() {
  fprintf(stderr, "Please install gflags to run rocksdb tools\n");
  return 1;
}
#else
#include <rocksdb/db_bench_tool.h>
int main(int argc, char** argv) { rocksdb::db_bench_tool(argc, argv); }
#endif  // GFLAGS

```


**Second, db_bench_tool function in rocksdb/tools/db_bench_tool.cc file**

    - keywords : rocksdb::Benchmark benchmark;, rocksdb::Benchmark benchmark;, FLAGS_db

```c++
int db_bench_tool(int argc, char** argv) {
  rocksdb::port::InstallStackTraceHandler();
  SetUsageMessage(std::string("\nUSAGE:\n") + std::string(argv[0]) +
                  " [OPTIONS]...");
  ParseCommandLineFlags(&argc, &argv, true);

  FLAGS_compaction_style_e = (rocksdb::CompactionStyle) FLAGS_compaction_style;
  if (FLAGS_statistics) {
    dbstats = rocksdb::CreateDBStatistics();
  }
  FLAGS_compaction_pri_e = (rocksdb::CompactionPri)FLAGS_compaction_pri;

  std::vector<std::string> fanout = rocksdb::StringSplit(
      FLAGS_max_bytes_for_level_multiplier_additional, ',');
  for (size_t j = 0; j < fanout.size(); j++) {
    FLAGS_max_bytes_for_level_multiplier_additional_v.push_back(
#ifndef CYGWIN
        std::stoi(fanout[j]));
#else
        stoi(fanout[j]));
#endif
  }

  FLAGS_compression_type_e =
    StringToCompressionType(FLAGS_compression_type.c_str());

  if (!FLAGS_hdfs.empty()) {
    FLAGS_env  = new rocksdb::HdfsEnv(FLAGS_hdfs);
  }

  if (!strcasecmp(FLAGS_compaction_fadvice.c_str(), "NONE"))
    FLAGS_compaction_fadvice_e = rocksdb::Options::NONE;
  else if (!strcasecmp(FLAGS_compaction_fadvice.c_str(), "NORMAL"))
    FLAGS_compaction_fadvice_e = rocksdb::Options::NORMAL;
  else if (!strcasecmp(FLAGS_compaction_fadvice.c_str(), "SEQUENTIAL"))
    FLAGS_compaction_fadvice_e = rocksdb::Options::SEQUENTIAL;
  else if (!strcasecmp(FLAGS_compaction_fadvice.c_str(), "WILLNEED"))
    FLAGS_compaction_fadvice_e = rocksdb::Options::WILLNEED;
  else {
    fprintf(stdout, "Unknown compaction fadvice:%s\n",
            FLAGS_compaction_fadvice.c_str());
  }

  FLAGS_rep_factory = StringToRepFactory(FLAGS_memtablerep.c_str());

  // The number of background threads should be at least as much the
  // max number of concurrent compactions.
  FLAGS_env->SetBackgroundThreads(FLAGS_max_background_compactions);
  FLAGS_env->SetBackgroundThreads(FLAGS_max_background_flushes,
                                  rocksdb::Env::Priority::HIGH);

  // Choose a location for the test database if none given with --db=<path>
  if (FLAGS_db.empty()) {
    std::string default_db_path;
    rocksdb::Env::Default()->GetTestDirectory(&default_db_path);
    default_db_path += "/dbbench";
    FLAGS_db = default_db_path;
  }

  if (FLAGS_stats_interval_seconds > 0) {
    // When both are set then FLAGS_stats_interval determines the frequency
    // at which the timer is checked for FLAGS_stats_interval_seconds
    FLAGS_stats_interval = 1000;
  }

  //so far, rocksdb option setting 

  rocksdb::Benchmark benchmark;   // from now on, benchmark go newly 
  benchmark.Run();                // Run() function is next target for source analyzation.
  return 0;
}
```


**third, Run() function /rocksdb/tools/db_bench_tool.cc**

    - keywords : PrintHeader();, Open(&open_options_);, RunBenchmark(num_threads, name, method);

```c++
void Run() {
    if (!SanityCheck()) {
      exit(1);
    }
    PrintHeader();
    Open(&open_options_);
    std::stringstream benchmark_stream(FLAGS_benchmarks);
    std::string name;
    while (std::getline(benchmark_stream, name, ',')) {
      // Sanitize parameters
      num_ = FLAGS_num;
      reads_ = (FLAGS_reads < 0 ? FLAGS_num : FLAGS_reads);
      writes_ = (FLAGS_writes < 0 ? FLAGS_num : FLAGS_writes);
      value_size_ = FLAGS_value_size;
      key_size_ = FLAGS_key_size;
      entries_per_batch_ = FLAGS_batch_size;
      write_options_ = WriteOptions();
      read_random_exp_range_ = FLAGS_read_random_exp_range;
      if (FLAGS_sync) {
        write_options_.sync = true;
      }
      write_options_.disableWAL = FLAGS_disable_wal;

      void (Benchmark::*method)(ThreadState*) = nullptr;
      void (Benchmark::*post_process_method)() = nullptr;

      bool fresh_db = false;
      int num_threads = FLAGS_threads;

      if (name == "fillseq") {
        fresh_db = true;
        method = &Benchmark::WriteSeq;
      } else if (name == "fillbatch") {
        fresh_db = true;
        entries_per_batch_ = 1000;
        method = &Benchmark::WriteSeq;
      } else if (name == "fillrandom") {
        fresh_db = true;
        method = &Benchmark::WriteRandom;
      } else if (name == "filluniquerandom") {
        fresh_db = true;
        if (num_threads > 1) {
          fprintf(stderr,
                  "filluniquerandom multithreaded not supported"
                  ", use 1 thread");
          num_threads = 1;
        }
        method = &Benchmark::WriteUniqueRandom;
      } else if (name == "overwrite") {
        method = &Benchmark::WriteRandom;
      } else if (name == "fillsync") {
        fresh_db = true;
        num_ /= 1000;
        write_options_.sync = true;
        method = &Benchmark::WriteRandom;
      } else if (name == "fill100K") {
        fresh_db = true;
        num_ /= 1000;
        value_size_ = 100 * 1000;
        method = &Benchmark::WriteRandom;
      } else if (name == "readseq") {
        method = &Benchmark::ReadSequential;
      } else if (name == "readtocache") {
        method = &Benchmark::ReadSequential;
        num_threads = 1;
        reads_ = num_;
      } else if (name == "readreverse") {
        method = &Benchmark::ReadReverse;
      } else if (name == "readrandom") {
        method = &Benchmark::ReadRandom;
      } else if (name == "readrandomfast") {
        method = &Benchmark::ReadRandomFast;
      } else if (name == "multireadrandom") {
        fprintf(stderr, "entries_per_batch = %" PRIi64 "\n",
                entries_per_batch_);
        method = &Benchmark::MultiReadRandom;
      } else if (name == "readmissing") {
        ++key_size_;
        method = &Benchmark::ReadRandom;
      } else if (name == "newiterator") {
        method = &Benchmark::IteratorCreation;
      } else if (name == "newiteratorwhilewriting") {
        num_threads++;  // Add extra thread for writing
        method = &Benchmark::IteratorCreationWhileWriting;
      } else if (name == "seekrandom") {
        method = &Benchmark::SeekRandom;
      } else if (name == "seekrandomwhilewriting") {
        num_threads++;  // Add extra thread for writing
        method = &Benchmark::SeekRandomWhileWriting;
      } else if (name == "seekrandomwhilemerging") {
        num_threads++;  // Add extra thread for merging
        method = &Benchmark::SeekRandomWhileMerging;
      } else if (name == "readrandomsmall") {
        reads_ /= 1000;
        method = &Benchmark::ReadRandom;
      } else if (name == "deleteseq") {
        method = &Benchmark::DeleteSeq;
      } else if (name == "deleterandom") {
        method = &Benchmark::DeleteRandom;
      } else if (name == "readwhilewriting") {
        num_threads++;  // Add extra thread for writing
        method = &Benchmark::ReadWhileWriting;
      } else if (name == "readwhilemerging") {
        num_threads++;  // Add extra thread for writing
        method = &Benchmark::ReadWhileMerging;
      } else if (name == "readrandomwriterandom") {
        method = &Benchmark::ReadRandomWriteRandom;
      } else if (name == "readrandommergerandom") {
        if (FLAGS_merge_operator.empty()) {
          fprintf(stdout, "%-12s : skipped (--merge_operator is unknown)\n",
                  name.c_str());
          exit(1);
        }
        method = &Benchmark::ReadRandomMergeRandom;
      } else if (name == "updaterandom") {
        method = &Benchmark::UpdateRandom;
      } else if (name == "appendrandom") {
        method = &Benchmark::AppendRandom;
      } else if (name == "mergerandom") {
        if (FLAGS_merge_operator.empty()) {
          fprintf(stdout, "%-12s : skipped (--merge_operator is unknown)\n",
                  name.c_str());
          exit(1);
        }
        method = &Benchmark::MergeRandom;
      } else if (name == "randomwithverify") {
        method = &Benchmark::RandomWithVerify;
      } else if (name == "fillseekseq") {
        method = &Benchmark::WriteSeqSeekSeq;
      } else if (name == "compact") {
        method = &Benchmark::Compact;
      } else if (name == "crc32c") {
        method = &Benchmark::Crc32c;
      } else if (name == "xxhash") {
        method = &Benchmark::xxHash;
      } else if (name == "acquireload") {
        method = &Benchmark::AcquireLoad;
      } else if (name == "compress") {
        method = &Benchmark::Compress;
      } else if (name == "uncompress") {
        method = &Benchmark::Uncompress;
#ifndef ROCKSDB_LITE
      } else if (name == "randomtransaction") {
        method = &Benchmark::RandomTransaction;
        post_process_method = &Benchmark::RandomTransactionVerify;
#endif  // ROCKSDB_LITE
      } else if (name == "randomreplacekeys") {
        fresh_db = true;
        method = &Benchmark::RandomReplaceKeys;
      } else if (name == "stats") {
        PrintStats("rocksdb.stats");
      } else if (name == "levelstats") {
        PrintStats("rocksdb.levelstats");
      } else if (name == "sstables") {
        PrintStats("rocksdb.sstables");
      } else if (!name.empty()) {  // No error message for empty name
        fprintf(stderr, "unknown benchmark '%s'\n", name.c_str());
        exit(1);
      }

      if (fresh_db) {
        if (FLAGS_use_existing_db) {
          fprintf(stdout, "%-12s : skipped (--use_existing_db is true)\n",
                  name.c_str());
          method = nullptr;
        } else {
          if (db_.db != nullptr) {
            db_.DeleteDBs();
            DestroyDB(FLAGS_db, open_options_);
          }
          for (size_t i = 0; i < multi_dbs_.size(); i++) {
            delete multi_dbs_[i].db;
            DestroyDB(GetDbNameForMultiple(FLAGS_db, i), open_options_);
          }
          multi_dbs_.clear();
        }
        Open(&open_options_);  // use open_options for the last accessed
      }

      if (method != nullptr) {
        fprintf(stdout, "DB path: [%s]\n", FLAGS_db.c_str());
        RunBenchmark(num_threads, name, method);
      }
      if (post_process_method != nullptr) {
        (this->*post_process_method)();
      }
    }
    if (FLAGS_statistics) {
     fprintf(stdout, "STATISTICS:\n%s\n", dbstats->ToString().c_str());
    }
  }
```


** fourth, PrintHeader() function in rocksDB/tools/db_bench_tool.cc file**

    - keywords : there is no keyword. just print function

```c++
void PrintHeader() {
    PrintEnvironment();
    fprintf(stdout, "Keys:       %d bytes each\n", FLAGS_key_size);
    fprintf(stdout, "Values:     %d bytes each (%d bytes after compression)\n",
            FLAGS_value_size,
            static_cast<int>(FLAGS_value_size * FLAGS_compression_ratio + 0.5));
    fprintf(stdout, "Entries:    %" PRIu64 "\n", num_);
    fprintf(stdout, "Prefix:    %d bytes\n", FLAGS_prefix_size);
    fprintf(stdout, "Keys per prefix:    %" PRIu64 "\n", keys_per_prefix_);
    fprintf(stdout, "RawSize:    %.1f MB (estimated)\n",
            ((static_cast<int64_t>(FLAGS_key_size + FLAGS_value_size) * num_)
             / 1048576.0));
    fprintf(stdout, "FileSize:   %.1f MB (estimated)\n",
            (((FLAGS_key_size + FLAGS_value_size * FLAGS_compression_ratio)
              * num_)
             / 1048576.0));
    fprintf(stdout, "Write rate: %" PRIu64 " bytes/second\n",
            FLAGS_benchmark_write_rate_limit);
    if (FLAGS_enable_numa) {
      fprintf(stderr, "Running in NUMA enabled mode.\n");
#ifndef NUMA
      fprintf(stderr, "NUMA is not defined in the system.\n");
      exit(1);
#else
      if (numa_available() == -1) {
        fprintf(stderr, "NUMA is not supported by the system.\n");
        exit(1);
      }
#endif
    }

    auto compression = CompressionTypeToString(FLAGS_compression_type_e);
    fprintf(stdout, "Compression: %s\n", compression.c_str());

    switch (FLAGS_rep_factory) {
      case kPrefixHash:
        fprintf(stdout, "Memtablerep: prefix_hash\n");
        break;
      case kSkipList:
        fprintf(stdout, "Memtablerep: skip_list\n");
        break;
      case kVectorRep:
        fprintf(stdout, "Memtablerep: vector\n");
        break;
      case kHashLinkedList:
        fprintf(stdout, "Memtablerep: hash_linkedlist\n");
        break;
      case kCuckoo:
        fprintf(stdout, "Memtablerep: cuckoo\n");
        break;
    }
    fprintf(stdout, "Perf Level: %d\n", FLAGS_perf_level);

    PrintWarnings(compression.c_str());
    fprintf(stdout, "------------------------------------------------\n");
  }
```


**fifth, PrintEnvironment() function in rocksDB/tools/db_bench_tool.cc file**

    - keywords : there is no keywords, just print process

```c+
void PrintEnvironment() {
    fprintf(stderr, "RocksDB:    version %d.%d\n",
            kMajorVersion, kMinorVersion);

#if defined(__linux)
    time_t now = time(nullptr);
    char buf[52];
    // Lint complains about ctime() usage, so replace it with ctime_r(). The
    // requirement is to provide a buffer which is at least 26 bytes.
    fprintf(stderr, "Date:       %s",
            ctime_r(&now, buf));  // ctime_r() adds newline

    FILE* cpuinfo = fopen("/proc/cpuinfo", "r");
    if (cpuinfo != nullptr) {
      char line[1000];
      int num_cpus = 0;
      std::string cpu_type;
      std::string cache_size;
      while (fgets(line, sizeof(line), cpuinfo) != nullptr) {
        const char* sep = strchr(line, ':');
        if (sep == nullptr) {
          continue;
        }
        Slice key = TrimSpace(Slice(line, sep - 1 - line));
        Slice val = TrimSpace(Slice(sep + 1));
        if (key == "model name") {
          ++num_cpus;
          cpu_type = val.ToString();
        } else if (key == "cache size") {
          cache_size = val.ToString();
        }
      }
      fclose(cpuinfo);
      fprintf(stderr, "CPU:        %d * %s\n", num_cpus, cpu_type.c_str());
      fprintf(stderr, "CPUCache:   %s\n", cache_size.c_str());
    }
#endif
  }
```


**sixth, Open(options * opts) in rocksdb/tools/db_bench_tool.cc **

    - keywords : this just configure option

```c++
void Open(Options* opts) {
    Options& options = *opts;

    assert(db_.db == nullptr);

    options.create_if_missing = !FLAGS_use_existing_db;
    options.create_missing_column_families = FLAGS_num_column_families > 1;
    options.db_write_buffer_size = FLAGS_db_write_buffer_size;
    options.write_buffer_size = FLAGS_write_buffer_size;
    options.max_write_buffer_number = FLAGS_max_write_buffer_number;
    options.min_write_buffer_number_to_merge =
      FLAGS_min_write_buffer_number_to_merge;
    options.max_write_buffer_number_to_maintain =
        FLAGS_max_write_buffer_number_to_maintain;
    options.max_background_compactions = FLAGS_max_background_compactions;
    options.max_subcompactions = static_cast<uint32_t>(FLAGS_subcompactions);
    options.max_background_flushes = FLAGS_max_background_flushes;
    options.compaction_style = FLAGS_compaction_style_e;
    options.compaction_pri = FLAGS_compaction_pri_e;
    if (FLAGS_prefix_size != 0) {
      options.prefix_extractor.reset(
          NewFixedPrefixTransform(FLAGS_prefix_size));
    }
    if (FLAGS_use_uint64_comparator) {
      options.comparator = test::Uint64Comparator();
      if (FLAGS_key_size != 8) {
        fprintf(stderr, "Using Uint64 comparator but key size is not 8.\n");
        exit(1);
      }
    }
    options.memtable_prefix_bloom_bits = FLAGS_memtable_bloom_bits;
    options.bloom_locality = FLAGS_bloom_locality;
    options.max_open_files = FLAGS_open_files;
    options.max_file_opening_threads = FLAGS_file_opening_threads;
    options.new_table_reader_for_compaction_inputs =
        FLAGS_new_table_reader_for_compaction_inputs;
    options.compaction_readahead_size = FLAGS_compaction_readahead_size;
    options.random_access_max_buffer_size = FLAGS_random_access_max_buffer_size;
    options.writable_file_max_buffer_size = FLAGS_writable_file_max_buffer_size;
    options.statistics = dbstats;
    if (FLAGS_enable_io_prio) {
      FLAGS_env->LowerThreadPoolIOPriority(Env::LOW);
      FLAGS_env->LowerThreadPoolIOPriority(Env::HIGH);
    }
    if (FLAGS_disable_flashcache_for_background_threads &&
        cachedev_fd_ == -1) {
      // Avoid creating the env twice when an use_existing_db is true
      cachedev_fd_ = open(FLAGS_flashcache_dev.c_str(), O_RDONLY);
      if (cachedev_fd_ < 0) {
        fprintf(stderr, "Open flash device failed\n");
        exit(1);
      }
      flashcache_aware_env_ = NewFlashcacheAwareEnv(FLAGS_env, cachedev_fd_);
      if (flashcache_aware_env_.get() == nullptr) {
        fprintf(stderr, "Failed to open flashcache device at %s\n",
                FLAGS_flashcache_dev.c_str());
        std::abort();
      }
      options.env = flashcache_aware_env_.get();
    } else {
      options.env = FLAGS_env;
    }
    options.disableDataSync = FLAGS_disable_data_sync;
    options.use_fsync = FLAGS_use_fsync;
    options.wal_dir = FLAGS_wal_dir;
    options.num_levels = FLAGS_num_levels;
    options.target_file_size_base = FLAGS_target_file_size_base;
    options.target_file_size_multiplier = FLAGS_target_file_size_multiplier;
    options.max_bytes_for_level_base = FLAGS_max_bytes_for_level_base;
    options.level_compaction_dynamic_level_bytes =
        FLAGS_level_compaction_dynamic_level_bytes;
    options.max_bytes_for_level_multiplier =
        FLAGS_max_bytes_for_level_multiplier;
    options.filter_deletes = FLAGS_filter_deletes;
    if (FLAGS_row_cache_size) {
      if (FLAGS_cache_numshardbits >= 1) {
        options.row_cache =
            NewLRUCache(FLAGS_row_cache_size, FLAGS_cache_numshardbits);
      } else {
        options.row_cache = NewLRUCache(FLAGS_row_cache_size);
      }
    }
    if ((FLAGS_prefix_size == 0) && (FLAGS_rep_factory == kPrefixHash ||
                                     FLAGS_rep_factory == kHashLinkedList)) {
      fprintf(stderr, "prefix_size should be non-zero if PrefixHash or "
                      "HashLinkedList memtablerep is used\n");
      exit(1);
    }
    switch (FLAGS_rep_factory) {
      case kSkipList:
        options.memtable_factory.reset(new SkipListFactory(
            FLAGS_skip_list_lookahead));
        break;
#ifndef ROCKSDB_LITE
      case kPrefixHash:
        options.memtable_factory.reset(
            NewHashSkipListRepFactory(FLAGS_hash_bucket_count));
        break;
      case kHashLinkedList:
        options.memtable_factory.reset(NewHashLinkListRepFactory(
            FLAGS_hash_bucket_count));
        break;
      case kVectorRep:
        options.memtable_factory.reset(
          new VectorRepFactory
        );
        break;
      case kCuckoo:
        options.memtable_factory.reset(NewHashCuckooRepFactory(
            options.write_buffer_size, FLAGS_key_size + FLAGS_value_size));
        break;
#else
      default:
        fprintf(stderr, "Only skip list is supported in lite mode\n");
        exit(1);
#endif  // ROCKSDB_LITE
    }
    if (FLAGS_use_plain_table) {
#ifndef ROCKSDB_LITE
      if (FLAGS_rep_factory != kPrefixHash &&
          FLAGS_rep_factory != kHashLinkedList) {
        fprintf(stderr, "Waring: plain table is used with skipList\n");
      }
      if (!FLAGS_mmap_read && !FLAGS_mmap_write) {
        fprintf(stderr, "plain table format requires mmap to operate\n");
        exit(1);
      }

      int bloom_bits_per_key = FLAGS_bloom_bits;
      if (bloom_bits_per_key < 0) {
        bloom_bits_per_key = 0;
      }

      PlainTableOptions plain_table_options;
      plain_table_options.user_key_len = FLAGS_key_size;
      plain_table_options.bloom_bits_per_key = bloom_bits_per_key;
      plain_table_options.hash_table_ratio = 0.75;
      options.table_factory = std::shared_ptr<TableFactory>(
          NewPlainTableFactory(plain_table_options));
#else
      fprintf(stderr, "Plain table is not supported in lite mode\n");
      exit(1);
#endif  // ROCKSDB_LITE
    } else if (FLAGS_use_cuckoo_table) {
#ifndef ROCKSDB_LITE
      if (FLAGS_cuckoo_hash_ratio > 1 || FLAGS_cuckoo_hash_ratio < 0) {
        fprintf(stderr, "Invalid cuckoo_hash_ratio\n");
        exit(1);
      }
      rocksdb::CuckooTableOptions table_options;
      table_options.hash_table_ratio = FLAGS_cuckoo_hash_ratio;
      table_options.identity_as_first_hash = FLAGS_identity_as_first_hash;
      options.table_factory = std::shared_ptr<TableFactory>(
          NewCuckooTableFactory(table_options));
#else
      fprintf(stderr, "Cuckoo table is not supported in lite mode\n");
      exit(1);
#endif  // ROCKSDB_LITE
    } else {
      BlockBasedTableOptions block_based_options;
      if (FLAGS_use_hash_search) {
        if (FLAGS_prefix_size == 0) {
          fprintf(stderr,
              "prefix_size not assigned when enable use_hash_search \n");
          exit(1);
        }
        block_based_options.index_type = BlockBasedTableOptions::kHashSearch;
      } else {
        block_based_options.index_type = BlockBasedTableOptions::kBinarySearch;
      }
      if (cache_ == nullptr) {
        block_based_options.no_block_cache = true;
      }
      block_based_options.cache_index_and_filter_blocks =
          FLAGS_cache_index_and_filter_blocks;
      block_based_options.pin_l0_filter_and_index_blocks_in_cache =
          FLAGS_pin_l0_filter_and_index_blocks_in_cache;
      block_based_options.block_cache = cache_;
      block_based_options.block_cache_compressed = compressed_cache_;
      block_based_options.block_size = FLAGS_block_size;
      block_based_options.block_restart_interval = FLAGS_block_restart_interval;
      block_based_options.filter_policy = filter_policy_;
      block_based_options.skip_table_builder_flush =
          FLAGS_skip_table_builder_flush;
      block_based_options.format_version = 2;
      options.table_factory.reset(
          NewBlockBasedTableFactory(block_based_options));
    }
    if (FLAGS_max_bytes_for_level_multiplier_additional_v.size() > 0) {
      if (FLAGS_max_bytes_for_level_multiplier_additional_v.size() !=
          (unsigned int)FLAGS_num_levels) {
        fprintf(stderr, "Insufficient number of fanouts specified %d\n",
                (int)FLAGS_max_bytes_for_level_multiplier_additional_v.size());
        exit(1);
      }
      options.max_bytes_for_level_multiplier_additional =
        FLAGS_max_bytes_for_level_multiplier_additional_v;
    }
    options.level0_stop_writes_trigger = FLAGS_level0_stop_writes_trigger;
    options.level0_file_num_compaction_trigger =
        FLAGS_level0_file_num_compaction_trigger;
    options.level0_slowdown_writes_trigger =
      FLAGS_level0_slowdown_writes_trigger;
    options.compression = FLAGS_compression_type_e;
    options.compression_opts.level = FLAGS_compression_level;
    options.WAL_ttl_seconds = FLAGS_wal_ttl_seconds;
    options.WAL_size_limit_MB = FLAGS_wal_size_limit_MB;
    options.max_total_wal_size = FLAGS_max_total_wal_size;

    if (FLAGS_min_level_to_compress >= 0) {
      assert(FLAGS_min_level_to_compress <= FLAGS_num_levels);
      options.compression_per_level.resize(FLAGS_num_levels);
      for (int i = 0; i < FLAGS_min_level_to_compress; i++) {
        options.compression_per_level[i] = kNoCompression;
      }
      for (int i = FLAGS_min_level_to_compress;
           i < FLAGS_num_levels; i++) {
        options.compression_per_level[i] = FLAGS_compression_type_e;
      }
    }
    options.soft_rate_limit = FLAGS_soft_rate_limit;
    options.hard_rate_limit = FLAGS_hard_rate_limit;
    options.soft_pending_compaction_bytes_limit =
        FLAGS_soft_pending_compaction_bytes_limit;
    options.hard_pending_compaction_bytes_limit =
        FLAGS_hard_pending_compaction_bytes_limit;
    options.delayed_write_rate = FLAGS_delayed_write_rate;
    options.allow_concurrent_memtable_write =
        FLAGS_allow_concurrent_memtable_write;
    options.enable_write_thread_adaptive_yield =
        FLAGS_enable_write_thread_adaptive_yield;
    options.write_thread_max_yield_usec = FLAGS_write_thread_max_yield_usec;
    options.write_thread_slow_yield_usec = FLAGS_write_thread_slow_yield_usec;
    options.rate_limit_delay_max_milliseconds =
      FLAGS_rate_limit_delay_max_milliseconds;
    options.table_cache_numshardbits = FLAGS_table_cache_numshardbits;
    options.max_grandparent_overlap_factor =
      FLAGS_max_grandparent_overlap_factor;
    options.disable_auto_compactions = FLAGS_disable_auto_compactions;
    options.source_compaction_factor = FLAGS_source_compaction_factor;

    // fill storage options
    options.allow_os_buffer = FLAGS_bufferedio;
    options.allow_mmap_reads = FLAGS_mmap_read;
    options.allow_mmap_writes = FLAGS_mmap_write;
    options.advise_random_on_open = FLAGS_advise_random_on_open;
    options.access_hint_on_compaction_start = FLAGS_compaction_fadvice_e;
    options.use_adaptive_mutex = FLAGS_use_adaptive_mutex;
    options.bytes_per_sync = FLAGS_bytes_per_sync;
    options.wal_bytes_per_sync = FLAGS_wal_bytes_per_sync;

    // merge operator options
    options.merge_operator = MergeOperators::CreateFromStringId(
        FLAGS_merge_operator);
    if (options.merge_operator == nullptr && !FLAGS_merge_operator.empty()) {
      fprintf(stderr, "invalid merge operator: %s\n",
              FLAGS_merge_operator.c_str());
      exit(1);
    }
    options.max_successive_merges = FLAGS_max_successive_merges;
    options.compaction_measure_io_stats = FLAGS_compaction_measure_io_stats;

    // set universal style compaction configurations, if applicable
    if (FLAGS_universal_size_ratio != 0) {
      options.compaction_options_universal.size_ratio =
        FLAGS_universal_size_ratio;
    }
    if (FLAGS_universal_min_merge_width != 0) {
      options.compaction_options_universal.min_merge_width =
        FLAGS_universal_min_merge_width;
    }
    if (FLAGS_universal_max_merge_width != 0) {
      options.compaction_options_universal.max_merge_width =
        FLAGS_universal_max_merge_width;
    }
    if (FLAGS_universal_max_size_amplification_percent != 0) {
      options.compaction_options_universal.max_size_amplification_percent =
        FLAGS_universal_max_size_amplification_percent;
    }
    if (FLAGS_universal_compression_size_percent != -1) {
      options.compaction_options_universal.compression_size_percent =
        FLAGS_universal_compression_size_percent;
    }
    options.compaction_options_universal.allow_trivial_move =
        FLAGS_universal_allow_trivial_move;
    if (FLAGS_thread_status_per_interval > 0) {
      options.enable_thread_tracking = true;
    }
    if (FLAGS_rate_limiter_bytes_per_sec > 0) {
      options.rate_limiter.reset(
          NewGenericRateLimiter(FLAGS_rate_limiter_bytes_per_sec));
    }

#ifndef ROCKSDB_LITE
    if (FLAGS_readonly && FLAGS_transaction_db) {
      fprintf(stderr, "Cannot use readonly flag with transaction_db\n");
      exit(1);
    }
#endif  // ROCKSDB_LITE

    if (FLAGS_num_multi_db <= 1) {
      OpenDb(options, FLAGS_db, &db_);
    } else {
      multi_dbs_.clear();
      multi_dbs_.resize(FLAGS_num_multi_db);
      for (int i = 0; i < FLAGS_num_multi_db; i++) {
        OpenDb(options, GetDbNameForMultiple(FLAGS_db, i), &multi_dbs_[i]);
      }
    }
    if (FLAGS_min_level_to_compress >= 0) {
      options.compression_per_level.clear();
    }
  }
```


**seventh, After I looked into FLAGS_db variable in rocksDB/tools/db_bench_too.cc file, I tested about creating Database.**


the following is results :

```shell
[hyunyoung.lee@localhost ~]$ cd rocksdb-4.3.1/
[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench
LevelDB:    version 4.3
Date:       Wed Apr 13 10:53:18 2016
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
fillseq      :       1.293 micros/op 773175 ops/sec;   85.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillsync     :       2.868 micros/op 348677 ops/sec;   38.6 MB/s (1000 ops)
DB path: [/tmp/rocksdbtest-1000/dbbench]
fillrandom   :       2.800 micros/op 357188 ops/sec;   39.5 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
overwrite    :       2.858 micros/op 349954 ops/sec;   38.7 MB/s
DB path: [/tmp/rocksdbtest-1000/dbbench]
readrandom   :       8.079 micros/op 123782 ops/sec;   13.7 MB/s (1000000 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
newiterator  :       0.814 micros/op 1228303 ops/sec; 
DB path: [/tmp/rocksdbtest-1000/dbbench]
newiteratorwhilewriting :       1.891 micros/op 528781 ops/sec;
DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandom   :      10.043 micros/op 99569 ops/sec; (816350 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
seekrandomwhilewriting :      51.014 micros/op 19602 ops/sec; (917578 of 1000000 found)

DB path: [/tmp/rocksdbtest-1000/dbbench]
put or merge error: Not implemented: Provide a merge_operator when opening DB
pure virtual method called
pure virtual method called
terminate called without an active exception
terminate called without an active exception
Received signal 6 (Aborted)
Aborted
[hyunyoung.lee@localhost rocksdb-4.3.1]$ ./db_bench --db=/dev/nvme0n1
LevelDB:    version 4.3
Date:       Wed Apr 13 10:56:58 2016
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
open error: IO error: `/dev/nvme0n1' exists but is not a directory
```

after source analyzation of db_bench_tools.cc, rocksDB relies on filesystem as levelDB.

if you know more about it, please refer to <a href ="https://github.com/facebook/rocksdb/issues/1016">this site</a>
