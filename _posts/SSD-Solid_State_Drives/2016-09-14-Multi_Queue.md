---
layout: post
title: Multi-Queu on block layer in Linux Kernel
subtitle: What is the concept of Multi-Queue, And code analysis of Multi-Queue on Block layer
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

Now, I'm interested in multi-block layer and open source. 

So, this article is for me to study about multi queue, 

This article is refered from [one URL, The Multi-Queue Interface](http://ari-ava.blogspot.com/2014/07/opw-linux-block-io-layer-part-4-multi.html) and [NVM Express ver 1.2 specification](http://nvmexpress.org/wp-content/uploads/NVM_Express_1_2_Gold_20141209.pdf)

Also, I recommend [this site,"Linux Kernel Newbies".](https://kernelnewbies.org/) for kernel newvbies.

And If you want to see the linux kernel, Just click [this site, Linux Kernel's Version](https://kernelnewbies.org/LinuxVersions).

!!! So, If you want know why mutilqueu is good for SSD. Just try to read [this](http://kernel.dk/blk-mq.pdf) 

# Multi Block layer 

 This multi queue layer's summary is from [The Multi-Queue Interface Article](http://ari-ava.blogspot.com/2014/07/opw-linux-block-io-layer-part-4-multi.html)
 
 [Linux kernel git](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=a4aea5623d4a54682b6ff5c18196d7802f3e478f) shows you conversion into blk-mq
 
 The blk_mq API Implements a two-levels block layer design which use two separate sets of request queues.
 
 **software staging queues, allocated per-CPU**
 
 **hardware dispatch queues, whose number typically match the number of actual haraware queues supported by th blcok device.**
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-14-Multi_Queue/mutil_queue_basic.png)
 
 as you can see the above picture. 
 
 the number of mapped queues between **software staging queues** and **hardware dispatch queues** is different 
 
 Now, let's think of case that two queue put differently. 
 
 let's say, three cases are in here. 
 
 1. **software staging queues** > **hardware dispatch queues**
 
 In this case, two or more **software staging queues** is allocated to one of hardware context. 
 And  a dispatch is performed while the hardware context will pull requests in from all the associated software queues. 
 
 2. **software staging queue** < **hardware dispatch queues**
 
 In this case, mapping between **software staging queues** and **hardware dispatch queues** is sequential. 

 3. **software staging queue** == **hardware dispatch queue** 
  
 In this case, this is the most simple case. i.e a direct 1 : 1 mapping is performed.


# Main data structure in mulit-queue block layer. 

## Basic Archictecture 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-14-Multi_Queue/multi-queue2-block layer.png)

## 1. blk_mq_reg (in kernel 4.5) 

 according to [The Multi-Queue Interface Article](http://ari-ava.blogspot.com/2014/07/opw-linux-block-io-layer-part-4-multi.html), 
 
 blk_mq_reg structure contains all of important information during the register of a new block device to the block layer.
 
 This data structure includes the pointer to a blk_mq_ops data structure, used to keep track of the specific routines to be used by the multi-queue block layer to interact with the device's driver.
 
 blk_mq_reg structure also keeps the number of hardware queues to be initialized and so on.
 
 ** However, blk_mq_reg disappear.
 
 **I think I need to consider blk_mq_ops to understand operation between block layer and block device**
 
 So you can ckeck the data structure in [kernel 3.15](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=3.15#L52)
 
```c
 52 struct blk_mq_reg {
 53         struct blk_mq_ops       *ops;
 54         unsigned int            nr_hw_queues;
 55         unsigned int            queue_depth;
 56         unsigned int            reserved_tags;
 57         unsigned int            cmd_size;       /* per-request extra data */
 58         int                     numa_node;
 59         unsigned int            timeout;
 60         unsigned int            flags;          /* BLK_MQ_F_* */
 61 };
```
 
 But, In kernel 4.5, You can not check this data structure. 
 
 I think this data structure is changed to [**struct blk_mq_tag_set *set in kernel 4.5**](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=4.5#L67)
 
```c
 67 struct blk_mq_tag_set {
 68         struct blk_mq_ops       *ops;
 69         unsigned int            nr_hw_queues;
 70         unsigned int            queue_depth;    /* max hw supported */
 71         unsigned int            reserved_tags;
 72         unsigned int            cmd_size;       /* per-request extra data */
 73         int                     numa_node;
 74         unsigned int            timeout;
 75         unsigned int            flags;          /* BLK_MQ_F_* */
 76         void                    *driver_data;
 77 
 78         struct blk_mq_tags      **tags;
 79 
 80         struct mutex            tag_list_lock;
 81         struct list_head        tag_list;
 82 };
```
 
 Because, In kernel 3.15, [**function(struct request_queue *blk_mq_init_queue(struct blk_mq_reg *reg, void *driver_data))**](http://lxr.free-electrons.com/source/block/blk-mq.c?v=3.15#L1297) is changed to [**function(struct request_queue *blk_mq_init_queue(struct blk_mq_tag_set *set))**](lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L1961)
 
## 2. [blk_mq_ops structure(in kernel 4.5)](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=4.5#L106) 
 
 as you can read above, this data structure is used to communicate multi-queue block layer with the block device's layer.

 In this data structure, the function performing mapping contexts between the **blk_mq_hw_ctx** and the **blk_mq_ctx** is stored in **map_queue** field. 

```c
106 struct blk_mq_ops {
107         /*
108          * Queue request
109          */
110         queue_rq_fn             *queue_rq; // this part
111 
112         /*
113          * Map to specific hardware queue
114          */
115         map_queue_fn            *map_queue; // this part
116 
117         /*
118          * Called on request timeout
119          */
120         timeout_fn              *timeout;
121 
122         /*
123          * Called to poll for completion of a specific tag.
124          */
125         poll_fn                 *poll;
126 
127         softirq_done_fn         *complete;
128 
129         /*
130          * Called when the block layer side of a hardware queue has been
131          * set up, allowing the driver to allocate/init matching structures.
132          * Ditto for exit/teardown.
133          */
134         init_hctx_fn            *init_hctx;
135         exit_hctx_fn            *exit_hctx;
136 
137         /*
138          * Called for every command allocated by the block layer to allow
139          * the driver to set up driver specific data.
140          *
141          * Tag greater than or equal to queue_depth is for setting up
142          * flush request.
143          *
144          * Ditto for exit/teardown.
145          */
146         init_request_fn         *init_request;
147         exit_request_fn         *exit_request;
148 };
```
 
## 3. [blk_mq_hw_ctx structure (in kernel 4.5)](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=4.5#L21)

 blk_mq_hw_ctx structure represents the hardware context which a request_queue is associated to.
 
 And this corresponding structure is the [blk_mq_ctx structure.(in kernel 4.5)](http://lxr.free-electrons.com/source/block/blk-mq.h?v=4.5#L6)

```c
 21 struct blk_mq_hw_ctx {
 22         struct {
 23                 spinlock_t              lock;
 24                 struct list_head        dispatch;
 25         } ____cacheline_aligned_in_smp;
 26 
 27         unsigned long           state;          /* BLK_MQ_S_* flags */
 28         struct delayed_work     run_work;
 29         struct delayed_work     delay_work;
 30         cpumask_var_t           cpumask;
 31         int                     next_cpu;
 32         int                     next_cpu_batch;
 33 
 34         unsigned long           flags;          /* BLK_MQ_F_* flags */
 35 
 36         struct request_queue    *queue;
 37         struct blk_flush_queue  *fq;
 38 
 39         void                    *driver_data;
 40 
 41         struct blk_mq_ctxmap    ctx_map;
 42 
 43         unsigned int            nr_ctx;
 44         struct blk_mq_ctx       **ctxs;
 45 
 46         atomic_t                wait_index;
 47 
 48         struct blk_mq_tags      *tags;
 49 
 50         unsigned long           queued;
 51         unsigned long           run;
 52 #define BLK_MQ_MAX_DISPATCH_ORDER       10
 53         unsigned long           dispatched[BLK_MQ_MAX_DISPATCH_ORDER];
 54 
 55         unsigned int            numa_node;
 56         unsigned int            queue_num;
 57 
 58         atomic_t                nr_active;
 59 
 60         struct blk_mq_cpu_notifier      cpu_notifier;
 61         struct kobject          kobj;
 62 
 63         unsigned long           poll_invoked;
 64         unsigned long           poll_success;
 65 };
```
 
## 4. [blk_mq_ctx structure.(in kernel 4.5)](http://lxr.free-electrons.com/source/block/blk-mq.h?v=4.5#L6)

 As you can read above, blk_mq_ctx as **software staging queue** is allocated per CPU. 
 
``` c
 6 struct blk_mq_ctx {
 7         struct {
 8                 spinlock_t              lock;
 9                 struct list_head        rq_list;
 10         }  ____cacheline_aligned_in_smp;
 11 
 12         unsigned int            cpu;
 13         unsigned int            index_hw;
 14 
 15         unsigned int            last_tag ____cacheline_aligned_in_smp;
 16 
 17         /* incremented at dispatch time */
 18         unsigned long           rq_dispatched[2];
 19         unsigned long           rq_merged;
 20 
 21         /* incremented at completion time */
 22         unsigned long           ____cacheline_aligned_in_smp rq_completed[2];
 23 
 24         struct request_queue    *queue;
 25         struct kobject          kobj;
 26 } ____cacheline_aligned_in_smp;
```
 
## 5. the [request_queue structure (in kernel 4.5)](http://lxr.free-electrons.com/source/include/linux/blkdev.h?v=4.5#L283)

The mapping of contexts between between the **blk_mq_hw_ctx** and the **blk_mq_ctx** is built on **map_queue field** of **blk_mq_ops structure**. The mapping is kept as the[**mq_map**](http://lxr.free-electrons.com/source/include/linux/blkdev.h?v=4.5#L312) of [**request_queue**](http://lxr.free-electrons.com/source/include/linux/blkdev.h?v=4.5#L283) data structure related to the block device in kernel 4.5

```c
283 struct request_queue {
284         /*
285          * Together with queue_head for cacheline sharing
286          */
287         struct list_head        queue_head;
288         struct request          *last_merge;
289         struct elevator_queue   *elevator;
290         int                     nr_rqs[2];      /* # allocated [a]sync rqs */
291         int                     nr_rqs_elvpriv; /* # allocated rqs w/ elvpriv */
292 
293         /*
294          * If blkcg is not used, @q->root_rl serves all requests.  If blkcg
295          * is used, root blkg allocates from @q->root_rl and all other
296          * blkgs from their own blkg->rl.  Which one to use should be
297          * determined using bio_request_list().
298          */
299         struct request_list     root_rl;
300 
301         request_fn_proc         *request_fn;
302         make_request_fn         *make_request_fn;
303         prep_rq_fn              *prep_rq_fn;
304         unprep_rq_fn            *unprep_rq_fn;
305         softirq_done_fn         *softirq_done_fn;
306         rq_timed_out_fn         *rq_timed_out_fn;
307         dma_drain_needed_fn     *dma_drain_needed;
308         lld_busy_fn             *lld_busy_fn;
309 
310         struct blk_mq_ops       *mq_ops;
311 
312         unsigned int            *mq_map;
313 
314         /* sw queues */
315         struct blk_mq_ctx __percpu      *queue_ctx;
316         unsigned int            nr_queues;
317 
318         /* hw dispatch queues */
319         struct blk_mq_hw_ctx    **queue_hw_ctx;
320         unsigned int            nr_hw_queues;
321 
322         /*
323          * Dispatch queue sorting
324          */
325         sector_t                end_sector;
326         struct request          *boundary_rq;
327 
328         /*
329          * Delayed queue handling
330          */
331         struct delayed_work     delay_work;
332 
333         struct backing_dev_info backing_dev_info;
334 
335         /*
336          * The queue owner gets to use this for whatever they like.
337          * ll_rw_blk doesn't touch it.
338          */
339         void                    *queuedata;
340 
341         /*
342          * various queue flags, see QUEUE_* below
343          */
344         unsigned long           queue_flags;
345 
346         /*
347          * ida allocated id for this queue.  Used to index queues from
348          * ioctx.
349          */
350         int                     id;
351 
352         /*
353          * queue needs bounce pages for pages above this limit
354          */
355         gfp_t                   bounce_gfp;
356 
357         /*
358          * protects queue structures from reentrancy. ->__queue_lock should
359          * _never_ be used directly, it is queue private. always use
360          * ->queue_lock.
361          */
362         spinlock_t              __queue_lock;
363         spinlock_t              *queue_lock;
364 
365         /*
366          * queue kobject
367          */
368         struct kobject kobj;
369 
370         /*
371          * mq queue kobject
372          */
373         struct kobject mq_kobj;
374 
375 #ifdef  CONFIG_BLK_DEV_INTEGRITY
376         struct blk_integrity integrity;
377 #endif  /* CONFIG_BLK_DEV_INTEGRITY */
378 
379 #ifdef CONFIG_PM
380         struct device           *dev;
381         int                     rpm_status;
382         unsigned int            nr_pending;
383 #endif
384 
385         /*
386          * queue settings
387          */
388         unsigned long           nr_requests;    /* Max # of requests */
389         unsigned int            nr_congestion_on;
390         unsigned int            nr_congestion_off;
391         unsigned int            nr_batching;
392 
393         unsigned int            dma_drain_size;
394         void                    *dma_drain_buffer;
395         unsigned int            dma_pad_mask;
396         unsigned int            dma_alignment;
397 
398         struct blk_queue_tag    *queue_tags;
399         struct list_head        tag_busy_list;
400 
401         unsigned int            nr_sorted;
402         unsigned int            in_flight[2];
403         /*
404          * Number of active block driver functions for which blk_drain_queue()
405          * must wait. Must be incremented around functions that unlock the
406          * queue_lock internally, e.g. scsi_request_fn().
407          */
408         unsigned int            request_fn_active;
409 
410         unsigned int            rq_timeout;
411         struct timer_list       timeout;
412         struct work_struct      timeout_work;
413         struct list_head        timeout_list;
414 
415         struct list_head        icq_list;
416 #ifdef CONFIG_BLK_CGROUP
417         DECLARE_BITMAP          (blkcg_pols, BLKCG_MAX_POLS);
418         struct blkcg_gq         *root_blkg;
419         struct list_head        blkg_list;
420 #endif
421 
422         struct queue_limits     limits;
423 
424         /*
425          * sg stuff
426          */
427         unsigned int            sg_timeout;
428         unsigned int            sg_reserved_size;
429         int                     node;
430 #ifdef CONFIG_BLK_DEV_IO_TRACE
431         struct blk_trace        *blk_trace;
432 #endif
433         /*
434          * for flush operations
435          */
436         unsigned int            flush_flags;
437         unsigned int            flush_not_queueable:1;
438         struct blk_flush_queue  *fq;
439 
440         struct list_head        requeue_list;
441         spinlock_t              requeue_lock;
442         struct work_struct      requeue_work;
443 
444         struct mutex            sysfs_lock;
445 
446         int                     bypass_depth;
447         atomic_t                mq_freeze_depth;
448 
449 #if defined(CONFIG_BLK_DEV_BSG)
450         bsg_job_fn              *bsg_job_fn;
451         int                     bsg_job_size;
452         struct bsg_class_device bsg_dev;
453 #endif
454 
455 #ifdef CONFIG_BLK_DEV_THROTTLING
456         /* Throttle data */
457         struct throtl_data *td;
458 #endif
459         struct rcu_head         rcu_head;
460         wait_queue_head_t       mq_freeze_wq;
461         struct percpu_ref       q_usage_counter;
462         struct list_head        all_q_node;
463 
464         struct blk_mq_tag_set   *tag_set;
465         struct list_head        tag_set_list;
466         struct bio_set          *bio_split;
467 
468         bool                    mq_sysfs_init_done;
469 };
```

## Initialization of Queue

 When a new devie driver using the multi-queue API is loaded, It creates and initializes a new blk_mq_ops structure and sets to its address the associated pointer of a new blk_mq_reg.
 
 More In detail, except for the below structure, other operations are now strictly required, 
 
 But, other operations can be specified in order to perform specific operations on allocation of contexts or on completion of an I/O request. 
 
 As of necessary data, the driver must initialize the number of submission queues it supports, along with their size.
 
 other data are required, to determine the size of the command supported by the driver and specific flags that must be exposed to the block layer. 
 
 <strong>BUT, in kernel version 4.5, [struct blk_mq_tag_set](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=4.5#L67) is important, The above job is implemented in this struct blk_mq_tag_set.</strong>
 
### queue_fn 
 
 this must be set to a function in charge of handling the command, for example, by passing the command to the low-level driver. 

### map_queue

  performs the mapping between hardware and software context. 
  
### [blk_mq_init_queue function (in kernel 4.5 source)](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L1961)

 after getting ready for gendisk and request_queue related to the device. It(driver) invokes the [blk_mq_init_queue function (in kernel 4.5 source)](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L1961)
 
 This function intializes the hardware and software contexts and performs the mapping between them.
 
 This intialization routine also sets an alternate make_request function, subsituting to the conventional request submission path which would includes the function [blk_make_request() (in kernel 4.5 code)](http://lxr.free-electrons.com/source/block/blk-core.c?v=4.5#L1342) the multi-queue submission path(which includes, instead, [blk_mq_make_request() (in kernel 4.5 code)](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L1243)). 
 
 In other words, the alternate make_request function is set with blk_queue_make_reqeust() helper. 
 
## Submission of Request

 Device initialization substituted the conventional block I/O submission function with [blk_mq_make_request()](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L1243) (in kernel 4.5 code), letting the multi-queue structures be used the perspective of the upper layer. 
 
 The make_request function (in kernel 4.5 no exist) used by the mutil-queue block layer includes the possibility to benefit from per-process plugging,But only for drivers supporting a single hardware queue or for async requests.
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-14-Multi_Queue/process_state.png)
 
 In case the request is sync and the driver actively uses the multi-queue interface, No plugging is performed. 
 
 if plugging is allowed, The make_request function also performs request merging, searching for a candidate first inside the task's plug list, 
 
 And finally in the software queue mapped to current CPU, The submission path does not involve any I/O sheduling-related call-back. 
 
 <strong>Finally, make_request sends immediately to th correspoding hardware queue any sync request, While it delays this transition in cas of async or flush requests, to allow for subsequent merging and more efficient dispatching.</strong>
 
 
## Request dispatch

 In case that an I/O request is synchronous (and therefore no plugging is allowed for it form the multi-queue block layer)
 
 Its dispatch to the device driver is performed int the context is performed in the context of the same request. 
 
 If the request is instead async or flush, Task plugging is present, 
 
 the dispatch is performed as The following timing :
 
 1 - In the context of the submission of another I/O reqeust to a software queue associated to the same hardware queue 

 2 - When the delayed work scheduled during reqeust submission is executed.
 
 
 The main run-of-queue function of the multi-queue block layer is the [blk_mq_run_hw_queue()](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L861) (in kernel 4.5 code) which basically depends on another driver-specific routine, pointed by the [queue_rq](http://lxr.free-electrons.com/source/include/linux/blk-mq.h?v=4.5#L106) (in kernel 4.5) field of its blk_mq_ops structure 
 
 !!I have to check relationship between <strong>blk_mq_run_hw_queue and request_qu!!</strong>
 
 !!This function delays any run of queue for an async reqeust, While it dispatches a sync reqeuest immediately to the driver.
 
 The inner function [__blk_mq_run_hw_queue()](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L727) (in kernel 4.5 code), called by [blk_mq_run_hw_queue()](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L861) (in kernel 4.5 code) in case the reqeust is sync, first joins any software queue associated to the currently-in-service hardware queue, Then it joins the resulting list with any entry already on the dispatch list.
 
 After collecting all to-be-served entries, the function [__blk_mq_run_hw_queue()](http://lxr.free-electrons.com/source/block/blk-mq.c?v=4.5#L727) (in kernel 4.5 code) processes them(entries), starting each reqeust and passing it on to the driver, with its queue_rq function.
 
 
 The function finally handles possible errors, by requeue or deletion of the associated requests.
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-14-Multi_Queue/Mutil_queue3.png)







# Reference 

 - [The Multi-Queue Interface](http://ari-ava.blogspot.com/2014/07/opw-linux-block-io-layer-part-4-multi.html)
 
 - [NVM Express 1.2](http://nvmexpress.org/wp-content/uploads/NVM_Express_1_2_Gold_20141209.pdf)
 
 - [Linux Kernel Newbies](https://kernelnewbies.org/)
 
 - [Linux Kernel's Version](https://kernelnewbies.org/LinuxVersions)
 
 - [Linux kernel git of convert into multi-queue](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=a4aea5623d4a54682b6ff5c18196d7802f3e478f)
