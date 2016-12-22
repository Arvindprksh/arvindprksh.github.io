---
layout: post
title: Over Provisioning in SSD
subtitle: What is Over Provisioning in SSD ?
category: SSD (Solid State Drives)
tags: [nvme]
permalink: /2016/11/21/Over_Provisioning_In_SSD/
---

I quote this atricle from [SEGATE's blog](http://www.seagate.com/tech-insights/ssd-over-provisioning-benefits-master-ti/)  

# Over provisioning. 

  Many of us fondly remember the traditional "15 squeres puzzle". with just one empty square, shifting pieces to new locations requires a fair amount of effort because there is so little free sapce. 
  
  having the puzzle fifteen-sixthenths full makes for challenging and entertaining gameplay. But it's certainly not the kind of performance limitation you want in your solid state drive(SSD). 
  
  Image if the same puzzle were only half-full with eight pieces. It could be solved almost instantly. More free space enables faster piece movement and task (game) completion. 
  
  ![](/img/Image/SSD-Solid_State_Drives/2016-11-21-Over_Provisioning_In_SSD/Puzzle.png)


  SSDs work on a very similar principle. visualize the NAND flash memory inside of an SSD as a puzzle. Except that the amount of free sapce in a drive is not fixed. Manufacturers utilize various tatics to improve performance. and one of these is to allocate moer free space. a process  known as over-provisioning.
  
  the miminum amount of over-provisioning for an SSD is set at the factory. but users can allocate more sapce for better performance. Either way, a moderate understading  of over provisioning is necessary in order to make better SSD puchasing decisions and to configure drvices in the most advantageous way possible for each unique environment and use case. 
 
# Background : SSD writes. 

  SDDs work very differently from HDD. The fundamental unit of NAND flash memory is typically a 4 kilobyte (4KB) page. and there are usually 128 pages in a block. Writes can happen one page at a time. but only on blank(or erased) pages. 
  
  Pages cannot be directly overwritten. Rather, they must first be erased. however, erasing a page is complicated because of the fact that entire blocks of pages must be erase at one time.
  
  When the host wants to rewrite to an address. the SSD actually writes to a different, black page and then updates the logical block address (LBA) table (much like the MFT of an HDD). Inside the LBA table, the original page is marked as 'invalid' and the new page is marked as the current location for the new data. 
  
  Of course, SSDs must erase these invalid pages of data at some point, or the usable space on the SSD would eventually fill up. 
  
  SSDs periodically go through a process called _garbage collection_ to clear out invalid pages of data. During this process. the SSD controller, or flash controller, that manages NAND flash memory in an SSD, reads all the good pages of a block (skipping the invalid pages) and writes them to a new erased block. 
  
  Then, the original block is erased. Thus preparing it for new data.

  ![](/img/Image/SSD-Solid_State_Drives/2016-11-21-Over_Provisioning_In_SSD/Over-provisioning.png)

# Reference. 

  - [SEAGATE's page](http://www.seagate.com/tech-insights/ssd-over-provisioning-benefits-master-ti/)
  
  - [wikipedia's over write amplification](https://en.wikipedia.org/wiki/Write_amplification)
  
  - [Swap directory](https://www.linux.com/news/all-about-linux-swap-space)  
    
     * Just reference of what the swap directory is. 
