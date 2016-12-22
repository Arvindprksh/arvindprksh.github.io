---
layout: post
title: LightNVM code of Generic Media 
subtitle: analysis of Generic Media code of LightNVM
category: SSD (Solid State Drives)
tags: [lightnvm, nvme]
permalink: /2016/11/07/LightNVM_Code_Of_Generic_Media/
---

<!-- lightNVM pblk 19 version when I clone git of linux of lightnvm november 7. 2016-->


# comparasion of each Headerfile ( pblk vs rrpc )

## gennvm.h

![](/img/Image/SSD-Solid_State_Drives/2016-11-07-LightNVM_Code_Of_Generic_Media/pblk(19) vs rrpc of gennvm header file.png)

## lightnvm.h

![](/img/Image/SSD-Solid_State_Drives/2016-11-07-LightNVM_Code_Of_Generic_Media/pblk(19) vs rrpc of lightNVM header file.png)

## rrpc.h

![](/img/Image/SSD-Solid_State_Drives/2016-11-07-LightNVM_Code_Of_Generic_Media/pblk (19) vs rrpc of rrpc header file.png)

# LightNVM's function calls

# Check if the kernel support LightNVM. 

<!--here, pblk 19 -->

## 2. int nvme_nvm_ns_supported(struct nvme_ns *ns,struct nvme_id_ns *id)

From linux/drivers/nvme/host/lightnvm.c

```c
630 /* move to shared place when used in multiple places. */
631 #define PCI_VENDOR_ID_CNEX 0x1d1d
632 #define PCI_DEVICE_ID_CNEX_WL 0x2807
633 #define PCI_DEVICE_ID_CNEX_QEMU 0x1f1f
634 
635 int nvme_nvm_ns_supported(struct nvme_ns *ns, struct nvme_id_ns *id)
636 {
637         struct nvme_ctrl *ctrl = ns->ctrl;
638         /* XXX: this is poking into PCI structures from generic code! */
639         struct pci_dev *pdev = to_pci_dev(ctrl->dev);
640 
641         /* QEMU NVMe simulator - PCI ID + Vendor specific bit */
642         if (pdev->vendor == PCI_VENDOR_ID_CNEX &&
643                                 pdev->device == PCI_DEVICE_ID_CNEX_QEMU &&
644                                                         id->vs[0] == 0x1)
645                 return 1; 
.......
660         return 0;
661 }
```

The following shows you which calls the above function. 

## 1. static void nvme_alloc_ns(struct nvme_ctrl * ctrl, unsigned nsid) 

From linux/drivers/nvme/host/core.c

```c
1651 static void nvme_alloc_ns(struct nvme_ctrl *ctrl, unsigned nsid)
1652 {
1653         struct nvme_ns *ns;
1654         struct gendisk *disk;
1655         struct nvme_id_ns *id;
1656         char disk_name[DISK_NAME_LEN];
1657         int node = dev_to_node(ctrl->dev);
....... 
1686         if (nvme_nvm_ns_supported(ns, id)) {
1687                 if (nvme_nvm_register(ns, disk_name, node,
1688                                                         &nvme_ns_attr_group)) {
1689                         dev_warn(ctrl->dev, "%s: LightNVM init failure\n",
1690                                                                 __func__);
1691                         goto out_free_id;
1692                 }
1693         } else {
.......
1706         }
.......
1719         device_add_disk(ctrl->device, ns->disk);
.......
1724         return;
.......
1733 }
```

## 3. int nvme_nvm_resgiter(struct nvme_ns *ns, char *disk_name, int node, const struct attribute_group *attrs)

from linux/drivers/nvme/host/nvme.h

 - struct nvme_ns
 
```c
149 /*
150  * An NVM Express namespace is equivalent to a SCSI LUN
151  */
152 struct nvme_ns {
153         struct list_head list;
154 
155         struct nvme_ctrl *ctrl;
156         struct request_queue *queue;
157         struct gendisk *disk;
158         struct nvm_dev *ndev;          // new addition in pblk kernel version.
159         struct kref kref;
.......
177 };
```

