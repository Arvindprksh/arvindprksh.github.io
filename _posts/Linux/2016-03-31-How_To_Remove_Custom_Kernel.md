---
layout: post
title: Removing Custom kernel
subtitle: How can I remove my custom kernel
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

this refers to <a href ="https://community.linuxmint.com/tutorial/view/1718">linuxmint</a> & <a href ="http://askubuntu.com/questions/594443/how-can-i-remove-compiled-kernel">how-can-i-remove-compiled-kernel</a>

If you had a complied custom kernel & if have installed via make install, For uninstall the kernel installed from source,

you have to remove the below entries:

  - /boot/vmlinuz*KERNEL-VERSION*
  - /boot/initrd*KERNEL-VERSION*
  - /boot/System-map*KERNEL-VERSION*
  - /boot/config-*KERNEL-VERSION*
  - /lib/modules/*KERNEL-VERSION*/

For removing the above entries :

 - sudo rm -rf /lib/modules/kernel_version
 - sudo rm -f /boot/vmlinuz-kernel_version*
 - sudo rm -f /boot/initrd.img-kernel_version*
 - sudo rm -f /boot/config-kernel_version*
 - sudo rm -f /boot/System.map-kernel_version*
  
Finally, after uninstalling the kernel, run :

  sudo update-grub(ubuntu)
  
to clean the grub menu.

But if the instruction don't work, try this intruction "grub2-mkconfig -o /boot/grub2/grub.cfg" 

the instruction above refers to <a href= "https://wiki.centos.org/HowTos/Grub2">Grub2</a>-->


this relate centos upgrade to 7.2 with <a href = "http://tecadmin.net/upgrade-centos-7-to-latest-release/#">tecadmin</a>

this relate chainge centos kernel(4.5)  with <a href = "http://www.ostechnix.com/install-linux-kernel-4-5-centos-ubuntu/">ostechnix</a>
