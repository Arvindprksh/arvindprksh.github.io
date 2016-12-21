---
layout: post
title: Block device and BIO(block I/O) Architecture
subtitle: Information of data structure associated with block dievice and layer
category: SSD (Solid State Drives)
tags: [block layer, block device driver]
permalink: /2016/09/08/Block_Device/
---

First of all, I refer to [this site(blkdevarch)](https://yannik520.github.io/blkdevarch.html)

and basic concept block device(Lecture 4 - Storage Systems in the_Kernel)

here is the above [file(Lecture 4 - Storage Systems in the_Kernel)](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/Lecture_4_-_Storage_Systems_in_the_Kernel.pdf)


## Introducntion of Block device.

 Block device provides storage for a large amount of data. 
 
 the kernel tries to make maximum performance with caching the data in memory, Because The I/O operations are costly.
 
 every actual I/O operation is performed by the deive drivers, The kernel provides various function and data structure for device drivers to register their handlers.
 
 Another requirement of the block driver layer is to hide the property of specific hardware and provide a general API to access the devices. 
 
 in hard disk, the sequence of request affects performance of device I/O, So The kernel Collect I/O requests and sorts them in block layer before calling device driver to precess I/O request. 
 
 So In block layer, kernel tries to improve performance of I/O operations with grouping the contiguous sertors and sorting  I/O requests. 
 
 And this algorithm that sorting and grouping I/O requests is called elevator algorithm. 
 
## access to block device from user space. 

 Block device are access as using the regular fiile. 
 
 Block device is verified with **major and minor number**, major number link file to device driver. And You can check partition inside block device with minor number.

 In other words, kernel only notices the device with major and minor number combination.

 managing the device file under /dev folder is convention.
 
## Basically data structure. 

 I will explain you these data structure as based on kernel version 4.5.3
 
 The data from the block device is accessed as blocks defined by [the structure buffer_head](http://lxr.linux.no/#linux+v4.5.3/include/linux/buffer_head.h#L44). 
 
 For example, when a file is read from the device, the file system handler for the read operation converts the file offset into a block number and issues a request to load that particular block.
 
 So there are registration mechanism for the device driver to register their handlers. 
 
 After that registration, The kernel calls the registered handler to perform the actual operation.
 
 The kernel als uses elevator algorithm to sort the **I/O requests** in the request queue.
 
 So The kernel give you different types of elevator algorithms. 
 
 from now on. I will introduce you data structure of kernel used by the block device drive layer.
 
### First, gendisk
   
   gendis has informations about a disk, The important fields are queue, part and fops in a gendisk. 
   
<pre><code>
<a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/genhd.h#L100">struct gendisk</a> {
 .....
 struct hd_struct  ** part; // partition information - this point is an array of the pointer to
 <strong>hd_struct</strong> indicating a partition.
 struct block_device_operations *fops; //block device operations table.
 request_queue_t * queue // to store request queue.
 .....
 };</code></pre>

 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/Gendisk_structure.png)
 
 block device operation
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/block device operation.png)

### Second, hd_struct

   hd_struct is information about partition on a disk. 
   
<pre><code>
 <a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/genhd.h#L77">struct hd_struct</a> {
 sector_t start_sector;
   sector_t nr_sects;
   int partno;
   ......
 };</code></pre>

### Third, block_device 

  each of disks is represented by **struct block_deivce** and **struct gendisk**. 
  
  This is used to represent a block device in the kernel. This can represent the whole disk or a particular partition. 
  
  when the structure represents a partition, the **bd_contains** field points to the device object which contains the partition.
  
  The **bd_part** field points to the partition structure of the device. this **bd_part** is structure representing the device.
  
  The field **bd_disk** points to the **gendisk structure** of the device.
  
  This structure is created only when the device is opened.(??? **fopen function** of file system).
  
  In here, Key point is the device driver still creates the **gendisk structure** and allocates **the request queue** and registers the structures into kernel. But until The device is actually opened for reading through the device file or mounting it. this structure will not be created.
  
  The field **bd_inode** points to the inode in the bdev file system.
  
  In other words, When the device file of block device is opened for the first time, the kernel allocates the block_device structure and fills structures in block_device structure.
  
  the Actual allocating function is **[bdev_alloc_inode](http://lxr.linux.no/#linux+v4.5.3/fs/block_dev.c#L243)**
  
<pre><code>
<a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/fs.h#L367">struct block_device</a> {
    dev_t bd_bdev;
    struct inode *bd_inode;
    struct list_head bd_inodes;
    struct block_device *bd_contains;
    struct hd_struct *bd_part;
    struct gendisk *bd_disk;
    struct list_head bd_list;
    }</code></pre>
 
 block device structure
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/structure of block device.png)
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/block_device_structure.png)
 

