---
layout: post
title: NVMe Driver Source code
subtitle: Analysis of NVMe Driver Source Code in linux kernel 4.5
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

 I'm doing analysis about nvme driver source code of linux kernel version 4.5, refering to [this URL](http://lxr.free-electrons.com/source/drivers/nvme/host/pci.c?v=4.5)
 
## Initialization of nvme pci module. 

  As you can see **2294 [module_init(nvme_init);](http://lxr.free-electrons.com/source/drivers/nvme/host/pci.c?v=4.5#L2256)**in pci.c file, First of all You have to search for this function,"2256 [static int __init nvme_init(void)](http://lxr.free-electrons.com/source/drivers/nvme/host/pci.c?v=4.5#L2256)"
  
  the following is information of nvme driver. 
  
  > 2291 MODULE_AUTHOR("Matthew Wilcox ~~~");  
  > 2292 MODULE_LICENSE("GPL");  
  > 2293 MODULE_VERSION("1.0");  
  > 2294 module_init(nvme_init);  
  > 2295 module_exit(nvme_exit);  
 

## Flow of [static int _init nvme_int(void);](http://lxr.free-electrons.com/source/drivers/nvme/host/pci.c?v=4.5#L2256) of moudle_init(nvme_init)

 ![](/img/Image/SSD-Solid_State_Drives/2016-09-19-NVMe_Driver_Source_Code/module_init(nvme_init).png)
 

## [&Nvme_driver](http://lxr.free-electrons.com/source/drivers/nvme/host/pci.c?v=4.5#L2244) of pci_register_driver(&nvme_driver)

basically, the following is a original shape(pci_driver) of nvme_driver for pci_register_driver function

![](/img/Image/SSD-Solid_State_Drives/2016-09-19-NVMe_Driver_Source_Code/nvme_pci_driver.png)


```c
665 <a href ="http://lxr.free-electrons.com/source/include/linux/pci.h?v=4.5#L665">struct pci_driver</a> {
666         struct list_head node;
667         const char *name;
668         const struct pci_device_id *id_table;   /* must be non-NULL for probe to be called */
669         int  (*probe)  (struct pci_dev *dev, const struct pci_device_id *id);   /* New device inserted */
670         void (*remove) (struct pci_dev *dev);   /* Device removed (NULL if not a hot-plug capable driver) */
671         int  (*suspend) (struct pci_dev *dev, pm_message_t state);      /* Device suspended */
672         int  (*suspend_late) (struct pci_dev *dev, pm_message_t state);
673         int  (*resume_early) (struct pci_dev *dev);
674         int  (*resume) (struct pci_dev *dev);                   /* Device woken up */
675         void (*shutdown) (struct pci_dev *dev);
676         int (*sriov_configure) (struct pci_dev *dev, int num_vfs); /* PF pdev */
677         const struct pci_error_handlers *err_handler;
678         struct device_driver    driver;
679         struct pci_dynids dynids;
680 };
```

The following is when init function calls the [pci_register_driver](http://lxr.free-electrons.com/source/include/linux/pci.h?v=4.5#L1171) with &nvme_driver

in pci.c file, The following structure is intialized as follows. 

```c
  2244 static struct pci_driver nvme_driver = {
  2245         .name           = "nvme",
  2246         .id_table       = nvme_id_table,
  2247         .probe          = nvme_probe,
  2248         .remove         = nvme_remove,
  2249         .shutdown       = nvme_shutdown,
  2250         <a href = "http://lxr.free-electrons.com/source/include/linux/device.h?v=4.5#L260">.driver</a>         = {   // device driver structure. 
  2251                 .pm     = <a href ="http://lxr.free-electrons.com/source/include/linux/pm.h?v=4.5#L295">&nvme_dev_pm_ops,</a> // this function is associated with power management interface.
  2252         },
  2253         .err_handler    = &nvme_err_handler,
  2254 };
  2255
```

 each role of pci_driver variable is here 
 
### What is role of probe() function in driver. 
 
 
 If you want to know probe(), I recommend you have to read <a href = "http://lwn.net/Kernel/LDD3/">this URL</a>  
 
 In linux kernel code 4.5 version, Page with [device_driver structure](http://lxr.free-electrons.com/source/include/linux/device.h?v=4.5#L260) explain to me about role of probe() function.   
   
 
 That is @probe called to query the existence of a specific device, Whether this driver can work with it, and bind the driver to a specific device.
 
 
```c
227 /**
228  * struct device_driver - The basic device driver structure
229  * @name:       Name of the device driver.
230  * @bus:        The bus which the device of this driver belongs to.
231  * @owner:      The module owner.
232  * @mod_name:   Used for built-in modules.
233  * @suppress_bind_attrs: Disables bind/unbind via sysfs.
234  * @probe_type: Type of the probe (synchronous or asynchronous) to use.
235  * @of_match_table: The open firmware table.
236  * @acpi_match_table: The ACPI match table.
237  * @probe:      Called to query the existence of a specific device,
238  *              whether this driver can work with it, and bind the driver
239  *              to a specific device.
240  * @remove:     Called when the device is removed from the system to
241  *              unbind a device from this driver.
242  * @shutdown:   Called at shut-down time to quiesce the device.
243  * @suspend:    Called to put the device to sleep mode. Usually to a
244  *              low power state.
245  * @resume:     Called to bring a device from sleep mode.
246  * @groups:     Default attributes that get created by the driver core
247  *              automatically.
248  * @pm:         Power management operations of the device which matched
249  *              this driver.
250  * @p:          Driver core's private data, no one other than the driver
251  *              core can touch this.
252  *
253  * The device driver-model tracks all of the drivers known to the system.
254  * The main reason for this tracking is to enable the driver core to match
255  * up drivers with new devices. Once drivers are known objects within the
256  * system, however, a number of other things become possible. Device drivers
257  * can export information and configuration variables that are independent
258  * of any specific device.
259  */
260 struct device_driver {
261         const char              *name;
262         struct bus_type         *bus;
263 
264         struct module           *owner;
265         const char              *mod_name;      /* used for built-in modules */
266 
267         bool suppress_bind_attrs;       /* disables bind/unbind via sysfs */
268         enum probe_type probe_type;
269 
270         const struct of_device_id       *of_match_table;
271         const struct acpi_device_id     *acpi_match_table;
272 
273         int (*probe) (struct device *dev);
274         int (*remove) (struct device *dev);
275         void (*shutdown) (struct device *dev);
276         int (*suspend) (struct device *dev, pm_message_t state);
277         int (*resume) (struct device *dev);
278         const struct attribute_group **groups;
279 
280         const struct dev_pm_ops *pm;
281 
282         struct driver_private *p;
283 };
```
 

## Nvme_drv_fops in __register_chrdev(nvme_char_major, 0, NVME_MINORS, "nvme", &nvme_drv_fops);

The following is basic fileoperation structure of linux 4.5 

```c
1627 <a href="http://lxr.free-electrons.com/source/include/linux/fs.h?v=4.5#L1627">struct file_operations</a> {
1628         struct module *owner;
1629         loff_t (*llseek) (struct file *, loff_t, int);
1630         ssize_t (*read) (struct file *, char __user *, size_t, loff_t *);
1631         ssize_t (*write) (struct file *, const char __user *, size_t, loff_t *);
1632         ssize_t (*read_iter) (struct kiocb *, struct iov_iter *);
1633         ssize_t (*write_iter) (struct kiocb *, struct iov_iter *);
1634         int (*iterate) (struct file *, struct dir_context *);
1635         unsigned int (*poll) (struct file *, struct poll_table_struct *);
1636         long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
1637         long (*compat_ioctl) (struct file *, unsigned int, unsigned long);
1638         int (*mmap) (struct file *, struct vm_area_struct *);
1639         int (*open) (struct inode *, struct file *);
1640         int (*flush) (struct file *, fl_owner_t id);
1641         int (*release) (struct inode *, struct file *);
1642         int (*fsync) (struct file *, loff_t, loff_t, int datasync);
1643         int (*aio_fsync) (struct kiocb *, int datasync);
1644         int (*fasync) (int, struct file *, int);
1645         int (*lock) (struct file *, int, struct file_lock *);
1646         ssize_t (*sendpage) (struct file *, struct page *, int, size_t, loff_t *, int);
1647         unsigned long (*get_unmapped_area)(struct file *, unsigned long, unsigned long, unsigned long, unsigned long);
1648         int (*check_flags)(int);
1649         int (*flock) (struct file *, int, struct file_lock *);
1650         ssize_t (*splice_write)(struct pipe_inode_info *, struct file *, loff_t *, size_t, unsigned int);
1651         ssize_t (*splice_read)(struct file *, loff_t *, struct pipe_inode_info *, size_t, unsigned int);
1652         int (*setlease)(struct file *, long, struct file_lock **, void **);
1653         long (*fallocate)(struct file *file, int mode, loff_t offset,
1654                           loff_t len);
1655         void (*show_fdinfo)(struct seq_file *m, struct file *f);
1656 #ifndef CONFIG_MMU
1657         unsigned (*mmap_capabilities)(struct file *);
1658 #endif
1659         ssize_t (*copy_file_range)(struct file *, loff_t, struct file *,
1660                         loff_t, size_t, unsigned int);
1661         int (*clone_file_range)(struct file *, loff_t, struct file *, loff_t,
1662                         u64);
1663         ssize_t (*dedupe_file_range)(struct file *, u64, u64, struct file *,
1664                         u64);
1665 };
```

the following is structure the nvme driver uses for register of [__register_chrdev](http://lxr.free-electrons.com/source/fs/char_dev.c?v=4.5#L242) of nvme 


![](/img/Image/SSD-Solid_State_Drives/2016-09-19-NVMe_Driver_Source_Code/nvme_dev_fops_file_operation.png)

```c
1009 static const struct file_operations nvme_dev_fops = {
1010         .owner          = THIS_MODULE,
1011         .open           = nvme_dev_open,
1012         .release        = nvme_dev_release,
1013         .unlocked_ioctl = nvme_dev_ioctl,
1014         .compat_ioctl   = nvme_dev_ioctl,
1015 };
```
