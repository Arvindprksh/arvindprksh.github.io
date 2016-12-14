---
layout: post
title: pblk 19 Document of OpenchannelSSD Linux, Work queue, memory barrier, write back cache control and Circular queue
subtitle: What is the concept of OpenChannelSSD's LightNVM ? and background knowledge
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

I quoute the article below from [git commit of openchannelSSD](https://github.com/OpenChannelSSD/linux/commit/87b8c926e627c63bdadce6e64a8a497c8126c894)

# Summary of OpenchannelSSD blk19. 

  after reading the linux's document, Pblk document, on OpenchannelSSD's officail site of linux. 
  
  I am going to summarize about the document as I understood. 

---
  1. pblk shows user openchannelSSD storage device as **block storage**. 
    
  2. the main tasks is **L2P(data placement), GC and recovery(mapping table, write)**. i.e user need to know constraints of Controller and media of ssd. 
    
  3. for now. pblk is based on **make_request_fn which issues REQ_PREFLUSH and REQ_FUA**. But, after reading Writeback_cache of linux document, the real device don't have to seriously take into consideration about this FLUSH bit. i.e for make_request_fn based block drivers neet to handle this without any help of block layer. To sum up, driver are responsible for FlUSH and not block layer. 
    
  4. In order to access the Physical flash, pblk make use of **general media manager**. i.e this general media make nvm storage that pblk view with the actual SSD device, collaborating with NVMe Driver. in addition, general media manager is in charge of a get/put block provisioning interface and Wear-leveling. specifically, I don't know how much general media deals with the level of wear-leveling and provisioning
    
  5. first Of all, Pblk has the late-mapping strategy. i.e just that has write buffer like ring buffer, as pblk document says, So I think I have to be carefule of **submit function** of data to flash layer.
    
  6. one I want summarize from the pblk document is upside of this mapping strategy. If what I understood is right. First, pblk maintain user I/O rating easily. Second, simplicity of requeue, Third, Using the same mapping for user I/O and garbage collection --**I think I can't understand Seconde and third before I investigate the source.**
    
  7. pblk now has round robin mapping strategy. If unbalaced LUN usage exists due to GC. At this time. pblk proiritizes less used LUN 
    
  8. Buffering write in ringbuffer, is useful to be suitable of constraints of controller and media. i.e page granularity that controller can handle, Write Unit(8 Page), whether media of SSD is SLC, MLC, TLC.
    
  9. pblk has grace areas for persistence of wirte data. 
    
  10. Ring write buffer of pblk design components like mem(producer), subm(consumer), sync(write failure), flush=sync_pointer(REQ_PREFLUSH or REQ_FUA), l2p_update.
    
basically write 
   
  11. In order to understand each role of the above pointers, refer to [Ring Write Buffer Design](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L94) of pblk document
   
  12. write context buffer has room for metadata for each 4KB write. [simple figure](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L145) on plbk documents
   
  13. wirte path is bio -> wirte context(pblk_w_ctx) -> bio is copied to write buffer -> (if pblk need flush) after storing data in wirte buffer, bio is completed.
                                                                                      -> (if not) after data is sent to media, bio is completed. 
   
  14. when data is written to wirte buffer. the L2P table updated so that LBAs point to the buffer entries.
    
  15. with separate write thread, user data from write buffer is consumed, At this time, new bio is made. 
    
  16. when flush is needed but write buffer has no enough data. At this time. padding is performed.
    
  17. on the completion path of write. sync pointer will be updated. 
    
  18. mem pointer wraps up and overwrite the old data. l2p_update will take care of updating the transalation table. 
    
basic write is done.
    
  19. [pblk's read path](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L181)
    
  20. [provisioning](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L210), to sum up, provisiong thread is separated from write thread. **after reading this part on pblk document before investigating the source. I think pblk dynamic provisioning is offered.**
    
  21. [traslation table recovery on outage](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L232), plbk manage two ways. the mapping information store two parts. one is out-of-bound area for that sector. the other one is the last page block with block information, for example, LBA-PPA mapping list, block status and counters. 
    
  22. [write recovery](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L258), When writes failure occur in pblk, pblk has 3-step process to handle it. we will talk about the three steps.
    
    22 - 1. pblk can find which PPAs failed with the 64-bit result field of the NVMe command. 
    
    22 - 2. The failed block is marked as bad block.  
    
    22 - 3. After making the failed block to bad block. All entries before the first error can be completed. A new nvme command is issued with the remaining PPAs and immediately sedt to the media. sync pointer waiting for buffer entries to be completed in order. this method only happens when bad block grow.
  
    22 - 4. [step 2](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L276) 
  
    22 - 5. if mapping to bad block is success, GC happens. you can check out this content in [CG section](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt#L290)
  
  23. Timing of triggering GC is when the number of free blocks on the LUN go blew threshold.
    
  * The above article is my summary of pblk document of openChannelSSD. The following arranges my thought, while reading the documents of linux, that contains my wondering and my thought at that time. 

---

The following is just my summaries of linux document(pblk 19) I read concerning OpenChannelSSD. 

# Basic concept. 

  - pblk is a LightNVM target implemeting a full host-side Flash Translation Layer(FTL).
  
  - pblk presents itself as a **mak_request_fn base driver** to the block layer. Specifically as block device driver. 
  
    * there is last work above block layer, i.e after target -> general media manager, call block layer ?  
     
  - Thus, The primary task of pblk is to translate logical block addresses(LBAs), into physical page addressed (PPAs), safely and efficiently under ther constraints imposed by SSD controllers and media.
  
    * it works as FTL(L2P).  ---> this meaning is pblk has part reading **SSD constraints** 
    
  - implements of pblk include everything related to **data placement, garbage collection (GC), and recovery.**
  
  - Also, by design, pblk supports **pluggable mapping and GC algorithm**
  
  - A siggle hardware device can ,thereby, accommodate specific workload by making changes in software to the desired module. 
  
    * Mapping algorithm(from logical to physical address) is developed in host side by host developer.
    
  - In its current state, pblk implements the following functionality :
      
       - Sector-based host-side translation table management. -- L2P table. 
       
       - Write buffering for write to physical flash pages. ---- ring buffer ?

       - Provisioning -- reserve space ? 

       - Translation table recovery on power outage  -- how ? 
       
          * this is about ,when the write fail, how to recover.
       
       - Retire bad flash blocks on write failure.
       
       - simple cost-based garbage collector (GC)
       
       - Sysfs integration. 
       
       - I/O rate-limiting ??
       
  - To access the physical flash, pblk makes use of LightNVM's general media manager, which exposes a get/put block provisioning interface. 
  
     * I think LightNVM's general media manager makes a new SSD for host.
      
  - Wear-levering is an integral part of the media manager and not a responsibility of pblk. 
  
     * How to do wear-levering in media manager ?
  
---

## Mapping Strategy. in Sector-based translation table management in host side.

   - In pblk, mapping strateg follows a late-mapping approach. i.e the mapping happen when data is going to be written to the media. So, data is written to **a write buffer** to start with. 

   - by this way, there are several reason. 
 
      - we can eable user I/O rating without breaking the actual mapping strategy
      
        * I think this is considered for user programmer to use lightNVM library.
    
      - we can simplify requeues
    
        * I think when requeueing, you don't have to do remapping. 
      
      - we can use the same mapping for user I/O and garbage collection.
    
        * how ?
      
  - i.e Mapping occurs on Write Thread moving a write buffer to the media, bases on algrith of Round Robin/ 
 
    * I Think write unit is 4KB.
  
  - In the event of unbalanced active LUNs usage due to GC, we prioritize less used LUNs, Note that wear-leveling is the media manager's responsibility, 
 

## Write Buffer 

  - pblk uses a ring write buffer of size N, where N is the power of two. 
  
  - Buffering facilitates sending writes to the controller in the size of and aligned to a given page size. 
  
     * this means alignment of flash addresses and Write unit is appropriate for Controller. 
     
     * what is the grace area in pblk ? I feel like it is just to check the number of sectors that must reside in the write buffer.
     
     **grace areas are difference between completed write (sync) and l2p_pointer.**
     
     OOB area is similar to metadata area.

## Ring Write Buffer Design.

  - Memory point (mem) : the head pointer (producer). It points to the next writalbe entry in the buffer. 
  
  - Submission Pointer (subm) : the tail pointer (consumer). It points to the next buffered entry. buffer count is calculated using mem and subm.
  
  - Sync Pointer (sync) : It signals the last submitted entry that has compeleted.  
    
     * I think this indicated the last entry that is persisted to media. that entry is completed.  
  
  - Flush Pointer (flush) : It guarantees taht flushes are respected by signaling the last entry associated with a REQ_FLUSH request. 

      * which one is the last entry with REQ_FLUSH. this is responsible to flush cache in SSD. 
      
      this pointer is not present in pblk 19. just name is just different. the name is **sync_point**.  

  - mapping Update pointer (l2p_update) : It guarantees that L2P lookups for entries that sitll reside in the write buffer, cache will point to it. even if they have successfully been peristed to the media. By doing this. this gauratees that all entries residing in the write buffer will be read from cache.
    
     * which location is the cache ?? in SSD  or for fs ?? But I think this is cache in device. 

### Write path

  - on a new write, That bio assiciated with it is converted a write context(plbk_w_ctx), where the logical block address(LBA), length and flush requirements are stored. 
 
    * bio -> pblk_w_ctx stores the logical block address (LBA), length and flush requirements. 
  
  - The bio data is copied to internal write buffer and completed if a flush is not requried. (in case of a flush, the bio is completed after all data in write buffer has been persisted to the media). 
  
  - when data is stored, the translation table is updated so that LBAs point to the buffer entries.
  
    * constraint of write is, when there is no enought data, that padding is performed.  
  
  - If write is successful.
  
    * The sync pointer will be updated on the completion path. 
    
  - When the head pointer(mem) wraps up and overwrites old data --- when ?
  
    * the l2p_update pointer takse care of updating the translation table so that future lookups will point to physical addresses on the device.  
  
    If you read in detail. you can get much information. 

## Read path

  - just this procedure is simple. but pblk doesn't gaurantee ordering. If you want ordering, Just use sync. 
  
# provisioning

  - Now LightNVM delegates block erases to the target. but later on,LightNVM moves it into Media manager.
 
# Translation table recovery.

  - The L2P translation table is maintained entirely in host memory. 
  
  - the ratio is approcaimately 1GB of L2P per 1TB of flash.
  
  - to restruct the table, pblk scan the media.
    
     * in detail, how to do that ? 
  
  
# Write Recovery

 -  simply speaking, in case of failure of write. this chapter explain to you plkd do how to take care of that problem. 


# Garbage Collection

 - When the number of free blocks on the LUN go below a certain threshold, GC kick off, 
 
 - it selects a victim block based on the invalid page counter and it moves all valid sectors back on the write buffer to be assigned to a new PPa
 
 
---

# [What is a circular buffer](https://github.com/OpenChannelSSD/linux/tree/pblk.19/Documentationcir) ??

  
  here circular buffer is like what I knew. that is similar to circular queue.  
 
  you have to remember that head fills up the buffer but tail is opposite, i.e head is produce but tail is consumer.
  
  here, pblk 19 uses this circular buffer to ring buffer with particular pointers.
  
  like sync,flush, l2pupdate. 
  
  
# [What is the memory barrier](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/memory-barriers.txt)

  memory barrier maens guaranteeing the suquence of memory access.
  
  cpu and complier carry out performance opitimization that can cause out-of-order execution on instruction of the code.
  
  **So barrier force some part to keep order of intructions.**
  
  The above words is summary of linux's document, memory-barries. about what the memory barriers is. 
  
  In detail, if you get experience of using memory. I recommend that case in the above document.
  
  
# [What is the Workqueueu](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/workqueue.txt)?

  - **I think workqueue is needed for asynchronous programming.**

  - **Workqueue API is for asynchronous process execution context.**
  
  **this concurrency managed Workqueue (cmwq) kewors is important**
  
  - worker is just thread to use the a work item on the workqueue. 
      
     * functions in workqueue run in process context. 
  
  - When there are work items on the workqueue, the worker executes the functions associated with the work items one after the other. On the other hand, when workqueue has no work item. the worker become idle. So when a new work item gets queued, the worker begins executing again.
  
  - Work item points to function to be executed asynchronously, work item is include on workqueue. 
  
  - In other words, if no work is queued, the worek threads become idle. These worker Threads are managed in so-called worker pools. 
  
  **Since the above is about concept of what workqueue is. If you want to use workqueue concurrently, I recommend you to read document of linux's workqueue.txt**
  
# [Write back_chache_control](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/block/writeback_cache_control.txt)

 - Many storage devieces, especially in the consumer market, come with volatile write back caches. 
 
 - That means the devices signal I/O completion to the operating system. before data actually hat hit the non-volatile storage. 
 
 - This behavior obviously speeds up various workloads, but it means the operating system needs to force data out to the non-volatile storage when It perfoms a data integrity operation like fsync, sync or an unmount.
 
 - The Linux block layer provides two simple mechanisms that let filesystems control the caching behavior of the storage device. 
 
      * filesystem controls the caching behavior of storage with two ways. 
      
  - one is a forced cached flush, and the other is the Forced Unit Access (FUA) flag for requests.
  
## Explicit cache flushes (a forced cached flush)
  
  - The **REQ_PREFLUSH** flag can be OR ed into The r/w flags of a bio submitted from the filesystem. 
  
  - The **REQ_PREFLUSH** flag will make sure the volatile cache of the storage device has been flushed before the actual I/O operation is started. 
  
  - Sometimes, The **REQ_PREFLUSH** flag can set on an empty bio structure, which causes only an explicit cache flush without any dependent I/O. It is recommend to use the **blkdev_issue_flus()** helper for a pure cache flush. 
  
## Forced Unit Access (I think Wirte Through)

  - The **REQ_FUA** flag can be OR ed into r/w flags of a bio submitted from filesystem.
  
  - The **REQ_FUA** will make sure that I/O completion for this request is only signaled after the data has been committed to non-volatile storage.
  
  
## Implementation details for filesystem.

  - Filesystems can simply set the **REQ_PREFLUSH** and **REQ_FUA** bits.
  
  - Filesystems do not have to worry if the Underlying devices need an explicit cache flushing and how the Forced Unit Access is implemented.
  
  - The **REQ_PREFLUSH** and **REQ_FUA** flags may both be set on a single bio. 

## Implementation details for make_request_fn based block derivers. 

  - These drivers will always see the **REQ_PREFLUSH** and **REQ_FUA** bits as they sit directly below the submit_bio interface. 
  
  - For remapping drivers, the **REQ_FUA** bits need to be propagated to nuderlying device, and a global flush needs to be implemented for bios with the **REQ_PREFLUSH** bit set. 
  
  - For real device drivers that do not have a volite cache, the **REQ_PREFLUSH** and **REQ_FUA** bits on non-empty bios can simply be ignored, and **REQ_PREFLUSH** requests without data can be completed without doing any work. 
  
## Implementation details for request_fn based block drivers.

  this part I recommend you to read on [the site](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/block/writeback_cache_control.txt)


# Reference

  - [Openchannel pblk document](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/lightnvm/pblk.txt)
  
  - [circular buffer for ring buffer](https://github.com/OpenChannelSSD/linux/tree/pblk.19/Documentationcir)
  
  - [WriteBack_cashe_control for ring buffer](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/block/writeback_cache_control.txt)
  
  - [Memory barrier](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/memory-barriers.txt)
  
  - [additional explanation of memory barrier](http://events.linuxfoundation.org/sites/events/files/slides/dbueso-elc2016-membarriers-final.pdf)
  
  - [Work queue](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/workqueue.txt)
  
  - [work queue, deferrable function vs workqueue function](https://www.safaribooksonline.com/library/view/understanding-the-linux/0596005652/ch04s08.html)
  
  - [Write back_chache_control](https://github.com/OpenChannelSSD/linux/blob/pblk.19/Documentation/block/writeback_cache_control.txt)
  
  
<!-- github log  of OpenchannelSSD    
```
commit 1064a37e1213a4cd6f047496431776dfd98ec810
Author: Javier González <javier@cnexlabs.com>
Date:   Wed Jul 27 10:09:01 2016 +0200

    lightnvm: physical block device (pblk) target
    
    This patch introduces a new LightNVM target implementing a full
    host-based Flash Translation Layer (FTL): pblk. It differs from the
    existing rrpc target in that rrpc is a hybrid approach, where
    the L2P table is maintained both on the host and on the device.
    
    pblk operates around a ring write buffer. Apart from buffering writes,
    this buffer allows to respect controller constrains on how flash pages
    must be written. The write buffer is complemented with a write context
    buffer, which stores metadata for each 4KB write. With regards to the
    mapping strategy, we follow a late-map approach, where the actual
    mapping to flash pages is done when the write buffer is being written to
    the media. Logical addresses are mapped physical flash pages in a
    round-robin fashion in relation to the active LUNs on the target.
    
    Apart from the typical head an tail pointers, the write buffer maintains
    a number of pointers to:
      - Submission pointer: Keeps track of the last entry submitted to the
        media.
      - Sync pointer: Keeps track of entries successfully stored on the
        flash. It acts as a backpointer that guarantees that I/Os are
        completed in order. This is necessary to guarantee that flushes are
        completed when they should. It delegates too some responsibility
        to the block layer since bios are completed in order.
      - Sync-point pointer: Guarantees that flushes are respected.
      - L2p-update pointer: Guarantees that lookups to cache entries will
        point to their cache line after L2P mapping takes place for as long
        as they remain in cache.
    
    The size of the ring buffer is the closest power-of-2 size to the
    number of active LUNs in the target X the size of a flash block.
    
    pblk implements basic FTL functionality:
      - GC: A simple cost-base garbage collector.
      - Write recovery: If a block becomes bad after writes have
        successfully been committed to it, the block is garbage collected,
        marked as bad and returned to the media manager.
      - Scan recovery: The last page of each block is used to store
        metadata that allows to reconstruct the L2P table in case of a
        crash. This is the current recovery strategy until we implement L2P
        snapshoting.
      - Rate limiter: TO DESCRIBE
      - Sysfs integration: Information about the target and its
        state is exposed through sysfs. This includes statistics and
        open, closed and bad blocks.
```
-->