### Fourth, buffer_head.

 The sector size is physical property of block device. this sector is the funndamental unit of all block device. 
 
 device cannot address or operation on the sector unit smaller than the sector, 
 
 Software has different view, however and therefore imposes its own smallest logically addressable unit, which is block size. 
 
 here is the above's [reference(makelinux)](http://www.makelinux.net/books/lkd2/ch13lev1sec1)
 
 The buffer serves as the object that represents a disk block in memory. 

 The block is comprised of one or more sectors. but no more than a page in size. therefore a single page hold one or more blocks in memory. 
 
 Because The kernel requires some associated control information to accompany the data ( such as from which block device and which specific block the buffer is), each buffer is associated with a descriptor. The descriptor is called a buffer head and is of type [struct buffer_head](http://lxr.linux.no/#linux+v4.5.3/include/linux/buffer_head.h#L44).
 
 this struct buffer_head holds all the information that the kernel needs to manipulate buffers.
 
<pre><code>
<a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/buffer_head.h#L44">struct buffer_head</a> {
        unsigned long        b_state;          /* buffer state flags */
        atomic_t             b_count;          /* buffer usage counter */
        struct buffer_head   *b_this_page;     /* buffers using this page */
        struct page          *b_page;          /* page storing this buffer */
        sector_t             b_blocknr;        /* logical block number */
        u32                  b_size;           /* block size (in bytes) */
        char                 *b_data;          /* buffer in the page */
        struct block_device  *b_bdev;          /* device where block resides */
        bh_end_io_t          *b_end_io;        /* I/O completion method */
        void                 *b_private;       /* data for completion method */
        struct list_head     b_assoc_buffers;  /* list of associated mappings */
 }</code></pre>
 
 The above struture's reference is [here(makelinux)](http://www.makelinux.net/books/lkd2/ch13lev1sec2)
 
 The **b_state** field specifies the state of this particular buffer. It can be one or more of the flage.
 
 The purpose of a buffer head is to describe this mapping between the on-disk block and the physical in memory buffer (which is a sequence of bytes on a specific page). Acting as a descriptor of this buffer-to-block mapping is the data structure's only role in the kernel.
 
### Fifth, bio 

 **bio structur** is born due to inefficiency of struct buffer_head..
 
 This structure is used to represent an ongoing block I/O operation. 
 
 The buffer_head structure allocates **a bio** structure, and fill the structure and submit to block layer.
 
 I recommend you [this site(makelinux)](http://www.makelinux.net/books/lkd2/ch13lev1sec3) about bio

 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/bi_io_vecs.png)

 If you want more, I recommend [this URL(lwn)](https://lwn.net/Articles/26404/)
 
### sixth request. 

 a request is comprise of more than one bio. 
 
 This is used to represent a pending I/O request. these are stored as a list (doubly linked List) to the request queue.
 
 And this is sorted by the elevator algorithm. 
 
 ! When a bio is submitted to block layer, it tried to see if it can be added to an existing request in the request queue. 
 
 at this time, bi_next field of the bio structure is used to store the next bio in the list. 
 
 <pre><code>
 <a ref="http://lxr.linux.no/#linux+v4.5.3/include/linux/blkdev.h#L107">struct request_list</a>{
    mempool_t *rq_pool;
 }</code></pre>
 
 <pre><code>
 <a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/blkdev.h#L107">struct request</a> {
    struct list_head            queuelist;
    struct list_head            donelist;
    struct bio                  *bio;
    struct bio                  *biotail;
    void                       *elevator_private;
    struct gendisk             *rq_gendisk;
    request_queue_t            *q;
    request_list               *rl;
    .....
 }</code></pre>
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/request_doubly_Linked_list.png)
 
 - sectore < block <= Segment <= Page.
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/bio.PNG)
 
### seventh request_queue

 simply, after [reference](http://www.makelinux.net/books/lkd2/ch13lev1sec4), you can see the elevator alorithm type. 

 The request queue contains a doubly linked list of requests and associated control information

 This data structure stores information about the pending requests and other information required to manag the request queue like the elevator algorithm. 
 
 The request_fn field is the most important handler from the device driver point of view. this is the handler that is called when the actual I/O has to be performed i.e.,
 
 When a request object has to be processed.
 
 <pre><code>
 <a href="http://lxr.linux.no/#linux+v4.5.3/include/linux/blkdev.h#L283">struct request_queue</a> {
    struct list_head            queue_head;
    struct request             *lastmerge;
    elevator_t                 *elevator;
    struct request_list         rq;
    request_fn_proc            *request_fn;
    merge_request_fn           *back_merge_fn;
    merge_request_fn           *front_merge_fn;
    merge_requests_fn          *merge_requests_fn;
    make_request_fn            *make_request_fn;
    prep_rq_fn                 *prep_rq_fn;
    unplug_fn                  *unplug_fn;
    ...
 }</code></pre>

 be careful, in the above structure, you have to be interested in both __*request_fn__ and __*make_request_fn__
 
  ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Devicee/reqeust_queue_structure.png)

 if you want to know more about request, reqeust_queue, bio, click [this site(URL)](http://www.makelinux.net/ldd3/chp-16-sect-3)

## Linux IO Path 
 
 ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/Linux_IO_Path.png)

 the reference related is [this URL](http://users.suse.com/~sjayaraman/talks/IO_Journey_osidays.pdf)
 
 this is [file](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/IO_Journey_osidays.pdf
)

## registeration of a block device driver. 

 when you register block device driver, driver need to allocated gendisk for each disk and assign a request queue for each gendisk. the gendisk. 
  
## [concept of plug on block device](https://lwn.net/Articles/438256/)

  this is not plugging.
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/kernel plug image.jpg)
  
  this is plugging
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-09-08-Block_Device/kernel plug image2.jpg)

  [korean site 1](http://egloos.zum.com/nimhaplz/v/5598614) and [korean site 2](http://egloos.zum.com/studyfoss/v/5585801) about plug and block device 

## multi-queue block device layer and block device 

 If you want to know more about multi-queue, I recommend you [this site(URL)](http://ari-ava.blogspot.com/2014/07/opw-linux-block-io-layer-part-3-make.html)

# Reference 

  - [driver book](http://www.oreilly.com/openbook/linuxdrive3/book/) 

  - [blkdevarch](https://yannik520.github.io/blkdevarch.html)
