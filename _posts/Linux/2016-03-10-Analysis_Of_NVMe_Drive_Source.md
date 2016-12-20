---
layout: post
title: analysis of NVMe Driver source 
subtitle: In order to register lightnvm, I analyzed kernel source, source version is 4.4
category: Linux
tags: [linux, kernel code]
permalink: /2016/03/10/Analysis_Of_NVMe_Drive_Source/
---

If you want to debug kernel source, use "printk" function, 

and click [this site](https://www.kernel.org/doc/Documentation/printk-formats.txt)

```c
 1. /linux/drviers/nvme/host/pci.c file 
2027 static int nvme_revalidate_disk(struct gendisk *disk) call 
      identifying nvme support nvm, if do. 
      if ns -> type is not NVME_NS_LIGHTNVM, kernel calls nvme_nvm_register for resgister   
2046         if (nvme_nvm_ns_supported(ns, id) && ns->type != NVME_NS_LIGHTNVM) {    
2047                 if ( nvme_nvm_register(ns->queue, disk->disk_name)) {   
2048                         dev_warn(dev->dev,    
2049                                 "%s: LightNVM init failure\n", __func__);    
2050                         kfree(id);    
2051                         return -ENODEV;    
2052                 }    
2053                 ns->type = NVME_NS_LIGHTNVM;    
2054         }     
        
        continue~~~~ 

2. /linux/drivers/nvme/host/lightnvm.c file     
581 int  nvme_nvm_ns_supported(struct nvme_ns *ns, struct nvme_id_ns *id) call   
      kernel indetify the supported vendor & PCI ID    
582 {    
583         struct nvme_dev *dev = ns->dev;    
584         struct pci_dev *pdev = to_pci_dev(dev->dev);    
585     
586         /* QEMU NVMe simulator - PCI ID + Vendor specific bit */   
587         if (pdev->vendor == PCI_VENDOR_ID_CNEX &&    
588                                 pdev->device == PCI_DEVICE_ID_CNEX_QEMU &&    
589                                                         id->vs[0] == 0x1)   
590                 return 1;    
591    
592         /* CNEX Labs - PCI ID + Vendor specific bit */    
593         if (pdev->vendor == PCI_VENDOR_ID_CNEX &&    
594                                 pdev->device == PCI_DEVICE_ID_CNEX_WL &&    
595                                                         id->vs[0] == 0x1)    
596                 return 1;    
597     
598         return 0;    
599 }    
600     

3.  /linux/drivers/nvme/host/lightnvm.c file    
   register function    
566 int nvme_nvm_register(struct request_queue *q, char *disk_name)    
567 {    
568         return nvm_register(q, disk_name, &nvme_nvm_dev_ops);    
569 }    

4. /linux/drivers/lifghtnvm/core.c file    
   now, happen error, when init function    
305 int nvm_register(struct request_queue *q, char *disk_name,   
306                                                         struct nvm_dev_ops *ops)    
307 {    
308         struct nvm_dev *dev;    
309         int ret;    
310     
311         if (!ops->identity)  
312                 return -EINVAL;   
313     
314         dev = kzalloc(sizeof(struct nvm_dev), GFP_KERNEL);    
315         if (!dev)    
316                 return -ENOMEM;    
317     
318         dev->q = q;    
319         dev->ops = ops;    
320         strncpy(dev->name, disk_name, DISK_NAME_LEN);    
          -- this is error    
321        
322         ret = nvm_init(dev);    
323         if (ret)    
324                 goto err_init;    
325     
326         if (dev->ops->max_phys_sect > 256) {    
327                 pr_info("nvm: max sectors supported is 256.\n");    
328                 ret = -EINVAL;    
329                 goto err_init;    
330         }    
331     
332         if (dev->ops->max_phys_sect > 1) {    
333                 dev->ppalist_pool = dev->ops->create_dma_pool(dev, "ppalist");    
334                 if (!dev->ppalist_pool) {    
335                         pr_err("nvm: could not create ppa pool\n");    
336                         ret = -ENOMEM;    
337                         goto err_init;    
338                 }    
339         }    
340     
341         /* register device with a supported media manager */    
342         down_write(&nvm_lock);    
343         dev->mt = nvm_init_mgr(dev);    
344         list_add(&dev->devices, &nvm_devices);    
345         up_write(&nvm_lock);    
346     
347         return 0;    
348 err_init:    
349         kfree(dev);    
350         return ret;   
351 }    


4. /linux/drivers/lifghtnvm/core.c file    
    error init    
254 static int nvm_init(struct nvm_dev *dev)    
255 {    
256         int ret = -EINVAL;    
257     
258         if (!dev->q || !dev->ops)    
259                 return ret;    
260     
261         if (dev->ops->identity(dev, &dev->identity)) {    
                   here, kernel say, device could not be  identified    
                    why ??? above function dev->ops->identity(dev, & dev-> identity) error!!!!!    
262                 pr_err("nvm: device could not be identified\n");    
263                 goto err;    
264         }    
265     
266         pr_debug("nvm: ver:%x nvm_vendor:%x groups:%u\n",    
267                         dev->identity.ver_id, dev->identity.vmnt,    
268                                                         dev->identity.cgrps);    
269     
270         if (dev->identity.ver_id != 1) {    
271                 pr_err("nvm: device not supported by kernel.");    
272                 goto err;    
273         }    
274     
275         if (dev->identity.cgrps != 1) {    
276                 pr_err("nvm: only one group configuration supported.");    
277                 goto err;    
278         }    
279     
280         ret = nvm_core_init(dev);    
281         if (ret) {    
282                 pr_err("nvm: could not initialize core structures.\n");    
283                 goto err;    
284         }    
285     
286         pr_info("nvm: registered %s [%u/%u/%u/%u/%u/%u]\n",    
287                         dev->name, dev->sec_per_pg, dev->nr_planes,    
288                         dev->pgs_per_blk, dev->blks_per_lun, dev->nr_luns,    
289                         dev->nr_chnls);    
290         return 0;    
291 err:    
292         pr_err("nvm: failed to initialize nvm\n");    
293         return ret;    
294 }    


5. /linux/include/linux/lightnvm.h file    
     data structure of struct nvm_dev     
240 struct nvm_dev {   
241         struct nvm_dev_ops *ops;    
242     
243         struct list_head devices;    
244         struct list_head online_targets;    
245     
246         /* Media manager */    
247         struct nvmm_type *mt;    
248         void *mp;    
249     
250         /* Device information */    
251         int nr_chnls;    
252         int nr_planes;    
253         int luns_per_chnl;    
254         int sec_per_pg; /* only sectors for a single page */    
255         int pgs_per_blk;    
256         int blks_per_lun;    
257         int sec_size;    
258         int oob_size;    
259         struct nvm_addr_format ppaf;    
260     
261         /* Calculated/Cached values. These do not reflect the actual usable    
262          * blocks at run-time.    
263          */    
264         int max_rq_size;    
265         int plane_mode; /* drive device in single, double or quad mode */    
266     
267         int sec_per_pl; /* all sectors across planes */    
268         int sec_per_blk;    
269         int sec_per_lun;    
270     
271         unsigned long total_pages;    
272         unsigned long total_blocks;    
273         int nr_luns;    
274         unsigned max_pages_per_blk;    
275     
276         void *ppalist_pool;    
277      
    
            tomorrow search for this variable
278         struct nvm_id identity;    
279     
280         /* Backend device */    
281         struct request_queue *q;    
282         char name[DISK_NAME_LEN];    
283 };    


6. /linux/include/linux/lightnvm.h file    
    other data structure of nvm_dev_ops    
200 struct nvm_dev_ops {    
201         nvm_id_fn               *identity;    
202         nvm_get_l2p_tbl_fn      *get_l2p_tbl;    
203         nvm_op_bb_tbl_fn        *get_bb_tbl;    
204         nvm_op_set_bb_fn        *set_bb_tbl;    
205     
206         nvm_submit_io_fn        *submit_io;    
207         nvm_erase_blk_fn        *erase_block;    
208     
209         nvm_create_dma_pool_fn  *create_dma_pool;    
210         nvm_destroy_dma_pool_fn *destroy_dma_pool;    
211         nvm_dev_dma_alloc_fn    *dev_dma_alloc;    
212         nvm_dev_dma_free_fn     *dev_dma_free;    
213     
214         unsigned int            max_phys_sect;    
215 };    
    
  this is function typedef for dev -> ops -> indentify(       ) why error ?????    
186 typedef int (nvm_id_fn)(struct nvm_dev *, struct nvm_id *); 

7.  /linux/drivers/block/null_blk.c file 
     check up struct nvm_id identity of struct nvm_dev
     so  
643 
644 static int null_add_dev(void) function call
645 {
722         if (use_lightnvm) {
723                 rv = nvm_register(nullb->q, nullb->disk_name,
724                                                         &null_lnvm_dev_ops);
725                 if (rv)
726                         goto out_cleanup_blk_queue;
727                 goto done;
728         }
 3/10/2016 will use printk at this 

3/11/2016 debugging linux/drivers/nvme/host/pci.c file
1031 /*
1032  * Returns 0 on success.  If the result is negative, it's a Linux error code;
1033  * if the result is positive, it's an NVM Express status code
1034  */
1035 int __nvme_submit_sync_cmd(struct request_queue *q, struct nvme_command *cmd,
1036                 void *buffer, void __user *ubuffer, unsigned bufflen,
1037                 u32 *result, unsigned timeout)
1038 {
1039         bool write = cmd->common.opcode & 1;
1040         struct bio *bio = NULL;
1041         struct request *req;
1042         int ret;
1043 
1044         req = blk_mq_alloc_request(q, write, GFP_KERNEL, false);
1045         if (IS_ERR(req))
1046                 return PTR_ERR(req);
1047 
1048         req->cmd_type = REQ_TYPE_DRV_PRIV;
1049         req->cmd_flags |= REQ_FAILFAST_DRIVER;
1050         req->__data_len = 0;
1051         req->__sector = (sector_t) -1;
1052         req->bio = req->biotail = NULL;
1053 
1054         req->timeout = timeout ? timeout : ADMIN_TIMEOUT;
1055 
1056         req->cmd = (unsigned char *)cmd;
1057         req->cmd_len = sizeof(struct nvme_command);
1058         req->special = (void *)0;
1059 
1060         if (buffer && bufflen) {
1061                 ret = blk_rq_map_kern(q, req, buffer, bufflen,
1062                                       __GFP_DIRECT_RECLAIM);
1063                 if (ret)
1064                         goto out;
1065         } else if (ubuffer && bufflen) {
1066                 ret = blk_rq_map_user(q, req, NULL, ubuffer, bufflen,
1067                                       __GFP_DIRECT_RECLAIM);
1068                 if (ret)
1069                         goto out;
1070                 bio = req->bio;
1071         }
1072 
1073         blk_execute_rq(req->q, NULL, req, 0);
1074         if (bio)
1075                 blk_rq_unmap_user(bio);
1076         if (result)
1077                 *result = (u32)(uintptr_t)req->special;
1078         ret = req->errors;
1079  out:
1080         blk_mq_free_request(req);
1081         return ret;
1082 }

now i wil test if return value is positive, negative or zero next week.

as the result of return value, I decide the direction.

```

when debugging kernel you have to use the short statement.

```shell
[    1.366214] hyun2 : nvme_revalidate_dist function call
[    1.368053] hyun2 : function call int nvme_nvm_ns_supported(struct nvme_ns *ns, struct nvme_id_ns *id)
[    1.368055] hyun2 pdev -> vendor : ###, pdev->device : ###, id->vs[0] : ##
[    1.368125] hyun2 : nvme_revalidate_dist function call
[    1.369995] hyun2 : function call int nvme_nvm_ns_supported(struct nvme_ns *ns, struct nvme_id_ns *id)
[    1.369997] hyun2 pdev -> vendor : ####, pdev->device : ###, id->vs[0] :##
```

the above log, kernel decide if nvme_revalidate_disk is valid or not, 

there are two PCI bus. so kernel check up that PCI is connected at two times while calling funtion," nvme_revalidate_disk"

with the above long, to search for kerenl source, refer to <a href = "http://lxr.free-electrons.com">this site</a>  


---

3/16/ log analization

```shell
[    1.451514] hyun2 :function call static int nvme_revalidate_disk(struct gendisk * disk)
[    1.451515] hyun2 : befor if (nvme_nvm_ns_supported(ns, id) && ns -> type != NVME_NS_LIGHTNVM
[    1.451515] hyun2 : function call
[    1.451516] hyun2 : pdev -> vendor : ### , pdev -> device : ### , iv->vs[0] : ##
[    1.451516] hyun2 : before if (pdev -> vendor == ### && pdev -> device == ### && id -> vs[0] == ##
[    1.451517] hyun2 : after if (pdev -> vendor == ### && pdev -> device == #### && id -> vs[0] == ##
[    1.451518] hyun2 : after if (nvme_nvm_ns_supported(ns, id) && ns -> type != NVME_NS_LIGHTNVM
[    1.451606] hyun2 :function call end static int nvme_revalidate_disk(struct gendisk * disk)
[    1.453466] hyun2 :function call static int nvme_revalidate_disk(struct gendisk * disk)
[    1.453467] hyun2 : befor if (nvme_nvm_ns_supported(ns, id) && ns -> type != NVME_NS_LIGHTNVM
[    1.453468] hyun2 : function call
[    1.453468] hyun2 : pdev -> vendor : ### , pdev -> device : ### , iv->vs[0] : #
[    1.453469] hyun2 : before if (pdev -> vendor == ### && pdev -> device == ### && id -> vs[0] == #
[    1.453470] hyun2 : after if (pdev -> vendor == ### && pdev -> device == ### && id -> vs[0] == #
[    1.453471] hyun2 : after if (nvme_nvm_ns_supported(ns, id) && ns -> type != NVME_NS_LIGHTNVM
[    1.453614] hyun2 :function call end static int nvme_revalidate_disk(struct gendisk * disk)
```

above all, kernel noticed SSD, and then registered SSD in order to use open-channel SSD, lightnvm.