from linux/drivers/nvme/host/nvme.h

```c
98 struct nvme_ctrl {
 99         enum nvme_ctrl_state state;
100         spinlock_t lock;
101         const struct nvme_ctrl_ops *ops;
102         struct request_queue *admin_q;
103         struct request_queue *connect_q;
.....
107         struct blk_mq_tag_set *tagset;
108         struct list_head namespaces;
109         struct mutex namespaces_mutex;
110         struct device *device;  /* char device */
.....
147 };
```


From linux/drivers/nvme/host/lightnvm.c

```c
596 int nvme_nvm_register(struct nvme_ns *ns, char *disk_name, int node,
597                       const struct attribute_group *attrs)
598 {
599         struct request_queue *q = ns->queue;
600         struct nvm_dev *dev;
.....
607         dev->q = q;
608         memcpy(dev->name, disk_name, DISK_NAME_LEN);
609         dev->ops = &nvme_nvm_dev_ops;
610         dev->parent_dev = ns->ctrl->device;
611         dev->private_data = ns;
612         ns->ndev = dev;
613 
614         ret = nvm_register(dev);
.....
621         return ret;
622 }
```

## 4.  int nvm_register(struct nvm_dev *dev)

from linux/drivers/lightnvm/core.c

```c
 729 int nvm_register(struct nvm_dev *dev)
 730 {
 731         int ret;
 732 
 733         ret = nvm_init(dev);
 .....
 752         ret = nvm_sysfs_register_dev(dev);
 .....
 756         if (dev->identity.cap & NVM_ID_DCAP_BBLKMGMT) {
 757                 ret = nvm_get_sysblock(dev, &dev->sb);
 758                 if (!ret)
 759                         pr_err("nvm: device not initialized.\n");
 760                 else if (ret < 0)
 761                         pr_err("nvm: err (%d) on device initialization\n", ret);
 762         }
 763 
 764         /* register device with a supported media manager */
 765         down_write(&nvm_lock);
 766         if (ret > 0)
 767                 dev->mt = nvm_init_mgr(dev);
 768         list_add(&dev->devices, &nvm_devices);
 769         up_write(&nvm_lock);
 770 
 771         return 0;
 ......
 777 }
```

## 5. int nvm_get_sysblock(struct nvm_dev *dev, struct nvm_sb_info *info)

form linux/include/lightnvme.h

 -  nvm_system_block 
 
```c 
583 /* sysblk.c */
584 #define NVM_SYSBLK_MAGIC 0x4E564D53 /* "NVMS" */
585 
586 /* system block on disk representation */
587 struct nvm_system_block {
588         __be32                  magic;          /* magic signature */
589         __be32                  seqnr;          /* sequence number */
590         __be32                  erase_cnt;      /* erase count */
591         __be16                  version;        /* version number */
592         u8                      mmtype[NVM_MMTYPE_LEN]; /* media manager name */
593         __be64                  fs_ppa;         /* PPA for media manager
594                                                  * superblock */
595 };
```
  - nvm_sb_info
  
```c
298 /* system block cpu representation */
299 struct nvm_sb_info {
300         unsigned long           seqnr;
301         unsigned long           erase_cnt;
302         unsigned int            version;
303         char                    mmtype[NVM_MMTYPE_LEN];
304         struct ppa_addr         fs_ppa;
305 };
```

from linux/drivers/lightnvm/sysblk.c

