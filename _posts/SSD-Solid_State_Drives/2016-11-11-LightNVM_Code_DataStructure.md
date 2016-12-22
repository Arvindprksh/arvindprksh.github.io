---
layout: post
title: LightNVM's DataStructure code for generic media manager
subtitle: What DataStructure does lightNVM have for generic media manager ?
category: SSD (Solid State Drives)
tags: [lightnvm]
permalink: /2016/11/11/LightNVM_Code_DataStructure/
---

LightNVM pblk 19 

# Data structure 

## struct ppa_addr 

 from linux/include/lightnvm.h
 
```c
 18 #define NVM_BLK_BITS (16)
 19 #define NVM_PG_BITS  (16)
 20 #define NVM_SEC_BITS (8)
 21 #define NVM_PL_BITS  (8)
 22 #define NVM_LUN_BITS (8)
 23 #define NVM_CH_BITS  (7)
 24 
 25 struct ppa_addr {
 26         /* Generic structure for all addresses */
 27         union {
 28                 struct {
 29                         u64 blk         : NVM_BLK_BITS;
 30                         u64 pg          : NVM_PG_BITS;
 31                         u64 sec         : NVM_SEC_BITS;
 32                         u64 pl          : NVM_PL_BITS;
 33                         u64 lun         : NVM_LUN_BITS;
 34                         u64 ch          : NVM_CH_BITS;
 35                         u64 reserved    : 1;
 36                 } g;
 37 
 38                 struct {
 39                         u64 line        : 63;
 40                         u64 is_cached   : 1;
 41                 } c;
 42 
 43                 u64 ppa;
 44         };
 45 };
```

## struct nvm_dev

from linux/include/linux/lightnvm.h

```c
307 struct nvm_dev {
308         struct nvm_dev_ops *ops;
309 
310         struct list_head devices;
311 
312         /* Media manager */
313         struct nvmm_type *mt;
314         void *mp;
315 
316         /* System blocks */
317         struct nvm_sb_info sb;
318 
319         /* Device information */
320         int nr_chnls;
321         int nr_planes;
322         int luns_per_chnl;
323         int sec_per_pg; /* only sectors for a single page */
324         int pgs_per_blk;
325         int blks_per_lun;
326         int fpg_size;
327         int pfpg_size; /* size of buffer if all pages are to be read */
328         int sec_size;
329         int oob_size;
330         int mccap;
331         struct nvm_addr_format ppaf;
332 
333         /* Calculated/Cached values. These do not reflect the actual usable
334          * blocks at run-time.
335          */
336         int max_rq_size;
337         int plane_mode; /* drive device in single, double or quad mode */
338 
339         int sec_per_pl; /* all sectors across planes */
340         int sec_per_blk;
341         int sec_per_lun;
342 
343         /* lower page table */
344         int lps_per_blk;
345         int *lptbl;
346 
347         unsigned long total_secs;
348         int nr_luns;
349 
350         unsigned long *lun_map;
351         void *dma_pool;
352 
353         struct nvm_id identity;
354 
355         /* Backend device */
356         struct request_queue *q;
357         struct device dev;
358         struct device *parent_dev;
359         char name[DISK_NAME_LEN];
360         void *private_data;
361 
362         struct mutex mlock;
363         spinlock_t lock;
364 };
```

## struct nvm_target & struct nvm_tgt_instance

from linux/include/lightnvm.h

```c
211 struct nvm_target {
212         struct list_head list;
213         struct nvm_dev *dev;
214         struct nvm_tgt_type *type;
215         struct gendisk *disk;
216 
217         struct kobject kobj;
218 };
219 
220 struct nvm_tgt_instance {
221         struct nvm_tgt_type *tt;
222 };
```

## struct nvm_tgt_type

from linux/include/linux/lightnvm.h

```c 
446 struct nvm_tgt_type {
447         const char *name;
448         unsigned int version[3];
449 
450         /* target entry points */
451         nvm_tgt_make_rq_fn *make_rq;
452         nvm_tgt_capacity_fn *capacity;
453         nvm_end_io_fn *end_io;
454 
455         /* module-specific init/teardown */
456         nvm_tgt_init_fn *init;
457         nvm_tgt_exit_fn *exit;
458 
459         nvm_tgt_sysfs_init_fn *sysfs_init;
460         nvm_tgt_sysfs_exit_fn *sysfs_exit;
461         nvm_tgt_sysfs_show_fn *sysfs_show;
462         nvm_tgt_sysfs_store_fn *sysfs_store;
463 
464         /* For internal use */
465         struct list_head list;
466 };
```