``` c
373 int nvm_get_sysblock(struct nvm_dev *dev, struct nvm_sb_info *info)
374 {
375         struct ppa_addr sysblk_ppas[MAX_SYSBLKS];
376         struct sysblk_scan s;
377         struct nvm_system_block *cur;
......
381         /*
382          * 1. setup sysblk locations
383          * 2. get bad block list
384          * 3. filter on host-specific (type 3)
385          * 4. iterate through all and find the highest seq nr.
386          * 5. return superblock information
387          */
....
392         nvm_setup_sysblk_scan(dev, &s, sysblk_ppas);
393 
394         mutex_lock(&dev->mlock);
395         ret = nvm_get_all_sysblks(dev, &s, sysblk_ppas, 0);
......
399         /* no sysblocks initialized */
400         if (!s.nr_ppas)
401                 goto err_sysblk;
.....
407         /* find the latest block across all sysblocks */
408         for (i = 0; i < s.nr_rows; i++) {
409                 for (j = 0; j < MAX_BLKS_PR_SYSBLK; j++) {
410                         struct ppa_addr ppa = s.ppas[scan_ppa_idx(i, j)];
411 
412                         ret = nvm_scan_block(dev, &ppa, cur);
.....
417                 }
418         }
419 
420         nvm_sysblk_to_cpu(info, cur);
......
428         return ret;
429 }
```
So far, just  after booting, initialization 
---

# From now on just, How sumbit IO function 

from linux/drivers/lightnmv/gennvm.c

 - gen_submit_io

```c
754 static int gen_submit_io(struct nvm_dev *dev, struct nvm_rq *rqd)
755 {
756         if (!dev->ops->submit_io)
757                 return -ENODEV;
758 
759         /* Convert address space */
760         nvm_generic_to_addr_mode(dev, rqd);
761 
762         rqd->dev = dev;
763         rqd->end_io = gen_end_io;
764         return dev->ops->submit_io(dev, rqd);
765 }
```

from linux/drivers/lightnvm/core.c

 - void nvm_generic_to_addr_mode(struct nvme_dev *dev, struct nvme_rq *rqd)
 
```
282 void nvm_generic_to_addr_mode(struct nvm_dev *dev, struct nvm_rq *rqd)
 283 {
 284         int i;
 285 
 286         if (rqd->nr_ppas > 1) {
 287                 for (i = 0; i < rqd->nr_ppas; i++)
 288                         rqd->ppa_list[i] = generic_to_dev_addr(dev,
 289                                                         rqd->ppa_list[i]);
 290         } else {
 291                 rqd->ppa_addr = generic_to_dev_addr(dev, rqd->ppa_addr);
 292         }
 293 }
 294 EXPORT_SYMBOL(nvm_generic_to_addr_mode);
```


from include/linux/lightnvm.h

 - struct nvm_dev_ops

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

from linux/drivers/nvme/host/lightnvm.c

 - maching the above part with function in NVMe driver code

```c
577 static struct nvm_dev_ops nvme_nvm_dev_ops = {
578         .identity               = nvme_nvm_identity,
579 
580         .get_l2p_tbl            = nvme_nvm_get_l2p_tbl,
581 
582         .get_bb_tbl             = nvme_nvm_get_bb_tbl,
583         .set_bb_tbl             = nvme_nvm_set_bb_tbl,
584 
585         .submit_io              = nvme_nvm_submit_io,
586         .erase_block            = nvme_nvm_erase_block,
587 
588         .create_dma_pool        = nvme_nvm_create_dma_pool,
589         .destroy_dma_pool       = nvme_nvm_destroy_dma_pool,
590         .dev_dma_alloc          = nvme_nvm_dev_dma_alloc,
591         .dev_dma_free           = nvme_nvm_dev_dma_free,
592 
593         .max_phys_sect          = 64,
594 };
```

## static int nvme_nvm_submit_io(struct nvm_dev *dev, struct nvm_rq *rqd)

from linux/drivers/nvme/host/lightnvm.c

```c
495 static int nvme_nvm_submit_io(struct nvm_dev *dev, struct nvm_rq *rqd)
496 {
497         struct request_queue *q = dev->q;
498         struct nvme_ns *ns = q->queuedata;
499         struct request *rq;
500         struct bio *bio = rqd->bio;
501         struct nvme_nvm_command *cmd;
..... 
523         nvme_nvm_rqtocmd(rq, rqd, ns, cmd);
.....
531         blk_execute_rq_nowait(q, NULL, rq, 0, nvme_nvm_end_io);
532 
533         return 0;
534 }
```

## void blk_execute_rq_nowait(struc request_queue *q, struct gendisk *bd_disk, struct request *rq, int at_head, rq_end_io_fn *done)

from linux/block/blk-exec.c

```c
 36 /**
 37  * blk_execute_rq_nowait - insert a request into queue for execution
 38  * @q:          queue to insert the request in
 39  * @bd_disk:    matching gendisk
 40  * @rq:         request to insert
 41  * @at_head:    insert request at head or tail of queue
 42  * @done:       I/O completion handler
 43  *
 44  * Description:
 45  *    Insert a fully prepared request at the back of the I/O scheduler queue
 46  *    for execution.  Don't wait for completion.
 47  *
 48  * Note:
 49  *    This function will invoke @done directly if the queue is dead.
 50  */
 51 void blk_execute_rq_nowait(struct request_queue *q, struct gendisk *bd_disk,
 52                            struct request *rq, int at_head,
 53                            rq_end_io_fn *done)
 54 {
 55         int where = at_head ? ELEVATOR_INSERT_FRONT : ELEVATOR_INSERT_BACK;
.....
 63         /*
 64          * don't check dying flag for MQ because the request won't
 65          * be reused after dying flag is set
 66          */
 67         if (q->mq_ops) {
 68                 blk_mq_insert_request(rq, at_head, true, false);
 69                 return;
 70         }
.....
 81 
 82         __elv_add_request(q, rq, where);
 83         __blk_run_queue(q);
 84         spin_unlock_irq(q->queue_lock);
 85 }
 86 EXPORT_SYMBOL_GPL(blk_execute_rq_nowait);
```
 - Why do they transfer to blk-mq ???

# linux/include/lightnvm.h

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
# lightNVM.h

## struct nvm_lun_mgmt {

```c
struct nvm_lun_mgmt {
        /* lun block lists */
        struct list_head used_list;     /* In-use blocks */
        struct list_head free_list;     /* Not used blocks i.e. released
                                         * and ready for use
                                         */
        struct list_head bb_list;       /* Bad blocks. Mutually exclusive with
                                         * free_list and used_list
                                         */

        unsigned int nr_free_blocks;    /* Number of unused blocks */
};
```

# gennvm.h

## struct gen_lun {

```c
struct gen_lun {
        struct nvm_lun vlun;

        /* A LUN can either be managed by the media manager if it is shared
         * among several used through the generic get/put block interface or
         * exclusively owned by a target. In this case, the target manages
         * the LUN. gen_lun always maintains a reference to the LUN management.
         *
         * Exclusive access is managed by the dev->lun_map bitmask. 0:
         * non-exclusive, 1: exclusive.
         */
        struct nvm_lun_mgmt *mgmt;
        struct nvm_target *tgt;
};
```

## struct gen_dev {

```c
struct gen_dev {
        struct nvm_dev *dev;  // nvme device

        int nr_luns;  // the number of luns. 
        struct gen_lun *luns; // the above struct, gen_lun
        struct list_head area_list; // ??

        struct mutex lock;
        struct list_head targets; // ?? 
};
```

## struct gen_area {

```c
struct gen_area {
        struct list_head list;
        sector_t begin;
        sector_t end;   /* end is excluded */
};
```

# gennvm.c 

## function list of gennvm.c