## struct nvm_lun_mgmt

from linux/include/linux/lightnvm.h

```c
468 struct nvm_lun_mgmt {
469         /* lun block lists */
470         struct list_head used_list;     /* In-use blocks */
471         struct list_head free_list;     /* Not used blocks i.e. released
472                                          * and ready for use
473                                          */
474         struct list_head bb_list;       /* Bad blocks. Mutually exclusive with
475                                          * free_list and used_list
476                                          */
477 
478         unsigned int nr_free_blocks;    /* Number of unused blocks */
479 };
```




## static inline struct ppa_addr generic_to_dev_addr(struct nvm_dev *dev, struct ppa_addr r)

from linux/include/linux/lightnvm.h

```c
366 static inline struct ppa_addr generic_to_dev_addr(struct nvm_dev *dev,
367                                                 struct ppa_addr r)
368 {
369         struct ppa_addr l;
370 
371         l.ppa = ((u64)r.g.blk) << dev->ppaf.blk_offset;
372         l.ppa |= ((u64)r.g.pg) << dev->ppaf.pg_offset;
373         l.ppa |= ((u64)r.g.sec) << dev->ppaf.sect_offset;
374         l.ppa |= ((u64)r.g.pl) << dev->ppaf.pln_offset;
375         l.ppa |= ((u64)r.g.lun) << dev->ppaf.lun_offset;
376         l.ppa |= ((u64)r.g.ch) << dev->ppaf.ch_offset;
377 
378         return l;
379 }
```

-----

# Funtion 

## struct nvm_dev_ops 

from linux/include/linux/lightnvm.h

```c
 65 struct nvm_dev_ops {
 66         nvm_id_fn               *identity;
 67         nvm_get_l2p_tbl_fn      *get_l2p_tbl;
 68         nvm_op_bb_tbl_fn        *get_bb_tbl;
 69         nvm_op_set_bb_fn        *set_bb_tbl;
 70 
 71         nvm_submit_io_fn        *submit_io;
 72         nvm_erase_blk_fn        *erase_block;
 73 
 74         nvm_create_dma_pool_fn  *create_dma_pool;
 75         nvm_destroy_dma_pool_fn *destroy_dma_pool;
 76         nvm_dev_dma_alloc_fn    *dev_dma_alloc;
 77         nvm_dev_dma_free_fn     *dev_dma_free;
 78 
 79         unsigned int            max_phys_sect;
 80 };
```

## struct nvm_tgt_type

```c
446 struct nvm_tgt_type {
447         const char *name;
448         unsigned int version[3];
449 
450         /* target entry points */
451         nvm_tgt_make_rq_fn *make_rq;
452         nvm_tgt_capacity_fn *capacity;
453         nvm_end_io_fn *end_io;
454 
455         /* module-specific init/teardown */
456         nvm_tgt_init_fn *init;
457         nvm_tgt_exit_fn *exit;
458 
459         nvm_tgt_sysfs_init_fn *sysfs_init;
460         nvm_tgt_sysfs_exit_fn *sysfs_exit;
461         nvm_tgt_sysfs_show_fn *sysfs_show;
462         nvm_tgt_sysfs_store_fn *sysfs_store;
463 
464         /* For internal use */
465         struct list_head list;
466 };
```

## struct nvmm_type 

```c
511 struct nvmm_type {
512         const char *name;
513         unsigned int version[3];
514 
515         nvmm_register_fn *register_mgr;
516         nvmm_unregister_fn *unregister_mgr;
517 
518         nvmm_create_tgt_fn *create_tgt;
519         nvmm_remove_tgt_fn *remove_tgt;
520 
521         /* Block administration callbacks */
522         nvmm_get_blk_fn *get_blk;
523         nvmm_put_blk_fn *put_blk;
524         nvmm_open_blk_fn *open_blk;
525         nvmm_close_blk_fn *close_blk;
526         nvmm_flush_blk_fn *flush_blk;
527 
528         nvmm_submit_io_fn *submit_io;
529         nvmm_erase_blk_fn *erase_blk;
530 
531         /* Bad block mgmt */
532         nvmm_mark_blk_fn *mark_blk;
533 
534         /* Configuration management */
535         nvmm_get_lun_fn *get_lun;
536         nvmm_reserve_lun *reserve_lun;
537         nvmm_release_lun *release_lun;
538 
539         /* Statistics */
540         nvmm_lun_info_print_fn *lun_info_print;
541 
542         nvmm_get_area_fn *get_area;
543         nvmm_put_area_fn *put_area;
544 
545         struct list_head list;
546 };
```