```c
1. 
static struct attribute gen_type_attr = {
        .name = "type",
        .mode = S_IRUGO
};

2.
static struct attribute *gen_target_attrs[] = {
        &gen_type_attr,
        NULL,
};

3.
static const struct sysfs_ops target_sysfs_ops = {
        .show = gen_target_attr_show,
        .store = gen_target_attr_store,
};

4.
static struct kobj_type nvm_target_type = {
        .sysfs_ops      = &target_sysfs_ops,
        .default_attrs  = gen_target_attrs,
        .release        = gen_target_release
};

5. 
static const struct block_device_operations gen_fops = {
        .owner          = THIS_MODULE,
};

6. 
static DEVICE_ATTR(blocks, S_IRUGO, gen_sysfs_show, NULL);

7.
static struct attribute *gen_attrs[] = {
        &dev_attr_blocks.attr,
        NULL,
};

8.
static struct attribute_group gen_attr_group = {
        .name = "mediamgr",
        .attrs = gen_attrs,
};

9.
static struct nvmm_type gen = {
        .name                   = "gennvm",
        .version                = {0, 1, 0},

        .register_mgr           = gen_register,
        .unregister_mgr         = gen_unregister,

        .create_tgt             = gen_create_tgt,
        .remove_tgt             = gen_remove_tgt,

        .get_blk                = gen_get_blk,
        .put_blk                = gen_put_blk,

        .submit_io              = gen_submit_io,
        .erase_blk              = gen_erase_blk,

        .mark_blk               = gen_mark_blk,

        .get_lun                = gen_get_lun,
        .reserve_lun            = gen_reserve_lun,
        .release_lun            = gen_release_lun,
        .lun_info_print         = gen_lun_info_print,

        .get_area               = gen_get_area,
        .put_area               = gen_put_area,

};
```
##  lists of static struct nvmm_type gen = {

### .register_mgr = gen_register

#### static int gen_register(struct nvm_dev *dev)

```c
                                  |---  initialize **struct gen_dev**
                                  |---  ret = gen_luns_init(dev(struct nvm_dev), gn) |--- initialize struct nvm_lun_mgmt of struct gen_lun
gen -> register_mgr(gen_register) |  
                                  |---  ret = gen_blocks_init(dev(struct nvm_dev), gn) |--- initialize struct nvme_block with truct gen_lnu
                                  |                                                    |--- if (dev->ops->get_bb_tbl)  |--- ret = nvm_get_bb_tbl(dev, ppa, blks);
                                                                                                                       |--- ret = gen_block_bb(gn, ppa, blks, nr_blks);
                                                                                       |--- if (dev->identity.dom & NVM_RSP_L2P && dev->ops->get_l2p_tbl)                                                                                              |--- ret = dev->ops->get_l2p_tbl(dev, 0, dev->total_secs,
                                                        gen_block_map, dev); 
                                  |---  if (sysfs_create_group(&dev->dev.kobj, &gen_attr_group))
                                  |--- return 1;
```

### .unregister_mgr = gen_unregister 

##### static void gen_unregister(struct nvm_dev *dev)

```c
                                      |--- _gen_remove_target(t(nvm_target)) |--- gen_unregister_target(t(nvm_target))
                                      |
gen -> unregister_mgr(gen_unregister) |--- sysfs_remove_group(&dev->dev.kobj, &gen_attr_group);
                                      |
                                      |--- gen_free(dev);
```

###  .create_tgt = gen_create_tgt

##### static int gen_create_tgt(struct nvm_dev *dev, struct nvm_ioctl_create *create)

this part means handling create command of lnvm tool about create

```c
                                  |--- tt(struct nvm_tgt_type) = nvm_find_target_type(create->tgttype, 1);
                                  |--- t(struct nvm_target) = gen_find_target(gn, create->tgtname);
gen -> create_tgt(gen_create_tgt) |--- tqueue(request_queue) = blk_alloc_queue_node(GFP_KERNEL, dev->q->node);
                                  |--- blk_queue_make_request(tqueue, tt->make_rq);
                                  |--- targetdata = tt->init(dev, tdisk, s->lun_begin, s->lun_end);
                                  |--- return 0;
```

### .remove_tgt = gen_remove_tgt

####  static int gen_remove_tgt(struct nvm_dev *dev, struct nvm_ioctl_remove *remove)

This part handling remove command of lnvm

/**
 * gen_remove_tgt - Removes a target from the media manager
 * @dev:        device
 * @remove:     ioctl structure with target name to remove.
 *
 * Returns:
 * 0: on success
 * 1: on not found
 * <0: on error
 */


```c
                                  | --- t(nvm_target) = gen_find_target(gn, remove->tgtname);
gen -> remove_tgt(gen_remove_tgt) |
                                  | --- __gen_remove_target(t(nvm_target)); | --- gen_unregister_target(t(nvm_target));
                                  | --- return 0;                            
```

### .get_blk = gen_get_blk

#### static struct nvm_block *gen_get_blk(struct nvm_dev *dev, struct nvm_lun *vlun) 

get free blocks. 

```c
                            | --- blk(nvme_blk) = list_first_entry(&lun->mgmt->free_list, struct nvm_block, list);
gen -> get_blk(gen_get_blk) |
                            | --- return blk;
```

### .put_blk = gen_get_blk

#### static void gen_put_blk(struct nvm_dev *dev, struct nvm_block *blk)

```c
                            | --- if (blk->state & NVM_BLK_ST_TGT)
gen -> put_blk(gen_get_blk) | --- else if (blk->state & NVM_BLK_ST_BAD)
                            | --- else
```

### .submit_io = gen_submit_io

#### static int gen_submit_io(struct nvm_dev *dev, struct nvm_rq *rqd)

```c
                                     /* Convert address space */
                                |--- nvm_generic_to_addr_mode(dev, rqd);
gen -> submit_io(gen_submit_io) | 
                                |--- return dev->ops->submit_io(dev, rqd);
```


### .erase_blk = gen_erase_blk

#### static int gen_erase_blk(struct nvm_dev *dev, struct nvm_blk, int flags)

```c
                                  |--- struct ppa_addr addr = block_to_ppa(dev, blk);
gen -> create_tgt(gen_remove_tgt) |
                                  |--- return nvm_erase_ppa(dev, &addr, 1, flags);  
```

### .mark_blk = gen_mark_blk

#### static void gen_mark_blk(struct nvm_dev *dev, struct ppa_addr gen_ppa, int type)

```c
                                  | --- pr_debug("gen: ppa  (ch: %u lun: %u blk: %u pg: %u) -> %u\n",gen_ppa.g.ch,gen_ppa.g.lun, gen_ppa.g.blk,gen_ppa.g.pg, type);
                                  | --- if (unlikely(gen_ppa.g.ch > dev->nr_chnls || gen_ppa.g.lun > dev->luns_per_chnl || gen_ppa.g.blk > dev->blks_per_lun)) {
gen -> create_tgt(gen_remove_tgt) | 
                                  | /* will be moved to bb list on put_blk from target */ 
                                     blk->state = type;
```

### .get_lun = gen_get_lun

#### static struct nvm_lun *gen_get_lun(struct nvm_dev *dev, int lunid)

```c
                                  | --- struct gen_dev *gn = dev->mp;
gen -> get_lun(gen_get_lun) | 
                                  | --- return &gn->luns[lunid].vlun;
```

### .reserve_lun = gen_reserve_lun

#### static struct nvm_lun_mgmt *gen_reserve_lun(struct nvm_dev *dev, int lunid, struct gendisk *tdisk)

```c
                                    | --- lun = &gn->luns[lunid];
                                    | --- mgmt = lun -> mgmt;
gen -> reserve_lun(gen_reserve_lun) | 
                                    | --- lun->tgt = gen_find_target(gn, tdisk->disk_name);
                                    | --- return mgmt;
```


### .release_lun = gen_release_lun

#### static void gen_release_lun(struct nvm_dev *dev, int lunid, struct nvm_lun_mgmt *mgmt)

```c
                                    | --- lun = &gn->luns[lunid];  
gen -> release_lun(gen_release_lun) |
                                    | --- lun->mgmt = mgmt;
```


### .lun_info_print = gen_lun_info_print

####  static void gen_lun_info_print(struct nvm_dev *dev)

```c
                                  | ---  gen_for_each_lun(gn, lun, i){
                                  |
gen -> create_tgt(gen_remove_tgt) |      pr_info("%s: lun%8u\t%u\n", dev->name, i,
                                                lun->mgmt->nr_free_blocks);
                                  | }
```

### .get_area = gen_get_area

#### satic int gen_get_area(struct nvm_dev *dev, sector_t *lba, sector_t len)

```c
                                  | --- area->begin = *lba = begin;
gen -> create_tgt(gen_remove_tgt) | --- area->end = begin + len;
                                  | --- return 0;
```


### .put_area = gen_put_area

#### static void gen_put_area(struct nvm_dev *dev, sector_t begin)

```c
gen -> create_tgt(gen_remove_tgt) | --- list_del(&area->list);
```


### total function list of gennvm.c file

```c 
1. static int __init gen_module_init(void)

2. static void gen_module_exit(void)

3. static void gen_lun_info_print(struct nvm_dev *dev)

4. static struct nvm_lun *gen_get_lun(struct nvm_dev *dev, int lunid)

5. static void gen_release_lun(struct nvm_dev *dev, int lunid, struct nvm_lun_mgmt *mgmt)

6. static struct nvm_lun_mgmt *gen_reserve_lun(struct nvm_dev *dev, int lunid, struct gendisk *tdisk)

7. static int gen_erase_blk(struct nvm_dev *dev, struct nvm_block *blk, int flags)

8. static int gen_submit_io(struct nvm_dev *dev, struct nvm_rq *rqd)

9. static void gen_end_io(struct nvm_rq *rqd)

10. static void gen_mark_blk(struct nvm_dev *dev, struct ppa_addr gen_ppa, int type)

11. static void gen_put_blk(struct nvm_dev *dev, struct nvm_block *blk)

12. static struct nvm_block *gen_get_blk(struct nvm_dev *dev, struct nvm_lun *vlun)

13. static void gen_unregister(struct nvm_dev *dev)

14. static int gen_register(struct nvm_dev *dev)

15. static ssize_t gen_sysfs_show(struct device *dev, struct device_attribute *dattr, char *page)

16. static ssize_t gen_sysfs_blocks(struct nvm_dev *dev, char *page)

17. static void gen_free(struct nvm_dev *dev)

18. static int gen_blocks_init(struct nvm_dev *dev, struct gen_dev *gn)

19. static int gen_block_map(u64 slba, u32 nlb, __le64 *entries, void *private)

20. static int gen_block_bb(struct gen_dev *gn, struct ppa_addr ppa, u8 *blks, int nr_blks)

21. static int gen_luns_init(struct nvm_dev *dev, struct gen_dev *gn)

22. static void gen_luns_free(struct nvm_dev *dev)

23. static void gen_blocks_free(struct nvm_dev *dev)

24. static void gen_put_area(struct nvm_dev *dev, sector_t begin)

25. static int gen_get_area(struct nvm_dev *dev, sector_t *lba, sector_t len)

26. static int gen_remove_tgt(struct nvm_dev *dev, struct nvm_ioctl_remove *remove)

27. static void __gen_remove_target(struct nvm_target *t)

28. static int gen_create_tgt(struct nvm_dev *dev, struct nvm_ioctl_create *create)

29. static struct nvm_target *gen_find_target(struct gen_dev *gn, const char *name)

30. int gen_register_target(struct nvm_target *t)

31. void gen_unregister_target(struct nvm_target *t)

32. static void gen_target_release(struct kobject *kobj)

33. static ssize_t gen_target_attr_store(struct kobject *kobj,struct attribute *attr,const char *page, size_t len)

34. static ssize_t gen_target_attr_show(struct kobject *kobj,struct attribute *attr,char *page)

```


# Data structure of lightNVM 

/include/linux/lightnvm.h

## struct nvm_lun_mgmt {

```c
struct nvm_lun_mgmt {
        /* lun block lists */
        struct list_head used_list;     /* In-use blocks */
        struct list_head free_list;     /* Not used blocks i.e. released
                                         * and ready for use
                                         */
        struct list_head bb_list;       /* Bad blocks. Mutually exclusive with
                                         * free_list and used_list
                                         */

        unsigned int nr_free_blocks;    /* Number of unused blocks */
};
```
